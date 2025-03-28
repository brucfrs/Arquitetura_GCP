<h1><center>Projeto de Infraestrutura em Google Cloud Platform (GCP)</center></h1>

Este repositório contém a documentação detalhada da arquitetura de um projeto de infraestrutura no Google Cloud Platform (GCP) para o ambiente de produção, utilizando boas práticas de escalabilidade, alta disponibilidade, segurança e otimização de custos. O objetivo é criar um ambiente eficiente, resiliente e automatizado, garantindo integração on-premises e cloud, além de uma estratégia robusta de Disaster Recovery.

<h2>Principais Pontos</h2><br/>

[Documentação da infraestrutura](infra.md)<br/>
  Diagrama da arquitetura em ambiente do Google Cloud com a lista de recursos utilizados.<br/>

[Estratégia de FinOps](finops.md)<br/>
  Monitoramento contínuo de custos, automação de provisionamento e escalabilidade eficiente.<br/>

[Topologia de Rede](network.md)<br/>
  Configuração de redes públicas e privadas, firewalls, Cloud Armor e Load Balancers.<br/>

[Estratégia de Automação](automation.md)<br/>
  Terraform e Github para provisionamento e configuração da infraestrutura.<br/>

[Plano de Disaster Recovery](disaster_recovery.md)<br/>
  Estratégia de backup, failover e testes periódicos para garantir alta disponibilidade.<br/>

[Estratégia de Monitoramento e Observabilidade](monitoring.md)<br/>
  Stack de monitoramento para redes e aplicações, incluindo Google Cloud Operations Suite.<br/>


<h2>Tecnologias Utilizadas</h2><br/>
•	Cloud DNS para hospedagem do dominio e resoluçãoo de nomes.<br/>
•	Cloud Load Balancing para balanceamento de carga e redirecionamento de requisições.<br/>
•	Cloud Armor e IAM para segurança da aplicação e controle de acesso.<br/>
•	Compute Engine e GKE para execução das aplicações.<br/>
•	Cloud SQL e Filestore e Cloud Storage para armazenamento de dados.<br/>
•	Cloud VPN e/ou Interconnect para integração on-premises.<br/>
•	Cloud Nat para saida de internet de forma segura para atualização de software e S.O..<br/>
•	Terraform para automação da infraestrutura.<br/>
•	Cloud Firewall Rules para liberações e bloqueios de trafegos de redes.<br/>
•	Cloud KMS para gerenciamento de chaves de criptografia de dados em transito e repouso..<br/>
•	Cloud Logging e Cloud Monitoring para auditoria e monitoramento.<br/>
•	Big Query e Looker para acompanhamento de custos dos projetos.<br/>










