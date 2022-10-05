
# Instalação do Zabbix Server 4.0

Site : https://www.zabbix.com/br/download

<br>

### 1° Passo Escolha sua plataforma

![ITENS](./img/1.png)

### 2° Passo - Update do Sistema Operacional
```
yum update 
```

### 3° Passo - Instalação do editor de texto
```
yum install vim 
```

### 4° Passo - Instalação do repositorio do Zabbix
```
rpm -Uvh https://repo.zabbix.com/zabbix/4.0/rhel/7/x86_64/zabbix-release-4.0-2.el7.noarch.rpm

yum clean all
```

### 5° Passo - Instale o servidor, o frontend e o agente Zabbix
```
yum install zabbix-server-mysql zabbix-web-mysql zabbix-agent
```
### 6° Passo - Instalação do Banco de Dados
```
yum install mariadb-server
```
### 7° Passo - Inicie o banco de dados
```
systemctl start mariadb.service
```

### 8° Passo - Criar banco de dados inicial
```
mysql -uroot -p
Obs: Vai solicitar senha, basta clicar na tecla ENTER.

Comandos: 

create database zabbix character set utf8 collate utf8_bin;

create user zabbix@localhost identified by '123456';

grant all privileges on zabbix.* to zabbix@localhost;

quit;
```

### 9° Passo - Importe o esquema inicial
```
zcat /usr/share/doc/zabbix-server-mysql*/create.sql.gz | mysql -uzabbix -p zabbix

Obs: Vai solicitar senha , digite : 123456
```

### 10° Passo - Configure o banco de dados para o servidor Zabbix
```
vim /etc/zabbix/zabbix_server.conf

Ajuste a linha abaixo :

DBPassword=123456
```

### 11° Passo - Configure o PHP para o frontend Zabbix
```
vim /etc/httpd/conf.d/zabbix.conf

Ajuste para : America/Sao_Paulo
```

Antes 

![ITENS](./img/2.png)

Depois  

![ITENS](./img/3.png)

### 12° Passo - Stop Firewalld Service
```
systemctl stop firewalld
```

### 13° Passo - Disable SELinux at Next Reboot
```
vim /etc/selinux/config

Ajuste para : disabled
```

Antes 

![ITENS](./img/4.png)

Depois  

![ITENS](./img/5.png)


### 14° Passo - Set SELinux in Permissive Mode
```
setenforce 0
```

### 15° Passo - Inicie o servidor Zabbix e os processos do agente
```
systemctl restart zabbix-server zabbix-agent httpd

systemctl enable zabbix-server zabbix-agent httpd
```
### 16° Passo - Acesse via WEB

```
http>//(IP DO SEU SERVIDOR)/zabbix
```

### 17° Passo - Tela de Bem vindo
![ITENS](./img/6.png)

### 18° Passo - Verificação de pré-requisitos
```
Informe a senha do banco : 123456
```

![ITENS](./img/7.png)

### 19° Passo - Configurar conexão de banco de dados
![ITENS](./img/8.png)

### 20° Passo - Detalhes do servidor Zabbix
![ITENS](./img/9.png)

### 22° Passo - Você instalou com sucesso o frontend do Zabbix.
![ITENS](./img/10.png)

### 23° Passo - Dados de Acesso
```
usuario: Admin
Senha: zabbix
```
