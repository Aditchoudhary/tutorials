# RUN LOCALSTACK ON MAC 


Pull localstack latest image using docker

```
docker pull localstack/localstack
```


Start LocalStack Container: Run the following command to start the LocalStack container. This command exposes the required ports and mounts the data directory for persistent storage:

```
- docker run -d --name localstack -p 4566:4566 -e SERVICES=s3,dynamodb -e DATA_DIR=/tmp/localstack/data localstack/localstack
```


Explanation of the options used in the docker run command:

-d: Run the container in detached mode.
--name localstack: Assign the name "localstack" to the container for easier management.
-p 4566:4566: Map port 4566 from the container to the same port on the host machine. This is the port used by LocalStack for services like S3 and DynamoDB.
-e SERVICES=s3,dynamodb: Specify which AWS services to run. In this example, we're running S3 and DynamoDB, but you can add more services separated by commas if needed.
-e DATA_DIR=/tmp/localstack/data: Set the data directory path inside the container for persistent storage.



Verify LocalStack Status: You can check if the LocalStack container is running using the following command:

```
docker ps
```



Test LocalStack: LocalStack is now running, and you can interact with it using AWS CLI or SDKs.

```
aws --endpoint-url=http://localhost:4566 s3 ls
```



Install Homebrew (if not already installed):
Open Terminal and run the following command to install Homebrew, which is a popular package manager for macOS:

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```


Install AWS CLI using Homebrew:
After installing Homebrew, run the following command to install the AWS CLI:

```
brew install awscli
```


Once the installation is complete, verify that the AWS CLI is working correctly by running:

```
aws --version
```


Run the following command to create a dummy AWS profile named "localstack":

```
aws configure --profile localstack
```


You will be prompted to provide AWS Access Key ID, AWS Secret Access Key, Default region name, and Default output format. However, since LocalStack doesn't require actual AWS credentials, you can input dummy values for them. For example:
```
AWS Access Key ID [None]: dummy-access-key
AWS Secret Access Key [None]: dummy-secret-key
Default region name [None]: us-west-2
Default output format [None]: json
```

Now, you can run AWS CLI commands with the --profile option set to "localstack" and get s3 bucket list
```
aws --profile localstack --endpoint-url=http://localhost:4566 s3 ls
```


To create an S3 bucket using the AWS CLI with LocalStack, follow these steps:

```
aws --profile localstack --endpoint-url=http://localhost:4566 s3 mb s3://my-test-bucket
```
