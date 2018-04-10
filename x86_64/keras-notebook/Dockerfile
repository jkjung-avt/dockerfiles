## Dockerfile for keras (tensorflow backend) with ipyhton notebook

FROM jkjung:keras

USER root

# ARG https_proxy
# ARG http_proxy

RUN pip3 --no-cache-dir install ipython ipykernel jupyter \
                                jupyter-kernel-gateway \
                                jupyter-tensorboard && \
    python3 -m ipykernel.kernelspec && \
    rm -rf /tmp/* && \
    pip3 freeze && \
    jupyter notebook --version && \
    jupyter nbextension list 2>&1

# run as 'user'
USER user

# publicly accessible on any IP
ENV IP=*

# IPython
EXPOSE 8888

# start the jupyter notebook server
WORKDIR /
CMD /bin/bash -c 'jupyter notebook \
                  --NotebookApp.open_browser=False \
                  --NotebookApp.allow_root=True \
                  --NotebookApp.ip="$IP" \
                  --JupyterWebsocketPersonality.list_kernels=True \
                  "$@"'
