# ====================================================================== #
# Android SDK Docker Image (VNC enabled)
# ====================================================================== #

# Base image
# ---------------------------------------------------------------------- #
FROM thyrlian/android-sdk:latest

# Author
# ---------------------------------------------------------------------- #
LABEL maintainer "thyrlian@gmail.com"

# install and configure VNC server
ENV USER root
ENV DISPLAY :1
EXPOSE 5901
ADD vncpass.sh /tmp/
ADD watchdog.sh /usr/local/bin/
ADD supervisord_vncserver.conf /etc/supervisor/conf.d/
RUN apt-get update -y && \
    apt-get install -y --no-install-recommends xfce4 xfce4-goodies xfonts-base tightvncserver expect && \
    chmod +x /tmp/vncpass.sh; sync && \
    /tmp/vncpass.sh && \
    rm /tmp/vncpass.sh && \
    apt-get remove -y expect && apt-get autoremove -y && \
    FILE_SSH_ENV="/root/.ssh/environment" && \
    echo "DISPLAY=:1" >> $FILE_SSH_ENV

RUN apt-get update -y && \
    apt-get install -y qemu-kvm libvirt-bin ubuntu-vm-builder && \
    bridge-utils virt-manager

RUN adduser root kvm
RUN adduser root libvirt
