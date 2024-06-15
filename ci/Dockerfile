FROM php:8.2-alpine as ci-formatter

ENV PHP_CS_FIXER_VER="3.57.2"
# add composer binaries to path
ENV PATH="/root/.composer/vendor/bin:${PATH}"

# Install node
COPY --from=node:lts-alpine /usr/lib /usr/lib
COPY --from=node:lts-alpine /usr/local/lib /usr/local/lib
COPY --from=node:lts-alpine /usr/local/include /usr/local/include
COPY --from=node:lts-alpine /usr/local/bin /usr/local/bin
# Install composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Install blade-formatter and php-cs-fixer
RUN npm install -g blade-formatter && \
      composer global require friendsofphp/php-cs-fixer:${PHP_CS_FIXER_VER}

WORKDIR /root
