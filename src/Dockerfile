# Use the official PHP image
FROM php:7.4-fpm

# Set working directory
WORKDIR /var/www/html

# Install dependencies
RUN apt-get update && \
    apt-get install -y \
    git \
    unzip \
    libpng-dev \
    libjpeg-dev \
    libfreetype6-dev \
    zip \
    curl \
    libonig-dev \
    libxml2-dev \
    libzip-dev \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install gd pdo pdo_mysql mbstring exif pcntl bcmath zip \
    && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Copy existing application directory contents
COPY ./app .

# Install Composer dependencies
RUN composer install --no-interaction --optimize-autoloader

# Create index.php with "Hello World!" content
RUN echo "<?php echo 'Hello World!'; ?>" > index.php

# Expose port 9000 and start php-fpm server
EXPOSE 9000
CMD ["php-fpm"]
