# YOLO Dataset for Cyclist Hand Signal Detection

## 1. Folder Structure

```
cyclist_signals/
├── images/
│   ├── train/    ← img001.jpg ...
│   └── val/
├── labels/
│   ├── train/    ← img001.txt ...
│   └── val/
└── data.yaml
```

Image and label files must share the same filename.

## 2. Classes

| id | name | Signal |
|----|------|--------|
| 0 | left_turn | Left arm extended straight out |
| 1 | right_turn | Right arm extended straight out (or left arm bent up) |
| 2 | stop | Left arm bent down, palm back |
| 3 | no_signal | Cyclist with both hands on handlebars |

Pick one convention for "right turn" (right arm out vs. left arm bent up) and apply it everywhere.

## 3. Label Format

One line per object, values normalized to 0-1:

```
class_id x_center y_center width height
```

Example (`img001.txt`, one cyclist signaling left):

```
0 0.480 0.520 0.360 0.610
```

Example with two cyclists in one frame:

```
0 0.300 0.550 0.280 0.580
3 0.720 0.500 0.250 0.560
```

## 4. Annotation Rule

Draw the box around the **whole cyclist (rider + extended arm)**, and label it with the signal class. This keeps the box large enough for the model to see the arm pose, and it works with a single-stage detector.

## 5. data.yaml

```yaml
path: /path/to/cyclist_signals
train: images/train
val: images/val

names:
  0: left_turn
  1: right_turn
  2: stop
  3: no_signal
```

## 6. Training

```python
from ultralytics import YOLO

model = YOLO("yolo11s.pt")
model.train(
    data="cyclist_signals/data.yaml",
    epochs=100,
    imgsz=640,
    fliplr=0.0,   # IMPORTANT: no horizontal flip
)
```

**Disable horizontal flip (`fliplr=0.0`).** Flipping turns a left signal into a right signal while the label stays the same, which corrupts the training data. If you want flip augmentation, swap class 0 and 1 labels in the flipped copies yourself.

## 7. Data Tips

- Capture from the **same viewpoint** as deployment (behind, front, or side). Left/right swap depending on the camera side.
- Include varied lighting, backgrounds, bikes, clothing, and distances.
- Include small and partially occluded riders.
- Aim for at least 300-500 images per class to start.
- Add background images (no cyclist) with empty label files to reduce false positives.
- Keep train and val from different videos or locations to avoid inflated metrics.


## 9. Checklist

- [ ] Every image has a matching `.txt` (or is an intentional background image)
- [ ] All values are between 0 and 1
- [ ] class_id is within 0-3
- [ ] `fliplr=0.0` set
- [ ] No train/val overlap
