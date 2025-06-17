# VPN-AWS-AZURE

![multi](https://github.com/user-attachments/assets/69a471e2-73a8-40e9-96b8-763c65d6da39)

[PASSO - PASSO - PROJETO MULTICLOUD VPN AZURE TO AWS.docx](https://github.com/user-attachments/files/20782648/PASSO.-.PASSO.-.PROJETO.MULTICLOUD.VPN.AZURE.TO.AWS.docx)


Configuração Azure e AWS - Passo a Passo

ETAPA 1: CONFIGURAÇÃO NO AZURE
Criar um grupo de recursos no Azure para implantar os recursos
- Nome do Grupo de Recursos: rg_azure_aws_project
- Região: East-US

Criar uma Rede Virtual (VNet)
- Nome do Grupo de Recursos: rg-azure-aws
- Região: East-US
- Nome da VNet: vnet-azure
- Espaço de Endereços IPv4 da VNet (AZURE REDE PRINCIPAL): 10.0.0.0/16  # AZURE REDE PRINCIPAL
- Nome da Sub-rede: subnet-01
- Espaço de Endereços IPv4 da Sub-rede (SUB REDE PRIVADA): 10.0.0.0/24  # SUB REDE PRIVADA

Criar o Gateway VPN
- Nome do Gateway VPN: vpn-azure-aws
- Região: East-US
- Tipo de Gateway: VPN
- SKU: VpnGw1
- Geração: Geração 1
- Rede Virtual: vnet-azure
- Endereço IP Público: pip-vpn-azure-aws
- Tipo de Endereço IP Público: Básico
- Atribuição: Dinâmica
- Modo ativo-ativo habilitado: Desabilitado
- Configurar BGP: Desabilitado


CONFIGURAÇÃO NA AWS

Criar uma VPC (Virtual Private Cloud)
- Nome: my-vpc-01
- CIDR IPv4: 172.16.0.0/16  # REDE AWS

Criar uma sub-rede dentro da VPC
- Nome: my-subnet-01
- Nome da VPC: my-vpc-01
- CIDR IPv4 da VPC: 172.16.0.0/16  # REDE AWS
- CIDR IPv4 da Sub-rede: 172.16.0.0/24  # SUB REDE PUBLICA AWS

Criar um Customer Gateway apontando para o IP público do Azure VPN Gateway
- Endereço IP: IP Público do Gateway VPN do Azure
- Demais configurações: Padrão

Criar o Virtual Private Gateway e anexar à VPC
- Nome: vpg-aws-azure


Criar a conexão Site-to-Site VPN
- Nome: vpn-aws-azure
- Tipo de gateway de destino: Virtual Private Gateway
- Customer Gateway: Existente
- Opções de roteamento: Estático
- Prefixos IP estáticos: 10.0.0.0/24  # SUB REDE PRIVADA
- Demais configurações: Padrão

Baixar o arquivo de configuração
- Fornecedor: Genérico
- Plataforma: Genérico
- Software: Agnóstico ao fornecedor

CONECTANDO O AZURE À AWS
Criar o Local Network Gateway no Azure
- Nome: lng-azure-aws
- Grupo de Recursos: rg-azure-aws
- Região: East-US
- Endereço IP: IP externo do arquivo de configuração
- Espaço(s) de Endereço: 172.16.0.0/16  # REDE AWS


Criar a conexão no Virtual Network Gateway do Azure
- Nome: connection-azure-aws
- Tipo de Conexão: Site-to-Site
- Local Network Gateway: Selecionar o criado anteriormente
- Chave Compartilhada: Do arquivo de configuração
- Esperar até o status mudar para: Conectado

Verificar no Console da AWS se o 1º túnel está ATIVO

CONFIGURAR ACESSO À INTERNET E ROTAS NA AWS

Criar Internet Gateway e anexar à VPC
- Nome: my-internet-gateway

Editar a tabela de rotas associada à VPC
- Destino: 10.0.0.0/24  # SUB REDE PRIVADA - Target: Virtual Private Gateway
- Destino: 0.0.0.0/0 - Target: Internet Gateway

CRIAR MÁQUINAS VIRTUAIS EM AMBAS AS PLATAFORMAS (AZURE E AWS) E TESTAR A CONEXÃO


PASSO A PASSO COM OS PRINTS

Criar um grupo de recursos no Azure para implantar os recursos
- Nome do Grupo de Recursos: rg_azure_aws_project
- Região: East-US
 

Criar uma Rede Virtual (VNet)
- Nome do Grupo de Recursos: rg_azure_aws_project
- Região: East-US
- Nome da VNet: vnet-azure-project
- Espaço de Endereços IPv4 da VNet (AZURE REDE PRINCIPAL): 10.0.0.0/16  # AZURE REDE PRINCIPAL
- Nome da Sub-rede: subnet-01
- Espaço de Endereços IPv4 da Sub-rede (SUB REDE PRIVADA): 10.0.0.0/24  # SUB REDE PRIVADA
Cria uma outra SubRede e marca ela como VIRTUAL NETWORK GATEWAY e o nome padrão dela vai ser  GatewaySubnet
 

Criar o Gateway VPN (Virtual Network Gateway)
- Nome do Gateway VPN: vpn-azure-aws-project
- Região: East-US
- Tipo de Gateway: VPN
- SKU: VpnGw1
- Geração: Geração 1
- Rede Virtual: vnet-azure-project
- Endereço IP Público: pip-vpn-azure-aws-project
- Tipo de Endereço IP Público: Básico
- Atribuição: 
- Modo ativo-ativo habilitado: Desabilitado
- Configurar BGP: Desabilitado


CONFIGURAÇÃO NA AWS

Criar uma VPC (Virtual Private Cloud)
- Nome: my-vpc-01-project
- CIDR IPv4: 172.16.0.0/16 # REDE AWS

Criar uma sub-rede dentro da VPC
- Nome: my-subnet-01-project
- Nome da VPC: my-vpc-01-project
- CIDR IPv4 da VPC: 172.16.0.0/16 # REDE AWS
- CIDR IPv4 da Sub-rede: 172.16.0.0/24 # SUB REDE PUBLICA AWS

Criar um Customer Gateway apontando para o IP público do Azure VPN Gateway
- Endereço IP: IP Público do Gateway VPN do Azure
- Demais configurações: Padrão
 


ENTRA NO Virtual network gateway NA AZURE E VERIFICA O IP QUE MOSTRA EM OVERVIEW
Criar o Virtual Private Gateway e anexar à VPC
- Nome: vpg-aws-azure-project
 

Seleciona a VPC que criamos anteriormente
Criar a conexão Site-to-Site VPN
- Nome: vpn-aws-azure-project
- Tipo de gateway de destino: Virtual Private Gateway
- Customer Gateway: Existente
- Opções de roteamento: Estático
- Prefixos IP estáticos: 10.0.0.0/24  # SUB REDE PRIVADA
- Demais configurações: Padrão



Clicar em Criar Conexão VPN

Baixar o arquivo de configuração
- Fornecedor: Genérico
- Plataforma: Genérico
- Software: Agnóstico ao fornecedor



Clique na VPN e Clique no canto superior direito, BAIXAR a configuração e deixa as seguinte opções igual esta na imagem acim


Abra o documento e pegue os IP para colocar na configuração da AZURE





CONECTANDO O AZURE À AWS
Criar o Local Network Gateway no Azure
- Nome: lng-azure-aws-project
- Grupo de Recursos: rg-azure-aws
- Região: East-US
- Endereço IP: IP externo do arquivo de configuração
- Espaço(s) de Endereço: 172.16.0.0/16 #REDE AWS

PROCURE NO DOCUMENTO O VPW e coloque no local network gateway do azure 
esse ip e da AWS, devemos apontas na AZURE
 


Entre em Local Network Gateways na AZURE


Criar a conexão no Virtual Network Gateway do Azure
- Nome: connection-azure-aws-project
- Tipo de Conexão: Site-to-Site
- Local Network Gateway: Selecionar o criado anteriormente
- Chave Compartilhada: Do arquivo de configuração
- Esperar até o status mudar para: Conectado
 

COLA A CHAVE CRIADA ANTERIORMENTE
Verificar no Console da AWS se o 1º túnel está ATIVO
 

CONFIGURAR ACESSO À INTERNET E ROTAS NA AWS

Criar Internet Gateway e anexar à VPC
- Nome: my-internet-gateway


Editar a tabela de rotas associada à VPC
- Destino: 10.0.0.0/24 # SUB REDE PRIVADA - Target: Virtual Private Gateway
- Destino: 0.0.0.0/0 - Target: Internet Gateway

CRIAR MÁQUINAS VIRTUAIS EM AMBAS AS PLATAFORMAS (AZURE E AWS) E TESTAR A CONEXÃO





