# ======== BASE IMAGE ========
FROM debian:bookworm-slim as debian

# Env vars
ENV DEBIAN_FRONTEND=noninteractive
ENV USER=alan

ENV USER_PW=alan
# Define the root user
USER root
RUN echo 'root:root' | chpasswd

# Define the local user
RUN useradd -ms /usr/bin/zsh ${USER}
RUN echo "${USER}:${USER_PW}" | chpasswd

# Grant sudo rights to the user
RUN usermod -aG sudo ${USER}

# Install base packages
RUN apt-get update && apt-get install -y sudo git curl wget nodejs npm 

# Run the script setup
RUN curl -sSf "https://raw.githubusercontent.com/alanfzf/dotfiles/main/scripts/deb_setup.sh" | sh

USER ${USER}
WORKDIR /home/${USER}
CMD ["zsh"]

# ======== PHP-7.4 ========
FROM debian AS debian-php74

USER root
RUN apt-get install -y apt-transport-https lsb-release ca-certificates
RUN wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg
RUN echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" | tee /etc/apt/sources.list.d/php.list 
RUN apt-get update && apt-get install -y php7.4 php7.4-cli php7.4-json \
      php7.4-common php7.4-mysql php7.4-zip php7.4-gd \
      php7.4-mbstring php7.4-curl php7.4-xml \
      php7.4-bcmath php7.4-intl

USER ${USER}
CMD ["zsh"]
