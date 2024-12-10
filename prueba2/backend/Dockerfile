# Usar imagen de Python como base
FROM python:3.8-slim

# Establecer la zona horaria
ENV TZ=UTC

# Instalar dependencias del sistema
RUN apt-get update && apt-get install -y \
    postgresql-client \
    libpq-dev \
    build-essential \
    tzdata \
    && rm -rf /var/lib/apt/lists/*

# Establecer el directorio de trabajo en el contenedor
WORKDIR /code

# Copiar los archivos de requisitos
COPY requirements.txt /code/

# Instalar las dependencias de Python
RUN pip install --no-cache-dir -r requirements.txt

# Copiar el resto del código de la aplicación
COPY . /code/

# Copiar el script de espera
COPY ./wait-for-db.sh /code/wait-for-db.sh
RUN chmod +x /code/wait-for-db.sh

# Exponer el puerto en el que la aplicación escuchará
EXPOSE 8000

# Comando para ejecutar la aplicación
CMD ["./wait-for-db.sh", "db", "python", "manage.py", "runserver", "0.0.0.0:8000"]
