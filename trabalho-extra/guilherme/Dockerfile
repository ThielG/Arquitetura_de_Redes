# Use a imagem base do Ubuntu
FROM ubuntu:latest

# Atualize o sistema e instale o servidor SSH e outros aplicativos
RUN apt-get update && \
    apt-get install -y openssh-server && \
    apt-get install -y vim && \
    apt-get install -y sudo && \
    apt-get install -y nano && \
    apt-get install -y iputils-ping && \
    apt-get install -y net-tools && \
    mkdir /run/sshd

# Configuração do usuário e senha para SSH (não é recomendado em produção)
RUN useradd -rm -d /home/senac -s /bin/bash -g root -G sudo -u 1001 senac && \
    echo 'senac:senac' | chpasswd && \
    echo "senac ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

# Copia o arquivo de configuração SSH para permitir login com senha (não é recomendado em produção)
RUN sed -i 's/#PasswordAuthentication yes/PasswordAuthentication yes/' /etc/ssh/sshd_config

# Inicia o serviço SSH durante a execução do container
CMD ["/usr/sbin/sshd", "-D"]

