FROM circleci/php:7.0.30-apache-node-browsers

RUN sudo npm install uglify-js -g
RUN sudo npm install uglifycss -g
RUN sudo apt-get install python-dev python-pip jq
RUN sudo pip install --upgrade awscli
RUN sudo apt-get install libmemcached-dev
RUN sudo apt-get install mysql-client
RUN sudo apt-get install mysql-server
RUN sudo apt-get install zlib1g-dev
RUN sudo docker-php-ext-install pdo_mysql

RUN sudo mkdir /usr/src/php
RUN sudo tar --file /usr/src/php.tar.xz --extract --strip-components=1 --directory /usr/src/php
RUN sudo cp /usr/src/php/php.ini-production /usr/local/etc/php/php.ini

RUN sudo git clone https://github.com/php-memcached-dev/php-memcached.git
RUN cd php-memcached && sudo git checkout php7
RUN cd php-memcached && sudo phpize
RUN cd php-memcached && sudo PATH=/usr/local/bin/phpize:$PATH ./configure --disable-memcached-sasl
RUN cd php-memcached && sudo make install

RUN echo "pdo_mysql.default_socket=/var/run/mysqld/mysqld.sock" | sudo tee --append /usr/local/etc/php/conf.d/pdo.ini
RUN echo "extension=/var/www/html/php-memcached/modules/memcached.so" | sudo tee --append /usr/local/etc/php/php.ini
