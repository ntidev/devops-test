# DevOps - Test

This is a test to be done as part of the recruitment process at Net Tech International.

The test has a time to completion of **7 days** after the initial email is sent by one of our members.

**IMPORTANT: THE COMPLETION OF THIS TEST DOES NOT GUARANTEE THAT A CANDIDATE WILL GET HIRED**

## Test

The development team is working on a new revolutionary application coded in Javascript with a NodeJS server that shows the IP address of the server running it.

As part of the deployment to production, the team needs your help setting up the necessary infrastructure for the app and the deployment process of it. You can find the app to be deployed at this link https://github.com/ntidev/revolutionary-app

For a successful deployment to production of this and future versions of the app, we need you to establish our deployment process using multiple well known tools. These are the requirements for this project:

### Setting up AWS Infrastructure

In the two sections below this one, we are going to be setting up the project image creation and deployment process, but before doing all of that, we need to have our infrastructure ready:

1. Set up a new EC2 instance with a Linux distro of your preference (should be appropriate for server usage).

2. Configure security groups for the instance so that ports for HTTP and HTTPS are accessible by everyone, but SSH access requires adding the public IP of the person trying to access the server.

3. Create the next four IAM users in your AWS account:
 - One admin user for yourself, so you don't access your account with the root user.
 - One user for the NTI team to evaluate the exam, this user should **only have access to**:
    - EC2.
    - S3.
    - ECR
    - Read-only access to IAM.
    - Any additional service you use for your exam that you need us to have access to evaluate the exam.
 - One support user with READ-only access to EC2 and S3.
 - One user with permission to write images to ECR only. You will need this later for the image creation process. This user will need to have their access key generated.
 

**Additional IAM requirements**:

- All of the users above should have permissions set by the group they belong to (create any group if necessary) and not individually.

- All users should have 2FA enabled. Make sure to securely store the credentials and 2FA token used for every user. This will be evaluated.


### Setting Up the Image Creation Process

1. Clone the app project and set it up with Docker and Docker Compose allowing easy docker image creation and easily running our production version with Docker.

2. Upload your project to GitHub.

3. Setup GitHub Actions (in the **production** branch of the project)that does this:
    - Install the dependencies for the app (using yarn).
    - Builds the docker image.
    - Pushes the image to AWS ECR (Elastic Container Registry) service.

To confirm the process above works as intended, the image should be reconstructed and pushed to AWS ECR service every time a new commit is pushed to the `production branch only` or every time a new merge from another branch to the production branch is completed. This will allow the development team to have their production image automatically constructed and ready in AWS every time they have new changes ready on this branch.

### Setting up the deployment process 

1. Having your image creation process ready, you now need to set up the deployment process of your images:

    - Set up the project to use Ansible for configuration management and deployment, the environment variables file `.env` should have a template version `.env.j2` that allows loading these variables from a `hosts.yml` file as typically used with Ansible. The Ansible configuration should be set up in a way that executing the template pulls the image from AWS ECR (automatically uploaded by GitHub Actions) and runs it with docker locally.

    - Set up an AWX instance (Ansible GUI) and configure a new project that allows easy deployment of the new changes to your server.

If all of the above is correctly set up, you should be able to log in to AWX and with the simple push of a button, execute the ansible template and install the project by pulling the docker image in AWS ECR service and running it with docker into your EC2 machine. After the project is installed it should be accessible via the internet either on its dynamic public IP or in its domain (if you complete the bonus task below)


### Bonus Points

- Using Bitbucket Pipelines instead of GitHub Actions for building and uploading the image to AWS ECR service. 

- Representing your AWS infrastructure in Terraform.

- Setting up the project with Traefik with a domain name and HTTPS so the service is accessible to the public via a domain (This might cost you money, so it is completly optional).

- The dev team is planning on uploading some files and integrating the APP with S3 in the future. Set up some S3 buckets as follows:
    - One `public-resources` bucket that has public access for everyone with a simple HMTL file on it. The contents of the file can be whatever you want.
    - One `private-resources` that **cannot be** accessed via any public method. You can host any files you want here.

### NOTES
- If there's anything you need that is not provided, please let us know

- Try to keep your expenses in the free tier, we designed the test in a way that you don't have to spend money or the amount spent is a minumum.

### Submission

In order for the submission of the test to be successful you need to reply to the email with the documents attached to it if any documents are created. We will definitely meet to review all of the above. 


**IMPORTANT**
- **As a common practice, try to make your documentation/explanations be as friendly as possible. We might assign someone who's not technical to review it**
- **Documentation is very important to us**


### Questions
If you have any questions or doubts regarding what needs to be done feel free to contact us using the same email trail and we will be happy to assist you.
