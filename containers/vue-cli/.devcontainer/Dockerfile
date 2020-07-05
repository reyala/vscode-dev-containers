#-------------------------------------------------------------------------------------------------------------
# Copyright (c) Reyala PVT LTD. All rights reserved.
# Licensed under the MIT License.
#-------------------------------------------------------------------------------------------------------------

# To fully customize the contents of this image, use the following Dockerfile instead:
# https://github.com/reyala/dev-containers/node-12/Dockerfile
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

RUN apt-get update \
   && apt-get -y install --no-install-recommends \
   #
   # Install vue cli
   && sudo -u ${USERNAME} npm install -g @vue/cli@${VUE_CLI_VERSION} \
   #
   # Install powerlevel10k theme
   && sh -c "$(git clone --depth=1 https://github.com/romkatv/powerlevel10k.git /root/.oh-my-zsh/custom/themes/powerlevel10k)" \
   && sed -i "s/ZSH_THEME=\"robbyrussell\"/ZSH_THEME=\"powerlevel10k\/powerlevel10k\"/g" /root/.zshrc \
   # prevent p10k configure from prompting 
   && echo "POWERLEVEL9K_DISABLE_CONFIGURATION_WIZARD=true" >> /root/.zshrc \
   # add a line between prompts
   && echo "POWERLEVEL9K_PROMPT_ADD_NEWLINE=true" >> /root/.zshrc \
   && cp -R /root/.oh-my-zsh /home/$USERNAME \
   && cp /root/.zshrc /home/$USERNAME \
   && sed -i -e "s/\/root\/.oh-my-zsh/\/home\/$USERNAME\/.oh-my-zsh/g" /home/$USERNAME/.zshrc \
   && chown -R $USER_UID:$USER_GID /home/$USERNAME/.oh-my-zsh /home/$USERNAME/ \
   #
   # Clean up
   && apt-get autoremove -y \
   && apt-get clean -y \
   && rm -rf /var/lib/apt/lists/*

ENV DEBIAN_FRONTEND=dialog
