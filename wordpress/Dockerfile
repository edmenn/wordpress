FROM wordpress:latest-php8.2-apache

# Instalar extensiones y dependencias necesarias
RUN apt-get update && apt-get install -y \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    libzip-dev \
    libonig-dev \
    libxml2-dev \
    libicu-dev \
    libxslt1-dev \
    libmagickwand-dev \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install -j$(nproc) \
    gd \
    mysqli \
    mbstring \
    zip \
    intl \
    soap \
    xsl \
    opcache \
    bcmath \
    xml \
    exif \
    pcntl \
    gettext \
    && pecl install imagick \
    && docker-php-ext-enable imagick

# Copiar el archivo php.ini personalizado
COPY php.ini /usr/local/etc/php/

# Establecer la zona horaria (opcional)
ENV TZ=America/Mexico_City
RUN echo "date.timezone=${TZ}" > /usr/local/etc/php/conf.d/timezone.ini
