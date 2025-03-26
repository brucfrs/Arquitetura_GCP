<h1><center>Projeto de Infraestrutura em Google Cloud Platform (GCP)</center>center</h1>

Este repositório contém a documentação e implementação de um projeto de infraestrutura no Google Cloud Platform (GCP), utilizando boas práticas de escalabilidade, segurança e otimização de custos. O objetivo é criar um ambiente eficiente, resiliente e automatizado, garantindo integração on-premises e cloud, além de uma estratégia robusta de Disaster Recovery.

<h2>Principais Componentes</h2><br/>
<b>Dimensionamento de Recursos:</b> Autoscaling de VMs, uso de Kubernetes (GKE) e soluções serverless para otimização de carga.
<b>FinOps:</b> Monitoramento contínuo de custos, automação de provisionamento e escalabilidade eficiente.
<b>Topologia de Rede:</b> Configuração de redes públicas e privadas, firewalls, Cloud Armor e Load Balancers.
<b>Orquestração e Automação:</b> Terraform e Ansible para provisionamento e configuração da infraestrutura.
<b>Plano de Disaster Recovery (DR):</b> Estratégia de backup, failover e testes periódicos para garantir alta disponibilidade.
<b>Monitoramento e Observabilidade:</b> Stack de monitoramento para redes e aplicações, incluindo Google Cloud Operations Suite.<br/>

<h2>Tecnologias Utilizadas</h2><br/>
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
