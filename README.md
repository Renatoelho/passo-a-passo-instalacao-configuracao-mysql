# Passo a passo de instalação e configuração do MySQL

### Requisitos mínimos para instalação:

>> Sistema operacional Linux (Ubuntu 20.04.2 LTS)  <br/>Memória RAM de 4GB ou mais

## **1º Passo** - Instalação do MySQL

- Atualize o ambiente antes de iniciar o processo com os seguintes comandos:

````
sudo apt update && sudo apt upgrade -y
````

- Esse comando efetivamente executa a instalação:

````
sudo apt install mysql-server -y
````

![](https://drive.google.com/uc?export=view&id=14LhzpS-GYfjmDY3HoR7pdzZKeAMOxcQf)

## **2º Passo** - Verificando se o serviço do MySQL está rodando

````
systemctl status mysql
````

![](https://drive.google.com/uc?export=view&id=14Lu2HkYjibw4PsNGrxTcC-YFoI_Az8yd)

>> **Observação:** para o passo seguinte é importante que o serviço do MySQL esteja em execução.

## **3º Passo** - Configurações de segurança para acesso ao MYSQL

````
sudo mysql_secure_installation
````

**Usar o pluing de validação de senhas?**  <br/>
Fica a seu critério escolher qual vai ser o nível de complexidade das senhas usadas no seu banco de dados, nesse exemplo vou escolher **NÂO** e definir uma senha mais simples, pois como é um ambiente de testes, mas em produção não é aconselhável essa abordagem.  

![](https://drive.google.com/uc?export=view&id=14PpwnXRekvvMt-ATQ0eZ036T_BEq3wIW)

**Remover usuário anônimo?**  <br/>
**SIM**, pois pode evitar problemas futuros.

![](https://drive.google.com/uc?export=view&id=14S1lqr86E0eseNxoQj5v8XoH9VJwBmgv)

**Acesso remoto liberado?**  <br/>
**SIM**, é interessante esse acesso estar liberado para aplicações que vão ficar online, mas com muito cuidado.

![](https://drive.google.com/uc?export=view&id=14SyHcJsdzcpT1dgMBksH7wh8U0ii9NC3)

**Remover o database test?**  <br/>
**SIM**, isso vai evitar o acumulo de databases desnecessários.

![](https://drive.google.com/uc?export=view&id=14XkKklaU9NW55laRa3H0hTdxZkneJJXa)

**Gostaria que todas as configurações feitas sejam aplicadas imediatamente?**  <br/>
**SIM**, isso vai valer a parti de agora no banco de dados.

![](https://drive.google.com/uc?export=view&id=14ZLmZtk2nFDCUc9xASRDALOgfzaxzU4D)

Tudo OK até aqui...

## **4º Passo** - Primeiro acesso ao banco MySQL

````
sudo mysql -u root -p
````

![](https://drive.google.com/uc?export=view&id=14iNCayZe1L1xnCnv4LDbUlUrlss1HbCs)

Tudo funcionando.

## **5º Passo** - Liberando acesso remoto ao MySQL

Agora para efetivar o acesso remoto ao servidor temos 2 itens que serão necessários configurar, que é o arquivo de configurações do MySQL e liberar a porta 3306 do servidor que está hospedando o banco de dados.

- Usando um editor de texto (no caso aqui vou usar o nano) acesse o arquivo listado abaixo e procure o item ````bind-address```` e atualize o IP ````127.0.0.1```` para ````0.0.0.0````, isso vai possibilitar acesso a partir de qualquer origem. 

````
sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf
````

- No arquivo de configurações (Usando o editor nano)

![](https://drive.google.com/uc?export=view&id=14jIz3_C2V_czqGdvSrqe8DC2savUd-Pj)

Saia e salva o arquivo.

- Vai ser necessários abrir as portas do Firewall para o serviço do Mysql.

Execute as seguintes linhas de comandos:

````
sudo ufw status verbose
````
````
sudo ufw enable 
````
````
sudo ufw allow mysql 
````
````
sudo ufw status verbose
````

![](https://drive.google.com/uc?export=view&id=14knt0sHSlkPGVkDxata9Sg6xAx6THE9a)

>> **Observação:** Essas configurações devem ser feitas com cuidado para evitar problemas futuros.
	
## **6º Passo** - Reiniciar o serviço do banco de dados

Agora é só reiniciar o serviço do banco de dados e ele já estará pronto para ser utilizados para os mais variados objetivos.

````
sudo systemctl restart mysql
````

Visualizando status do serviço MySQL novamente:

````
sudo systemctl status mysql 
````

![](https://drive.google.com/uc?export=view&id=14kwBtqqyHvBkoeVgP48BXGK-FkIi5qgb)

Agora você já tem um banco de dados **MySQL instalado e configurado**, que permite acessos remotos. Em breve eu volto para ensinar os principais comandos SQL que ajudaram na administração do seu banco de dados.

**Até breve!**

**Referências:**  <br/><font size="1">Dev.mysql.com, **MySQL APT Repository.** Disponível em: https://dev.mysql.com/doc/mysql-apt-repo-quick-guide/en/. Acesso em: 13 nov. 2021.  <br/>Dev.mysql.com, **mysql_secure_installation.** Disponível em: <https://dev.mysql.com/doc/refman/8.0/en/mysql-secure-installation.html>. Acesso em: 13 nov. 2021.  <br/></font>
