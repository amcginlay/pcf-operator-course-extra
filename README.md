# pcf-operator-course-extra

The Terraform config file (the heredoc way)

```bash
cat > ./terraform.tfvars <<-EOF
env_name            = "${PCF_SUBDOMAIN_NAME}"
project             = "${PCF_PROJECT_ID}"
region              = "us-central1"
zones               = ["us-central1-b", "us-central1-a", "us-central1-c"]
dns_suffix          = "${PCF_DOMAIN_NAME}"
opsman_image_url    = "https://storage.googleapis.com/ops-manager-us/pcf-gcp-2.3-build.146.tar.gz"
create_gcs_buckets  = "false"
external_database   = "false"
isolation_segment   = "false"
ssl_cert            = <<SSL_CERT
$(cat ../${PCF_SUBDOMAIN_NAME}.${PCF_DOMAIN_NAME}.cert)
SSL_CERT
ssl_private_key     = <<SSL_KEY
$(cat ../${PCF_SUBDOMAIN_NAME}.${PCF_DOMAIN_NAME}.key)
SSL_KEY
service_account_key = <<SERVICE_ACCOUNT_KEY
$(cat ../gcp_credentials.json)
SERVICE_ACCOUNT_KEY
EOF
```
