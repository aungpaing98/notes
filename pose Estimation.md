## Pose Estimation
Human pose estimation, the problem of localizing anatomical keypoints or parts of individuals.

### Challenges
---
- each image(frame) may contain an unknown number of people that can occur at any position or scale.
- Interactions between people induce complex spatial interference, due to contact, occlusion and limb articulation making association of parts difficult.
- Runtime complexity tends to grow with the number of people in the image.

### Common Practices
---
#### Top down Approach
Employ a person detector before keypoint detector. So that the keypoint detector will only have to detect the keypoints for the single person.

##### Advantages
- High accuracy since no need for grouping (associtate) the keypoints.
- Simple architecture.
- Model modularize enabled.

##### Disadvantages
- Low inference speed. Inference speed increase with the number of person in the image.
- Dependent on the person detection model.

##### Feature methods
- [[Deep High Resolution Representation Learning for Human Pose Estimation (CVPR 2019)]]

#### Bottom-up Approach
Group the keypoints generated from the heatmap output for all person instance from the image. There is no person detection phase. 

##### Advantages
- Roust to early commitment (no person detection model needed)
- Can reduce runtime regardless of the number of person in the image provided the grouping algorithm is great.

##### Disadvantages
- Often low accuracy than top down approach.
- Complex model, need careful engineering (hard to modularize) 

##### Feature Methods
[[Realtime Mulit-Person 2D Pose Estimation using Part Affinity Fields]]