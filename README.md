# 🔒 Compartilhamento de Fotos e Vídeos com Samba
ALUNOS: Fco Vitor Castro e Tauã Silva 
## 🖥️ Implementação do Samba para Compartilhamento entre Windows e Linux

Este projeto propõe a configuração de um servidor multimídia baseado em Linux, utilizando Samba para compartilhar arquivos de mídia (fotos e vídeos) de forma segura entre sistemas Windows e Linux em uma rede doméstica ou de pequeno escritório. 

🔹 **Motivação**: Porque o Windows e Linux não possuem compatibilidade nativa para compartilhamento de arquivos. 

🔹 **Vantagens**:

- **Flexibilidade**: Compartilhamento eficiente entre diferentes sistemas operacionais.
- **Eficiência**: Transferência rápida e estável de arquivos de mídia.

## 🛠️ Ferramentas e Softwares Utilizados para a Atividade

- 🔹 **Linux Debian 12.9.0** (servidor Samba)
- 🔹 **Windows 11 Home (versão 23H2)** (cliente)
- 🔹 **Oracle VM VirtualBox 7.0.20** (virtualização)

Os testes serão realizados nos seguintes cenários:
✅ Virtual para Virtual  
✅ Virtual para Física  
✅ Física para Física  

## 🔧 Passo a Passo: Instalação e Configuração do Samba

### 1️⃣ **Atualizar a máquina virtual**
```bash
sudo apt update && sudo apt upgrade -y
```

### 2️⃣ **Instalar o Samba**
```bash
sudo apt install samba -y
```

### 3️⃣ **Criar a pasta para arquivos compartilhados**
```bash
sudo mkdir -p /home/usuario/midias
```

### 4️⃣ **Configurar permissões de acesso**
```bash
sudo chown -R administrador:usuário /home/usuario/midias
sudo chmod -R 777 /home/usuario/midias
```
🔹 *Somente usuários autenticados terão acesso ao diretório.*

### 5️⃣ **Editar a configuração do Samba**
```bash
sudo nano /etc/samba/smb.conf
```
Adicionar a seguinte configuração:
```ini
[Midia]
path = /home/usuario/midias
read only = no
browsable = yes
guest ok = yes
force user = nobody
force group = nogroup
create mask = 0666
directory mask = 0777
veto files = /*.exe/*.sh/*.bat/*.zip/*.rar/*.pdf/*.doc/*.docx/*.xlsx/*.pptx/
veto oplock files = yes
```
🔹 *Essa configuração VETO FILES e VETO OPLOCK restringe o compartilhamento de arquivos que não sejam foto ou midia, garantindo assim a excluisividade da pasta, para a proposta visada pelo projeto*

### 6️⃣ **Reiniciar e verificar o status do Samba**
```bash
sudo systemctl restart smbd
sudo systemctl enable smbd
sudo systemctl status smbd
```

## 📂 Acessando a Pasta Compartilhada no Windows

Para acessar a pasta de mídia no Windows, pressione `WIN + R` e digite:
```plaintext
\\<IP_DO_SERVIDOR>\midia
```


## 🚀 Conclusão e Testes

Após configurar o Samba, testaremos a transferência de arquivos entre os dispositivos e validaremos a segurança do compartilhamento.


🚀 **Obrigado e se divirta com o compartilhamento de midias entre os sistemas operacionais [Vitor Castro]**


