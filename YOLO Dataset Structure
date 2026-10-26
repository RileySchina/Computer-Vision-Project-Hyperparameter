# YOLO Dataset Structure and Examples

A YOLO dataset keeps **images and annotations in separate folders, paired by identical filenames**.

## 1. Folder Structure (Ultralytics Format)

```
dataset/
├── images/
│   ├── train/    ← cat001.jpg, cat002.jpg ...
│   └── val/      ← cat101.jpg ...
├── labels/
│   ├── train/    ← cat001.txt, cat002.txt ...
│   └── val/      ← cat101.txt ...
└── data.yaml
```

**Why it works this way:** the training code takes each image path, swaps `/images/` for `/labels/` and the file extension for `.txt`, then looks for the annotation there. If the folder structure or filenames don't match exactly, the label isn't found and the image is treated as containing no objects.

## 2. Label File Format (Object Detection)

One `.txt` file per image, **one line per object**:

```
class_id x_center y_center width height
```

Example (`cat001.txt`):

```
0 0.512 0.430 0.250 0.380
2 0.130 0.700 0.100 0.150
```

Rules:

- **class_id starts at 0** and matches the class order in `data.yaml`.
- **Coordinates are the box center**, not the top-left corner.
- **All values are normalized to 0-1**: x and width are divided by image width; y and height are divided by image height.

**Why normalize:** during training, images are resized (e.g. to 640x640), flipped, and cropped. With pixel coordinates, every transform would require recalculating the labels. With ratios, labels stay correct however the image is scaled.

### Reading the example

For a 1000x800 image, the first line `0 0.512 0.430 0.250 0.380` means:

| Value | Meaning | Pixels |
|-------|---------|--------|
| 0 | class_id (e.g. cat) | - |
| 0.512 | x center | 512 px |
| 0.430 | y center | 344 px |
| 0.250 | box width | 250 px |
| 0.380 | box height | 304 px |

## 3. Converting from Pascal VOC (xmin, ymin, xmax, ymax)

```
x_center = (xmin + xmax) / 2 / image_width
y_center = (ymin + ymax) / 2 / image_height
width    = (xmax - xmin) / image_width
height   = (ymax - ymin) / image_height
```

Python example:

```python
def voc_to_yolo(xmin, ymin, xmax, ymax, img_w, img_h):
    x_center = (xmin + xmax) / 2 / img_w
    y_center = (ymin + ymax) / 2 / img_h
    width = (xmax - xmin) / img_w
    height = (ymax - ymin) / img_h
    return x_center, y_center, width, height

# Example: box (200, 150, 450, 450) in a 1000x800 image
print(voc_to_yolo(200, 150, 450, 450, 1000, 800))
# (0.325, 0.375, 0.25, 0.375)
```

## 4. Images With No Objects

Leave the label file empty (or don't create one). These "background images" help reduce false positives, because the model learns that some scenes contain nothing to detect.

## 5. data.yaml

```yaml
path: /path/to/dataset
train: images/train
val: images/val

names:
  0: cat
  1: dog
  2: person
```

This tells the trainer where the data is and what the classes are. Class names are only for display; internally the model uses only the numeric class_id.

Optional: add a `test: images/test` entry if you have a test split.

## 6. Instance Segmentation Format

For segmentation, each line holds polygon vertices instead of a box (also normalized to 0-1):

```
class_id x1 y1 x2 y2 x3 y3 ...
```

Example:

```
0 0.410 0.300 0.620 0.310 0.600 0.560 0.430 0.570
```

## 7. Training Example (Ultralytics)

```python
from ultralytics import YOLO

model = YOLO("yolo11n.pt")
model.train(data="dataset/data.yaml", epochs=100, imgsz=640)
```

## 8. Common Mistakes

1. Using pixel coordinates instead of 0-1 ratios.
2. Treating the top-left corner as the center point.
3. Starting class_id at 1, which pushes the last class out of range.
4. Mismatched subfolder names or filenames between `images/` and `labels/`.
5. Duplicate images across train and val, which inflates validation metrics.

## 9. Quick Validation Checklist

- [ ] Every image in `images/` has a matching `.txt` in `labels/` (or is intentionally a background image).
- [ ] All coordinate values are between 0 and 1.
- [ ] All class_ids are within the range defined in `data.yaml`.
- [ ] No overlap between train and val images.
- [ ] `path`, `train`, and `val` in `data.yaml` resolve to real folders.
