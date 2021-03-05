# Use ubuntu:latest as parent image
FROM ubuntu:latest

# Set maintainer
LABEL maintainer='BGameiro <projects+docker@bgameiro.me>'

# Update mirrors and packages. Install jupyterlab
RUN pacman --noconfirm -Syyu python-pip jupyterlab

ENV JUPYTERLAB_DIR /appdata/lab

# Build the lab
RUN jupyter lab build --minimize=False

# Expose port and path
EXPOSE 8888
VOLUME /appdata

# Add packages and functionalities
# ENV pkgs=PACKAGES
# CMD pacman --noconfirm -S 

# Run JupyterLab
CMD cp -R -n /usr/share/jupyter/* /appdata && jupyter lab --ip=* --port=8888 --no-browser --notebook-dir=/opt/app/data --allow-root
