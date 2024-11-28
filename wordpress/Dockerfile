FROM wordpress:php8.2-apache

# Actualizar paquetes e instalar dependencias necesarias
RUN apt-get update && apt-get install -y --no-install-recommends \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    libzip-dev \
    libxml2-dev \
    libicu-dev \
    libxslt1-dev \
    libmagickwand-dev \
    libmagickcore-dev \
    imagemagick \
    pkg-config \
    libonig-dev \
    && rm -rf /var/lib/apt/lists/*

# Configurar e instalar la extensión gd
RUN docker-php-ext-configure gd --with-freetype --with-jpeg
RUN docker-php-ext-install -j$(nproc) gd

# Instalar otras extensiones de PHP
RUN docker-php-ext-install -j$(nproc) \
    mysqli \
    mbstring \
    zip \
    intl \
    soap \
    xsl \
    opcache \
    bcmath \
    exif \
    pcntl \
    gettext

# Instalar y habilitar imagick (versión compatible con PHP 8.2)
RUN pecl install imagick-beta && docker-php-ext-enable imagick

# Copiar el archivo php.ini personalizado
COPY php.ini /usr/local/etc/php/

# Establecer la zona horaria
ENV TZ=America/Asuncion
RUN echo "date.timezone=${TZ}" > /usr/local/etc/php/conf.d/timezone.ini
