# NANOPI NEO2 v1.1 1711 H5 QUADCORE

https://www.armbian.com/nanopi-neo-2/

http://download.friendlyarm.com/nanopineo2


Armbian_21.08.1_Nanopineo2_focal_current_5.10.60.img.xz

root login >  user=root pass=1234

* tras el primer login cambiar el pass y si quieres crear otro usuario


## instalar hat oled nano pi neo2

apt-get install git

git clone --depth=1 https://github.com/friendlyarm/NanoHatOLED.git
 
cd NanoHatOLED
 
sudo -H ./install.sh

armbian-config

configurar idioma i zona horaria

Seleccione Opciones de interfaz-> I2C elija y presione Entrar, luego vaya a Finalizar y reinicie.

* si todo fue bien ya se encendera el hat oled y veras el script /usr/local/bin/oled-start con cat /etc/rc.local 


## instalar wakeserver

sudo apt-get install wakeonlan nginx php php-cli php-fpm php-json php-common php-mysql php-zip php-gd php-mbstring php-curl php-xml php-pear php-bcmath 

copiar folder  wakeserver en /var/www/  editar index.php y config.php con user, pass, ip, mac  y en nginx  sites-enabled  wakeserver.conf para el proxy

chown -R www-data:www-data /var/www/wakeserver

* si todo fue bien ya podras navegar hasta la ip y ver el server , no olvides abrir puertos del router y asignar ip fija para cada mac de las maquinas de la red y del server nanopi y  tambien puedes configurar dns dinamico para acceder desde fuera de tu red local .


## fail2ban 

apt-get install fail2ban

/etc/fail2ban/

nano jail.conf

nano jail.local

[sshd]

maxretry = 5

bantime=10800

/filter.d  > wakeserver.conf

/jail.d > wakeserver.conf

sudo systemctl restart fail2ban.service

fail2ban-client status

fail2ban-client status sshd

fail2ban-client status wakeserver

service fail2ban status


## firewall

sudo apt-get install ufw

sudo ufw status

ufw allow http, https, ssh, portwakeserver

ufw enable


![alt tag](https://github.com/reproteq/nanopi2_hat_oled_wol_server/blob/main/wake.png)


![GitHub Logo](https://github.com/reproteq/nanopi2_hat_oled_wol_server/blob/main/nanopi2-wol-server.png)


![GitHub Logo](/images/logo.png)
Format: ![Alt Text](url)
