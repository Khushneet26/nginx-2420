Setting Up a Web Server with Arch Linux
This tutorial will guide you through setting up a web server using Arch Linux on DigitalOcean. We will start after connecting to the Arch Linux server using SSH key authentication.

1. Connecting to Arch Linux Server:
Creating a digital Ocean Account:
Sure, here's how you can create a DigitalOcean droplet:

Sign in to DigitalOcean:
Go to the DigitalOcean website (https://www.digitalocean.com/) and sign in to your account. If you don't have an account, you'll need to create one.

Create a New Droplet:
Once logged in, navigate to the "Droplets" section in the DigitalOcean dashboard and click the "Create Droplet" button.

Choose an Operating System:
Select the operating system you want to use for your droplet. In this case, choose "Arch Linux" from the available options.

Choose a Plan:
Select the plan that best fits your requirements. DigitalOcean offers various plans with different amounts of CPU, RAM, and storage.

Choose a Datacenter Region:
Choose the datacenter region where you want to deploy your droplet. Select the region closest to your target audience for optimal performance.

Select Additional Options (Optional):
You can configure additional options such as enabling backups, adding SSH keys for secure authentication, enabling monitoring, and more. Configure these options according to your needs.

Add SSH Keys (Optional but Recommended):
If you haven't already added SSH keys to your DigitalOcean account, you can add them during droplet creation. SSH keys provide a more secure way to access your droplet compared to passwords.

Finalize and Create Droplet:
Review your selections and configurations, then click the "Create Droplet" button to deploy your droplet. DigitalOcean will provision the droplet according to your specifications.

Accessing Your Droplet:
Once the droplet is created, you will receive an email with the droplet's IP address and login credentials. You can use SSH to connect to your droplet using the provided IP address and username/password.

Configuring Your Droplet:
After accessing your droplet, you can follow the instructions in the previous tutorial to set up a web server using Arch Linux and Nginx.
Connect to your Arch Linux server using SSH. Replace your_username and your_server_ip with your server's username and IP address:

bash
Copy code
ssh -i /.ssh/do-key arch@143.198.155.245
Enter your password or passphrase when prompted.

2. Installing Necessary Software
First, let's install the necessary software, including Vim for editing files and Nginx for serving web pages.

Installing Vim
bash
Copy code
sudo pacman -S vim
Installing Nginx
bash
Copy code
sudo pacman -S nginx
3. Configuring Nginx
Now, let's configure Nginx to serve web pages.

Creating Project Directory
Create a directory to store your website documents:

bash
Copy code
sudo mkdir -p /web/html/nginx-2420
Creating Server Block Configuration
Create a new server block configuration file for your project:

bash
Copy code

server {
    listen 80;
    server_name 143.198.155.245;

    root /web/html/nginx-2420;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }
}
EOF
Replace your_server_ip with your server's IP address.

Enabling Server Block
Create a symbolic link to enable the server block:

bash
Copy code
sudo ln -s /etc/nginx/sites-available/nginx-2420 /etc/nginx/sites-enabled/
Testing Nginx Configuration
Test the Nginx configuration to ensure there are no syntax errors:

bash
Copy code
sudo nginx -t
If the test is successful, reload Nginx to apply the changes:

bash
Copy code
sudo systemctl reload nginx
4. Serving a Sample Web Page
Let's serve a sample web page to verify that Nginx is working correctly.

Create an index.html file with sample content:
bash
Copy code
sudo tee /web/html/nginx-2420/index.html >/dev/null <<EOF
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>2420</title>
    <style>
        * {
            color: #db4b4b;
            background: #16161e;
        }
        body {
            display: flex;
            align-items: center;
            justify-content: center;
            height: 100vh;
            margin: 0;
        }
        h1 {
            text-align: center;
            font-family: sans-serif;
        }
    </style>
</head>
<body>
    <h1>All your base are belong to us</h1>
</body>
</html>

5. Create a git hub Repository:
Sign in to GitHub:
Open your web browser and go to the GitHub website (https://github.com/). If you don't have an account, you'll need to sign up for one.

Navigate to Your Profile:
Once logged in, click on your profile icon in the top-right corner of the page to access your profile.

Create a New Repository:
On your profile page, click on the "Repositories" tab, then click on the green "New" button.

Fill in Repository Details:
You'll be taken to a page where you can fill in the details for your new repository:

Repository Name: Enter a name for your repository. This should be unique and descriptive.
Description (Optional): Add a brief description of your repository to help others understand its purpose.
Visibility: Choose whether you want your repository to be public (visible to everyone) or private (visible only to you and collaborators).
Initialize this repository with a README: Check this option if you want to create a README file for your repository. It's recommended to do this, especially if you're starting a new project.
Add .gitignore: You can select a template for the .gitignore file, which specifies which files and directories should be ignored by Git.
Add a license: You can choose a license for your repository to specify how others can use your code.
Create Repository:
After filling in the details, click the green "Create repository" button. Your new repository will be created, and you'll be taken to its main page.

Clone Repository (Optional):
If you want to work with the repository on your local machine, you can clone it using Git. Copy the repository's URL from the address bar and use the git clone command in your terminal:

bash
Copy code
git clone <repository_url>
Replace <repository_url> with the URL of your repository.
Verify that Nginx is serving the web page by accessing it in your web browser. Open a web browser and enter the IP address of your server. You should see the sample web page.
Conclusion
Congratulations! You have successfully set up a web server using Arch Linux and Nginx. You can now host your website or web applications on your server.

This tutorial has covered the installation of necessary software, configuration of Nginx, serving a sample web page, and verifying the setup.
