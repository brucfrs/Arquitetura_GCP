<h1><center>Projeto de Infraestrutura em Google Cloud Platform (GCP)</center>center</h1>

Este repositório contém a documentação e implementação de um projeto de infraestrutura no Google Cloud Platform (GCP), utilizando boas práticas de escalabilidade, segurança e otimização de custos. O objetivo é criar um ambiente eficiente, resiliente e automatizado, garantindo integração on-premises e cloud, além de uma estratégia robusta de Disaster Recovery.

<h2>Principais Componentes<h2><br/>
<b>Dimensionamento de Recursos:</h2>b Autoscaling de VMs, uso de Kubernetes (GKE) e soluções serverless para otimização de carga.
FinOps: Monitoramento contínuo de custos, automação de provisionamento e escalabilidade eficiente.
Topologia de Rede: Configuração de redes públicas e privadas, firewalls, Cloud Armor e Load Balancers.
Orquestração e Automação: Terraform e Ansible para provisionamento e configuração da infraestrutura.
Plano de Disaster Recovery (DR): Estratégia de backup, failover e testes periódicos para garantir alta disponibilidade.
Monitoramento e Observabilidade: Stack de monitoramento para redes e aplicações, incluindo Google Cloud Operations Suite.
Segurança e Modelo OSI: Aplicação de camadas do modelo OSI para diagnóstico e proteção do tráfego na solução.
🚀 Tecnologias Utilizadas
Compute Engine, Cloud Run e GKE para execução das aplicações.
Cloud SQL e Filestore para armazenamento de dados.
Cloud VPN e Interconnect para integração on-premises.
Terraform e Ansible para automação da infraestrutura.
Cloud Armor e IAM para segurança da aplicação e controle de acesso.


[Visão geral do projeto](README.md)

[Documentação da infraestrutura](infra.md)

[Estratégia de FinOps](finops.md)

[Estratégia de Automação](automation.md)

[Plano de Disaster Recovery](disaster_recovery.md)

[Estratégia de Monitoramento e Observabilidade](monitoring.md)
