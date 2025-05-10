# AWS_ouadal_issifou
FINAL_EXAM

# 🖼️ Image Metadata Processing on AWS

Ce projet déploie une infrastructure Cloud AWS permettant de :
1. Télécharger des fichiers image (`.jpg`) dans un bucket S3.
2. Déclencher automatiquement une fonction AWS Lambda.
3. Extraire et enregistrer les métadonnées dans une table DynamoDB.
4. Utiliser une instance EC2 comme client de test.

---

## 🚀 Technologies utilisées

- **Amazon S3** : Stockage d’images
- **AWS Lambda** : Traitement d’événements
- **Amazon DynamoDB** : Stockage des métadonnées
- **Amazon EC2** : Simulateur de client
- **AWS CloudFormation** : Déploiement de l'infrastructure
- **IAM** : Gestion des permissions

---

## 📁 Structure du projet

```
.
├── template.yaml         # Template CloudFormation principal
├── lambda_function.py    # Code de la fonction Lambda (si hors ligne)
└── README.md             # Ce fichier
```



## 📦 Déploiement via AWS CloudFormation

1. Va dans **AWS Console > CloudFormation > Create Stack**
2. Téléverse `template.yaml`
3. Renseigne les paramètres :
   - `EnvName` : Nom de l’environnement (ex : `dev`)
   - `VpcId`, `SubnetId`, etc. si demandés
4. Lance le déploiement

---

## ⚙️ Fonction Lambda

- Déclenchée automatiquement lors de l’ajout d’un fichier `.jpg` dans S3
- Enregistre :
  - Le nom du fichier (`FileName`)
  - Le nom du bucket (`BucketName`)
- Dans la table DynamoDB `FileMetadata-dev`

---

## 🧪 Tester avec une instance EC2

1. Connecte-toi à l’instance :
   ```bash
   ssh -i your-key.pem ec2-user@<ip>
   ```
2. Installe AWS CLI si besoin :
   ```bash
   sudo yum install -y awscli
   ```
3. Upload un fichier vers S3 :
   ```bash
   aws s3 cp image.jpg s3://dev-file-metadata-bucket/
   ```
4. Vérifie dans DynamoDB :
   ```bash
   aws dynamodb get-item --table-name FileMetadata-dev \
   --key '{"FileName": {"S": "image.jpg"}}' --region eu-west-1
   ```

