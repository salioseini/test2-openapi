

# validation du template pour controler erreurs
aws cloudformation validate-template --template-body file://resources.yml  --profile admin-dev-account

#  deploy 

0. Pour la première fois , créer un bucket:
aws s3 mb s3://pi-spi-api-packaged  --region eu-west-1 --profile admin-dev-account

1. aws cloudformation package --template-file resources.yml --output-template packaged.yaml --s3-bucket pi-spi-api-packaged  --profile admin-dev-account

2. aws cloudformation deploy --region eu-west-1 --template-file packaged.yaml --stack-name api-spi --capabilities CAPABILITY_NAMED_IAM --profile admin-dev-account

#  delete 
aws cloudformation delete-stack --stack-name api-spi --region eu-west-1 

# snyk test
1. snyk iac test --json > snyk_report.json   
2. snyk auth "auth token"
3. snyk-to-html -i snyk_report.json -o snyk_report.html