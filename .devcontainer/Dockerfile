FROM ros:foxy
LABEL maintainer="adam.krawczyk@husarion.com"
# we want to be able to source
SHELL ["/bin/bash", "-c"]

ARG DEBIAN_FRONTEND=noninteractive

RUN apt-get update && \
    apt-get install -y git && \
    apt-get install -y libssl-dev dirmngr apt-utils && \
    apt-get update && apt-get install -y -qq apt-utils && \
    apt-get install -y -qq dirmngr && \
    apt-get install -y -qq apt-transport-https software-properties-common && \
    apt-get install -y -qq lsb-release gnupg gnupg-l10n gnupg-utils gpg gpg-agent gpg-wks-client gpg-wks-server gpgconf gpgsm gpgv dialog nano vim wget curl unzip gnupg2 && \
    apt-get install -y -qq ca-certificates

# clone the test repos
RUN cd /root && mkdir -p ros2_workspace/src && \
    cd ros2_workspace/src 
    # git clone https://github.com/ros2/examples

# build the workspace
RUN cd /root/ros2_workspace && \
    source /opt/ros/foxy/setup.bash && \
    colcon build --symlink-install

CMD ["bash"]
ENV NVIDIA_VISIBLE_DEVICES \
    ${NVIDIA_VISIBLE_DEVICES:-all}
ENV NVIDIA_DRIVER_CAPABILITIES \
    ${NVIDIA_DRIVER_CAPABILITIES:+$NVIDIA_DRIVER_CAPABILITIES,}graphics