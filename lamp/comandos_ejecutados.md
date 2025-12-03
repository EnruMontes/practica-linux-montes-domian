# Documentación de Instalación LAMP

Para la implementación del servidor LAMP, ejecutamos los siguientes pasos y comandos en la terminal:

## 1. Instalación de Paquetes
Actualizamos repositorios e instalamos el stack completo:
```bash
sudo apt-get update
sudo apt-get install -y apache2 mysql-server php libapache2-mod-php php-mysql
```

## 2. Configuración de Base de Datos (MySQL)
Iniciamos el servicio y configuramos usuario y base de datos mediante SQL:
```bash
sudo systemctl start mysql
sudo systemctl enable mysql
# Comandos SQL ejecutados:
# CREATE DATABASE tp_final_db;
# CREATE USER 'alumno'@'localhost' IDENTIFIED BY 'practica123';
# GRANT ALL PRIVILEGES ON tp_final_db.* TO 'alumno'@'localhost';
# FLUSH PRIVILEGES;
```

## 3. Configuración de Apache
Habilitamos módulos necesarios y reiniciamos el servicio:
```bash
sudo a2enmod rewrite
sudo a2enmod php*
sudo systemctl restart apache2
sudo systemctl enable apache2
```

## 4. Despliegue de Archivos Web
Creamos los archivos en el directorio raíz del servidor `/var/www/html/`:
- `index.html`: Creado con el diseño solicitado usando `cat <<EOF`.
- `info.php`: Script con función `phpinfo()`.
- `test_db.php`: Script de prueba de conexión a MySQL.

Finalmente, ajustamos permisos:
```bash
sudo chown -R www-data:www-data /var/www/html/
sudo chmod -R 755 /var/www/html/
```
