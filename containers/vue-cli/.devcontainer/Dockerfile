#-------------------------------------------------------------------------------------------------------------
# Copyright (c) Reyala PVT LTD. All rights reserved.
# Licensed under the MIT License.
#-------------------------------------------------------------------------------------------------------------

# To fully customize the contents of this image, use the following Dockerfile instead:
# https://github.com/reyala/vscode-dev-containers/node-12/.devcontainer/Dockerfile
FROM docker.pkg.github.com/reyala/vscode-dev-containers/node:12

ARG USER_UID=1000
ARG USER_GID=$USER_UID
ARG USERNAME=node

ARG VUE_CLI_VERSION="4.4.6"

# [Optional] Update UID/GID if needed
RUN if [ "$USER_GID" != "1000" ] || [ "$USER_UID" != "1000" ]; then \
        groupmod --gid $USER_GID $USERNAME \
        && usermod --uid $USER_UID --gid $USER_GID $USERNAME \
        && chown -R $USER_UID:$USER_GID /home/$USERNAME; \
    fi

ENV DEBIAN_FRONTEND=noninteractive
#
# Install Vue CLI
RUN sudo -u ${USERNAME} npm install -g @vue/cli@${VUE_CLI_VERSION}
  
ENV DEBIAN_FRONTEND=dialog
