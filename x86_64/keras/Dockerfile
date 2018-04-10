## Dockerfile for keras (tensorflow backend)

FROM jkjung:opencv

USER root

# ARG https_proxy
# ARG http_proxy

ENV DEBIAN_FRONTEND=noninteractive
ENV KERAS_BACKEND=tensorflow

# Do remember to download the 2 libcudnn deb files to ./cudnn/
# before building this Docker image...
COPY cudnn/libcudnn7_7.0.4.31-1+cuda9.0_amd64.deb /tmp
COPY cudnn/libcudnn7-dev_7.0.4.31-1+cuda9.0_amd64.deb /tmp

# TensorBoard
EXPOSE 6006

RUN dpkg -i /tmp/libcudnn7_7.0.4.31-1+cuda9.0_amd64.deb && \
    dpkg -i /tmp/libcudnn7-dev_7.0.4.31-1+cuda9.0_amd64.deb && \
    apt-get update && \
    apt-get install -y libhdf5-10 graphviz && \
    apt-get install -y libopenblas-dev libzmq3-dev && \
    apt-get install -y libcurl3-dev libfreetype6-dev && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    pip3 --no-cache-dir install pandas scipy sklearn scikit-learn \
                                seaborn sympy \
                                Pillow bcolz h5py pydot && \
    pip3 --no-cache-dir install --upgrade tensorflow-gpu && \
    pip3 --no-cache-dir install keras && \
    # python3 -c "import numpy; print(numpy.__version__)" && \
    # MPLBACKEND=Agg python3 -c "import matplotlib.pyplot" && \
    # python3 -c "import tensorflow; print(tensorflow.__version__)" && \
    rm -rf /tmp/* && \
    dpkg-query -l && \
    pip3 freeze && \
    echo "nohup tensorboard --logdir /mnt/logs 2>&1 &" > /startup.sh

# run as 'user'
USER user

# RUN /bin/bash startup.sh && sleep 4
