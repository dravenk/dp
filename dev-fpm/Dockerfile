FROM dravenk/dp:fpm

# Install xdebug
RUN pecl install xdebug && docker-php-ext-enable xdebug

# See https://xdebug.org/docs/remote
RUN { \
    echo '[xdebug]'; \
    echo 'xdebug.remote_enable=1'; \
    echo 'xdebug.remote_handler=dbgp'; \
    echo 'xdebug.remote_host=host.docker.internal'; \
    echo 'xdebug.remote_port=9000'; \
    echo 'xdebug.remote_autostart=1'; \
    echo 'xdebug.remote_connect_back=1'; \
    } >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini

RUN set -eux; \
        composer global require drupal/coder && \
        composer global require dealerdirect/phpcodesniffer-composer-installer

RUN { \
    echo 'export PATH="$PATH:$HOME/.composer/vendor/bin"'; \
    echo 'alias drupalcs="phpcs --standard=Drupal --extensions='php,module,inc,install,test,profile,theme,css,info,txt,md,yml'"'; \
    echo 'alias drupalcsp="phpcs --standard=DrupalPractice --extensions='php,module,inc,install,test,profile,theme,css,info,txt,md,yml'"'; \
    echo 'alias drupalcbf="phpcbf --standard=Drupal --extensions='php,module,inc,install,test,profile,theme,css,info,txt,md,yml'"'; \
    } >> /root/.bashrc

RUN /bin/bash -c "source /root/.bashrc"