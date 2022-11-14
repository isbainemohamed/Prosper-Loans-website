# Caloans

Caloans is a plateform that helps peer to peer credits agencies (like Prosper) to determine whether a borrower will be able to pay his debts completely or not.
It is a ML-based application that returns predicted eligibility after entering data related to the client.

The particularity of this project is that it is cloud-based (Azure, IBM Cloud and Google Cloud Platform). We used different cloud providers to discover the maximum of them.

## Project structure
The project started from data ingestion techniques, data Lake, data warehousing , data visualization, Exploratory Data Analysis, Data Modeling, Web Development, and CI/CD Pipeline for deployment.

![project structure](https://github.com/isbainemohamed/Prosper-Loans-website/blob/e15b53e54fb5e70b54cd8d70b7e8c18e5becca68/images/project%20structure.png)

### Repository structure:
* Images: contains screenshots and code snippets from the project
* Data warehousing and laking: contains scripts and code used to perform data warehousing
* Data Modeling: contains machine learning notebooks used to build model 
* Presentation : contains project final presentation


## Deployment of application 

This part is a guide on how you can deploy our app on your local server:

1- prepare environment:

```bash
sudo apt update
```

![screen 1](https://github.com/isbainemohamed/Prosper-Loans-website/blob/e15b53e54fb5e70b54cd8d70b7e8c18e5becca68/images/screen1.png)


```bash
sudo apt install python3.8 -y
```
![screen 1](https://github.com/isbainemohamed/Prosper-Loans-website/blob/e15b53e54fb5e70b54cd8d70b7e8c18e5becca68/images/screen%202.png)

Check python version

```bash
python3.8 --version
```
![screen 1](https://github.com/isbainemohamed/Prosper-Loans-website/blob/e15b53e54fb5e70b54cd8d70b7e8c18e5becca68/images/screen%203.png)


```bash
apt-get upgrade -y
```

![screen 1](https://github.com/isbainemohamed/Prosper-Loans-website/blob/e15b53e54fb5e70b54cd8d70b7e8c18e5becca68/images/screen%204.png)

```bash
sudo apt-get install python3 python3-pip python3-dev build-essential libssl-dev libffi-dev python3-setuptools -y
```

![screen 1](https://github.com/isbainemohamed/Prosper-Loans-website/blob/e15b53e54fb5e70b54cd8d70b7e8c18e5becca68/images/screen%205.png)

```bash
sudo apt-get install python3-venv -y
```

![screen 1](https://github.com/isbainemohamed/Prosper-Loans-website/blob/e15b53e54fb5e70b54cd8d70b7e8c18e5becca68/images/screen%206.png)


```bash
sudo apt-get install nginx -y
```
![screen 1](https://github.com/isbainemohamed/Prosper-Loans-website/blob/e15b53e54fb5e70b54cd8d70b7e8c18e5becca68/images/screen%207.png)

```bash
sudo systemctl start nginx
```
![screen 1](https://github.com/isbainemohamed/Prosper-Loans-website/blob/e15b53e54fb5e70b54cd8d70b7e8c18e5becca68/images/screen%208.png)

==> systemctl start nginx

screen 8

==> systemctl enable nginx

screen 9


==> git clone https://github.com/isbainemohamed/Prosper-Loans-website.git
screen 10

==> python3 -m venv venv

screen 11

==> source venv/bin/activate

screen 12

==> pip install wheel
screen 13

==> pip install gunicorn flask

screen 14

==> create wsgi.py file with following content
from app import app
if __name__ == "__main__":
    app.run()

screen 15

==> pip install -r requirements.txt

screen 16

==> pip install scikit-learn

screen 17

==> gunicorn --bind 0.0.0.0:5000 wsgi:app

screen 18

==> deactivate ( to desactivate environment)

screen 19

==> sudo nano /etc/systemd/system/flask.service

content: 
[Unit]
Description=Gunicorn instance to serve Flask
After=network.target
[Service]
User=root
Group=www-data
WorkingDirectory=/home/productionmachine/Prosper-Loans-website
Environment="PATH=/home/productionmachine/Prosper-Loans-website/env/bin"
ExecStart=/home/productionmachine/Prosper-Loans-website/env/bin/gunicorn --bind 0.0.0.0:5000 wsgi:app
[Install]
WantedBy=multi-user.target

screen 20


==> sudo chown -R root:www-data /home/deploy/Prosper-Loans-website

screen 21

==> sudo chown -R 775 /home/deploy/Prosper-Loans-website
screen 22

==> systemctl daemon-reload
screen 23
==> systemctl start flask

screen 24

==> systemctl enable flask
screen 25

==> systemctl status flask

screen 26

==> nano /etc/nginx/conf.d/flask.conf

content: server {
    listen 80;
    server_name 20.126.48.131;  
    location / {
        include proxy_params;
        proxy_pass  http://127.0.0.1:5000;
    }
}
 
screen 27


==> sudo nginx -t

screen 28

==> systemctl restart nginx

screen 29


==> access to the website via ip address on browser

http://20.126.48.131/

screen 30
