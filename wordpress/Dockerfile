FROM wordpress:6.7.1-php8.3-apache

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

# Establecer la zona horaria
ENV TZ=America/Asuncion
RUN echo "date.timezone=${TZ}" > /usr/local/etc/php/conf.d/timezone.ini

# Configurar el entorno de Apache (opcional)
ENV APACHE_RUN_GROUP www-data
ENV APACHE_RUN_USER www-data
