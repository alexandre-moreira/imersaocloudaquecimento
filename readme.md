# Terraform com AWS na Prática
## Terraform com AWS na Prática encontra-se no arquivo main.tf

```
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
    region  = "us-east-1"
    }

    resource "aws_s3_bucket" "s3_bucket" {
    bucket = "tcb-app-qa-jr"
    }

    resource "aws_s3_bucket_public_access_block" "s3_block" {
    bucket = aws_s3_bucket.s3_bucket.id

    block_public_acls       = true
    block_public_policy     = true
    ignore_public_acls      = true
    restrict_public_buckets = true
    }
```
## Passos
- Criar pasta aquecimento
- Criar pasta live2-terraform-aws
- Abrir pasta aquecimento no VS Code
- Criar o arquivo [main.tf](http://main.tf/)
- Criar o arquivo de configuração Terraform para fazer deploy do S3 bucket
```
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
    region  = "us-east-1"
    }

    resource "aws_s3_bucket" "s3_bucket" {
    bucket = "tcb-app-qa-jr"
    }

```
- Login na AWS, open the Cloud Shell
- Instalar Terraform
https://learn.hashicorp.com/tutorials/terraform/install-cli?in=terraform/aws-get-started
- Subir o arquivo [main.tf](http://main.tf/) para o Cloud Shell
- Executar Init, plan e apply para criar o S3

```
    terraform init
    terraform plan
    terraform apply
```

- Adicionar novo bloco de configuração para prevenir acesso público ao S3
```
    resource "aws_s3_bucket_public_access_block" "s3_block" {
    bucket = aws_s3_bucket.s3_bucket.id

    block_public_acls       = true
    block_public_policy     = true
    ignore_public_acls      = true
    restrict_public_buckets = true
    }
```

## Troubleshooting:
```
Se a sessão do AWS CLI token no Cloud Shell expirar, executar qualquer comando AWS CLI para atualiza-lo. Exemplo:
aws s3 ls s3://tcb-app-qa-jr
```

### https://thecloudbootcamp.notion.site/Terraform-com-AWS-na-Pr-tica-f8fc022eba734cd08389ff021ad68a20