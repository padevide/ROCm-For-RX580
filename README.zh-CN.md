# ROCm-For-RX580

[中文](https://github.com/woodrex83/ROCm-For-RX580/blob/main/README.zh-CN.md)/
[English](https://github.com/woodrex83/ROCm-For-RX580/blob/main/README.md)


这个仓库托管支持额外架构gfx803 的 ROCm 后端的 Docker 镜像。
然而，目前只有 `Radeon RX 580 2048SP` 经过了测试，相同架構的RX570/580/590可以正常工作。

## 版本（已更新）
```
Ubuntu 22.04
ROCm 6.1
Python 3.10
Pytorch 2.4.0
Torchvision 0.19.0
```

镜像 | 描述 
--- | ---
[woodrex/rocm-for-gfx803-dev](https://hub.docker.com/r/woodrex/rocm-for-gfx803-dev)  | 包含 ROCm 6.1 的基础镜像（包括 rocBLAS）
[woodrex/pytorch-for-gfx803-dev](https://hub.docker.com/r/woodrex/pytorch-for-gfx803-dev)  | 使用 ROCm 6.1 的 PyTorch 镜像
[woodrex/sd-webui-for-gfx803](https://hub.docker.com/r/woodrex/sd-webui-for-gfx803)  | 用于 SD webui 的镜像

# 支援的gfx803显卡列表
    Polaris 30
        Radeon RX 590
    Polaris 20
        Radeon Pro 580
        Radeon RX 580
        Radeon Pro 575
        Radeon Pro 570
        Radeon RX 570
    Polaris 10
        Radeon RX 480
        Radeon RX 470
    Polaris 21
        Radeon Pro 560X
        Radeon Pro 560
        Radeon Pro 555X
        Radeon Pro 555
    Polaris 11
        Radeon RX 560D
        Radeon RX 460

+ 对于 pytorch/Stable-Diffusion，需要預留70-100GB的空間

## 运行 SD 容器 
```shell
cd SD-webui
sudo docker compose up -d
# 停止容器
sudo docker compose down
```
