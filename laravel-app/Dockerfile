FROM php:7.3.6-fpm-alpine3.9
# para nao ficar instalando o bash e mysql-client
RUN apk add --no-cache openssl bash mysql-client
RUN docker-php-ext-install pdo pdo_mysql

# Monitora
ENV DOCKERIZE_VERSION v0.6.1
RUN wget https://github.com/jwilder/dockerize/releases/download/$DOCKERIZE_VERSION/dockerize-alpine-linux-amd64-$DOCKERIZE_VERSION.tar.gz \
    && tar -C /usr/local/bin -xzvf dockerize-alpine-linux-amd64-$DOCKERIZE_VERSION.tar.gz \
    && rm dockerize-alpine-linux-amd64-$DOCKERIZE_VERSION.tar.gz

# Set working directory
WORKDIR /var/www

# Remove o html que vem por padrao
RUN rm -rf /var/www/html

# Install composer, greenciador do php
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Copy existentes aplicacoes e conteudos que estao no diretorio
COPY . /var/www

#link simbolico pasta public do laravel e aponta para o html
RUN ln -s public html

# Expose port 9000 and start php-fpm server
EXPOSE 9000

ENTRYPOINT ["php-fpm"]
