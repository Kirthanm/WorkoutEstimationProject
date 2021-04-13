# WorkoutEstimationProject

Pose Landmark Model (BlazePose GHUM 3D)
The landmark model in MediaPipe Pose comes in two versions: a full-body model that predicts the location of 33 pose landmarks (see figure below), and an upper-body version that only predicts the first 25. The latter may be more accurate than the former in scenarios where the lower-body parts are mostly out of view.

Please find more detail in the BlazePose Google AI Blog, this paper and the model card, and the attributes in each landmark below.


STATIC_IMAGE_MODE
If set to false, the solution treats the input images as a video stream. It will try to detect the most prominent person in the very first images, and upon a successful detection further localizes the pose landmarks. In subsequent images, it then simply tracks those landmarks without invoking another detection until it loses track, on reducing computation and latency. If set to true, person detection runs every input image, ideal for processing a batch of static, possibly unrelated, images. Default to false.

UPPER_BODY_ONLY
If set to true, the solution outputs only the 25 upper-body pose landmarks. Otherwise, it outputs the full set of 33 pose landmarks. Note that upper-body-only prediction may be more accurate for use cases where the lower-body parts are mostly out of view. Default to false.

SMOOTH_LANDMARKS
If set to true, the solution filters pose landmarks across different input images to reduce jitter, but ignored if static_image_mode is also set to true. Default to true.

MIN_DETECTION_CONFIDENCE
Minimum confidence value ([0.0, 1.0]) from the person-detection model for the detection to be considered successful. Default to 0.5.

MIN_TRACKING_CONFIDENCE
Minimum confidence value ([0.0, 1.0]) from the landmark-tracking model for the pose landmarks to be considered tracked successfully, or otherwise person detection will be invoked automatically on the next input image. Setting it to a higher value can increase robustness of the solution, at the expense of a higher latency. Ignored if static_image_mode is true, where person detection simply runs on every image. Default to 0.5.

Output
Naming style may differ slightly across platforms/languages.

POSE_LANDMARKS
A list of pose landmarks. Each lanmark consists of the following:

x and y: Landmark coordinates normalized to [0.0, 1.0] by the image width and height respectively.
z: Represents the landmark depth with the depth at the midpoint of hips being the origin, and the smaller the value the closer the landmark is to the camera. The magnitude of z uses roughly the same scale as x.

Note: z is predicted only in full-body mode, and should be discarded when upper_body_only is true.

visibility: A value in [0.0, 1.0] indicating the likelihood of the landmark being visible (present and not occluded) in the image.
