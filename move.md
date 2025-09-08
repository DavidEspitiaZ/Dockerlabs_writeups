## Levantamos la maquina
![despliegue](image.png)

## Conectividad

Tenemos conectividad con la maquina, además sabemos que es una maquina linux por el **TTL** 64
![ping a la maquina](image-1.png)

## Escaneo de Puertos
Hacemos un escaneo de puertos con **nmap**
sudo nmap -p- -sS -sC -sV --min-rate=5000 -n -vvv -Pn 172.17.0.2 -oN puertos


![alt text](image-2.png)

Hay 3 puertos abiertos
21 -> **FTP**
22 -> **SSH**
80 -> **HTTP**
3000 -> **GRAFANA**
## Fuzzing
si hacemos Fuzzing con **gobuster** vemos que hay un archivo llamado **maintenance.html.** 
instalamos Seclists
![alt text](image-6.png)

sudo gobuster dir -w /usr/share/wordlists/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt -x .php,.html,.sh,.py -u "http://172.17.0.2/"   
![alt text](image-7.png)

![alt text](image-8.png)
![alt text](image-9.png)
![alt text](image-10.png)
![alt text](image-11.png)
![alt text](image-12.png)
Vemos que hay un Usuario llamado Fredy 

Vemos que grafana tiene la version **8.3.0**
![Grafana](image-3.png)
Revisamos si hay alguna vulnerabilidad para esta version 


![alt text](image-4.png)
![alt text](image-5.png)
Si buscamos en internet vemos que el archivo database.kdbx se puede desencriptar con Keepassxc.

![alt text](image-14.png)

Y vemos la clave de freddy. Por lo que podemos probar por SSH ya que si recordamos, el puerto estaba abierto.

![alt text](image-15.png)
![alt text](image-16.png)

cd /opt
sudo git clone https://github.com/r1vs3c/searchbins.git
cd searchbins

sudo apt install jq yq -y

sudo bash install.sh


![alt text](image-17.png)
![alt text](image-18.png)
![alt text](image-19.png)
Somos Root