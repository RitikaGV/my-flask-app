# Flask EC2 Deployment with Gunicorn and NGINX

This project is a minimal Flask web application deployed on an AWS EC2 instance using **Gunicorn** as the WSGI server and **NGINX** as a reverse proxy.


## 📁 Project Structure

my-flask-app/
├── app.py                # Main Flask app
├── wsgi.py               # WSGI entry point for Gunicorn
├── requirements.txt      # Python dependencies
├── templates/
│   └── index.html        # HTML template
├── static/               # (Optional) Static assets
└── README.md             # This file


## ⚙️ Requirements

- AWS EC2 instance (Amazon Linux 2 or Ubuntu)
- Python 3 and pip3
- NGINX
- Gunicorn
- Flask

## 🚀 Deployment Steps (Manual)

### ✅ On EC2

1. **Install dependencies**

sudo yum update -y
sudo yum install python3 nginx -y
pip3 install flask gunicorn

2. **Clone or upload your Flask app to EC2**

git clone https://github.com/your-username/my-flask-app.git
cd my-flask-app

3. **Run Flask app using Gunicorn**

nohup gunicorn --bind 127.0.0.1:8000 wsgi:app > gunicorn.log 2>&1 &

4. **Configure NGINX**
   Edit `/etc/nginx/nginx.conf` and replace the default `server {}` block with:

server {
    listen 80;
    server_name _;

    location / {
        proxy_pass http://127.0.0.1:8000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}

Then restart NGINX:
sudo nginx -t
sudo systemctl restart nginx

5. **Visit your app**

http://<EC2_PUBLIC_IP>


## 🧪 Local Development

pip install -r requirements.txt
python app.py

Visit: [http://localhost:5000](http://localhost:5000)


