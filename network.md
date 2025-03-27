<h1><center>Topologia de Rede e Configuração de Segurança no Google Cloud</center></h1></br>

<h3>1. Estrutura da Rede e Configuração de Subnets</h3></br>

A arquitetura apresentada utiliza uma VPC híbrida com comunicação entre On-Premises e Google Cloud, garantindo redundância, escalabilidade e segurança.

<h4>1.1 VPCs e Subnets</h4></br>

Duas VPCs distintas (PRD e DR) para segmentação de tráfego e isolamento de falhas.</br>

<b>Regiões e zonas:</br></b>

&nbsp; &nbsp; •	PRD → us-east1</br>

&nbsp; &nbsp; •	DR → us-west1</br>

<b>Sub-redes públicas e privadas em ambas as VPCs:</b>

&nbsp; &nbsp; •	Subnet Pública → Para comunicação externa via Cloud NAT.

&nbsp; &nbsp; •	Subnet Privada → Hospeda os serviços internos e bancos de dados, isolados da internet.

<h4>Melhores práticas seguidas:</h4>

&nbsp; &nbsp; •	Uso de Private Services Access e Private Google Access para serviços internos sem exposição direta.</br>

&nbsp; &nbsp; •	Cloud NAT em subnets privadas para saída segura sem necessidade de IPs públicos.</br>

&nbsp; &nbsp; •	Subnets distribuídas em múltiplas zonas dentro da região, garantindo alta disponibilidade.</br>

<h3>2. Segurança e Controle de Tráfego</h3></br>

A configuração segue Zero Trust e Defesa em Profundidade, garantindo proteção de perímetro e segmentação de redes.

<h4>2.1 Firewall Rules</h4></br>

Restrições de entrada e saída baseadas em princípios de menor privilégio.</br>

<h4>Principais regras configuradas:</h4>

&nbsp; &nbsp; •	Permitir acesso SSH/RDP apenas para administradores internos via Cloud IAM.</br>

&nbsp; &nbsp; •	Bloquear tráfego direto da internet para as instâncias e Banco de Dados privados.</br>

&nbsp; &nbsp; •	Permitir somente comunicação interna entre VPCs via VPC Peering.</br>

&nbsp; &nbsp; •	Regras explícitas de negação para tráfego suspeito.</br>

<h4>Melhores práticas seguidas:</h4>

&nbsp; &nbsp; •	Uso de Cloud IAM para gerenciar políticas de acesso.</br>

&nbsp; &nbsp; •	Aplicação de políticas de firewall baseadas em identidade (IAM) para granularidade.</br>

&nbsp; &nbsp; •	Negação explícita para portas e protocolos não utilizados.</br>

<h3>3. Proteção Perimetral com Cloud Armor</h3></br>

O Cloud Armor está configurado no Load Balancer Global, garantindo proteção contra ameaças DDoS e injeção de tráfego malicioso.</br>

<h4>Políticas de proteção ativadas:</h4>

&nbsp; &nbsp; • Bloqueio de IPs suspeitos (geolocalização).</br>

&nbsp; &nbsp; • Regras de mitigação contra ataques Layer 7 (Web Application Firewall - WAF).</br>

&nbsp; &nbsp; • Regras personalizadas para bloquear scanners de vulnerabilidades.</br>

<h4>Melhores práticas seguidas:</h4>

&nbsp; &nbsp; • Aplicação de políticas baseadas em comportamento para tráfego legítimo.</br>

&nbsp; &nbsp; • Integração com Cloud Logging e Monitoring para auditorias em tempo real.</br>

&nbsp; &nbsp; • Redundância de mitigação utilizando múltiplos filtros e listas de controle.</br>

<h3>4. Balanceamento de Carga e Alta Disponibilidade</h3></br>

O Cloud Load Balancing (Global) distribui o tráfego entre as regiões PRD e DR, garantindo failover automático.</br>

<h4>Tipos de Load Balancer utilizados:</h4>

&nbsp; &nbsp; • Global HTTP(S) Load Balancer → Para balancear o tráfego de usuários externos.</br>

&nbsp; &nbsp; • Internal Load Balancer → Distribuição de tráfego entre Compute Engine, GKE e Cloud SQL.</br>

<h4>Configurações avançadas:</h4>

&nbsp; &nbsp; • SSL/TLS ativo com Managed Certificates.</br>

&nbsp; &nbsp; • Regras de roteamento inteligente → Direcionamento baseado em proximidade e regras de afinidade.</br>

&nbsp; &nbsp; • Configuração de failover para recuperação em DR.</br>

<h4>Melhores práticas seguidas:</h4> 

&nbsp; &nbsp; • Escalonamento automático de backend services.</br>

&nbsp; &nbsp; • GKE e Compute Engine configurados com Managed Instance Groups (MIGs) Autoscaling On.</br>

&nbsp; &nbsp; • Health checks ativos para redirecionamento de tráfego em caso de falhas.</br>

<h3>5. Comunicação Segura entre On-Premises e Google Cloud</h3></br>

A arquitetura utiliza Cloud VPN com High Availability (HA) para conectar On-Premises ao GCP.</br>

<h4>Características da configuração:</h4>

&nbsp; &nbsp; • Túnel IPsec criptografado para tráfego seguro.</br>

&nbsp; &nbsp; • Redundância com múltiplas VPNs garantindo failover automático.</br>

&nbsp; &nbsp; • Rotas dinâmicas via Cloud Router para otimizar conectividade.</br>

<h4>Melhores práticas seguidas:</h4>

&nbsp; &nbsp; • Criptografia AES-256 para comunicação segura.</br>

&nbsp; &nbsp; • Cloud Router configurado para otimizar o roteamento de tráfego.</br>

&nbsp; &nbsp; • Cloud VPN HA ativado para garantir conexão resiliente.</br>

<h3>6. Monitoramento e Logging</h3></br>

A arquitetura inclui Cloud Monitoring e Cloud Logging, fornecendo telemetria em tempo real.</br>

<h4>Componentes ativados:</h4>

&nbsp; &nbsp; • Cloud Logging → Coleta logs de tráfego, firewalls e auditoria.</br>

&nbsp; &nbsp; • Cloud Monitoring → Alertas para eventos críticos e métricas de desempenho.</br>

&nbsp; &nbsp; • BigQuery e Looker → Para análises avançadas.</br>

<h4>Melhores práticas seguidas:</h4>

&nbsp; &nbsp; • Alertas em tempo real para detecção de anomalias.</br>

&nbsp; &nbsp; • Coleta centralizada de logs para auditoria de segurança.</br>

&nbsp; &nbsp; • Dashboard de métricas para rastrear disponibilidade de serviços.</br>

<h3>7. Disaster Recovery e Alta Disponibilidade</h3></br>

A arquitetura inclui um ambiente DR (Disaster Recovery) em us-west1, garantindo continuidade dos serviços em caso de falha na região PRD.</br>

<h4>Principais estratégias:</h4>h4>

&nbsp; &nbsp; • Cloud SQL HA com replicação assíncrona entre regiões.</br>

&nbsp; &nbsp; • Filestore com persistência de dados replicada.</br>

&nbsp; &nbsp; • Failover automático via Load Balancer Global.</br>

<h4>Melhores práticas seguidas:</h4>

&nbsp; &nbsp; • Cross-region replication para recuperação de banco de dados.</br>

&nbsp; &nbsp; • Failover automático com balanceamento de carga inteligente.</br>

&nbsp; &nbsp; • Infraestrutura as Code (IaC) via Terraform para recriação rápida dos serviços.</br>
