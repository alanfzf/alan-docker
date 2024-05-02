FROM debian:bookworm-slim

# Env vars
ENV DEBIAN_FRONTEND=noninteractive
ENV USER=alan
ENV USER_PW=alan

# Define the root user
USER root
RUN echo 'root:root' | chpasswd

# Install base packages
RUN apt-get update && apt-get install -y git curl sudo nodejs npm

# Run the script setup
RUN curl -sSf "https://raw.githubusercontent.com/alanfzf/dotfiles/main/scripts/deb_setup.sh" | sh

# Define the local user
RUN useradd -ms /usr/bin/zsh ${USER}
RUN echo "${USER}:${USER_PW}" | chpasswd

# Grant sudo rights to the user
RUN usermod -aG sudo ${USER}

USER ${USER}
WORKDIR /home/${USER}
CMD ["zsh"]
