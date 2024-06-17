# QifengZhong-weekly-report
## 第一周

1. **学习卷积神经网络（CNN）**
   - 掌握了CNN
     
2. **理解关键算法和数学计算**
   - 理解了PoseCNN，PoseCNN+ICP，解了其中一些的基本算法的原理和作用（霍夫投票，Ploss,Sloss）。
   - 学习了PointNet和PointNet++(利用了对称函数解决了点云的无序性换位不变性)。

3. **环境配置和部署**
   - 在Ubuntu 22.04 LTS上配置了PoseCNN所需的环境并部署了NVlabs仓库中PoseCNN的PyTorch版本项目。
     
4.  **其他问题**
   - 环境配置的时候版本不兼容，就是比较麻烦（已配置PoseCNN，未配置PointNet）
   - 解决方法：对于PoseCNN来说，需要安装有opencv-python == 4.2.0.34的pytorch版本。
   - setup时（cuda版本为12.x）所对应的pytorch版本（其他版本没试）需要对lib/layers/ROIAlign_cuda.cu进行以下操作
   - 删除文件中的#include <ATen/ATen.h>（高版本torch已不再使用）。
   - 替换： dim3 grid(std::min(THCCeilDiv(output_size, 512L), 4096L));
   - 为dim3 grid(std::min(((int)output_size + 512 -1) / 512, 4096));
   - 替换：THCudaCheck
   - 为AT_CUDA_CHECK
