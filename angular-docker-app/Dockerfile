# Usar una imagen base de Debian
FROM debian:latest

# Actualizar paquetes e instalar herramientas necesarias
RUN apt-get update && apt-get install -y \
    apache2 \
    curl \
    gnupg \
    build-essential

# Instalar Node.js y npm
RUN curl -fsSL https://deb.nodesource.com/setup_18.x | bash - && \
    apt-get install -y nodejs

# Verificar la instalación de Node.js y npm
RUN node -v && npm -v

# Instalar Angular CLI globalmente
RUN npm install -g @angular/cli

# Establecer el directorio de trabajo
WORKDIR /app

# Copiar archivos necesarios para instalar dependencias
COPY package*.json ./

# Instalar dependencias
RUN npm install

# Copiar el código de la aplicación Angular al contenedor
COPY . .

# Construir la aplicación Angular
RUN ng build --configuration production

# Configurar Apache para servir los archivos estáticos de Angular
RUN rm -rf /var/www/html/* && \
    cp -r /app/dist/angular-docker-app/* /var/www/html/

# Exponer el puerto 80 para servir la aplicación
EXPOSE 80

# Iniciar Apache en primer plano
CMD ["apachectl", "-D", "FOREGROUND"]
