Dopo aver installato Terraform seguendo le istruzioni in [[Terraform Installation]] possiamo procedere a connettere AWS con Terraform, in locale.

Per l'utilizzo di Terraform con AWS per il provisioning di EC2, S3, ecc. è best-practice creare un utenza ad-hoc con privilegi: 
- EC2FullAccess
- IAMFullAccess
- S3FullAccess
- eventuali altre, in base a cosa vogliamo utilizzare con Terraform


Step 2: installare AWS-CLI ed utilizzarla (aws configure) per specificare Access Key ID, Secret Access Key, Default Region, ecc.

Setp 3:  Creare il file di setup per l'ambiente Terraform in connessione con AWS. Questo sarà il primo file che utilizzeremo per inizializzare il Provisioning, e successivamente per creare EC2 Instances, ecc.
```json:
terraform {
	required_prividers{
		aws = {
			source = "hashicorp/aws"
			version = "x.x"
			}
		}
	}

provider "aws" {
region = "us-east-1"
}

resource "aws_instance" "example"{
	ami = "ami-############"  #Specifica il sistema operativo ed altri valori.
	instance_type = "t2.micro"
}
```

Step 4: Initializzare Terraform con `terraform init` e successivamente `terraform plan` oppure direttamente `terraform apply` per visualizzare le differenze tra l'attuale EC2 State e quello che accadrà dopo il provisioning delle macchine dichiarate nel file `main.tf`; 
###### Note: possiamo usare successivamente `terraform destroy` per smantellare l'infrastruttura dichiarata nel file .tf

Questo produrrà una serie di file, tra cui lo [[State File]].

Di seguito continuiamo ad analizzare i comandi di Terraform:

- [[terraform plan]]
- terraform apply
- [[terraform destroy]]