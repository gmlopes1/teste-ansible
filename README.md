# Observações
- Foi criado um ambiente de teste para que eu pudesse criar os scripts e testá-los
- No ambiente criei 1 VM com Ansible, 2 VMs Linux e 1 VM Windows
- As VMs possuíam duas interfaces de rede, uma para manter a conexão entre elas e outra para executar o teste de troca de IP e transferência do arquivo de configuração do Zabbix Agent conforme a rede. 
- O arquivo de configuração do Zabbix-agent foi criado conforme as redes utilizadas no ambiente de teste (192.168.15.0/24 e 192.168.25.0/24)

# Execuções

## Linux Set IP
- Para execução do script é necessário editá-lo especificando o host e as variáveis, que são: a interface, o IP com o prefixo da rede, o gateway e o DNS.
- Para execução do script é necessário que o servidor Ansible já possua conexão com a VM e esteja registrada dentro do arquivo /etc/ansible/hosts

## Linux Install Zabbix Agent
- Pode ser executado para um host ou para um grupo de hosts, desde que seja especificado dentro do script.
- O script faz a instalação do pacote zabbix-agent utilizando o yum, copia o arquivo de configuração baseado na rede da VM e faz o start do serviço.
- Obs.: Para transferência do arquivo de configuração, ele irá verificar a rede da interface "eth1", mas caso seja necessário podemos alterar a interface.

## Windows Set IP
- Para execução do script é necessário editá-lo especificando o host e as variáveis, que são: a interface, o IP, prefixo da rede, o gateway e o DNS.
- Para execução do script é necessário que o servidor Ansible já possua conexão com a VM e esteja registrada dentro do arquivo /etc/ansible/hosts
- O script faz a remoção das configurações atuais da interface de rede e adiciona os novos IPs.
- Obs.: Precisei adicionar os comandos para remoção, pois quando a porta possuí um IP não é possível alterá-lo diretamente, então foi necessário remover as informações para adicionar as novas.

## Windows Install Zabbix Agent
- Pode ser executado para um host ou para um grupo de hosts, desde que seja especificado dentro do script.
- O script faz a cópia dos arquivos de instalação para o(s) host(s) destino, instala o pacote, copia o arquivo de configuração baseado no terceiro octeto da rede e inicia o serviço.

# Comentário Pessoal
- Acredito que em alguns pontos dos scripts exista uma maneira melhor para escrever os códigos, onde por exemplo precisei utilizar os comandos do SO para coletar as informações, pois não consegui encontrar os comandos do Ansible que fizessem isso, como por exemplo nos scripts do Windows em que precisei utilizar os comandos de PowerShell.
