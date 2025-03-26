<h1><center>Diagrama de arquitetura Cloud</center></h1></br>

<h2>1. Introdução</h2></br>

Este documento apresenta os recursos do Google Cloud utilizados na arquitetura apresentada na imagem e discute as melhores práticas para cada um em termos de performance, otimização de custos, escalabilidade e alta disponibilidade.</br>

<img src="GCP - Infra.png" alt="Diagrama de infraestrutura" /></br>

<h2><center>2. Recursos Utilizados</center></h2></br>

<h3>2.1. Google Kubernetes Engine (GKE)</h3></br>

<b>Descrição:</b> Serviço gerenciado de Kubernetes para orquestração de contêineres.</br>

<h4>Melhores Práticas:</h4></br>

<b>Performance:</b> Utilizar nós otimizados para cargas de trabalho, como máquinas N2 ou C2.</br>

<b>Otimização de Custos:</b> Habilitar escalonamento automático de nós para ajustar recursos conforme a demanda.</br>

<b>Escalabilidade:</b> Utilizar HPA (Horizontal Pod Autoscaler) para escalar pods dinamicamente.</br>

<b>Alta Disponibilidade:</b> Configurar GKE em múltiplas zonas e regiões para resiliência contra falhas.</br>

<h3>2.2. Compute Engine</h3></br>

Descrição: Máquinas virtuais para cargas de trabalho personalizadas.</br>

<h4>Melhores Práticas:</h4></br>

Performance: Escolher tipos de máquinas adequados (E2 para economia, N2/C2 para cargas pesadas).</br>

Otimização de Custos: Utilizar instâncias preemptivas ou Spot VMs para workloads tolerantes a falhas.</br>

Escalabilidade: Configurar Managed Instance Groups (MIGs) com autoscaling.</br>

Alta Disponibilidade: Distribuir instâncias entre múltiplas zonas.</br>

<h3>2.3. Cloud SQL</h3></br>

Descrição: Banco de dados gerenciado (PostgreSQL, MySQL, SQL Server).</br>

<h4>Melhores Práticas:</h4></br>

Performance: Ajustar tamanho das instâncias com base na carga de trabalho.</br>

Otimização de Custos: Utilizar escalonamento automático de armazenamento e backups automáticos.</br>

Escalabilidade: Configurar réplicas de leitura para melhorar desempenho.</br>

Alta Disponibilidade: Ativar alta disponibilidade (HA) e replicação entre regiões.</br>

<h3>2.4. Cloud Storage</h3></br>

Descrição: Armazenamento de objetos escalável.</br>

<h4>Melhores Práticas:</h4></br>

Performance: Usar classes de armazenamento adequadas (Standard para acesso frequente, Nearline para acesso esporádico, Coldline para backup).</br>

Otimização de Custos: Configurar regras de ciclo de vida para migração automática de classes de armazenamento.</br>

Escalabilidade: Armazenamento ilimitado e replicação automática.</br>

Alta Disponibilidade: Ativar replicação multi-região para redundância.</br>

<h3>2.5. Filestore</h3></br>

Descrição: Serviço de armazenamento de arquivos compartilhado via NFS.</br>

<h4>Melhores Práticas:</h4></br>

Performance: Utilizar classes de alto desempenho (Enterprise para baixa latência).</br>

Otimização de Custos: Escolher classes Standard para cargas menos exigentes.</br>

Escalabilidade: Expandir armazenamento dinamicamente.</br>

Alta Disponibilidade: Configurar redundância e snapshots.</br>

<h3>2.6. Cloud Load Balancing</h3></br>

Descrição: Balanceador de carga global para distribuir tráfego.</br>

<h4>Melhores Práticas:</h4></br>

Performance: Usar balanceamento global para menor latência.</br>

Otimização de Custos: Configurar regras de roteamento eficientes para evitar consumo excessivo.</br>

Escalabilidade: Configurar autoscaling para suportar variações de tráfego.</br>

Alta Disponibilidade: Implementar em múltiplas regiões para failover automático.</br>

<h3>2.7. Cloud Armor</h3></br>

Descrição: Firewall para proteger contra ataques DDoS e outras ameaças.</br>

<h4>Melhores Práticas:</h4></br>

Performance: Configurar regras para mitigar ataques sem impactar usuários legítimos.</br>

Otimização de Custos: Aplicar políticas apenas onde necessário.</br>

Escalabilidade: Proteção automática contra tráfego malicioso em grande escala.</br>

Alta Disponibilidade: Configuração integrada ao Load Balancing para proteção contínua.</br>

<h3>2.8. Cloud VPN</h3></br>

Descrição: Conexão segura entre on-premises e Google Cloud.</br>

<h4>Melhores Práticas:</h4></br>

Performance: Usar VPN HA para maior largura de banda.</br>

Otimização de Custos: Avaliar o uso de Interconnect para cargas pesadas.</br>

Escalabilidade: Configurar múltiplos túneis para maior resiliência.</br>

Alta Disponibilidade: Implementar failover automático.</br>

<h3>2.9. Cloud DNS</h3></br>

Descrição: Serviço gerenciado de DNS.</br>

<h4>Melhores Práticas:</h4></br>

Performance: Resolver DNS com baixa latência globalmente.</br>

Otimização de Custos: Utilizar registros TTL adequados para evitar consultas excessivas.</br>

Escalabilidade: Suporta alto volume de consultas automaticamente.</br>

Alta Disponibilidade: Distribuição em múltiplas regiões para redundância.</br>

<h3>2.10. Cloud Key Management (KMS)</h3></br>

Descrição: Gerenciamento de chaves de criptografia.</br>

<h4>Melhores Práticas:</h4></br>

Performance: Integrar com serviços do Google Cloud para baixa latência.</br>

Otimização de Custos: Usar chaves gerenciadas pelo Google para evitar custos extras.</br>

Escalabilidade: Suporte a múltiplas chaves e políticas de rotação automatizadas.</br>

Alta Disponibilidade: Replicação automática das chaves.</br>

<h3>2.11. Cloud Monitoring e Logging</h3></br>

Descrição: Solução de monitoramento e análise de logs.</br>

<h4>Melhores Práticas:</h4></br>

Performance: Criar dashboards personalizados para insights em tempo real.</br>

Otimização de Custos: Configurar retenção de logs apenas pelo período necessário.</br>

Escalabilidade: Ajustar métricas para monitoramento automático.</br>

Alta Disponibilidade: Alertas em tempo real para evitar falhas.</br>

<h3>2.12. BigQuery</h3></br>

Descrição: Data warehouse serverless para análise de grandes volumes de dados.</br>

<h4>Melhores Práticas:</h4></br>

Performance: Otimizar consultas usando partições e clustering.</br>

Otimização de Custos: Usar tabelas externas e modelos de preço adequados.</br>

Escalabilidade: Processamento massivo de dados sem necessidade de provisionamento.</br>

Alta Disponibilidade: Serviço totalmente gerenciado e redundante.</br>

<h3>2.13. DevOps - Terraform e GitHub</h3></br>

Descrição: Infraestrutura como Código (IaC) e versionamento.</br>

<h4>Melhores Práticas:</h4></br>

Performance: Automação de deploys para redução de tempo de provisionamento.</br>

Otimização de Custos: Gerenciamento eficiente dos recursos provisionados.</br>

Escalabilidade: Infraestrutura definida como código, permitindo ajustes dinâmicos.</br>

Alta Disponibilidade: Pipelines automatizados para recuperação rápida de falhas.</br>

