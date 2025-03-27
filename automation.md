<h1><center>Estratégia de Automação: Terraform e GitHub no Google Cloud</center></h1></br>

A infraestrutura segue um modelo Infrastructure as Code (IaC) com Terraform para gerenciamento automatizado e GitHub para versionamento e integração contínua (CI/CD). Isso garante eficiência, reprodutibilidade e segurança na configuração da infraestrutura.</br>

<h3>1. Arquitetura de Automação e Provisionamento</h3></br>

A estratégia de automação segue o modelo GitOps, onde todo provisionamento e configuração de infraestrutura é gerenciado por código armazenado no GitHub e aplicado no Google Cloud via Terraform.</br>

<h4>1.1 Fluxo de Automação</h4></br>

<b>Desenvolvimento da Infraestrutura</b></br>

&nbsp; &nbsp; •	Equipe define a infraestrutura no Terraform.</br>

&nbsp; &nbsp; •	Código armazenado no repositório GitHub.</br>

<b>Versionamento e Revisão</b></br>

&nbsp; &nbsp; •	Alterações são feitas via Pull Requests.</br>

&nbsp; &nbsp; •	Revisão e aprovação por pares antes da aplicação.</br>

<b>Pipeline de CI/CD (GitHub Actions/Terraform Cloud)</b></br>

&nbsp; &nbsp; •	Terraform fmt e validate: valida a sintaxe do código.</br>

&nbsp; &nbsp; •	Terraform plan: gera plano de execução para revisão.</br>

&nbsp; &nbsp; •	Terraform apply: aplica mudanças aprovadas na infraestrutura.</br>

<b>Monitoramento e Auditoria</b></br>

&nbsp; &nbsp; •	Registros de alterações mantidos no GitHub.</br>

&nbsp; &nbsp; •	Log centralizado de execuções para auditoria.</br></br>

<h3>2. Boas Práticas na Automação com Terraform</h3></br>

A implementação do Terraform segue práticas recomendadas para garantir segurança, modularidade e eficiência.</br>

<h4>2.1 Estrutura Modularizada do Código Terraform</h4>

<h4>Separação por módulos:</h4>

&nbsp; &nbsp; •	Módulos reutilizáveis para componentes como rede, compute, storage e segurança.</br>

&nbsp; &nbsp; •	Uso de Workspaces para gerenciar ambientes distintos (PRD, DR, DEV).</br>

Exemplo de Estrutura de Diretórios:</br>

```
/terraform  
  ├── modules/  
  │   ├── network/  
  │   ├── compute/  
  │   ├── storage/  
  │   ├── security/  
  ├── environments/  
  │   ├── dev/  
  │   ├── prd/  
  │   ├── dr/  
```
  </br>

<h4>2.2 Segurança no Terraform</h4>

<h4>Melhores práticas aplicadas:</h4>

&nbsp; &nbsp; •	Uso de Remote Backend (Cloud Storage) para armazenar estados com segurança.</br>

&nbsp; &nbsp; •	Bloqueio de estado com Terraform State Locking para evitar execuções simultâneas.</br>

&nbsp; &nbsp; •	Variáveis sensíveis armazenadas no Secret Manager ao invés de hardcoded.</br>

&nbsp; &nbsp; •	Least Privilege (Princípio do Menor Privilégio) no IAM para evitar acesso excessivo.</br>

<h4>2.3 Escalabilidade e Reutilização</h4>

Uso de variáveis dinâmicas para tornar os módulos mais reutilizáveis:</br>

```
variable "region" {
  description = "Região do Google Cloud"
  type        = string
}

variable "network_name" {
  description = "Nome da VPC"
  type        = string
  default     = "gcp-vpc-environment"
}
```
</br>

 <h4>Benefícios:</h4>

&nbsp; &nbsp; •	Facilidade na replicação de infraestrutura em diferentes ambientes.</br>

&nbsp; &nbsp; •	Redução de código duplicado e manutenção mais simples.</br></br>

<h3>3. Integração com GitHub e CI/CD</h3></br>

A automação é estendida para o GitHub Actions, garantindo integração contínua (CI/CD) para infraestrutura.</br>

<h4>3.1 Pipeline de CI/CD no GitHub Actions</h4>

<h4>Automação do Terraform no GitHub:</h4>

```
name: Terraform CI/CD

on:
  push:
    branches:
      - main

jobs:
  terraform:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout do repositório
        uses: actions/checkout@v2

      - name: Setup Terraform
        uses: hashicorp/setup-terraform@v1

      - name: Terraform Init
        run: terraform init

      - name: Terraform Validate
        run: terraform validate

      - name: Terraform Plan
        run: terraform plan

      - name: Terraform Apply
        if: github.ref == 'refs/heads/main'
        run: terraform apply -auto-approve
```
</br></br>

<h3>4. Provisionamento de Infraestrutura com Terraform</h3></br>

O Terraform é utilizado para provisionar toda a arquitetura da infraestrutura, incluindo:</br>

<h4>4.1 Rede (VPC, Subnets e Firewalls)</h4>

<h4>Exemplo de provisionamento de VPC:</h4>

```
resource "google_compute_network" "vpc" {
  name                    = "gcp-vpc-environment"
  auto_create_subnetworks = false
}
```
</br>

<h4>4.2 Compute Engine e GKE</h4>

<h4>Provisionamento de máquinas virtuais e Kubernetes:</h4>

```
resource "google_container_cluster" "gke_cluster" {
  name     = "gke-cluster"
  location = var.region
  remove_default_node_pool = true
}
```
</br>

<h4>4.3 Cloud SQL com HA</h4>

<h4>Banco de dados gerenciado com replicação:</h4>

```
resource "google_sql_database_instance" "sql_instance" {
  name             = "cloud-sql-instance"
  region           = var.region
  database_version = "MYSQL_8_0"
  settings {
    availability_type = "REGIONAL"
  }
}
```
</br></br>

<h3>5. Benefícios da Automação com Terraform e GitHub</h3></br>

&nbsp; &nbsp; •	Implementação eficiente e segura da infraestrutura.</br>

&nbsp; &nbsp; •	Redução de erros manuais com provisionamento automatizado.</br>

&nbsp; &nbsp; •	Facilidade na escalabilidade com infraestrutura modular.</br>

&nbsp; &nbsp; •	Histórico e versionamento completo da infraestrutura.</br>

&nbsp; &nbsp; •	Maior segurança com controle de acesso via GitHub e Terraform.</br>
