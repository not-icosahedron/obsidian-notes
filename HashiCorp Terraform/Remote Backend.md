Ci sono due principali Remote Backend:
### Terraform Cloud:
 ```json:
 terraform {
	 backend "remote" {
	 organization = "devops-directive"
	
	workspaces {
	name = "terraform-example"
			}
		 }
	 }
```
Questo codice di esempio è ciò che connette l'istanza locale di Terraform a Terraform Cloud. 

### AWS
 utilizzando un S3 Bucket e una DynamoDB Table come Backend.
 ```json:
 terraform {
 backend "s3" {
		 bucket = "devops-directive-tf-state"
		 key = "tf-infra/terraform.tfstate"
		 region = "us-east-1"
		 dynamodb_table = "terraform-state-locking"
		 encrypt = true
	 }
 }
 ```
 per creare queste risorse in Terraform possiamo inizializzare l'infrastruttura in locale e poi utilizzare .tf per creare le risorse necessarie, e infine utilizzare le risorse come backend remoto (cambiando il file .tf con `backend "s3"` )

```json:
resource "aws_s3_bucket" "terraform_state" {
	bucket = "devops-directive-tf-state"
	force_destroy = true
	versioning { 
		enabled = true 
		}
		
	server_side_encryption_configuration {
		rule {
			apply_server_side_encryption_by_default { 
				sse_algorithm = "AES256"
				}
			}
	}
}

resource "aws_dynamodb_table" "terraform_locks" {
	name = "terraform-state-locking"
	billing_mode = "PAY_PER_REQUEST"
	hash_key = "LockID"
	attribute {
		name = "LockID"
		type = "S"
		}
}
```
Possiamo usare questa configurazione per creare il Bucket S3 e la DynamoDB Table; risorse necessarie per utilizzare AWS come Remote Backend.

Proseguiamo con il `terraform apply` per creare le risorse, successivamente cambiamo la config (main.tf) per utilizzare le risorse remote appena create, e nuovamente eseguiamo `terraform apply` per applicare le configurazioni.
