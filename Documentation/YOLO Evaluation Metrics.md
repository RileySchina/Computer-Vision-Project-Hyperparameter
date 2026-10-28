# YOLO Evaluation Metrics

How to read the results of an object detection model.

## The validation table: `Box(P  R  mAP50  mAP50-95)`

"Box" means these scores are for the bounding boxes. They rely on one idea first.

### IoU (intersection over union)

IoU measures how much a predicted box overlaps the true box, from 0 (no overlap) to 1 (identical). A prediction counts as correct only if it has the right class **and** an IoU above a threshold, usually 0.5.

### P (precision)

Of all the boxes the model drew, what share were correct? High precision means few false alarms.

Example: 100 boxes drawn, 80 correct, so P = 0.80.

### R (recall)

Of all the real objects, what share did the model find? High recall means few misses.

Example: 100 real objects, 70 found, so R = 0.70.

P and R trade off. A model that draws boxes only when very sure has high precision and low recall, and the reverse for a model that draws many.

### mAP50

The average over all classes of the model's score (average precision, which combines P and R across confidence levels) when a match needs IoU of at least 0.5. It is a single number from 0 to 1, and higher is better.

### mAP50-95

The same, but averaged over IoU thresholds from 0.5 to 0.95. It rewards tightly placed boxes, so it is always lower than mAP50. It is the stricter, more standard headline number.

| Metric | Question it answers | Higher means |
|---|---|---|
| P | How many drawn boxes were right? | Fewer false alarms |
| R | How many real objects were found? | Fewer misses |
| mAP50 | Overall quality with a loose box match | Better detector |
| mAP50-95 | Overall quality including tight box placement | Better, more precise boxes |

## Confusion matrix

A grid with true classes on one axis and predicted classes on the other.

- The diagonal is correct predictions.
- Off-diagonal cells show mix-ups, such as a true Left Turn predicted as Right Turn.
- YOLO adds a **background** row and column. An object predicted as background is a miss, and a prediction on something that is background is a false alarm.

Saved automatically as `confusion_matrix.png` and `confusion_matrix_normalized.png` in the run folder.

## Training curves

Plots over epochs of the training loss, the validation loss (how wrong the model is), and the validation mAP.

- Show whether the model is learning.
- Show when it starts **overfitting**: validation gets worse while training keeps improving.
- Come from a single training run (`results.png` and `results.csv`).

## Learning curve

A plot of validation score against the **amount of training data**, made by training several models on, for example, 10%, 25%, 50%, and 100% of the data (`fraction=`).

- Answers "would more data help?"
- A curve still rising at 100% means more data would help.
- A flat curve means the data amount is not the limit.
- Needs several training runs, so it is optional.

## Which to use when

| Goal | Tool |
|---|---|
| Overall score of the final model | mAP50 and mAP50-95 on the test split |
| Which classes fail | Per-class P and R, confusion matrix |
| Is it overfitting? | Training curves |
| Should I collect more data? | Learning curve |
| Why does it fail? | Look at the validation prediction images (`val_batch*_pred.jpg` vs. `val_batch*_labels.jpg`) |
