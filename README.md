<h1><center>Projeto de Infraestrutura em Google Cloud Platform (GCP)</center>center</h1>

Este repositório contém a documentação detalhada da arquitetura de um projeto de infraestrutura no Google Cloud Platform (GCP) para o ambiente de produção, utilizando boas práticas de escalabilidade, alta disponibilidade, segurança e otimização de custos. O objetivo é criar um ambiente eficiente, resiliente e automatizado, garantindo integração on-premises e cloud, além de uma estratégia robusta de Disaster Recovery.

<h2>Principais Pontos</h2><br/>

[Documentação da infraestrutura](infra.md)
  Dimensionamento de Recursos: Autoscaling de VMs, uso de Kubernetes (GKE) e soluções serverless para otimização de carga.<br/>
  Armazenamento de Dados: Soluções gerenciadas como Cloud SQL e Cloud Storage. <br/>

[Estratégia de FinOps](finops.md)
  Monitoramento contínuo de custos, automação de provisionamento e escalabilidade eficiente.<br/>
<b>Topologia de Rede:</b> Configuração de redes públicas e privadas, firewalls, Cloud Armor e Load Balancers.<br/>

[Estratégia de Automação](automation.md)
  Terraform e Ansible para provisionamento e configuração da infraestrutura.<br/>

[Plano de Disaster Recovery](disaster_recovery.md)
  Estratégia de backup, failover e testes periódicos para garantir alta disponibilidade.<br/>

[Estratégia de Monitoramento e Observabilidade](monitoring.md)<br/>
  Stack de monitoramento para redes e aplicações, incluindo Google Cloud Operations Suite.<br/>


<h2>Tecnologias Utilizadas</h2><br/>
Compute Engine, Cloud Run e GKE para execução das aplicações.
Cloud SQL e Filestore para armazenamento de dados.
Cloud VPN e Interconnect para integração on-premises.
Terraform e Ansible para automação da infraestrutura.
Cloud Armor e IAM para segurança da aplicação e controle de acesso.


[Visão geral do projeto](README.md)










