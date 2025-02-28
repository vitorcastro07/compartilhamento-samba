# compartilhamento-samba
Samba para Compartilhamento de Mídia entre Windows e Linux (Fotos e Mídia):
Desenvolver um servidor multimídia baseado em Linux com Samba que permita o compartilhamento de grandes arquivos de mídia (fotos, vídeos) entre sistemas Windows e Linux em uma rede doméstica ou de pequeno escritório. Mas por que para compartilhar precisamos utilizar esse método? Porque o windows e o linux não são compatíveis entre si. Portanto esse projeto apresenta um meio para quem deseja ou precisa fazer esse compartilhamento entre essas duas máquinas.  Também incluindo a criação de uma interface simples para visualizar ou editar os arquivos. 

**● Vamos usar o samba na máquina linux Debian 12.9.0 para fazer conexão com windows 11 home versão 23H2, criando um diretório para o envio de imagens e vídeos JPG e PNG para imagens e MP4 e MOV para vídeos.**
O software utilizado para a emulação é o Oracle VM VirtualBox na versão 7.0.20 para a virtualização das máquinas tanto Windows e Linux.

Vamos realizar os teste com as maneiras possíveis de utilização das máquinas sendo eles virtual  para virtual, virtual para física e física para física. Tendo em vista a utilização de duas máquinas físicas para uma virtual .

Após apresentar os códigos e como ensinar fazer esse compartilhamento de arquivos, vamos verificar se os arquivos desejados estão na pasta certa, fazer a visualização e finalizar a apresentação.

➔ PASSO A PASSO EM CODIGOS :

**● Primeiro vamos atualizar a máquina virtual através do terminal com os comandos:**
sudo apt update && sudo apt upgrade 


**● Para fazer a instalação do samba pelo terminal do Debian vamos utilizar o comando**
sudo apt install samba


**● Agora vamos criar a pasta na qual vamos alocar os arquivos de midia que vão ser compartilhados entre os sistemas operacionais com o comando**
  
sudo mkdir -p /home/usuario/midias



**● Agora vamos alterar as permissões dos arquivos para ficarmos com acesso irrestrito com os comandos**
'Seu usuário administrador:seu usuário comum'

sudo chown -R blackk:aula /home/usuario/midias

sudo  chmod -R 777 /home/usuario/midias


**●Agora é necessário configurarmos o samba para que seja possível o windows acessar a pasta compartilhada com o comando**
sudo nano /etc/samba/smb.conf 

como editar o arquivo:

[Midia]
path = /home/usuario/midias
read only = no
browsable = yes
guest ok = yes
force user = nobody
force group = nogroup
create mask = 0666
directory mask = 0777
veto files = /*.txt/*.exe/*.sh/*.bat/*.zip/*.rar /*.pdf/*.doc/*.docx/*.xlsx/*.pptx/ 
veto oplock files = yes

OBSERVAÇÃO: A funcionalidade do **veto files** e **veto oplock**

**●Agora vamos reiniciar o samba e verificar se ele esta rodando corretamente com os comandos:**

sudo systemctl restart smbd

sudo systemctl enable smbd 

sudo systemctl status smbd

**● Por fim, para acessarmos a pasta no windows pressionamos a tecla WIN + R e vamos digitar o ip da sua máquina virtual e depois o caminho da pasta de mídia dessa maneira:**

EXEMPLO = \\ ip do servidor\midia 

