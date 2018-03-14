## Dockerfile for keras (tensorflow backend) with ipyhton notebook

FROM jkjung:keras

# ARG https_proxy
# ARG http_proxy

ENV KERAS_BACKEND=tensorflow

# run as user 1000
#RUN useradd --create-home --uid 1000 --user-group --groups video \
#            --shell /bin/bash user && \
#    cp -a /root/.jupyter /root/.local /home/user && \
#    chown -R user:user /home/user /srv
#USER user

# publicly accessible on any IP
ENV IP=*

# start the jupyter notebook server
EXPOSE 8888
WORKDIR /
CMD /bin/bash -c 'jupyter notebook \
                  --NotebookApp.open_browser=False \
                  --NotebookApp.allow_root=True \
                  --NotebookApp.ip="$IP" \
                  --JupyterWebsocketPersonality.list_kernels=True \
                  "$@"'
