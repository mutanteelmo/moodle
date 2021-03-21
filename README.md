
O processo de instalação LAMP foi realizado com base no passo a passo da Digital Ocean, mas não foi seguido a risca, devido a alguma diferenças que precisamos considerar ao ter um projeto localhost com moodle.
Referência:
https://www.digitalocean.com/community/tutorials/how-to-install-linux-apache-mysql-php-lamp-stack-ubuntu-18-04

1 - Instalação do VMWare Player e Ubuntu

2 - Instalação do Apache (apt install apache2)
	2.1 - Criação de config do virtual host apache (vi /etc/
	apache2/sites-available/moodle.conf), reload apache.
	2.2 - Definição de alias "localmoodle" em /etc/hosts.
	Obs: ncessário colocar http://localmoodle. Será redirecionado para localhost.

3 - Instalação do Mysql (apt install mysql-server)
 3.1 - Definido senha para root (pass: ubuntu)

4 - Instalação PHP (apt install php libapache2-mod-php php-mysql)
Obs: dependências serão instaladas futuramente, conforme serão apontadas na hora da instalação do Moodle.

5 - Download Moodle e config repositório
	5.1 - Criação da pasta moodle em /var/www (git clone mutanteelmo/moodle)
	5.2 - Adiciona o repositório remoto do moodle local (git remote add moodle https://github.com/moodle/moodle.git)
	5.3 - download de referencias das tags do repositório moodle - (Git fetch moodle).
	5.4 - Checkout para a branch mais atual estável (git checkout MOODLE_310_STABLE)
	5.5 - Checkout para branch que será criada em meu repositório - moodle moodle_v3.10.2 (git switch -c moodle_v3.10.2)
	5.6 - Adiciona todos os arquivos à branch (git add -A)
	5.7 - Push remoto (git push --set-upstream origin moodle_v3.10.2)

6 - Instalação Moodle
	6.1 - Definido usuário root como proprietário dos arquivos
	6.2 - Acesso ao passo a passo do Moodle, para instalação via navegador web.
	6.3 - Intalação de dependencias php, requisitadas pelo Moodle.
	6.4 - Definição de usuário admin. (User admin, pass @Ubuntu2021)

7 - Instalação tema.
	7.1 - Download do tema Fordson no site do Moodle, unzip e mv para o diretório moodle/themes (https://moodle.org/plugins/pluginversions.php?plugin=theme_fordson).
	7.2 - Instalação via interface.
	7.3 - Commit e push dos arquivos do tema;

8 - Alteração na página de perfil de usuário
	8.1 - Criado link do tipo "botão" na página de perfil do usuário, seguindo padrões da API de render do Moodle, que redireciona para página principal. (user/profile.php).
	8.2 - Adicionado String em theme/fordson/lang/en/theme_fordson.php
	8.3 - Criado diretório e arquivo para string em pt-br na pasta do tema Fordson (theme/fordson/lang/pt_br/theme_fordson.php)
	8.4 - Commit e push das alterações.

9 - Finalizando
	9.1 - Alterado permissões de diretórios para 755 e em arquivos 644,
	conforme recomendado na doc do moodle, em partes de segurança (https://docs.moodle.org/310/en/Security_recommendations).
	Comandos:
	chmod 755 $(find /path/to/base/dir -type d)
	chmod 644 $(find /path/to/base/dir -type f)
	9.2 - Commit e push
	9.3 - acidionado README.md
	9.4 - Commit e push

================================================

- Arquivos editados -
moodle/user/profile.php
moodle/theme/fordson/lang/en/theme_fordson.php
moodle/theme/fordson/lang/pt_br/theme_fordson.php

- Users -
Ubuntu: u Ubuntu, ubuntu (root é a mesma senha)
Moodle: u admin, pass @Ubuntu2021
Mysql: u root, pass ubuntu

- VM -
O arquivo da VM foi upado no Google drive.
Link: https://drive.google.com/file/d/1mLYxp5oU_Wy333HLABWsKDRPmSfBH3Rv/view?usp=sharing
Link também no e-mail.
