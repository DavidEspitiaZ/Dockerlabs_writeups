Se debe ejecutar este comando siempre para borrar la **huella** del ssh ya que la IP es la misma en las maquinas vulnerables.
ssh-keygen -R 172.17.0.2

![alt text](image-20.png)
sudo nmap -p- -sS -sC -sV --min-rate=5000 -n -vvv -Pn 172.17.0.2 -oN puertos

![alt text](image-21.png)

Carlota
![alt text](image-22.png)

Intentamos un Brute Force Attack
hydra -l carlota -P /usr/share/wordlists/rockyou.txt ssh://172.17.0.2 -I -t 64
![alt text](image-23.png)

![alt text](image-24.png)
![alt text](image-25.png)
![alt text](image-26.png)
![alt text](image-27.png)
![alt text](image-28.png)
echo "ZXNsYWNhc2FkZXBpbnlwb24=" | base64 -d; echo
![alt text](image-29.png)

cambiamos al usuario oscar con la contraseña obtenida
![alt text](image-30.png)
![alt text](image-31.png)
![alt text](image-32.png)