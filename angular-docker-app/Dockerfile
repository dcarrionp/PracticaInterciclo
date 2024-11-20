# Utilizar la imagen base de Debian
FROM debian:latest

# Actualizar paquetes y preparar el sistema
RUN apt-get update && apt-get install -y \
    apache2 \
    curl \
    gnupg \
    build-essential

# Instalar Node.js (versión 16, ya que es estable para proyectos)
RUN curl -fsSL https://deb.nodesource.com/setup_18.x | bash - && \
    apt-get install -y nodejs

# Verificar la instalación de Node.js y npm
RUN node -v && npm -v

# Instalar Angular CLI globalmente
RUN npm install -g @angular/cli

# Copiar el código de la aplicación al contenedor
COPY . /app

# Establecer el directorio de trabajo
WORKDIR /app

# Instalar dependencias
RUN npm install

# Compilar la aplicación Angular
RUN ng build --configuration production

# Configurar el servidor web para servir la aplicación Angular
RUN cp -r /app/dist/* /var/www/html/

# Exponer el puerto 80
EXPOSE 80

# Comando por defecto
CMD ["apachectl", "-D", "FOREGROUND"]
