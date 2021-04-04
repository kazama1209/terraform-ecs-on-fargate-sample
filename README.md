# terraform-ecs-on-fargate-sample

TerraformでAmazon ECS環境（on Fargate）を作成するためのコード。

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
$ terraform apply -target={aws_ecr_repository.sample_app,aws_ecr_lifecycle_policy.sample_app_lifecycle_policy,aws_ecr_repository.sample_nginx}
```

### RDSを作成

```
$ terraform apply -target={aws_db_subnet_group.sample_db_subnet_group,aws_db_instance.sample_db}
```

### その他リソースを一括で作成

```
$ terraform apply
```
