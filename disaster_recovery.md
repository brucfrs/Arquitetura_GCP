<h1><center>Plano de Disaster Recovery no Google Cloud</center></h1></br>

<h3>1. Estratégia de Recuperação e Objetivos de DR</h3></br>
 
O plano de DR segue um modelo Active-Passive, garantindo que os serviços críticos possam ser restaurados rapidamente em caso de falha na região principal.</br>

<h4>Objetivos de recuperação:</h4>

&nbsp; &nbsp; •	RPO (Recovery Point Objective): ≤ 5 minutos → Garantir mínima perda de dados.</br>

&nbsp; &nbsp; •	RTO (Recovery Time Objective): ≤ 15 minutos → Restaurar serviços rapidamente.</br>

<h4>Melhores práticas seguidas:</h4>

&nbsp; &nbsp; •	Definição clara de RPO e RTO alinhados aos requisitos de negócio.</br>

&nbsp; &nbsp; •	Replicação assíncrona entre regiões para reduzir perda de dados.</br>

&nbsp; &nbsp; •	Automação para ativação do ambiente DR via Terraform e GitHub Actions.</br></br>

<h3>2. Backup e Replicação de Dados</h3></br>

A arquitetura utiliza estratégias híbridas de backup para garantir a proteção e recuperação de dados.</br>

<h4>2.1 Backup do Cloud SQL</h4></br>

&nbsp; &nbsp; •	Cloud SQL HA com replicação assíncrona entre regiões PRD (us-east1) e DR (us-west1).</br>

&nbsp; &nbsp; •	Snapshots diários armazenados no Cloud Storage com retenção de 30 dias.</br>

&nbsp; &nbsp; •	Backups incrementais a cada 5 minutos para minimizar perda de dados.</br>

<h4>2.2 Backup do Filestore e Persistent Disks</h4></br>

&nbsp; &nbsp; •	Filestore com snapshots automáticos diários armazenados no Cloud Storage Nearline.</br>

&nbsp; &nbsp; •	Persistent Disks replicados entre regiões para recuperação rápida.</br>

<h4>2.3 Backup de Configuração e Infraestrutura</h4></br>

&nbsp; &nbsp; •	Terraform State Files armazenados no Cloud Storage para recriação da infraestrutura.</br>

&nbsp; &nbsp; •	Configurações do Kubernetes (GKE) versionadas no GitHub.</br>

&nbsp; &nbsp; •	Cloud Logging e Monitoring armazenados no BigQuery para auditoria.</br>

<h4>Melhores práticas seguidas:</h4>

&nbsp; &nbsp; •	Uso de diferentes classes de armazenamento para otimizar custo e recuperação.</br>

&nbsp; &nbsp; •	Testes periódicos de restauração para validar integridade dos backups.</br>

&nbsp; &nbsp; •	Automação para criar snapshots regulares e monitorar falhas.</br></br>

<h3>3. Estratégia de Failover</h3></br>

&nbsp; &nbsp; •	A arquitetura foi projetada para failover automatizado em caso de falha na região PRD.</br>

<h4>3.1 Cloud Load Balancing</h4></br>

&nbsp; &nbsp; •	Balanceador de carga global redireciona tráfego para a região DR em caso de falha na PRD.</br>

&nbsp; &nbsp; •	Cloud Armor mantém políticas de segurança ativas mesmo após failover.</br>

&nbsp; &nbsp; •	Failover baseado em Health Checks, garantindo que somente instâncias saudáveis recebam tráfego.</br>

<h4>3.2 Cloud DNS</h4></br>

&nbsp; &nbsp; •	DNS failover automático → Se a VPC PRD falhar, o tráfego é direcionado para DR.</br>

&nbsp; &nbsp; •	TTL reduzido para atualização rápida dos registros DNS.</br>

<h4>3.3 Failover de Banco de Dados</h4></br>

&nbsp; &nbsp; •	Cloud SQL replica dados de PRD para DR em tempo real.</br>

&nbsp; &nbsp; •	Em caso de falha, o ambiente DR assume a carga operacional.</br>

<h4>3.4 Failover de Aplicações</h4></br>

&nbsp; &nbsp; •	Compute Engine e GKE no ambiente DR aguardam ativação via Terraform.</br>

&nbsp; &nbsp; •	Armazenamento de imagens no Artifact Registry compartilhado entre regiões.</br>

&nbsp; &nbsp; •	GKE realiza escalonamento automático conforme a carga aumenta na região DR.</br>

<h4>Melhores práticas seguidas:</h4>

&nbsp; &nbsp; •	Automação do failover com Terraform.</br>

&nbsp; &nbsp; •	Simulação de falhas para validar a resposta do sistema.</br>

&nbsp; &nbsp; •	Monitoramento contínuo da saúde dos serviços para failover proativo.</br></br>

<h3>4. Testes Periódicos de Disaster Recovery</h3></br>

Para garantir que o plano de DR funcione conforme esperado, são realizados testes regulares de recuperação.</br>

<h4>4.1 Teste de Recuperação do Banco de Dados</h4></br>

&nbsp; &nbsp; •	Restaurar um backup recente do Cloud SQL na região DR.</br>

&nbsp; &nbsp; •	Validar integridade dos dados e tempo de recuperação.</br>

<h4>4.2 Teste de Failover</h4></br>

&nbsp; &nbsp; •	Simular falha do Load Balancer na PRD e verificar redirecionamento do tráfego para DR.</br>

&nbsp; &nbsp; •	Testar tempo de resposta do DNS e migração de serviços para DR.</br>

<h4>4.3 Teste de Restauração de Infraestrutura</h4></br>

&nbsp; &nbsp; •	Executar Terraform Apply para recriar serviços no ambiente DR.</br>

&nbsp; &nbsp; •	Validar configuração do GKE e Compute Engine.</br>

<h4>4.4 Teste de Backup e Restauração</h4></br>

&nbsp; &nbsp; •	Recuperar arquivos do Cloud Storage Nearline e testar tempos de acesso.</br>

&nbsp; &nbsp; •	Executar restauração de snapshots do Filestore e Persistent Disks.</br>

<h4>4.5 Teste de Segurança</h4></br>

&nbsp; &nbsp; •	Simular ataques DDoS e verificar resposta do Cloud Armor.</br>

&nbsp; &nbsp; •	Testar regras de firewall para evitar acessos indevidos após failover.</br>

<h4>Melhores práticas seguidas:</h4>

&nbsp; &nbsp; •	Execução de testes DR sem impactar produção.</br>

&nbsp; &nbsp; •	Documentação das falhas e otimizações necessárias.</br>

&nbsp; &nbsp; •	Automação dos testes para reduzir erros manuais.</br>
