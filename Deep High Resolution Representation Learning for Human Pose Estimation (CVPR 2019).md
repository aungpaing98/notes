Paper : 
Github : 
Reference : https://towardsdatascience.com/overview-of-human-pose-estimation-neural-networks-hrnet-higherhrnet-architectures-and-faq-1954b2f8b249


HR Net use the top-down method, the network is built for estimating keypoints based on person bounding boxes which are detected by another network (FasterRCNN) during inference \ testing.
During training, HRNet uses the annotated bounding boxes of the given dataset.


Input image is either 256 * 192 or 384 * 288 with corresponding heatmap output size of 64 * 48 or 96 * 72.
The network outputs the heatmap size and 17 channels - value per each pixel in the heatmap per each keypoint (17 keypoints).

The open source architecture depicted is for 32 channel configurations. For 48 channels change every last layer starting from first transition layer and forward to 48 and it;s different multiplications by 2.


## main contribution
The paper proposed a method to retain the high resolution for the DNN model with large receptive field.
Specifically, the model interconnect the low resolution and high resolution throughtout the model. So, the model is able to achieve high resolution and large receptive field at the same time.

