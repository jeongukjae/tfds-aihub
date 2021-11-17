# tfds aihub

A project to preprocess and store aihub data as TFRecord format in GCS. [PyPi](https://pypi.org/project/tfds-aihub/)

## How to build and cache datasets?

1. Create dataset file (example: [k_fashion_image.py](./tfds_aihub/k_fashion_image/k_fashion_image.py))
2. Build dataset using tfds cli (`tfds build tfds_aihub/...`)
3. Upload preprocessed dataset.
4. Access dataset using `tfds.load("...", data_dir="gs://bucket/path")`
   - detailed description: <https://www.tensorflow.org/datasets/gcs>
   - authentication: <https://www.tensorflow.org/datasets/gcs#authentication>

## Dataset

### [K-Fashion Image(`k_fashion_image`)](https://aihub.or.kr/aidata/7988/download)

- Version: 1.1
- splits
  - `Training`: `967806`
  - `Validation`: `120975`

**Features:**

```python
tfds.features.FeaturesDict(
    {
        "image": tfds.features.Image(shape=(None, None, 3)),
        "objects": tfds.features.Sequence({
            "type": tfds.features.ClassLabel(names=_BBOX_TYPE),
            "bbox": tfds.features.BBoxFeature(),
            "segmentation_mask": tfds.features.Image(shape=(None, None, 1)),
            # TODO labels for style
        })
    }
)
```
