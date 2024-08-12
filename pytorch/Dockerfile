FROM woodrex/rocm-for-gfx803-dev:latest

ENV HSA_OVERRIDE_GFX_VERSION=8.0.3
ENV ROCM_ARCH=gfx803
ENV ROC_ENABLE_PRE_VEGA=1
ENV USE_CUDA=0
ENV USE_ROCM=1
ENV USE_NINJA=1
ENV FORCE_CUDA=1
ENV MAX_JOBS=8
ENV PYTHONENCODING=UTF-8 
ENV TORCH_BLAS_PREFER_HIPBLASLT=0
ENV PYTORCH_ROCM_ARCH=gfx803

LABEL org.opencontainers.image.authors="Patrick Mok <woodrex83@gmail.com>"

## Write the Environment VARSs to global
RUN echo HSA_OVERRIDE_GFX_VERSION=${HSA_OVERRIDE_GFX_VERSION} >> /etc/environment && \ 
    echo ROCM_ARCH=${ROCM_ARCH} >> /etc/environment && \ 
    echo ROC_ENABLE_PRE_VEGA=${ROC_ENABLE_PRE_VEGA} >> /etc/environment && \
    echo USE_CUDA=${USE_CUDA} >> /etc/environment && \
    echo USE_ROCM=${USE_ROCM} >> /etc/environment && \
    echo USE_NINJA=${USE_NINJA} >> /etc/environment && \
    echo FORCE_CUDA=${FORCE_CUDA} >> /etc/environment && \
    echo MAX_JOBS=${MAX_JOBS} >> /etc/environment && \ 
    echo PYTORCH_ROCM_ARCH=${PYTORCH_ROCM_ARCH} >> /etc/environment && \ 
    echo TORCH_BLAS_PREFER_HIPBLASLT=${TORCH_BLAS_PREFER_HIPBLASLT} >> /etc/environment

RUN export HSA_OVERRIDE_GFX_VERSION=${HSA_OVERRIDE_GFX_VERSION} && \
    export ROCM_ARCH=${ROCM_ARCH} && \
    export ROC_ENABLE_PRE_VEGA=${ROC_ENABLE_PRE_VEGA} && \
    export TORCH_BLAS_PREFER_HIPBLASLT=${TORCH_BLAS_PREFER_HIPBLASLT} && \    
    export USE_CUDA=${USE_CUDA}  && \
    export USE_ROCM=${USE_ROCM}  && \
    export USE_NINJA=${USE_NINJA} && \
    export FORCE_CUDA=${FORCE_CUDA} && \
    export MAX_JOBS=${MAX_JOBS} && \
    export PYTORCH_ROCM_ARCH=${PYTORCH_ROCM_ARCH} && \
    export TORCH_BLAS_PREFER_HIPBLASLT=${TORCH_BLAS_PREFER_HIPBLASLT}

# Download Torch
ENV PYTORCH_GIT_VERSION="release/2.4"
RUN git clone --recursive https://github.com/pytorch/pytorch.git -b ${PYTORCH_GIT_VERSION} /pytorch

# Download Torchvision
ENV TORCH_GIT_VERSION="release/0.19"
RUN git clone https://github.com/pytorch/vision.git -b ${TORCH_GIT_VERSION} /vision


WORKDIR /pytorch
RUN python3 setup.py clean
RUN pip install -r requirements.txt

RUN python3 tools/amd_build/build_amd.py

# Build Torch wheel
RUN python3 setup.py bdist_wheel

# Install Torch
RUN pip install dist/torch*-cp310-cp310-linux_x86_64.whl

WORKDIR /vision

# Build Torchvision wheel
RUN python3 setup.py bdist_wheel

# Install Torchvision
RUN pip install dist/torchvision-*-cp310-cp310-linux_x86_64.whl

# Remove installed folder
RUN rm -rf /pytorch
RUN rm -rf /vision

CMD ["/bin/bash", "-c"]