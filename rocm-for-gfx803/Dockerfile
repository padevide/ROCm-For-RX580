FROM rocm/dev-ubuntu-22.04:6.1.2-complete

ENV HSA_OVERRIDE_GFX_VERSION=8.0.3
ENV ROCM_ARCH=gfx803
ENV ROC_ENABLE_PRE_VEGA=1
ENV USE_CUDA=0
ENV USE_ROCM=1
ENV USE_NINJA=1
ENV FORCE_CUDA=1
ENV MAX_JOBS=8
ENV PYTHONENCODING=UTF-8

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
    true

RUN export HSA_OVERRIDE_GFX_VERSION=${HSA_OVERRIDE_GFX_VERSION} && \
    export ROCM_ARCH=${ROCM_ARCH} && \
    export ROC_ENABLE_PRE_VEGA=${ROC_ENABLE_PRE_VEGA} && \
    export TORCH_BLAS_PREFER_HIPBLASLT=${TORCH_BLAS_PREFER_HIPBLASLT} && \    
    export USE_CUDA=${USE_CUDA}  && \
    export USE_ROCM=${USE_ROCM}  && \
    export USE_NINJA=${USE_NINJA} && \
    export FORCE_CUDA=${FORCE_CUDA} && \
    export MAX_JOBS=${MAX_JOBS} && \
    true

# Install ffmpeg for SDXL video
RUN --mount=type=cache,target=/var/cache/apt,rw --mount=type=cache,target=/var/lib/apt,rw \
    apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
    git ffmpeg virtualenv google-perftools ccache tmux mc pigz plocate python3-venv python3-yaml python3-joblib python3-pip libmsgpack-dev nano python-is-python3

RUN pip install cmake mkl mkl-include

# Download ROCBLAS
RUN git clone --branch rocm-6.1.2 https://github.com/ROCm/rocBLAS.git /rocblas

WORKDIR /rocblas
RUN ./install.sh -ida ${ROCM_ARCH} -j ${MAX_JOBS}

CMD ["/bin/bash","-c"]