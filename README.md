# primeiramente você criar um arquivo e nomea ele e depois da permisão de execução.
 |#bin/bash
# Segundo você faz a verificação do apache para ver se estar instalado.

if [ ! -x /etc/init.d/apache2 ]; then 
echo “Apache não encontrado, iniciando a instalação…”
sudo apt-get update
sudo apt-get install apache2 -y

else 
echo “Você já possui o apache instalado”
fi

# terceiro crie um diretorio no site.

sudo mkdir -p /var/www/ifrn/public_html
cd /var/www/ifrn/public_html 

# Quarto clona repositorio no git e mover arquivos

sudo git clone https://github.com/matheusmanuel/site-simples-com-html-e-css-.git
sudo cp -r site-simples-com-html-e-css-/* .
sudo rm -rf site-simples-com-html-e-css- /
cd /etc/apache2/sites-available/
sudo tee ifrn.conf<<EOF

# quinto criar um arquivo no Virtualhost

<Virtualhost *:80>
	ServerAdmin admim@ifrn

	ServerName ifrn
	ServerAlias www.ifrn
	DocumentRoot /var/www/ifrn/public_html
	ErrorLog ${APACHE_LOG_DIR}/error.log
	CustomLog${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
EOF

# sexto ativar um novo site e configura host

sudo a2ensite ifrn.conf

sudo echo “127.0.0.1		ifrn” | sudo tee -a /etc/hosts
# sétimo fazer a reiniciação do apache.

sudo /etc/init.d/apache2 restart
sudo /etc/init.d/apache2 status

# oitavo torna o script executavel e executar

sudo chmod +x script.sh 
./script.sh
vsudo nano script.sh
-
# Nono aqui foi feito script.

#! /bin/bash 
if [ ! -x /etc/init.d/apache2 ]; then 
echo “Apache não encontrado, iniciando a instalação…”
sudo apt-get update
sudo apt-get install apache2 -y

else 
echo “Você já possui o apache instalado”
fi

sudo mkdir -p /var/www/ifrn/public_html
cd /var/www/ifrn/public_html 
sudo git clone https://github.com/matheusmanuel/site-simples-com-html-e-css-.git
sudo cp -r site-simples-com-html-e-css-/* .
sudo rm -rf site-simples-com-html-e-css- /
cd /etc/apache2/sites-available/
sudo tee ifrn.conf<<EOF
(A partir daqui você pode simplesmente dar CTRL X e salvar e colar as particularidades aqui e no final colocar o EOF, ou fazer na mão)
<Virtualhost *:80>
	ServerAdmin admim@ifrn

	ServerName ifrn
	ServerAlias www.ifrn
	DocumentRoot /var/www/ifrn/public_html
	ErrorLog ${APACHE_LOG_DIR}/error.log
	CustomLog${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
EOF

sudo a2ensite ifrn.conf

sudo echo “127.0.0.1		ifrn” | sudo tee -a /etc/hosts

sudo /etc/init.d/apache2 restart
sudo /etc/init.d/apache2 status

(CTRL + X para salvar e sair)

sudo chmod +x script.sh 
./script.sh

# observação script tem que ser bem feito respeitando os espaços e todos caracteres.
