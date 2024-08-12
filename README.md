# ROCm-For-RX580

[中文](https://github.com/woodrex83/ROCm-For-RX580/blob/main/README.zh-CN.md)/
[English](https://github.com/woodrex83/ROCm-For-RX580/blob/main/README.md)

This repo hosts the docker images with ROCm backend support for extra architectures.
*Mainly focus on gfx803.*
However only the `Radeon RX 580 2048SP` is currently tested.
Since 2048SP is same as RX570, RX570/580/590 should work normally

## Version (UPDATED)
```
Ubuntu 22.04
ROCm 6.1
Python 3.10
Pytorch 2.4.0
Torchvision 0.19.0
```

Image | Description 
--- | ---
[woodrex/rocm-for-gfx803-dev](https://hub.docker.com/r/woodrex/rocm-for-gfx803-dev) | Base image with ROCm 5.5 (including rocBLAS and MAGMA) 
[woodrex/pytorch-for-gfx803-dev](https://hub.docker.com/r/woodrex/pytorch-for-gfx803-dev) | Images for PyTorch with ROCm backend support
[woodrex/sd-webui-for-gfx803](https://hub.docker.com/r/woodrex/sd-webui-for-gfx803) | Images for SD


# gfx803 Cards
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


# Recommended aliases

+ 70GB～100GB volume is preferred for pytorch/Stable-Diffusion

## Run SD container 
```shell
cd SD-webui
sudo docker compose up

# Stop container
sudo docker compose down
```
