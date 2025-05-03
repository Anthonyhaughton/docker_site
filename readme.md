# Dockerized Website with AWS S3 Integration

This project sets up a Docker container running an NGINX web server that serves static files from an AWS S3 bucket.

## Prerequisites

- Docker
- AWS account
- AWS CLI configured with appropriate access credentials
- Git

## Project Structure
```
├── group_vars
│ └── docker.yaml
├── hosts
├── playbooks
│ ├── deploy_website.yaml
│ ├── docker
│ │ └── dockerfile
│ └── roles
│ ├── build_docker_image
│ │ └── tasks
│ │ └── main.yaml
│ ├── copy_dockerfile
│ │ └── tasks
│ │ └── main.yaml
│ ├── install_docker
│ │ └── tasks
│ │ └── main.yaml
│ ├── run_docker_container
│ │ └── tasks
│ │ └── main.yaml
│ └── update_repos
│ └── tasks
│ └── main.yaml
└── readme.md
```

## Running the Project

1. **Create an IAM user for Docker**:

    - Sign in to the AWS Management Console.
    - Open the IAM console at https://console.aws.amazon.com/iam/.
    - In the navigation pane, choose **Users** and then choose **Add user**.
    - For **User name**, enter `docker`.
    - Choose **Attach existing policies directly** and select **AmazonS3ReadOnlyAccess** (or the appropriate policy for your needs).
    - Copy the **Access key ID** and **Secret access key**. You'll need these to fill in the Dockerfile environment variables.

2. **Fill in the Dockerfile environment variables**:

    Replace the placeholders in your Dockerfile with the AWS credentials you copied:

    ```Dockerfile
    ENV AWS_ACCESS_KEY_ID=your_access_key_id
    ENV AWS_SECRET_ACCESS_KEY=your_secret_access_key
    ```

3. **Run the Playbook**:

    Assuimg you have your hosts file set up along with the account you will be running the plays with on the remote host:

    ansible-playbook -i hosts -k -u ansible playbooks/deploy_website.yaml -vvv

6. **Access the website**:

   Open a web browser and navigate to `http://<your-ec2-instance-ip>`
