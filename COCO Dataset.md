# COCO dataset

| Dataset    | Filename  | Numbers of files |
| ---------- | --------- | ---------------- | 
| Train      | train2017 | 115k             | 
| Validation | val2017   | 5k               |  
| Test       | test-dev  | 20k              | 


## Annotation format

### Object Detection
```python
annotations.json

	| -- "info" : Dict = {'year', 'version', 'descriptions', 'contributor'}
	
	| -- "licenses" : List[Dict] = {'url', 'name'}
	
	| -- "categories" : List[Dict]
				{id            : Int , 
				 name          : Str, 
				 supercategory : Str }
	
	| -- "images" : List[Dict]
				{id            :  Int, 
				 license       :  Int, 
				 file_name     :  Str,
				 height        :  Int, 
				 width         :  Int, 
				 data_captured :  Str }
	
	| -- "annotations" : List[Dict]
				{id            :  Int, 
				 image_id      :  Int,
				 category_id   :  Int, 
				 bbox          :  List[FLoat] : xywh, 
				 area          :  Int, 
				 segmentation  :  List[Float], 
				 iscrowd       :  Bool }

```

### Keypoint annoation
```python
annotations.json

	| -- "info" : Dict = {'year', 'version', 'descriptions', 'contributor'}
	
	| -- "licenses" : List[Dict] = {'url', 'name'}
	
	| -- "categories" : List[Dict]
				{id            : 1 , 
				 name          : person, 
				 keypoints     : ['nose', 'left_eye', 'right_eye', 'left_ear', 'right_ear', 'left_shoulder', 'right_shoulder', 'left_elbow', 'right_elbow', 'left_wrist', 'right_wrist', 'left_hip', 'right_hip', 'left_knee', 'right_knee', 'left_ankle', 'right_ankle'],
				 skeleton      : [[16, 14], [14, 12], [17, 15], [15, 13], [12, 13], [6, 12], [7, 13], [6, 7], [6, 8], [7, 9], [8, 10], [9, 11], [2, 3], [1, 2], [1, 3], [2, 4], [3, 5], [4, 6], [5, 7]]}
	
	| -- "images" : List[Dict]
				{id            :  Int, 
				 license       :  Int, 
				 file_name     :  Str,
				 height        :  Int, 
				 width         :  Int, 
				 data_captured :  Str }
	
	| -- "annotations" : List[Dict]
				{segmentation  :  List[Float],
				 num_keypoints :  Int,
				 area          :  Float, 
				 iscrowd       :  Bool,
				 keypoints     :  List[Int],
				 image_id      :  Int,
				 bbox          :  List[FLoat] : xywh, 
				 category_id   :  1, 
				 id            :  Int}
```

#### CrowdPose Annotation

```python

annotations.json

	| -- "info" : Dict = {'year', 'version', 'descriptions', 'contributor'}
	
	| -- "licenses" : List[Dict] = {'url', 'name'}
	
	| -- "categories" : List[Dict]
				{id            : 1 , 
				 name          : person, 
				 keypoints     : ['left_shoulder', 'right_shoulder', 'left_elbow', 'right_elbow', 'left_wrist', 'right_wrist', 'left_hip', 'right_hip', 'left_knee', 'right_knee', 'left_ankle', 'right_ankle', 'head', 'neck'],
				 skeleton      : [[12, 13], [13, 0], [13, 1], [0, 2], [2, 4], [1, 3], [3, 5], [13, 7], [13, 6], [7, 9], [9, 11], [6, 8], [8, 10]]}
	
	| -- "images" : List[Dict]
				{id            :  Int, 
				 license       :  Int, 
				 file_name     :  Str,
				 height        :  Int, 
				 width         :  Int, 
				 data_captured :  Str }
	
	| -- "annotations" : List[Dict]
				{
				  num_keypoints      : int,
				  iscrowd            : int,
				  keypoints          : List[int] (len=14*3 = 42),
				  image_id           : int,
				  bbox: List[Float]  : xywh,
				  category_id        : 1,
				  id                 : Int}



```

#### MPII
Bounding box is a rectangle, with w, h = scale * * 200

```python
[{
  "joints_vis" : [1, 0, ...] (len : 16, 0:invisible, 1: visible),
  "joints" : [[x1, x2], ...],
  "images": "000003071.jpg",
  "scale"  : 1.946,
  "center": [40.0, 32.0]
}]
```

_0 - r ankle, 1 - r knee, 2 - r hip, 3 - l hip, 4 - l knee, 5 - l ankle, 6 - pelvis, 7 - thorax, 8 - upper neck, 9 - head top, 10 - r wrist, 11 - r elbow, 12 - r shoulder, 13 - l shoulder, 14 - l elbow, 15 - l wrist_