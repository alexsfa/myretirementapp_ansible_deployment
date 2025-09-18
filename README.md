Τhis repository contains two ansible playbooks, each serving a different scenario for the deployment of the MyRetirement app.

### Scenario A  
An ansible playbook launches 4 AWS EC2 Ubuntu24.04 instances, provisioning each to host an app's component.  

### Scenario B  
An ansible playbook launches an AWS EC2 Ubuntu24.04 instance that initializes a Docker environment for the MyRetirement app's deployment.

----

By default, the playbooks deploy a production-ready environment which creates:  
- an **A record** on a Route53' hostzone
- installs **nginx** and **certbot** to serve the app using https and a fqdn.
- serves the app over **HTTPS** using a FQDN (Full Qualified Domain Name)

By declaring the dev_environment environment variable as True, the playbooks deploy a development environment that is accessible only to the user who initiated the deployment.

----
In order to use any of the production environments, you will need to use certbot for requesting a file and add the returned content on a myretirementapp_ansible_deployment/ssl_certificate directory.  

For a personalized and smooth setup, please provide your credentials according the scenario you want to use. 

### Scenario A
In the directory myretirementapp_ansible_deployment/ansible_deploy/sub_playbooks/vars, add  .yml files that use these templates

**aws_credentials.yml file**
```yaml
aws_credentials:
  CERT_EMAIL: <your_email>
  aws_access_key: <your_aws_access_key>
  aws_secret_access_key: <your_aws_secret_access_key>

network_config:
  subnet_id: <your_subnet_id>
  vpc_id: <vpc_id>
```

**backend_variables.yml file**
```yaml
github_backend_priv_key: |
  <myretirement_api_github_key>

env_vars:
  DJANGO_SECRET_KEY: <your_django_secret_key>
  DJANGO_SUPERUSER_PASSWORD: <your_django_superuser_password>
  DJANGO_SUPERUSER_EMAIL: <your_django_superuser_email>
  DJANGO_EMPLOYEE_NAME: <your_django_employee_name>
  DJANGO_EMPLOYEE_PASSWORD: <your_django_employee_password>
  DJANGO_EMPLOYEE_EMAIL: <your_django_employee_email>
```

**frontend_variables.yml file**
```yaml
github_frontend_priv_key: |
  <myretirement_gui_github_key>
```

**db_credentials.yml file**
```yaml
DB_ADMIN_NAME: <your_db_admin_name>
DB_ADMIN_PASS: <your_db_admin_pass>

dev_db_credentials:
  ROOT_PASS: <your_dev_db_root_pass>
  DB_NAME: <your_dev_db_name>
  DB_USER: <your_dev_db_user>
  DB_PASS: <your_dev_db_pass>

prod_db_credentials:
  ROOT_PASS: <your_prod_db_root_pass>
  DB_NAME: <your_prod_db_name>
  DB_USER: <your_prod_db_user>
  DB_PASS: <your_dev_db_pass>
```
### Scenario B
In the directory /myretirementapp_ansible_deployment/ansible_deploy/sub_playbooks/vars, add  .yml files that use these templates

**aws_credentials.yml file**
```yaml
aws_credentials:
  CERT_EMAIL: <your_email>
  aws_access_key: <your_aws_access_key>
  aws_secret_access_key: <your_aws_secret_access_key>

network_config:
  subnet_id: <your_subnet_id>
  vpc_id: <vpc_id>
```

**deploy_backend_vars.yml file**
```yaml
github_backend_priv_key: |
  <myretirement_api_github_key>

backend_dev_env_vars:
  DB_HOST: <your_dev_db_host>
  DB_NAME: <your_dev_db_name>
  DB_USER: <your_dev_db_user>
  DB_PASS: <your_dev_db_password>
  ROOT_PASS: <your_dev_db_root_pass>
  DJANGO_SECRET_KEY: <your_django_secret_key>
  DJANGO_SUPERUSER_PASSWORD: <your_django_superuser_password>
  DJANGO_SUPERUSER_EMAIL: <your_django_superuser_email>
  DJANGO_EMPLOYEE_NAME: <your_django_employee_name>
  DJANGO_EMPLOYEE_PASSWORD: <your_django_employee_password>
  DJANGO_EMPLOYEE_EMAIL: <your_django_employee_email>
  DJANGO_CUSTOMER_NAME: <your_django_customer_name>
  DJANGO_CUSTOMER_PASSWORD: <your_django_customer_password>
  DJANGO_CUSTOMER_EMAIL: <your_django_customer_email>
  EMAIL_PORT: <your_mailhog_port>

backend_prod_env_vars:
  ROOT_PASS: <your_prod_db_root_pass>
  DB_NAME: <your_prod_db_name>
  DB_USER: <your_prod_db_user>
  DB_PASS: <your_prod_db_password>
  DJANGO_SECRET_KEY: <your_django_secret_key>
  DJANGO_SUPERUSER_PASSWORD: <your_django_superuser_password>
  DJANGO_SUPERUSER_EMAIL: <your_django_superuser_email>
  DJANGO_EMPLOYEE_NAME: <your_django_employee_name>
  DJANGO_EMPLOYEE_PASSWORD: <your_django_employee_password>
  DJANGO_EMPLOYEE_EMAIL: <your_django_employee_email>
  DJANGO_CUSTOMER_NAME: <your_django_customer_name>
  DJANGO_CUSTOMER_PASSWORD: <your_django_customer_password>
  DJANGO_CUSTOMER_EMAIL: <your_django_customer_email>
  EMAIL_PORT: <your_mailhog_port>
```

**deploy_frontend_vars.yml**
```yml
github_frontend_priv_key: |
  <myretirement_gui_github_key>
```
  






