# My EC2 Web App

This is a simple static website designed for automatic deployment on an EC2 instance using GitHub Actions.

## Files

- `index.html`: The main landing page

## Deployment

GitHub Actions workflow will:
1. SSH into the EC2 instance
2. Copy the latest files via SCP
3. Replace the existing web app
4. Restart Apache or NGINX server
