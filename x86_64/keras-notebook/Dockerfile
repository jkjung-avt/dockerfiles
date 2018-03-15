## Dockerfile for keras (tensorflow backend) with ipyhton notebook

FROM jkjung:keras

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

# run as user 1000
#RUN useradd --create-home --uid 1000 --user-group --groups video \
#            --shell /bin/bash user && \
#    cp -a /root/.jupyter /root/.local /home/user && \
#    chown -R user:user /home/user /srv
#USER user

# publicly accessible on any IP
ENV IP=*

# IPython
EXPOSE 8888

# Set up our notebook config
COPY jupyter_notebook_config.py /root/.jupyter/
COPY run_jupyter.sh /

# start the jupyter notebook server
WORKDIR /
CMD /bin/bash -c 'jupyter notebook \
                  --NotebookApp.open_browser=False \
                  --NotebookApp.allow_root=True \
                  --NotebookApp.ip="$IP" \
                  --JupyterWebsocketPersonality.list_kernels=True \
                  "$@"'
