# ☁️ Projeto Final — Modernização de Arquitetura AWS

> Projeto de arquitetura Cloud voltado à migração de uma aplicação legada para AWS, partindo de uma estratégia de lift-and-shift e avançando para uma arquitetura modernizada e conteinerizada.

[![Status](https://img.shields.io/badge/status-projeto%20acadêmico-blue)](#status)
[![Cloud](https://img.shields.io/badge/cloud-AWS-orange)](#arquitetura-proposta)
[![Container](https://img.shields.io/badge/container-Kubernetes-326CE5)](#arquitetura-proposta)
[![Database](https://img.shields.io/badge/database-MySQL-4479A1)](#arquitetura-proposta)

---

## Sobre o projeto

O **Projeto Final** documenta uma proposta de migração e modernização de uma arquitetura legada para serviços AWS. Trata-se de uma entrega de arquitetura e documentação: os diagramas representam a arquitetura-alvo, não uma infraestrutura AWS comprovadamente provisionada e em operação.

A iniciativa foi desenvolvida no contexto da **Compass UOL**, com foco na análise da arquitetura existente, definição de uma arquitetura-alvo e avaliação dos serviços necessários para obter maior escalabilidade, resiliência, segurança e eficiência operacional.

## Objetivos

- analisar uma arquitetura monolítica existente;
- propor uma estratégia de migração para AWS;
- utilizar serviços gerenciados sempre que apropriado;
- melhorar escalabilidade e disponibilidade;
- estruturar uma arquitetura conteinerizada;
- incorporar mecanismos de segurança e observabilidade;
- estimar os custos da solução;
- documentar tecnicamente a arquitetura proposta.

## Arquitetura atual

A estrutura legada é composta por três elementos principais:

```text
db01    → MySQL
back01  → APIs
front01 → Aplicação Web
```

A migração inicial considera uma abordagem de **lift-and-shift**, com serviços AWS destinados à movimentação da infraestrutura e do banco de dados.

### Componentes de migração

- AWS Database Migration Service (DMS)
- AWS Server Migration Service / recursos equivalentes de migração

Diagrama da arquitetura atual:

![Arquitetura Atual](image1.png)

## Arquitetura proposta

A arquitetura-alvo proposta utiliza serviços gerenciados e uma camada de containers baseada em Kubernetes. Os componentes abaixo descrevem o desenho técnico recomendado para o cenário acadêmico.

```text
Usuário
   │
   ▼
Route 53
   │
   ▼
CloudFront + WAF
   │
   ▼
Load Balancer
   │
   ▼
Amazon EKS
   │        │
   │        ├──► Amazon EFS
   │        │
   │        └──► Amazon RDS / MySQL
   │
   ▼
CloudWatch
```

### Componentes principais

- **Amazon EKS:** execução e gerenciamento da aplicação conteinerizada;
- **Amazon RDS:** banco de dados MySQL gerenciado;
- **Amazon EFS:** armazenamento compartilhado e persistente;
- **Elastic Load Balancing:** distribuição de tráfego;
- **Amazon CloudFront:** distribuição de conteúdo;
- **AWS WAF:** proteção da aplicação web;
- **Amazon Route 53:** DNS e roteamento;
- **AWS IAM:** controle de identidade e permissões;
- **Amazon CloudWatch:** métricas, logs e observabilidade;
- **AWS Backup:** estratégia de proteção dos dados;
- **AWS CodePipeline / CodeBuild:** automação de CI/CD.

Diagrama da arquitetura proposta:

![Arquitetura Proposta](image2.png)

## Segurança

A arquitetura proposta considera uma estratégia baseada em defesa em profundidade, combinando:

- VPC com segmentação de rede;
- subnets públicas e privadas;
- Security Groups;
- IAM e princípio do menor privilégio;
- WAF na camada de aplicação;
- isolamento do banco de dados;
- backups automatizados;
- monitoramento e logs.

A implementação real deve ser validada conforme requisitos de segurança, compliance e operação do ambiente de destino.

## Alta disponibilidade e resiliência

A proposta utiliza serviços gerenciados e componentes distribuídos para reduzir pontos únicos de falha.

Entre os mecanismos considerados estão:

- EKS para execução escalável;
- RDS com configuração Multi-AZ;
- EFS para armazenamento compartilhado;
- Load Balancer;
- CloudFront;
- mecanismos de backup;
- observabilidade com CloudWatch.

## CI/CD

A arquitetura contempla automação do ciclo de entrega por meio de **AWS CodePipeline** e **AWS CodeBuild**, permitindo estruturar um fluxo de integração e entrega contínuas para a aplicação executada no ambiente Kubernetes.

## Estimativa de custos

O projeto também contempla estimativa de custos utilizando a **AWS Pricing Calculator**.

A estimativa documentada originalmente foi de aproximadamente **US$ 1.213,90/mês**, considerando os componentes e premissas definidos naquele cenário.

Esse valor não deve ser interpretado como preço atual de execução. Custos AWS variam conforme região, capacidade, tráfego, armazenamento, utilização e modelo de contratação.

## Imagens e documentação

O repositório contém diagramas e materiais utilizados para documentar a arquitetura.

Arquivos de referência previstos no material original incluem os diagramas da arquitetura atual e proposta em formato visual/editável.

## Apresentação

O projeto também possui material de apresentação associado à entrega acadêmica original.

## Tecnologias e serviços

| Categoria | Tecnologia / Serviço |
|---|---|
| Cloud | AWS |
| Containers | Kubernetes / Amazon EKS |
| Banco | MySQL / Amazon RDS |
| Storage | Amazon EFS |
| CDN | Amazon CloudFront |
| Segurança | AWS WAF / IAM / Security Groups |
| DNS | Route 53 |
| Balanceamento | Elastic Load Balancing |
| Observabilidade | CloudWatch |
| Backup | AWS Backup |
| CI/CD | CodePipeline / CodeBuild |

## Roadmap

### Fase 1 — Migração

- [x] Análise da arquitetura legada
- [x] Estratégia de lift-and-shift
- [x] Definição dos serviços AWS
- [x] Documentação da arquitetura atual

### Fase 2 — Desenho da arquitetura modernizada

- [x] Proposta de arquitetura baseada em EKS
- [x] Seleção conceitual de RDS
- [x] Seleção conceitual de EFS
- [x] Desenho de balanceamento de carga
- [x] Proposta de CloudFront e WAF
- [x] Definição de Route 53
- [x] Planejamento de observabilidade com CloudWatch
- [x] Inclusão de estratégia de backup no desenho

> Os itens marcados representam componentes definidos na documentação da arquitetura proposta; não comprovam provisionamento ou operação desses serviços na AWS.

### Fase 3 — Evolução técnica

- [ ] Infraestrutura como código
- [ ] Pipeline CI/CD implementado
- [ ] Estratégia formal de secrets
- [ ] Testes automatizados
- [ ] Observabilidade avançada
- [ ] Revisão de custos baseada em workloads reais

## Status

📚 **Projeto acadêmico / arquitetura Cloud documentada.**

O repositório funciona como registro técnico da proposta de migração e modernização desenvolvida durante o projeto.

## Autor

Desenvolvido por **Bruno Silva** no contexto dos estudos e atividades relacionadas a Cloud Computing e arquitetura AWS.

GitHub: `eubruno-coder`

---

**Projeto:** Projeto Final — Modernização AWS  
**Categoria:** Cloud / AWS / Arquitetura  
**Status:** Projeto acadêmico documentado
