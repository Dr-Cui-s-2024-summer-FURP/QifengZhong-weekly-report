



# Week2

### What I have done
1. **Read PoseCNN repository code**:

   1. Gained some understanding of the PoseCNN project code.   - Trained on the dex-ycb dataset (setup=s0).

   2. Trained on the dex-ycb dataset (setup=s0).

   2. Used [coco2014/train/train]([COCO - Common Objects in Context (cocodataset.org)](https://cocodataset.org/#download)) as the background dataset during training (0.5 probability of replacing the original background). 

   4. Pre-trained weights ([vgg16](https://download.pytorch.org/models/vgg16-397923af.pth)).

2. **Understanding data requirements (still unclear, see Unresolved Difficulties section)**:
   
   1. Required data includes: object model masks, camera intrinsics, camera extrinsics (multiple cameras), and point clouds of object models.
   2. Did not find the specific usage of camera extrinsics in the code of PoseCNN project.
3. **Understanding of project code**
   1. Currently, I understand about 10% of the project code, but there is room for improvement.
   2. I would like to mention that key points is to understand include the data reading and preprocessing in the datasets module, particularly the __init__ function and __getitem__ function, as well as the implementation of the train function.

4. **Results**

    Approximately 6-7 fps,

     Batch size is 1 (if set to 2, memory will be insufficient; the original project default is 2):

![图片描述](./images/batch.JPG)

 At 2000 frames:

![图片描述](./images/2000.JPG)

![图片描述](./images/2000i.JPG)

 Weights after the first epoch ([checkpoint](https://drive.google.com/file/d/1MTVLZbQJKjnkJXIMnMX5M-T2DhATHbD_/view?usp=drive_link), loss did not converge for some reason![img](./images/0018D721.png)).

### Challenges (time-consuming, resolved)
1. Insufficient memory in the Linux system to accommodate the dataset

    Downloading and extracting the dataset was a painful process! The Linux system couldn't accommodate a 120GB dataset, so I bought an SSD(If your have no space on both systems windows and linux) or mounted the Windows partition on the Linux system. This solved the problem but wasted a lot of time (switching between the two systems).

2. If you encounter an error here ([in the original project](https://github.com/NVlabs/PoseCNN-PyTorch/blob/main/lib/datasets/dex_ycb.py#L151-L154)) when training...

   Refer to [issue46](https://github.com/NVlabs/PoseCNN-PyTorch/issues/46):

    The author's usage is as follows:

   ```python
   import numpy as np
   a = (0,1)
   b = np.array([1,0])
   print(b[a])
   ```

   Change it to the following to fix the error:

   ```python
   import numpy as np
   a = (0,1)
   b = np.array([1,0])
   print(b[np.array(a)])
   ```

   

### Unresolved Difficulties (very frustrating!)
1. There are many things I don't understand, especially the mathematical knowledge needed, such as how to calculate the coordinates of an object in an image based on camera parameters, etc.

 	2. Handling npz, xyz, ply files is difficult as it's hard to understand the meaning of the stored parameters.
 	3. The project also includes some data related to robotic arms (e.g., joint points for grasping objects). Applying this project (PoseCNN) fully to our ongoing project (drone pose estimation) is very challenging for me. I still have no clear idea of the data structure we need.
 	4. It is anticipated that I might need to write my own code (interface) for data processing to apply PoseCNN to the drone pose estimation project, which requires a comprehensive understanding of network structure and algorithm principles.

### Conclusion
The journey ahead is long and the task is arduous.