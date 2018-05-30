# vm-import-aws

Esse repositório mostra como importar um vmdk (arquivo de disco de uma máquina virtual do vmware) para a AWS.

## Getting Started

Para começar a importar suas vm's para a AWS, clone esse repositório. Lembre-se de ter o git instalado na sua máquina:

> git clone https://github.com/allysono/vm-import-aws

### Prerequisites

Para conseguir importar suas vm's para a AWS é necessário ter instalado em sua máquina 
> GIT = (https://git-scm.com/book/pt-br/v1/Primeiros-passos-Instalando-Git)

> AWS CLI = (https://docs.aws.amazon.com/pt_br/cli/latest/userguide/installing.html)

> Ter configurado uma conta da AWS no seu linux através do comando aws configure (https://docs.aws.amazon.com/pt_br/cli/latest/userguide/cli-chap-getting-started.html)

# Edite os seguintes campos do arquivo "containers.json"


> Description
> S3 Bucket
> S3 Key


# Edite os seguintes campos do arquivo "role-policy.json dentro de Resource


>"arn:aws:s3:::nome-do-bucket",
>"arn:aws:s3:::nome-do-bucket/*"



### Installing

O primeiro passo é criar um bucket para fazer o upload dos seus discos .vmdk para a nuvem

#Lembrando que o bucket tem que ter um unique name. Esse passo só é necessário caso você não tenha um bucket para importar os .vmdks. Esse bucket criado está com as permissões default. Lembre-se de apagá-lo após o uso. 

> aws s3 mb s3://nome-do-bucket

#Para apagá-lo
> aws s3 rb s3://nome-do-bucket

# Após criar o bucket, crie uma IAM ROLE a partir do arquivo vm-import-aws
> aws iam create-role --role-name vmimport --assume-role-policy-document file:///home/folder/vm-import-aws

> aws iam put-role-policy --role-name vmimport --policy-name vmimport --policy-document file://role-policy.json

# Importe a imagem através do comando abaixo:
> aws ec2 import-image --description "MyDescription" --disk-containers file:/home/folder/vm-import-aws/containers.json

# Acompanhe o upload através desse comando
> aws ec2 describe-import-image-tasks --import-task-ids

## Built With

* [Amazon Web Services](https://aws.amazon.com) 

