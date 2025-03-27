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
Restrições de entrada e saída baseadas em princípios de menor privilégio.

Principais regras configuradas:

Permitir acesso SSH/RDP apenas para administradores internos via Cloud IAM.

Bloquear tráfego direto da internet para as instâncias privadas.

Permitir somente comunicação interna entre VPCs via VPC Peering.

Regras explícitas de negação para tráfego suspeito.

Melhores práticas seguidas: ✅ Uso de Cloud IAM para gerenciar políticas de acesso.
✅ Aplicação de políticas de firewall baseadas em identidade (IAM) para granularidade.
✅ Negação explícita para portas e protocolos não utilizados.

<h3>3. Proteção Perimetral com Cloud Armor</h3></br>
O Cloud Armor está configurado no Load Balancer Global, garantindo proteção contra ameaças DDoS e injeção de tráfego malicioso.

Políticas de proteção ativadas:

Bloqueio de IPs suspeitos (geolocalização).

Regras de mitigação contra ataques Layer 7 (Web Application Firewall - WAF).

Regras personalizadas para bloquear scanners de vulnerabilidades.

Melhores práticas seguidas: ✅ Aplicação de políticas baseadas em comportamento para tráfego legítimo.
✅ Integração com Cloud Logging e Monitoring para auditorias em tempo real.
✅ Redundância de mitigação utilizando múltiplos filtros e listas de controle.

<h3>4. Balanceamento de Carga e Alta Disponibilidade</h3></br>
O Cloud Load Balancing (Global) distribui o tráfego entre as regiões PRD e DR, garantindo failover automático.

Tipos de Load Balancer utilizados:

Global HTTP(S) Load Balancer → Para balancear o tráfego de usuários externos.

Internal Load Balancer → Distribuição de tráfego entre Compute Engine, GKE e Cloud SQL.

Configurações avançadas:

SSL/TLS ativo com Managed Certificates.

Regras de roteamento inteligente → Direcionamento baseado em proximidade e regras de afinidade.

Configuração de failover para recuperação em DR.

Melhores práticas seguidas: ✅ Escalonamento automático de backend services.
✅ GKE e Compute Engine configurados com Managed Instance Groups (MIGs) Autoscaling On.
✅ Health checks ativos para redirecionamento de tráfego em caso de falhas.

<h3>5. Comunicação Segura entre On-Premises e Google Cloud</h3></br>
A arquitetura utiliza Cloud VPN com High Availability (HA) para conectar On-Premises ao GCP.

Características da configuração:

Túnel IPsec criptografado para tráfego seguro.

Redundância com múltiplas VPNs garantindo failover automático.

Rotas dinâmicas via Cloud Router para otimizar conectividade.

Melhores práticas seguidas: ✅ Criptografia AES-256 para comunicação segura.
✅ Cloud Router configurado para otimizar o roteamento de tráfego.
✅ Cloud VPN HA ativado para garantir conexão resiliente.

<h3>6. Monitoramento e Logging</h3></br>
A arquitetura inclui Cloud Monitoring e Cloud Logging, fornecendo telemetria em tempo real.

Componentes ativados:

Cloud Logging → Coleta logs de tráfego, firewalls e auditoria.

Cloud Monitoring → Alertas para eventos críticos e métricas de desempenho.

BigQuery e Looker → Para análises avançadas.

Melhores práticas seguidas: ✅ Alertas em tempo real para detecção de anomalias.
✅ Coleta centralizada de logs para auditoria de segurança.
✅ Dashboard de métricas para rastrear disponibilidade de serviços.

<h3>7. Disaster Recovery e Alta Disponibilidade</h3></br>
A arquitetura inclui um ambiente DR (Disaster Recovery) em us-west1, garantindo continuidade dos serviços em caso de falha na região PRD.

Principais estratégias:

Cloud SQL HA com replicação assíncrona entre regiões.

Filestore com persistência de dados replicada.

Failover automático via Load Balancer Global.

Melhores práticas seguidas: ✅ Cross-region replication para recuperação de banco de dados.
✅ Failover automático com balanceamento de carga inteligente.
✅ Infraestrutura as Code (IaC) via Terraform para recriação rápida dos serviços.
