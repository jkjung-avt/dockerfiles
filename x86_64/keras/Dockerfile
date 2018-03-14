## Dockerfile for keras (tensorflow backend)

FROM jkjung:opencv

# ARG https_proxy
# ARG http_proxy

ARG DEBIAN_FRONTEND=noninteractive
ENV KERAS_BACKEND=tensorflow

RUN apt-get update && \
    apt-get install -y libhdf5-10 graphviz && \
    apt-get install -y libopenblas-dev && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    pip3 --no-cache-dir install pandas scipy scikit-learn \
                                Pillow bcolz h5py pydot && \
    pip3 --no-cache-dir install tensorflow && \
    pip3 --no-cache-dir install keras && \
    pip3 --no-cache-dir install ipython ipykernel jupyter \
                                jupyter-kernel-gateway \
                                jupyter-tensorboard && \
    python3 -m ipykernel.kernelspec && \
    jupyter notebook --version && \
    jupyter nbextension list 2>&1 && \
    python3 -c "import numpy; print(numpy.__version__)" && \
    python3 -c "import tensorflow; print(tensorflow.__version__)" && \
    MPLBACKEND=Agg python3 -c "import matplotlib.pyplot" && \
    rm -rf /tmp/* && \
    dpkg-query -l > /dpkg-query-l.txt && \
    pip3 freeze | tee /pip3-freeze.txt
