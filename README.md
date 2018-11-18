Ubuntu 16.04 安裝Cuda 9.0和 CuDnn

## 1. 更新顯卡驅動程式
Setting裡面找Driver，點選最上面那個

## 2. 安裝CUDA 9.0

```
cd
wget https://developer.nvidia.com/compute/cuda/9.0/Prod/local_installers/cuda_9.0.176_384.81_linux-run
```

```
cd
chmod +x cuda_9.0.176_384.81_linux-run
./cuda_9.0.176_384.81_linux-run --extract=$HOME
```

### 執行下面三個:

* `NVIDIA-Linux-x86_64-384.81.run` (1. NVIDIA driver that we ignore),
* `cuda-linux.9.0.176-22781540.run` (2. CUDA 9.0 installer), and
* `cuda-samples.9.0.176-22781540-linux.run` (3. CUDA 9.0 Samples).

執行第二個，安裝CUDA Toolkit 9.0:

```
sudo ./cuda-linux.9.0.176-22781540.run
```

```
sudo ./cuda-samples.9.0.176-22781540-linux.run
```

```
sudo bash -c "echo /usr/local/cuda/lib64/ > /etc/ld.so.conf.d/cuda.conf"
sudo ldconfig
```

設定環境PATH:
```
sudo vim /etc/environments
```
在 PATH="/blah:/blah/blah" 後加入(在""內) `:/usr/local/cuda/bin` (包括:)

重開機後測試:

```
cd /usr/local/cuda-9.0/samples
sudo make
```

執行
```
cd /usr/local/cuda/samples/bin/x86_64/linux/release
./deviceQuery
```

結果會像:
```
./deviceQuery Starting...

 CUDA Device Query (Runtime API) version (CUDART static linking)

Detected 1 CUDA Capable device(s)

Device 0: "GeForce GTX 1060"
  CUDA Driver Version / Runtime Version          9.0 / 9.0
  CUDA Capability Major/Minor version number:    6.1
  Total amount of global memory:                 6073 MBytes (6367739904 bytes)
  (10) Multiprocessors, (128) CUDA Cores/MP:     1280 CUDA Cores
  GPU Max Clock rate:                            1671 MHz (1.67 GHz)
  Memory Clock rate:                             4004 Mhz
  Memory Bus Width:                              192-bit
  L2 Cache Size:                                 1572864 bytes
  Maximum Texture Dimension Size (x,y,z)         1D=(131072), 2D=(131072, 65536), 3D=(16384, 16384, 16384)
  Maximum Layered 1D Texture Size, (num) layers  1D=(32768), 2048 layers
  Maximum Layered 2D Texture Size, (num) layers  2D=(32768, 32768), 2048 layers
  Total amount of constant memory:               65536 bytes
  Total amount of shared memory per block:       49152 bytes
  Total number of registers available per block: 65536
  Warp size:                                     32
  Maximum number of threads per multiprocessor:  2048
  Maximum number of threads per block:           1024
  Max dimension size of a thread block (x,y,z): (1024, 1024, 64)
  Max dimension size of a grid size    (x,y,z): (2147483647, 65535, 65535)
  Maximum memory pitch:                          2147483647 bytes
  Texture alignment:                             512 bytes
  Concurrent copy and kernel execution:          Yes with 2 copy engine(s)
  Run time limit on kernels:                     Yes
  Integrated GPU sharing Host Memory:            No
  Support host page-locked memory mapping:       Yes
  Alignment requirement for Surfaces:            Yes
  Device has ECC support:                        Disabled
  Device supports Unified Addressing (UVA):      Yes
  Supports Cooperative Kernel Launch:            Yes
  Supports MultiDevice Co-op Kernel Launch:      Yes
  Device PCI Domain ID / Bus ID / location ID:   0 / 1 / 0
  Compute Mode:
     < Default (multiple host threads can use ::cudaSetDevice() with device simultaneously) >

deviceQuery, CUDA Driver = CUDART, CUDA Driver Version = 9.0, CUDA Runtime Version = 9.0, NumDevs = 1
Result = PASS
```
如果成功，記得`rm` 那4個檔案(1 downloaded and 3 extracted)

## 3. Install cuDNN 7.0

1. 下載 "cuDNN v7.0.5 Library for Linux" `tgz` 檔案

2. 利用`sudo mv` 將下載的檔案移動到`/usr/local`，

3. 之後便移動到`local`資料夾
```
cd /usr/local
``` 
解壓縮 `tgz` 

```
sudo tar -xvzf cudnn-9.0-linux-x64-v7.tgz
```

4. 最後執行 
```
sudo ldconfig
``` 

5. 清除檔案 

```
sudo rm cudnn-9.0-linux-x64-v7.tgz
```
