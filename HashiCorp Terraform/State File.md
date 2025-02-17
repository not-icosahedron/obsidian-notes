Lo State File per Terraform è un file il formato JSON che rappresenta tutto quello che abbiamo creato con Terraform, incluse variabili e metadati relativi alle risorse che abbiamo deployato.
###### Questo file contiene anche informazioni sensibili, come password e KEY, API, ecc. quindi questo file deve essere protetto in accordo con le guideline di sicurezza che stiamo rispettando.

Possiamo averlo in Locale, in formato PlainText/JSON, oppure in Remoto, tramite un Remote BackEnd, separando così lo StateFile che ora sarà su uno storage cloud, come Terraform Cloud oppure un S3Bucket, in modo da criptare il file e permettere a più persone di interagire con lo stesso StateFile.

Come detto in precedenza possiamo utilizzare un [[Remote Backend]] per amministrare l'infrastruttura.