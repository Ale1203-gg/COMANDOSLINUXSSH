# COMANDOS LINUX SSH

Para conectarte a tu servidor remoto usa el siguiente comando:  

```bash
ssh -i ~/.ssh/tu-clave.pem usuario@tu-dominio.com
```

 **Explicación:**  
- `-i ~/.ssh/tu-clave.pem`  Especifica la clave privada (si usas autenticación con clave).  
- `usuario`  Es el usuario en el servidor (por ejemplo, `ubuntu` para servidores en Oracle Cloud).  
- `tu-dominio.com`  Es el dominio o la dirección IP del servidor.  

Si es la primera vez que te conectas, te pedirá confirmación escribiendo `yes`.  

---

##  Transferencia de Archivos con SCP  

###  Subir Archivos al Servidor  

Para subir archivos desde tu computadora local al servidor:  

```bash
scp -i ~/.ssh/tu-clave.pem archivo.html usuario@tu-dominio.com:/var/www/html/
```

Si quieres subir una carpeta completa, usa `-r` (modo recursivo):  

```bash
scp -i ~/.ssh/tu-clave.pem -r carpeta/ usuario@tu-dominio.com:/var/www/html/
```

 **Explicación:**  
- `scp` → Comando para copiar archivos de manera segura.  
- `-i ~/.ssh/tu-clave.pem` Usar clave privada para la conexión.  
- `archivo.html` Archivo que deseas subir.  
- `usuario@tu-dominio.com:/var/www/html/`  Destino en el servidor (la carpeta donde Apache almacena los archivos web).  

---

###  Descargar Archivos desde el Servidor  

Si necesitas descargar un archivo desde el servidor a tu computadora:  

```bash
scp -i ~/.ssh/tu-clave.pem usuario@tu-dominio.com:/var/www/html/index.html ~/Descargas/
```

Para descargar una carpeta completa:  

```bash
scp -i ~/.ssh/tu-clave.pem -r usuario@tu-dominio.com:/var/www/html/ ~/Descargas/
```

---

## Configurar Apache y PHP en el Servidor  

### Actualizar el Servidor  

Antes de instalar Apache y PHP, asegúrate de actualizar los paquetes:  

```bash
sudo apt update && sudo apt upgrade -y
```

###  Instalar Apache  

Ejecuta el siguiente comando para instalar Apache en Ubuntu:  

```bash
sudo apt install apache2 -y
```

Verifica que el servicio de Apache esté corriendo:  

```bash
sudo systemctl status apache2
```

Para habilitar Apache al inicio del sistema:  

```bash
sudo systemctl enable apache2
```

###  Instalar PHP  

Si tu sitio web requiere PHP, instálalo con:  

```bash
sudo apt install php libapache2-mod-php -y
```

Verifica la instalación creando un archivo de prueba:  

```bash
echo "<?php phpinfo(); ?>" | sudo tee /var/www/html/info.php
```

Luego, abre en el navegador:  

```
http://tu-dominio.com/info.php
```

---

##  Reiniciar Apache después de Cambios  

Si haces cambios en la configuración de Apache, reinicia el servicio con:  

```bash
sudo systemctl restart apache2
```

---

##  Configuración de Permisos en `/var/www/html/`  

Si necesitas permisos para modificar los archivos de tu sitio web, usa:  

```bash
sudo chown -R $USER:$USER /var/www/html/
sudo chmod -R 755 /var/www/html/
```

---

## Conclusión  

Con estos comandos puedes:  
 Conectarte a tu servidor vía **SSH**.  
Subir y descargar archivos con **SCP**.  
Instalar **Apache** y **PHP** para tu sitio web.  
Configurar permisos para modificar archivos en el servidor.  
