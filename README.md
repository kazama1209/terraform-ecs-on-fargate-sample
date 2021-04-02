# terraform-ecs-sample

TerraformでAmazon ECS環境を作成するためのコード。

## セットアップ

全体的な流れとしては、ECR → RDS → その他リソースといった感じで作成していくとスムーズ。

### 環境変数をセット

```
$ cp terraform.tfvars.sample terraform.tfvars
```

terraform.tfvars内にAWSアクセスキーやデータベースの情報などを記述する。

```
aws_access_key    = "AWSアクセスキー"
aws_secret_key    = "AWSシークレットキー"
aws_account_id    = "AWSアカウントID"
database_name     = "sample_app_production"
database_username = "root"
database_password = "password"
```

### 初期化

```
$ terraform init
```

### ECRを作成

```
$ $ terraform apply `cat ecr.tf | terraform fmt - | grep -E 'resource |module ' | tr -d '"' | awk '{printf("-target=%s.%s ",$2,$3);}'`
```

### RDSを作成

```
$ terraform apply `cat rds.tf | terraform fmt - | grep -E 'resource |module ' | tr -d '"' | awk '{printf("-target=%s.%s ",$2,$3);}'`
```

### その他リソースを一括で作成

```
$ terraform apply
```
