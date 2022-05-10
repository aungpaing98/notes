[arxiv cs.CV2017](https://arxiv.org/abs/1611.08050)
[Github : ZheC/Realtime_Multi-Person_Pose_Estimation](https://github.com/ZheC/Realtime_Multi-Person_Pose_Estimation)


## Abstract
- 2D Pose Estimation using CNN.
- Contribution : non-parametric representation (Part Affinity Fields) to learn to associate body parts with individuals in the image. (In other words, the main contribution is in the grouping of keypoints)
- bottom-up approach, realtime, agnostic of number of person to detect.
- The architecture is designed to jointly learn part locations and their association via two branches of the same sequential prediction process.


## Keywords
- Part Affinity Fields : a set of 2D vector fields that encode both the **location and orientation** of limbs over the image domain.


## Model Architecture
### Overall model architecture
![Model Architecture](./embeds/PAF_pose_estimation_model.png)

The model take image as input, produce two main feature maps, one for predicting the location of the keypoints [w, h, K] (body part) and one for assoiciation between limbs (PAF) [w, h, C, 2], where `K` is the number of keypoints and `C` is the number of limbs.

### Model component
![Model component](./embeds/PAF_model_component.png)

Top branch : predict the confidence maps, Bottom branch : predict the affinity field that encode part-to-part association.
The model have many stages (up to 6), with intermediate suprevision at each stage.

### Model Specifications
#### Model architecture
Backbone : fine tuned first 10 layers of VGG-19, generating a set of feature maps  `F` in above image, that is input to the first stage of each branch.
The model use stages and in each stage, loss is calculated to avaid vanishing gradient. This method is not optimal, since model training procedure need to be carefully designed. 
#### Loss
Loss : 2 Loss function for both first and second branch. $L_2$ Loss. the loss function is weighted spatially to address the issues of unlabelled (missed or occlusion) label. So, the loss will be
$$f_s^t =\sum_{j=1}^J\sum_pW(p).L_2(ground_truth, prediction)$$ where $W(p)$ is a binary mask with $W(p)=0$  when the annotation is missing at image location ***p***. Since DNN models are negative reinforce learning, so, if there is no label, and the model predict there is one, the model will not be penalized for that prediction. This may cause the model to predict more `False Positive.


## Dataset
### Confidence map for Part Detection
To generate the grouth truth heatmap for each keypoints (or for the center of the body).
$$S^*_{j, k}(p)=exp(-\frac{||p-x_{j, k}||^2_2}{\sigma^2})$$
k for each person, $x_{j, k} \in R^2$  for the groundtruth position of the body part $j$ for person $k$ in the image. the value at location $p\in R^2$ in $S^*_{j,k}$ is defined as above.
where $\sigma$ control the spread of the peak.
If there is an overlap, the groundtruth will be the aggregation of the individual confidence maps via a max operator.

### Part Affinity Field for Part Association
The equation is
$$L^*_{c, k}(p)= \begin{cases} v=0 & \quad \text{if p on limb c, k} \\ 0 & \quad \text{otherwise} \end{cases}$$
Here, $v = (x_{j_2, k} - x_{j_1, k}) / ||x_{j_2, k}-x_{j_1, k}||_2$  is the *unit vector* in the direction of the limb. The set of points on the limb is defined as those within a distance threshold of the line segment, i.e. those points p for which,
$$0\le v . (p - x_{j_1, k} \le l_{c, k} \quad \text{and} \quad | v_ . (p - x_{j_1, k} | \le \sigma_l$$ where the limb width $\sigma_l$ is a distance in pixels, the limb lenght is $l_{c, k} = ||x_{j_2, k} - x_{j_1, k}||_2$ and v_ is a vector perpendicular to v.
The ground truth part affinity field average the affinity fields of all people in the image.
$$L^*_c(p) = \frac{1}{n_c(p)} \sum_k L^*_{c, k}(p)$$
where $n_c(p)$ is the number of non-zero vectors at point $p$ across all k people.