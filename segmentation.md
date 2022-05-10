# Segmentation

Grouping pixels with similar properties.

> Segmentation is very subjective to human.

## Segmentation and Grouping in Humans
- [[Gestalt Psychology]] (forms of shape in German)


## Segmentation Strategies
- Top-down segmentation : Pixels belongs together because they come from same object.
- Bottom-up Segmentation : Pixels belong together because they look similar.


## Segmentation as Clusters
Visual similarity can be based on:
	- Brightness
	- Color
	- Position
	- Depth
	- Motion
	- Texture
	- Material
	- etc.

## Methods for segmentation
### Traditional algorithm based
- [[K-Mean segmentation]]
- [[Mean Shift]]

### Deep Learning based
- [[Self-supervision-superpixels]]

## Metrics
### MeanIoU
```
iou = true_positives / (true_positives + false_positives + false_negatives)
```

In Keras
```python
tf.keras.metrics.MeanIoU(num_classes, name=None, dtype=None)
```
To compute IoUs, the predictions are accumulated in a confusion matrix, weighted by `sample_weight` and the metric is then calculated from it.

If `sample_weight` is None, weights default to 1. Use `sample_weight` of 0 to mask values.