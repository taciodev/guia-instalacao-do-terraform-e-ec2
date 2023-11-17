# Guia de Instalação do Terraform e Provisionamento de uma EC2

O Terraform é uma ferramenta de infraestrutura como código (IaC) que permite a automação da criação e gerenciamento de recursos de infraestrutura. Este guia fornecerá instruções passo a passo para instalar o Terraform em um ambiente Oracle Linux 8.

## Pré-requisitos

Certifique-se de que os seguintes pré-requisitos estejam instalados no seu sistema:

1. Oracle Linux 8
2. `yum-utils` para gerenciamento de repositórios

## Instalação do Terraform

### Passo 1: Instale o `yum-utils`

```bash
sudo yum install -y yum-utils
```

Este comando instala a ferramenta yum-utils necessária para gerenciar repositórios.

### Passo 2: Adicione o repositório HashiCorp

```bash
sudo yum-config-manager --add-repo https://rpm.releases.hashicorp.com/RHEL/hashicorp.repo
```

Este comando adiciona o repositório HashiCorp, fornecendo acesso aos pacotes Terraform.

### Passo 3: Instale o Terraform

```bash
sudo yum -y install terraform
```

Este comando instala o Terraform no sistema.

### Passo 4: Verifique a instalação

```bash
terraform --version
```

Este comando deve exibir a versão do Terraform instalada.

## Configuração do AWS CLI

### Passo 1: Instale o AWS CLI

```bash
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
```

### Passo 2: Configure o AWS CLI com suas credenciais

```bash
aws configure
```

Siga as instruções e forneça suas credenciais de acesso da AWS (chave de acesso, chave secreta, região padrão e formato de saída).

### Passo 3: Verifique a instalação

```bash
aws --version
```

Este comando deve exibir a versão do AWS CLI instalada.

## Criar e Implantar uma Instância EC2 com Terraform

Agora, para criar e implantar uma instância EC2 t2.micro na AWS usando o Terraform, siga os passos abaixo:

### Passo 1: Crie um diretório de trabalho

```bash
mkdir terraform-aws
cd terraform-aws
```

### Passo 2: Crie um arquivo chamado main.tf com o seguinte conteúdo

```hcl
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 4.16"
    }
  }

  required_version = ">= 1.2.0"
}

provider "aws" {
  region = "sua-regiao-aws"
}

resource "aws_instance" "app_server" {
  ami           = "ami-xxxxxxxxxxxxxxxxx" # AMI da sua escolha
  instance_type = "t2.micro"

  tags = {
    Name = "ExampleAppServerInstance"
  }
}

```

Substitua "sua-regiao-aws" pela região desejada e "ami-xxxxxxxxxxxxxxxxx" pela AMI desejada.

### Passo 3: Execute os seguintes comandos no terminal

```bash
terraform init
terraform apply
```

Isso inicializa o projeto Terraform e aplica as configurações para criar a instância EC2.

Agora, você concluiu com sucesso a instalação do Terraform, configurou o AWS CLI e criou/implantou uma instância EC2 na AWS.
