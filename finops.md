<h1><center>FinOps (Otimização de Custos)</center></h1></br>
Boas práticas para otimização de custos na implementação de novos recursos do Google Cloud e melhorias em cima de recursos já existentes, desde que não afete outros critérios com maior prioridade e esteja em conformidade com a empresa.</br></br>
A análise de custos será realizada por meio de um dashboard desenvolvido no Looker, que consumirá os dados armazenados no BigQuery. Para alimentar o BigQuery, será habilitada a exportação automatizada dos dados da conta de faturamento. O dashboard será estruturado em seções, exibindo os principais responsáveis pelos custos elevados, categorizados por projetos, recursos e SKUs. Essa abordagem facilitará a compreensão dos fatores que impactam os gastos, permitindo análises diretas e auxiliando na identificação de oportunidades de otimização e correções futuras.</br>

<h3>2.1. Google Kubernetes Engine (GKE)</h3></br>

<h4>Melhores Práticas:</h4></br>

&nbsp; &nbsp; •	Habilitar escalonamento automático de nós para ajustar recursos conforme a demanda.</br>

&nbsp; &nbsp; •	Usar instâncias Spot para workloads tolerantes a falhas.</br>

&nbsp; &nbsp; •	Ajustar tamanhos de clusters para evitar alocação excessiva de recursos.</br>

&nbsp; &nbsp; •	Consolidar workloads em menos nós para reduzir custos com instâncias.</br>

&nbsp; &nbsp; •	Configurar escalonamento horizontal e vertical para máxima eficiência.</br>

&nbsp; &nbsp; •	Implementar autoscaler para reduzir custos em horários de baixa demanda.</br>

&nbsp; &nbsp; •	Escolher regiões mais econômicas para hospedagem de clusters.</br>

&nbsp; &nbsp; •	Compartilhar clusters entre múltiplos projetos para otimizar custos.</br>

&nbsp; &nbsp; •	Utilizar armazenamento persistente apenas quando necessário.</br>

&nbsp; &nbsp; •	Configurar políticas de ciclo de vida para remoção automática de recursos inativos.</br></br>

<h3>2.2. Compute Engine</h3></br>

<h4>Melhores Práticas:</h4></br>

&nbsp; &nbsp; •	Utilizar instâncias preemptivas ou Spot VMs para workloads tolerantes a falhas.</br>

&nbsp; &nbsp; •	Dimensionar máquinas conforme a necessidade real, evitando superprovisionamento.</br>

&nbsp; &nbsp; •	Implementar desligamento automático de instâncias ociosas.</br>

&nbsp; &nbsp; •	Aplicar descontos por uso contínuo (CUDs - Committed Use Discounts).</br>

&nbsp; &nbsp; •	Migrar workloads para máquinas otimizadas para preço/desempenho.</br>

&nbsp; &nbsp; •	Reduzir tempo de execução de máquinas não essenciais.</br>

&nbsp; &nbsp; •	Consolidar cargas de trabalho em menos instâncias.</br>

&nbsp; &nbsp; •	Utilizar armazenamento temporário sempre que possível.</br>

&nbsp; &nbsp; •	Revisar logs e monitoramento para eliminar desperdícios.</br>

&nbsp; &nbsp; •	Programar desligamento de máquinas fora do horário comercial.</br></br>

<h3>2.3. Cloud SQL</h3></br>

<h4>Melhores Práticas:</h4></br>

&nbsp; &nbsp; •	Utilizar instâncias escalonáveis com ajuste automático de recursos.</br>

&nbsp; &nbsp; •	Configurar horários de desligamento para ambientes de desenvolvimento e teste.</br>

&nbsp; &nbsp; •	Adotar instâncias com preços reduzidos para workloads tolerantes a interrupções.</br>

&nbsp; &nbsp; •	Implementar Committed Use Discounts (CUDs) para obter descontos por uso contínuo.</br>

&nbsp; &nbsp; •	Escolher tamanhos de instância apropriados para evitar superprovisionamento.</br>

&nbsp; &nbsp; •	Utilizar Cloud SQL Insights para identificar queries ineficientes que consomem recursos.</br>

&nbsp; &nbsp; •	Configurar autoscaling de armazenamento para evitar custos desnecessários.</br>

&nbsp; &nbsp; •	Implementar políticas de retenção para backups automáticos e reduzir custos de armazenamento.</br>

&nbsp; &nbsp; •	Utilizar discos balanceados (PD-Balanced) ao invés de SSDs premium, caso a aplicação não exija alta performance.</br>

&nbsp; &nbsp; •	Consolidar bancos de dados pequenos em uma única instância quando possível.</br></br>

<h3>2.4. Cloud Storage</h3></br>

<h4>Melhores Práticas:</h4></br>

&nbsp; &nbsp; •	Utilizar Storage Classes apropriadas (Standard, Nearline, Coldline, Archive) conforme a frequência de acesso.</br>

&nbsp; &nbsp; •	Configurar ciclo de vida de objetos para mover ou excluir automaticamente dados antigos.</br>

&nbsp; &nbsp; •	Ativar redundância regional apenas quando necessário para evitar custos extras.</br>

&nbsp; &nbsp; •	Utilizar compressão e compactação de dados antes do upload para reduzir consumo de armazenamento.</br>

&nbsp; &nbsp; •	Evitar múltiplas cópias de um mesmo objeto usando versões controladas e deduplicação.</br>

&nbsp; &nbsp; •	Configurar Cloud Logging e Monitoring para identificar dados não acessados frequentemente.</br>

&nbsp; &nbsp; •	Aplicar Cloud CDN para evitar requisições repetidas diretamente ao Cloud Storage.</br>

&nbsp; &nbsp; •	Usar Signed URLs para conceder acesso temporário sem precisar de APIs adicionais.</br>

&nbsp; &nbsp; •	Consolidar buckets sempre que possível para reduzir o número de requisições inter-regionais.</br>

&nbsp; &nbsp; •	Utilizar instâncias Preemptible para processamentos temporários e evitar custos de VM permanentes.</br></br>

<h3>2.5. Filestore</h3></br>

<h4>Melhores Práticas:</h4></br>

&nbsp; &nbsp; •	Escolher a classe correta (Basic HDD, Basic SSD, High Scale SSD, Enterprise) com base na carga de trabalho.</br>

&nbsp; &nbsp; •	Reduzir o tamanho do Filestore conforme necessário, evitando alocações desnecessárias.</br>

&nbsp; &nbsp; •	Usar armazenamento Basic HDD para cargas de trabalho com menos requisitos de IOPS.</br>

&nbsp; &nbsp; •	Monitorar e ajustar o uso com Cloud Monitoring para identificar desperdícios.</br>

&nbsp; &nbsp; •	Configurar Cloud Storage para armazenar arquivos de acesso esporádico e integrar ao Filestore quando necessário.</br>

&nbsp; &nbsp; •	Consolidar múltiplos volumes para reduzir custos operacionais.</br>

&nbsp; &nbsp; •	Utilizar Snapshots para backups em vez de manter várias versões manuais dos arquivos.</br>

&nbsp; &nbsp; •	Agendar tarefas de limpeza automática para remover arquivos desnecessários.</br>

&nbsp; &nbsp; •	Usar Cloud Functions para mover automaticamente arquivos antigos para armazenamento de menor custo.</br>

&nbsp; &nbsp; •	Revisar periodicamente a necessidade do Filestore, substituindo por soluções mais econômicas quando possível.</br></br>

<h3>2.6. Cloud Load Balancing</h3></br>

<h4>Melhores Práticas:</h4></br>

&nbsp; &nbsp; •	Escolha o tipo de balanceador adequado: Utilize o balanceador de carga correto (HTTP(S), TCP/UDP, SSL Proxy, etc.) para seu caso de uso específico, evitando recursos desnecessários.</br>

&nbsp; &nbsp; •	Use balanceamento de carga global: Utilize o balanceamento de carga global para otimizar os custos de infraestrutura, reduzindo a necessidade de provisionar recursos em múltiplas regiões.</br>

&nbsp; &nbsp; •	Aproveite o escalonamento automático: Configure autoescalonamento para ajustar dinamicamente os recursos de backend com base na demanda, economizando custos em períodos de baixa carga.</br>

&nbsp; &nbsp; •	Distribuição de tráfego inteligente: Configure regras de tráfego para distribuir as cargas entre instâncias de forma eficiente, garantindo que não haja sobrecarga de recursos.</br>

&nbsp; &nbsp; •	Reduza a latência de rede: Use balanceamento de carga baseado em localidade para redirecionar o tráfego para as instâncias mais próximas ao usuário, diminuindo custos com largura de banda.</br>

&nbsp; &nbsp; •	Habilite o cache de conteúdo: Configure caching para conteúdo estático, como imagens e arquivos JS/CSS, diminuindo a necessidade de chamadas constantes ao backend e reduzindo custos.</br>

&nbsp; &nbsp; •	Use o Compute Engine Preemptible VMs: Se for apropriado, utilize VMs preemptivas para backends, que são mais econômicas, embora com disponibilidade limitada.</br>

&nbsp; &nbsp; •	Mantenha a infraestrutura sob monitoramento constante: Utilize o Google Cloud Monitoring para monitorar o uso do balanceador de carga e ajustar a escala conforme necessário para reduzir custos.</br>

&nbsp; &nbsp; •	Otimize o tráfego com CDNs: Utilize o Cloud CDN integrado ao load balancing para reduzir o tráfego originado no backend e melhorar a eficiência.</br>

&nbsp; &nbsp; •	Ajuste a configuração de backends: Evite manter servidores de backend subutilizados. Ajuste o número de instâncias de backend conforme a demanda do tráfego.</br></br>

<h3>2.7. Cloud Armor</h3></br>

<h4>Melhores Práticas:</h4></br>

&nbsp; &nbsp; •	Use regras personalizadas baseadas em IP: Em vez de usar regras amplas para tráfego, crie regras específicas para controlar o tráfego com base em IPs de origem ou regiões, economizando recursos.</br>

&nbsp; &nbsp; •	Aplique políticas de segurança apenas onde necessário: Não aplique o Google Cloud Armor a todas as instâncias. Use-o apenas onde há necessidade de proteção, economizando recursos em outras áreas.</br>

&nbsp; &nbsp; •	Monitore o tráfego para ajustar as regras: Monitore constantemente o tráfego para ajustar as regras de segurança, evitando a configuração excessiva de filtros que podem aumentar os custos.</br>

&nbsp; &nbsp; •	Ajuste as taxas de requisição de API: Limite o número de chamadas à API do Google Cloud Armor para reduzir custos associados ao uso excessivo de recursos.</br>

&nbsp; &nbsp; •	Aproveite os filtros baseados em geo-localização: Filtre o tráfego com base na localização geográfica para evitar a proteção de tráfego desnecessário de certas regiões e reduzir a carga.</br>

&nbsp; &nbsp; •	Ajuste de thresholds para mitigação: Configure adequadamente os thresholds para mitigação de DDoS para evitar o uso excessivo de recursos em momentos de tráfego intenso.</br>

&nbsp; &nbsp; •	Revisão e exclusão de regras antigas: Revise regularmente suas políticas e elimine regras obsoletas para reduzir a sobrecarga de processamento e os custos associados.</br>

&nbsp; &nbsp; •	Uso eficiente de regras de rate-limiting: Defina limites razoáveis de requisições para evitar excessos que possam gerar custos adicionais no Google Cloud Armor.</br>

&nbsp; &nbsp; •	Centralize a configuração de segurança: Use uma única configuração do Google Cloud Armor em vez de múltiplas instâncias para simplificar a administração e reduzir os custos.</br>

&nbsp; &nbsp; •	Utilize a integração com outros serviços do Google Cloud: Integrar o Google Cloud Armor com outros serviços como Google Cloud Load Balancing pode otimizar o uso e reduzir custos gerais de segurança.</br></br>

<h3>2.8. Cloud VPN</h3></br>

<h4>Melhores Práticas:</h4></br>

&nbsp; &nbsp; •	Escolha o tipo de VPN adequado: Utilize a VPN do Google Cloud apropriada para sua carga de trabalho, como a VPN de site a site ou VPN cliente, para evitar gastos excessivos com recursos desnecessários.</br>

&nbsp; &nbsp; •	Monitore o uso da VPN: Use ferramentas de monitoramento, como o Google Cloud Monitoring, para observar o tráfego da VPN e ajustar o uso conforme necessário, evitando custos desnecessários.</br>

&nbsp; &nbsp; •	Minimize o tráfego de saída: Configure a VPN para reduzir o tráfego de saída, controlando o tráfego que sai da nuvem para reduzir custos de largura de banda.</br>

&nbsp; &nbsp; •	Otimize a configuração de roteamento: Utilize roteamento eficiente para reduzir o tráfego desnecessário, limitando os recursos consumidos pela VPN.</br>

&nbsp; &nbsp; •	Aproveite o Cloud Interconnect para conexões de alta largura de banda: Se você tiver grandes volumes de dados sendo transferidos, considere usar o Cloud Interconnect em vez de VPN, para reduzir custos e melhorar a performance.</br>

&nbsp; &nbsp; •	Desative a VPN quando não for necessária: Se a VPN não estiver sendo usada, desative-a para evitar custos de uso contínuo desnecessários.</br>

&nbsp; &nbsp; •	Reveja os custos de recursos associados: Verifique frequentemente os custos associados às instâncias e à largura de banda para garantir que você não está pagando mais do que o necessário.</br>

&nbsp; &nbsp; •	Use VPNs somente quando necessário: Se as conexões privadas podem ser realizadas de outra maneira, como com VPC peering ou interconexão, utilize essas opções para reduzir o custo de VPN.</br>

&nbsp; &nbsp; •	Gerencie a largura de banda: Ajuste a largura de banda disponível para a VPN com base na demanda real, evitando provisionamento excessivo e custos elevados.</br>

&nbsp; &nbsp; •	Aproveite o escalonamento automático: Use escalabilidade dinâmica para ajustar os recursos da VPN conforme a necessidade, evitando sobrecarga e otimização de custos.</br></br>

<h3>2.9. Cloud DNS</h3></br>

<h4>Melhores Práticas:</h4></br>

&nbsp; &nbsp; •	Use o Cloud DNS para gerenciamento centralizado de DNS: Ao usar o Cloud DNS, centralize e simplifique o gerenciamento de DNS, reduzindo a necessidade de múltiplos provedores e o custo associado.</br>

&nbsp; &nbsp; •	Evite usar zonas DNS desnecessárias: Crie apenas as zonas DNS que são necessárias e remova as zonas desnecessárias para evitar custos adicionais.</br>

&nbsp; &nbsp; •	Gerencie o TTL (Time to Live) de forma eficiente: Configure TTL adequado para seus registros DNS. Um TTL muito curto pode gerar consultas frequentes e custos elevados, enquanto TTL muito longo pode levar a desatualizações.</br>

&nbsp; &nbsp; •	Utilize registros DNS eficientes: Utilize registros CNAME e ALIAS para evitar registros de múltiplos IPs e reduzir a carga no seu sistema DNS.</br>

&nbsp; &nbsp; •	Reduza a quantidade de consultas DNS: Minimize as consultas DNS frequentes ajustando os TTL e utilizando cache de DNS para reduzir os custos associados às consultas.</br>

&nbsp; &nbsp; •	Implemente a compactação de registros DNS: Utilize métodos de compactação de DNS para reduzir o volume de dados enviados, diminuindo os custos de tráfego.</br>

&nbsp; &nbsp; •	Revise periodicamente as entradas DNS: Realize auditorias regulares em suas entradas DNS e remova registros desnecessários ou obsoletos, otimizando o custo de operação.</br>

&nbsp; &nbsp; •	Use o Google Cloud Interconnect para reduzir latência: Se estiver usando uma grande quantidade de tráfego entre sua rede e o Google Cloud, o Cloud Interconnect pode ser mais barato em relação à execução do DNS via internet pública.</br>

&nbsp; &nbsp; •	Automatize a criação e remoção de zonas e registros: Use scripts e ferramentas de automação para criar e excluir zonas e registros DNS conforme necessário, evitando custos excessivos com registros não utilizados.</br>

&nbsp; &nbsp; •	Aproveite os recursos gratuitos do Cloud DNS: Use as opções gratuitas ou limitadas do Cloud DNS para testar e ajustar sua infraestrutura de DNS antes de escalar para uma versão paga.</br></br>

<h3>2.10. Cloud Key Management (KMS)</h3></br>

<h4>Melhores Práticas:</h4></br>

&nbsp; &nbsp; •	Escolha o tipo de chave correto: Use chaves simétricas quando possível, pois elas são mais baratas em termos de armazenamento e operações do que as chaves assimétricas.</br>

&nbsp; &nbsp; •	Use o KMS com o mínimo de chaves necessárias: Evite criar muitas chaves para reduzir o custo de armazenamento e manutenção de chaves.</br>

&nbsp; &nbsp; •	Exclua chaves não utilizadas: Audite e exclua regularmente as chaves que não estão sendo usadas, evitando custos de armazenamento desnecessários.</br>

&nbsp; &nbsp; •	Automatize a rotação de chaves: Defina políticas de rotação automática de chaves para reduzir o risco de exposição e evitar a criação manual de novas chaves, o que pode ser custoso.</br>

&nbsp; &nbsp; •	Implemente criptografia por demanda: Utilize KMS apenas quando necessário, para criptografar ou descriptografar dados, evitando operações desnecessárias.</br>

&nbsp; &nbsp; •	Otimize os intervalos de rotação de chaves: Configure intervalos de rotação de chaves de acordo com suas necessidades de segurança, não rotacionando as chaves com muita frequência, o que poderia gerar custos excessivos.</br>

&nbsp; &nbsp; •	Utilize o Cloud Key Management (Cloud KMS) em vez de soluções terceirizadas: Se possível, utilize o KMS do Google Cloud em vez de soluções de terceiros, já que é uma opção mais integrada e potencialmente mais barata.</br>

&nbsp; &nbsp; •	Monitoramento e alertas para uso excessivo de chaves: Configure alertas para detectar operações excessivas em chaves, garantindo que você pague apenas pelo uso necessário.</br>

&nbsp; &nbsp; •	Use a política de chaves de vida útil curta: Defina a vida útil das chaves para que elas sejam automaticamente desativadas após o uso, evitando o armazenamento desnecessário de chaves.</br>

&nbsp; &nbsp; •	Aproveite a integração com outras ferramentas do Google Cloud: Use o KMS de forma integrada com outros serviços do Google Cloud, como o Google Cloud Storage ou Compute Engine, para reduzir custos com chaves externas.</br></br>

<h3>2.11. Cloud Monitoring e Logging</h3></br>

<h4>Melhores Práticas:</h4></br>

&nbsp; &nbsp; •	Ajuste os intervalos de coleta de métricas: Reduza a frequência de coleta de métricas para dados não críticos. Coletar métricas com menos frequência ajuda a reduzir o volume de dados e, consequentemente, os custos.</br>

&nbsp; &nbsp; •	Use métricas personalizadas com parcimônia: Crie apenas métricas personalizadas essenciais. Múltiplas métricas personalizadas podem rapidamente aumentar os custos de armazenamento e análise.</br>

&nbsp; &nbsp; •	Armazene logs por períodos adequados: Configure políticas de retenção de logs que atendam às necessidades de conformidade, mas evite manter logs desnecessários por períodos mais longos do que o necessário.</br>

&nbsp; &nbsp; •	Aproveite os planos gratuitos e a camada de logs do Cloud: Utilize a camada gratuita do Google Cloud Logging para coletar e armazenar logs sem custos adicionais.</br>

&nbsp; &nbsp; •	Revise regularmente as métricas e logs coletados: Audite e ajuste periodicamente quais métricas e logs são coletados. Remova dados desnecessários para reduzir o uso de recursos.</br>

&nbsp; &nbsp; •	Configure alertas eficientes: Utilize alertas apenas para eventos críticos ou operacionais. Alertas desnecessários podem gerar notificações excessivas e custos com a infraestrutura.</br>

&nbsp; &nbsp; •	Comprimir e arquivar logs antigos: Configure regras de compressão e arquivamento de logs antigos, utilizando o Cloud Storage para reduzir custos com armazenamento.</br>

&nbsp; &nbsp; •	Use filtros de logs para reduzir volume: Implemente filtros para reduzir o volume de dados enviados para o Logging, focando apenas nas informações mais relevantes.</br>

&nbsp; &nbsp; •	Habilite métricas de agrupamento (aggregation): Quando possível, use métricas agregadas para reduzir o volume de dados a ser armazenado e analisado, minimizando custos.</br>

&nbsp; &nbsp; •	Automatize a limpeza de logs antigos: Configure processos automáticos para excluir ou transferir logs antigos e desnecessários para armazenamento de baixo custo.</br></br>

<h3>2.12. BigQuery</h3></br>

<h4>Melhores Práticas:</h4></br>

&nbsp; &nbsp; •	Use partições e clustering para tabelas grandes: Ao particionar suas tabelas, você pode reduzir a quantidade de dados lidos durante as consultas, economizando em custos de consulta.</br>

&nbsp; &nbsp; •	Otimize o armazenamento de dados com o uso de tabelas de longo prazo: Armazene dados em tabelas de longo prazo com menor custo e migre dados históricos para elas para reduzir o custo de armazenamento em tabelas ativas.</br>

&nbsp; &nbsp; •	Evite consultas que leem dados desnecessários: Limite as colunas e as linhas que você seleciona nas consultas para evitar ler dados desnecessários e reduzir os custos.</br>

&nbsp; &nbsp; •	Use o armazenamento de dados no formato columnar: Armazene os dados em formatos otimizados como Parquet ou ORC, que oferecem maior compressão e menor custo.</br>

&nbsp; &nbsp; •	Implemente a compactação de dados: Compacte seus dados para reduzir o volume de armazenamento necessário e, consequentemente, os custos de armazenamento no BigQuery.</br>

&nbsp; &nbsp; •	Aproveite as camadas de armazenamento de baixo custo: Para dados acessados com pouca frequência, utilize o armazenamento "cold" ou "long-term" para reduzir o custo.</br>

&nbsp; &nbsp; •	Use a consulta por demanda com restrição de uso: Execute consultas por demanda apenas quando necessário, e não deixe consultas em execução sem supervisão.</br>

&nbsp; &nbsp; •	Utilize a opção de "flat-rate pricing" se você tiver cargas de trabalho previsíveis: Para projetos com grandes volumes de consultas regulares, o modelo de preços de taxa fixa pode ser mais econômico.</br>

&nbsp; &nbsp; •	Use o controle de quotas e alertas de custo: Monitore e configure alertas de custo para garantir que o uso do BigQuery não ultrapasse o orçamento estipulado.</br>

&nbsp; &nbsp; •	Elimine dados redundantes e tabelas não usadas: Realize uma limpeza periódica para excluir ou arquivar dados e tabelas que não são mais necessários, evitando custos desnecessários de armazenamento.</br></br>

<h3>2.13. DevOps - Terraform e GitHub</h3></br>

<h4>Melhores Práticas:</h4></br>

<b>Terraform:</b></br>
&nbsp; &nbsp; •	Use o Terraform Cloud ou Terraform Enterprise para otimizar a infraestrutura: Com a opção de gerenciamento de estados no Terraform Cloud, você pode controlar melhor os recursos e reduzir custos com a automação.</br>

&nbsp; &nbsp; •	Utilize módulos reutilizáveis: Organize a infraestrutura usando módulos reutilizáveis, o que ajuda a evitar a duplicação e reduzir custos operacionais e de manutenção.</br>

&nbsp; &nbsp; •	Evite recursos desnecessários: No código Terraform, revise regularmente os recursos criados e exclua aqueles que não são necessários.</br>

&nbsp; &nbsp; •	Configure o Auto Scaling de recursos: Ao configurar instâncias e outros recursos, utilize o Auto Scaling para evitar provisionamento excessivo, garantindo que você pague apenas pelos recursos necessários.</br>

&nbsp; &nbsp; •	Use planos de preços escalonados: Aproveite planos de preços que oferecem descontos para grandes volumes, como os planos de instâncias reservadas ou descontos de longo prazo.</br>

&nbsp; &nbsp; •	Mantenha um bom controle de estados e variáveis: Um gerenciamento eficaz de estados e variáveis pode evitar custos com manutenção desnecessária e erros de provisionamento.</br>

&nbsp; &nbsp; •	Evite provisionamento de recursos durante a noite ou em horários ociosos: Use o terraform plan para revisar e evitar a criação de recursos desnecessários em horários de baixa utilização.</br>

&nbsp; &nbsp; •	Use tags para organizar e gerenciar custos: No Terraform, use tags para identificar recursos, ajudando a rastrear e otimizar custos por projeto ou unidade de negócios.</br>

&nbsp; &nbsp; •	Monitore a infraestrutura com o Terraform Cloud: Habilite monitoramento e alertas para evitar que recursos sejam provisionados desnecessariamente.</br>

&nbsp; &nbsp; •	Automatize a remoção de recursos temporários: Utilize o Terraform para provisionar e destruir recursos temporários automaticamente, como ambientes de teste.</br></br>

<b>GitHub:</b></br>
&nbsp; &nbsp; •	Use repositórios privados apenas quando necessário: Repositórios privados são pagos, então prefira repositórios públicos para minimizar os custos de armazenamento.</br>

&nbsp; &nbsp; •	Otimize o uso de GitHub Actions: Minimize os recursos utilizados por pipelines de CI/CD, evitando execuções desnecessárias e usando cache eficiente.</br>

&nbsp; &nbsp; •	Configure as permissões para evitar acessos desnecessários: Ao evitar acessos desnecessários, você pode reduzir custos operacionais e gerenciar melhor as funcionalidades pagas no GitHub.</br>

&nbsp; &nbsp; •	Utilize planos pagos do GitHub somente quando necessário: Avalie se os recursos oferecidos por planos pagos são realmente necessários para a equipe.</br>

&nbsp; &nbsp; •	Revise e remova repositórios não utilizados: Exclua repositórios antigos ou que não são mais necessários para evitar custos com armazenamento.</br>

&nbsp; &nbsp; •	Evite builds de longo prazo em GitHub Actions: Defina limites de tempo para execuções de CI/CD para evitar desperdício de recursos.</br>

&nbsp; &nbsp; •	Use pacotes GitHub em vez de pacotes privados sempre que possível: Para evitar custos com armazenamento privado de pacotes, prefira usar pacotes públicos quando possível.</br>

&nbsp; &nbsp; •	Centralize os workflows no GitHub Actions: Evite criar pipelines redundantes para o mesmo fluxo de trabalho e centralize as tarefas no GitHub Actions para maior eficiência.</br>

&nbsp; &nbsp; •	Monitore o uso de GitHub Actions: Configure alertas para monitorar a quantidade de minutos gastos em GitHub Actions e ajustar conforme necessário.</br>

&nbsp; &nbsp; •	Use o GitHub Pages para hospedagem estática gratuita: Use o GitHub Pages para hospedar sites estáticos gratuitamente em vez de recursos pagos.</br>
