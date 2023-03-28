## **Install and configuration Server TFTP in Dist_Debian** 
1. Antes de tudo configure um servidor na sua maquina, criando um novo perfil de rede, faça:

    1.1. Abra as configurações de rede e clique em criar um novo perfil, nomeie de acordo:
    ![](../tutorial_tftp/Sele%C3%A7%C3%A3o_002.png)
    1.2. Agora nas configurações de IPv4 logo ao lado configure o servidor com as configurações abaixo, faça:
    ![](../tutorial_tftp/Sele%C3%A7%C3%A3o_003.png)
    clique em Adicionar e pronto.


2. Certifique-se que o sistema esta atualizado, faça:
    ~~~
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    sudo apt-get install -f
    sudo apt-get autoremove
    ~~~
3. Criar e configurar o diretório que será utilizado pelo servidor, faça:
    ~~~
    sudo mkdir /home/tftp
    sudo chown tftp:nogroup /home/tftp
    sudo chmod -R 755 /home/tftp
    sudo chmod -R +s /home/tftp
    sudo chmod -R g+w /home/tftp
    ~~~
4. Instale o serviço Daemon do TFTP, faça:
    ~~~
    sudo apt-get install tftpd-hpa
    ~~~
5. Abra com algum editor de texto (no meu caso estou usando o nano) o arquivo de configuração "tftpd-hpa" do tftp, encontrado no caminho "/etc/default", faça:
    ~~~
    sudo nano /etc/default/tftpd-hpa
    ~~~
    O seguinte conteúdo sera exibido:
    ~~~
    # /etc/default/tftpd-hpa

    TFTP_USERNAME="tftp"
    TFTP_DIRECTORY="/var/lib/tftp"
    TFTP_ADDRESS=":69"
    TFTP_OPTIONS="--secure"
    ~~~
    5.1. Altere o valor da variável "TFTP-DIRECTORY" de acordo com o diretório
    criado no passo três, faça:
    ~~~
    TFTP-DIRECTORY="/home/tftp"
    ~~~
    5.2. Altere a variável "TFTP-ADDRESS" de acordo com o IP do servidor e
    a porta de comunicação criado no passo um, faça:
    ~~~
    TFTP-ADDRESS="10.10.0.1:69"
    ~~~
    5.3. Opcionalmente, adicione a opção "-create" na variável "TFTP-OPTIONS", faça:
    ~~~
    TFTP-OPTIONS="--secure --create"
    ~~~
    O resultado final do arquivo "tftpd-hpa" será o seguinte:
    ~~~
    # /etc/default/tftpd-hpa

    TFTP_USERNAME="tftp"
    TFTP_DIRECTORY="/home/tftp"
    TFTP_ADDRESS="10.10.0.1:69"
    TFTP_OPTIONS="--secure --create"
    ~~~
    Salve e feche o arquivo "tftp-hpa".

6. Agora reinicie o serviço tftp para que as configurações feitas possam
ser observadas pelo daemon do tftp, faça:
    ~~~
    service tftpd-hpa restart
    ~~~
7. Caso queira verificar o resultado, faça:
    ~~~
    service tftpd-hpa status
    ~~~
    caso tudo tenha ocorrido corretamente, o seguinte será mostrado:
    
    ![](../tutorial_tftp/Sele%C3%A7%C3%A3o_001.png)






