#### Apresentação do Trabalho 
Esse trabalho é um desafio passado pelo Compass.UOL no Programa de Estágio Devsecops - Outubro 2025 que se dá à criação e automatização de um script em shell que verifique de 5min em 5min o funcionamento do Web Server Nginx no Ubuntu 20.04.



### Nginx no Ubuntu pelo WSL 

## Passo 1: Windows PowerShell 
Vá na barra de pesquisa do gerenciador de tarefas e pesquise "Windows PowerShell", clique com o botão direito do mouser no item e execute como administrador.

## Passo 2: Instalação do WSL no Windows 
Com o "Windows PowerShell" já aberto, para instalar o WSL digite:

'wsl --install'

Agora segue para a instalação do Ubuntu, digite o camando:

'wsl --install -d Ubuntu-22.04`

Após a finalização da instalação crie um nome de usuário e uma senha em que você usará em alguns momentos.
Para continuar será necessário reniciar seu computador para finalizar a configurações internas do WSL. 
Após iniciar use:
'wsl -l -v'
para verificar se está em funcionamento.

Vá à barra de pesquisa do gerenciador e procure "Ubuntu". Ao encontrar estará pronto para iniciar o próximo passo.

## Passo 3: Servidor Nginx

