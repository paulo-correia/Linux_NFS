# NFS

NFS (acrônimo para Network File System) é um sistema de arquivos distribuídos desenvolvido inicialmente pela Sun Microsystems, Inc., a fim de compartilhar arquivos e diretórios entre computadores conectados em rede, formando assim um diretório virtual.

## Instalação

Toda a instalação é feita como **root**

### Servidor

#### Debian

Instale os seguintes pacotes com o comando:

 `apt-get install nfs-kernel-server nfs-common rpcbind`

Crie uma pasta para compartilhar com o comando mkdir pasta

Edite o arquivo:

 `/etc/hosts.allow`

Colocando portmap= IP(xxx.xxx.xxx.) onde o IP é o que vai acessar o compartilhamento e as permissões.

Edite o arquivo:

 `/etc/exports`

Colocando a pasta que vai compartilhar, os IP's ou \*(qualquer IP) que vão acessar o compartilhamento e as permissões.

**Exemplo:** /pasta xxx.xxx.xxx.xxx/xx(rw,no\_root\_squash) ou /pasta \*(rw,no\_root\_squash)

Reinicie o serviço do NFS com o comando:

 `service nfs-kernel-server restart`

Exporte a configuração com o comando:

 `exportfs -a`

#### CentOS

Instale o pacote nfs-utils com o comando:

 ` yum -y install nfs-utils`

Crie uma pasta para compartilhar com o comando mkdir pasta

Edite o arquivo:

 `/etc/hosts.allow`

Colocando portmap= IP(xxx.xxx.xxx.) onde o IP é o que vai acessar o compartilhamento e as permissões.

Edite o arquivo:

 `/etc/exports`

Colocando a pasta que vai compartilhar, os IP's ou \*(qualquer IP) que vão acessar o compartilhamento e as permissões.

**Exemplo:** /pasta xxx.xxx.xxx.xxx/xx(rw,no\_root\_squash) ou /pasta \*(rw,no\_root\_squash)

Coloque o serviço do NFS para carregar no boot estando com os comandos:

 ```
 systemctl start rpcbind nfs-server
 systemctl enable rpcbind nfs-server
```

### Estação

#### Debian

Instale os seguintes pacotes com o comando:

 ` apt-get install nfs-common `

Crie uma pasta para receber o compartilhamento estando com o comando mkdir pasta

Monte o compartilhamento com o comando:

 `mount IP ou nome_do_servidor:/pasta_compartilhada /pasta_que_recebeu_o_compartilhamento`

Para tornar este compartilhamento permanente edite o arquivo:

 `/etc/fstab`

Colocando no mesmo IP ou /nome\_do\_servidor:/pasta\_compartilhada /pasta\_que\_recebeu\_o\_compartilhamento nfs defaults 0 0

#### CentOS

Instale o pacote nfs-utils com o comando:

 ` yum -y install nfs-utils`

Crie uma pasta para receber o compartilhamento estando com o comando mkdir pasta

Monte a pasta do servidor com o comando:

 ` mount IP ou nome_do_servidor:/pasta_compartilhada pasta_que_recebeu_o_compartilhamento/`

Para tornar este compartilhamento permanente edite o arquivo:

 `/etc/fstab`

Colocando no mesmo IP ou nome\_do\_servidor:/pasta\_compartilhada /pasta\_que\_recebeu\_o\_compartilhamento nfs defaults 0 0