# nanopi2_hat_oled_wol_server


![alt tag](https://github.com/reproteq/nanopi2_hat_oled_wol_server/blob/main/wake.png)


![alt tag](https://github.com/reproteq/nanopi2_hat_oled_wol_server/blob/main/nanopi2-wol-server.png)


# NANOPI NEO2 v1.1 1711 H5 QUADCORE

http://download.friendlyarm.com/nanopineo2

https://www.armbian.com/nanopi-neo-2/

Armbian_21.08.1_Nanopineo2_focal_current_5.10.60.img.xz

root login >  user=root pass=1234

tras el primer login cambiar el pass y si quieres crear otro usuario

## instalar hat oled nano pi neo2

git clone --depth=1 https://github.com/friendlyarm/NanoHatOLED.git
 
cd NanoHatOLED
 
sudo -H ./install.sh

armbian-config

configurar idioma i zona horaria

Seleccione Opciones de interfaz-> I2C elija y presione Entrar, luego vaya a Finalizar y reinicie.


## instalar wakeserver

sudo apt-get install nginx php php-cli php-fpm php-json php-common php-mysql php-zip php-gd php-mbstring php-curl php-xml php-pear php-bcmath 

copiar folder  wakeserver en www y sites-enabled en nginx  wakeserver.conf

chown -R www-data:www-data /var/www/wakeserver

sudo apt-get install wakeonlan

* si todo fue bien ya se encendera el hat oled y en la ruta de abajo el script python ya estara

cat /etc/rc.local

#!/bin/sh -e

/usr/local/bin/oled-start

exit 0

root@nanopineo2:/usr/local/bin# cat oled-start

#!/bin/sh

cd /root/NanoHatOLED

./NanoHatOLED

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
