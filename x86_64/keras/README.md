# x86_64/keras

Build command: `docker built -t jkjung:keras .`

Run: `docker run --runtime=nvidia --rm -it -u `id -u`:`id -g` -v ~/data:/data -v ~/mnt:/mnt -v ~/mnt/.keras:/home/user/.keras -p 6006:6006 jkjung:keras
