# Apresentação do Trabalho 
Esse trabalho é um desafio passado pelo Compass.UOL no Programa de Estágio Devsecops - Outubro 2025 que se dá à criação e automatização de um script em shell que verifique de 5min em 5min o funcionamento do Web Server Nginx no Ubuntu 20.04.



# Nginx no Ubuntu pelo WSL 

## Passo 1: Windows PowerShell 
Vá na barra de pesquisa do gerenciador de tarefas e pesquise "Windows PowerShell", clique com o botão direito do mouser no item e execute como administrador.



## Passo 2: Instalação do WSL no Windows 
Com o "Windows PowerShell" já aberto, para instalar o WSL digite:

`wsl --install`

Agora segue para a instalação do Ubuntu, digite o camando:

`wsl --install -d Ubuntu-22.04`

Após a finalização da instalação crie um nome de usuário e uma senha em que você usará em alguns momentos.
Para continuar será necessário reniciar seu computador para finalizar a configurações internas do WSL. 
Após iniciar use:

`wsl -l -v`

para verificar se está em funcionamento.

Vá à barra de pesquisa do gerenciador e procure "Ubuntu". Ao encontrar estará pronto para iniciar o próximo passo.



## Passo 3: Servidor Nginx
Primeiro atualize os pacotes do Ubunto com o comando:

`sudo apt update`

Agora, para instalar o Nginx utilize o comando:

`sudo apt install nginx`

Feito isso, para verificar se está rodando corretamente digite:

`sudo systemctl status nginx`

![image](https://github.com/user-attachments/assets/8dda4ff8-0f60-42e1-a6f2-a9913acba7b9)


Para obter confirmação se o nginx está funcionando normalmente acesse: http://localhost/
![image](https://github.com/user-attachments/assets/23b0a1f5-f37f-4a37-90d1-c2ef08697b23)

Assim como na imagem, deve aparecer essa mensagem atestando o bom funcionamento do nginx.



## Passo 4: Criação do Script
Primeira coisa a se fazer nesse passo é criar um deretório, no entanto use o camando:

`mkdir nome_do_diretorio`

Navegue no diretório usando:

`cd nome_do_diretorio`

Agora para iniciar o código, usará o edito `nano`

`nano verificar_nginx.sh`

Adicione o sweguinte código:

```
#!/bin/bash

#Variáveis
DATA_E_HORA=$(date '+%Y-%m-%d %H:%M:%S')
SERVICO="Nginx"
DIRETORIO="/caminho/projeto_script/logs"
ONLINE="${projeto_script}/online.log"
OFFLINE="${projeto_script}/offline.log"

#Verifica o status do Nginx
STATUS=$(systemctl is-active nginx)

#Condição para verificar se o Nginx está online
if [ "$STATUS" = "active" ]; then
    echo "$DATA_E_HORA - $SERVICO - ONLINE - O serviço está ativo." >> $ONLINE
else
    echo "$DATA_E_HORA - $SERVICO - OFFLINE - O serviço não está ativo." >> $OFFLINE
fi`

````

![image](https://github.com/user-attachments/assets/2b916a43-7319-43a9-9b1f-0ea1e7f72b50)


Digite CTRL + O , ENTER para salvar e CTRL + X para sair da edição.

Para permitir o funcionamento do script como rpograma digite:

`chmod +x verificar_nginx.sh`


## Passo 5: Automatização do Script
O script será automatizado utilizando a ferramenta:

`Systemd Timers`

Faça a criação de arquivo de serviço com:

`sudo nano /etc/systemd/system/verificar_nginx.service`

Agora é só adicionar essa parte:

```
[Unit]
Description=Script para checar o status do Nginx

[Service]
Type=simple
ExecStart=/bin/bash /home/seu_usuario/nome_do_diretorio/verificar_nginx.sh

````

Digite CTRL + O , ENTER para salvar e CTRL + X para sair da edição.

Digite o seguinte comando para ativar e inicar o time:

`sudo systemctl enable verificar_nginx.timer`

Iiniciar o timer:

`sudo systemctl start checar_nginx.timer`

Checar status do timer:

`systemctl list-timers `

Checar os logs:

 `journalctl -u checar_nginx.service `
