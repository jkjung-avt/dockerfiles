# x86_64/keras-notebook

Build command: `docker built -t jkjung:keras-notebook .`

Run: `docker run --runtime=nvidia --rm -it -u `id -u`:`id -g` -v ~/data:/data -v ~/mnt:/mnt -v ~/mnt/.keras:/home/user/.keras -p 6006:6006 -p 8888:8888 jkjung:keras-notebook
