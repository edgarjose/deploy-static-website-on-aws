# Como hospedar um site estático na AWS

# static-website

## Passo 1: Atualizar pacotes do sistema
sudo yum update -y

## Passo 2: Instalar o Apache (HTTPD)
sudo yum install -y httpd

## Passo 3: Adicionar o utilizador ec2-user ao grupo apache
sudo usermod -a -G apache ec2-user

## Passo 4: Alterar a propriedade e permissões dos diretórios
sudo chown -R ec2-user:apache /var/www

sudo chmod 2775 /var/www && find /var/www -type d -exec sudo chmod 2775 {} \;

find /var/www -type f -exec sudo chmod 0664 {} \;

## Passo 5: Baixar e extrair o website estático
 cd /tmp
 
wget https://github.com/edgarjose/festava_live/archive/refs/heads/main.zip
          
unzip main.zip
          
cp -r festava_live-main/* .
          
rm -rf festava_live-main main.zip

## Passo 6: Configurar o Apache para iniciar automaticamente e iniciar o serviço
sudo systemctl enable httpd

sudo systemctl start httpd
