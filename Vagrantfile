
Vagrant.configure("2") do |config|
  
  config.vm.box = "ubuntu/xenial64"
  config.vm.network :private_network, ip: "10.11.12.50"
  #config.vm.network :private_network, ip: "192.168.12.50", virtualbox__intnet: true

  config.vm.provision "shell", inline: <<-SHELL
		sudo apt-get update
		sudo apt-get install -y nano imagemagick apache2 subversion
		echo "mysql-server-5.5 mysql-server/root_password password root" | debconf-set-selections
		echo "mysql-server-5.5 mysql-server/root_password_again password root" | debconf-set-selections
		apt-get -y install mysql-server
		sudo apt-get update
		sudo apt-get install -y antiword
		sudo apt-get install -y ghostscript
		sudo apt-get install -y xpdf
		echo "postfix postfix/mailname string pruebas.zonadam.com" | debconf-set-selections
		echo "postfix postfix/main_mailer_type string 'Internet Site'" | debconf-set-selections
		apt-get install -y postfix
		sudo apt-get install -y libimage-exiftool-perl
		sudo apt-get install -y cron
		sudo apt-get install -y wget
		sudo apt-get update && apt-get upgrade
		sudo apt-get install -y software-properties-common python-software-properties
		sudo apt-get install -y php7.0 php7.0-dev php7.0-gd php7.0-mysql php-mbstring php-zip libapache2-mod-php libav-tools
		service apache2 restart
		  
		mysql -u root -p"root" -e "CREATE DATABASE zonadam CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;"

		sudo mkdir /var/www/html/zonadam
		cd /var/www/html/zonadam
		sudo svn co https://svn.resourcespace.com/svn/rs/releases/8.6 .
		sudo mkdir filestore
		sudo chmod 777 filestore
		sudo chmod -R 777 include

		sudo chown -R www-data:www-data /var/www/html/zonadam/
		cp /etc/php/7.0/cli/php.ini /etc/php/7.0/cli/php.ini.bck
		sudo sed -i 's,^post_max_size =.*$,post_max_size = 100M,' /etc/php/7.0/cli/php.ini
		sudo sed -i 's,^memory_limit =.*$,memory_limit = 200M,' /etc/php/7.0/cli/php.ini
		sudo sed -i 's,^upload_max_filesize =.*$,upload_max_filesize = 100M,' /etc/php/7.0/cli/php.ini

   SHELL
end
