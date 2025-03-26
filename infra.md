<h1><center>Diagrama de arquitetura Cloud</center></h1></br>

<h2>1. Introdução</h2></br>

Este documento apresenta os recursos do Google Cloud utilizados na arquitetura apresentada na imagem e discute as melhores práticas para cada um em termos de performance, otimização de custos, escalabilidade e alta disponibilidade.</br>

<img src="GCP - Infra.png" alt="Diagrama de infraestrutura" /></br>

<h2><center>2. Recursos Utilizados</center></h2></br>

<h3>2.1. Google Kubernetes Engine (GKE)</h3></br>

<b>Descrição:</b> Serviço gerenciado de Kubernetes para orquestração de contêineres.</br>

<h4>Melhores Práticas:</h4></br>

<b>Performance:</b> Utilizar nós otimizados para cargas de trabalho, como máquinas N2 ou C2.</br>

<b>FinOps (Otimização de Custos):</b></br>
&nbsp; &nbsp; •	Habilitar escalonamento automático de nós para ajustar recursos conforme a demanda.</br>

&nbsp; &nbsp; •	Usar instâncias Spot para workloads tolerantes a falhas.</br>

&nbsp; &nbsp; •	Ajustar tamanhos de clusters para evitar alocação excessiva de recursos.</br>

Para uma lista mais completa basta clicar [aqui] (finops.md)

<b>Escalabilidade:</b> Utilizar HPA (Horizontal Pod Autoscaler) para escalar pods dinamicamente.</br>

<b>Alta Disponibilidade:</b> Configurar GKE em múltiplas zonas e regiões para resiliência contra falhas.</br></br>

<h3>2.2. Compute Engine</h3></br>

<b>Descrição:</b> Máquinas virtuais para cargas de trabalho personalizadas.</br>

<h4>Melhores Práticas:</h4></br>

<b>Performance:</b> Escolher tipos de máquinas adequados (E2 para economia, N2/C2 para cargas pesadas).</br>

<b>Otimização de Custos:</b></br>
&nbsp; &nbsp; •	Utilizar instâncias preemptivas ou Spot VMs para workloads tolerantes a falhas.</br>

&nbsp; &nbsp; •	Dimensionar máquinas conforme a necessidade real, evitando superprovisionamento.</br>

&nbsp; &nbsp; •	Implementar desligamento automático de instâncias ociosas.</br>

&nbsp; &nbsp; •	Aplicar descontos por uso contínuo (CUDs - Committed Use Discounts).</br>

&nbsp; &nbsp; •	Migrar workloads para máquinas otimizadas para preço/desempenho.</br>

<b>Escalabilidade:</b> Configurar Managed Instance Groups (MIGs) com autoscaling.</br>

<b>Alta Disponibilidade:</b> Distribuir instâncias entre múltiplas zonas.</br></br>

<h3>2.3. Cloud SQL</h3></br>

<b>Descrição:</b> Banco de dados gerenciado (PostgreSQL, MySQL, SQL Server).</br>

<h4>Melhores Práticas:</h4></br>

<b>Performance:</b> Ajustar tamanho das instâncias com base na carga de trabalho.</br>

<b>Otimização de Custos:</b> Utilizar escalonamento automático de armazenamento e backups automáticos.</br>

<b>Escalabilidade:</b> Configurar réplicas de leitura para melhorar desempenho.</br>

<b>Alta Disponibilidade:</b> Ativar alta disponibilidade (HA) e replicação entre regiões.</br></br>

<h3>2.4. Cloud Storage</h3></br>

<b>Descrição:</b> Armazenamento de objetos escalável.</br>

<h4>Melhores Práticas:</h4></br>

<b>Performance:</b> Usar classes de armazenamento adequadas (Standard para acesso frequente, Nearline para acesso esporádico, Coldline para backup).</br>

<b>Otimização de Custos:</b> Configurar regras de ciclo de vida para migração automática de classes de armazenamento.</br>

<b>Escalabilidade:</b> Armazenamento ilimitado e replicação automática.</br>

<b>Alta Disponibilidade:</b> Ativar replicação multi-região para redundância.</br></br>

<h3>2.5. Filestore</h3></br>

<b>Descrição:</b> Serviço de armazenamento de arquivos compartilhado via NFS.</br>

<h4>Melhores Práticas:</h4></br>

<b>Performance:</b> Utilizar classes de alto desempenho (Enterprise para baixa latência).</br>

<b>Otimização de Custos:</b> Escolher classes Standard para cargas menos exigentes.</br>

<b>Escalabilidade:</b> Expandir armazenamento dinamicamente.</br>

<b>Alta Disponibilidade:</b> Configurar redundância e snapshots.</br></br>

<h3>2.6. Cloud Load Balancing</h3></br>

<b>Descrição:</b> Balanceador de carga global para distribuir tráfego.</br>

<h4>Melhores Práticas:</h4></br>

<b>Performance:</b> Usar balanceamento global para menor latência.</br>

<b>Otimização de Custos:</b> Configurar regras de roteamento eficientes para evitar consumo excessivo.</br>

<b>Escalabilidade:</b> Configurar autoscaling para suportar variações de tráfego.</br>

<b>Alta Disponibilidade:</b> Implementar em múltiplas regiões para failover automático.</br></br>

<h3>2.7. Cloud Armor</h3></br>

<b>Descrição:</b> Firewall para proteger contra ataques DDoS e outras ameaças.</br>

<h4>Melhores Práticas:</h4></br>

<b>Performance:</b> Configurar regras para mitigar ataques sem impactar usuários legítimos.</br>

<b>Otimização de Custos:</b> Aplicar políticas apenas onde necessário.</br>

<b>Escalabilidade:</b> Proteção automática contra tráfego malicioso em grande escala.</br>

<b>Alta Disponibilidade:</b> Configuração integrada ao Load Balancing para proteção contínua.</br></br>

<h3>2.8. Cloud VPN</h3></br>

<b>Descrição:</b> Conexão segura entre on-premises e Google Cloud.</br>

<h4>Melhores Práticas:</h4></br>

<b>Performance:</b> Usar VPN HA para maior largura de banda.</br>

<b>Otimização de Custos:</b> Avaliar o uso de Interconnect para cargas pesadas.</br>

<b>Escalabilidade:</b> Configurar múltiplos túneis para maior resiliência.</br>

<b>Alta Disponibilidade:</b> Implementar failover automático.</br></br>

<h3>2.9. Cloud DNS</h3></br>

<b>Descrição:</b> Serviço gerenciado de DNS.</br>

<h4>Melhores Práticas:</h4></br>

<b>Performance:</b> Resolver DNS com baixa latência globalmente.</br>

<b>Otimização de Custos:</b> Utilizar registros TTL adequados para evitar consultas excessivas.</br>

<b>Escalabilidade:</b> Suporta alto volume de consultas automaticamente.</br>

<b>Alta Disponibilidade:</b> Distribuição em múltiplas regiões para redundância.</br></br>

<h3>2.10. Cloud Key Management (KMS)</h3></br>

<b>Descrição:</b> Gerenciamento de chaves de criptografia.</br>

<h4>Melhores Práticas:</h4></br>

<b>Performance:</b> Integrar com serviços do Google Cloud para baixa latência.</br>

<b>Otimização de Custos:</b> Usar chaves gerenciadas pelo Google para evitar custos extras.</br>

<b>Escalabilidade:</b> Suporte a múltiplas chaves e políticas de rotação automatizadas.</br>

<b>Alta Disponibilidade:</b> Replicação automática das chaves.</br></br>

<h3>2.11. Cloud Monitoring e Logging</h3></br>

<b>Descrição:</b> Solução de monitoramento e análise de logs.</br>

<h4>Melhores Práticas:</h4></br>

<b>Performance:</b> Criar dashboards personalizados para insights em tempo real.</br>

<b>Otimização de Custos:</b> Configurar retenção de logs apenas pelo período necessário.</br>

<b>Escalabilidade:</b> Ajustar métricas para monitoramento automático.</br>

<b>Alta Disponibilidade:</b> Alertas em tempo real para evitar falhas.</br></br>

<h3>2.12. BigQuery</h3></br>

<b>Descrição:</b> Data warehouse serverless para análise de grandes volumes de dados.</br>

<h4>Melhores Práticas:</h4></br>

<b>Performance:</b> Otimizar consultas usando partições e clustering.</br>

<b>Otimização de Custos:</b> Usar tabelas externas e modelos de preço adequados.</br>

<b>Escalabilidade:</b> Processamento massivo de dados sem necessidade de provisionamento.</br>

<b>Alta Disponibilidade:</b> Serviço totalmente gerenciado e redundante.</br></br>

<h3>2.13. DevOps - Terraform e GitHub</h3></br>

<b>Descrição:</b> Infraestrutura como Código (IaC) e versionamento.</br>

<h4>Melhores Práticas:</h4></br>

<b>Performance:</b> Automação de deploys para redução de tempo de provisionamento.</br>

<b>Otimização de Custos:</b> Gerenciamento eficiente dos recursos provisionados.</br>

<b>Escalabilidade:</b> Infraestrutura definida como código, permitindo ajustes dinâmicos.</br>

<b>Alta Disponibilidade:</b> Pipelines automatizados para recuperação rápida de falhas.</br>

