# lambda-containers


## Hello World Example

Docker build and run locally

```bash
cd helloworld

docker build -t helloworld:latest .

docker run -p 9000:8080 helloworld:latest

curl -XPOST "http://localhost:9000/2015-03-31/functions/function/invocations" -d '{}'
```

Deploy to ECR helloworld repository

```bash
aws ecr get-login-password --region eu-central-1 | docker login --username AWS --password-stdin  <aws-account-id>.dkr.ecr.eu-central-1.amazonaws.com

docker tag helloworld:latest <aws-account-id>.dkr.ecr.eu-central-1.amazonaws.com/helloworld:latest

docker push <aws-account-id>.dkr.ecr.eu-central-1.amazonaws.com/helloworld:latest
```

Use ECR container image in lambda

1. In AWS Lambda click `Create Function`
2. Choose `Container image`
3. As `Function name` pick `helloworld`
4. As `Container image URI` pick `helloworld` container image from ECR
5. Click `Create function`