# aws-highly-available-web-app
Provisionamento de uma infraestrutura web de alta disponibilidade e tolerante a falhas na AWS utilizando CloudFormation, RDS Aurora, EFS e ALB.


## 📜 Certificação de Conclusão

Provas de execução e conclusão do laboratório do **AWS Skill Builder**:

![Certificado de Conclusão AWS](951a3598-b73c-406a-9515-771bf5123304.pdf)

---

## 🏗️ Arquitetura da Solução

A aplicação foi estruturada em múltiplas camadas de resiliência e desempenho:

- **Rede Multi-AZ (VPC):** Subnets públicas e privadas distribuídas em duas Zonas de Disponibilidade (`us-west-2a` e `us-west-2b`).
- **Banco de Dados Relacional (RDS/Aurora):** Cluster com réplica de leitura para alta disponibilidade.
- **Camada de Cache (ElastiCache):** Redução de latência para consultas no banco de dados.
- **Armazenamento Compartilhado (Amazon EFS):** Sistema de arquivos NFS persistente e criptografado para os servidores web.
- **Computação e Balanceamento de Carga (EC2, Auto Scaling e ALB):** Application Load Balancer gerenciando o tráfego de entrada para um Auto Scaling Group rodando em subnets privadas.

---

## 🛠️ Etapas de Implantação e Evidências

### 1. Implantação da Rede e Infraestrutura de Base (CloudFormation)
Criação automatizada da pilha de rede (`VPCStack`), incluindo Subnets Públicas/Privadas, NAT Gateways e Tabelas de Rota.

![CloudFormation VPCStack](cloud%20formation%20criação%20de%20pilhas.png)

---

### 2. Configuração do Banco de Dados Relacional (Amazon Aurora / RDS)
Implantação do cluster `mydbcluster` com uma instância primária (`mydbcluster-instance-1`) e uma réplica de leitura (`mydbcluster-instance-1-reader`) em Zonas de Disponibilidade distintas.

![RDS Cluster Instance](db%20cluster%20instance.png)

---

### 3. Camada de Armazenamento Compartilhado (Amazon EFS)
Criação do sistema de arquivos `myWPEFS` com suporte a criptografia para compartilhamento de dados entre os nós da aplicação web.

![Amazon EFS](criar%20um%20sistema%20de%20arquivos%20do%20Amazon%20EFS.png)

---

### 4. Camada de Cache em Memória (Amazon ElastiCache)
Provisionamento do cluster de cache para otimização de leitura e performance das requisições.

![ElastiCache Cluster](criando%20cluster.png)

---

### 5. Modelos de Execução e Regras de Segurança
Criação das pilhas com modelos de execução (`LabLaunchTemplate`) e regras de grupo de segurança (`SecurityGroups`) para autorização de tráfego entre a camada web, banco e sistema de arquivos.

![Launch Configuration Stack](criar%20um%20modelo%20de%20execução%20usando%20o%20CloudFormation.png)

---

### 6. Balanceador de Carga de Aplicação (ALB)
Configuração do Application Load Balancer (`myWPAppALB`) público para distribuição de tráfego entre as zonas de disponibilidade.

![Application Load Balancer](grupo%20de%20destino%20e%20um%20balanceador%20de%20carga.png)
