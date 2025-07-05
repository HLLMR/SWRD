## 🔧 STEP 1: PROVISION YOUR VPS (THE RIGHT WAY)

### Recommended Specs:

- **Ubuntu 22.04 LTS**
    
- **2+ vCPU**, **4+ GB RAM** minimum
    
- **SSD-backed storage** (10GB+ for now)
    
- Optional: Enable swap if on small instance
    
- Domain (optional for now): `sword.local` or similar
    

### Recommended Providers:

- Hetzner, DigitalOcean, Linode, Vultr — all excellent
    
- Spin up via SSH key if possible (avoid password logins)
    

---

## 🧱 STEP 2: INSTALL DEPENDENCIES

SSH into your VPS and run the stack installer:

### ✅ 2.1 Install core packages

bash

sudo apt update && sudo apt upgrade -y
sudo apt install nginx php php-cli php-mbstring php-xml php-curl php-mysql php-bcmath php-zip php-gd unzip curl git mysql-server composer -y

### ✅ 2.2 Set up MySQL

bash

sudo mysql_secure_installation
# Then log in:
sudo mysql -u root -p

# Create database and user
CREATE DATABASE swrd DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
CREATE USER 'swrdu'@'localhost' IDENTIFIED BY 'yourpassword';
GRANT ALL PRIVILEGES ON swrd.* TO 'swrdu'@'localhost';
FLUSH PRIVILEGES;
EXIT;

---

## 🧰 STEP 3: INSTALL LARAVEL

bash

cd /var/www
composer create-project laravel/laravel swrd
cd swrd
cp .env.example .env
php artisan key:generate

Update `.env` with your DB settings:

ini

DB_DATABASE=swrdf
DB_USERNAME=swrdu
DB_PASSWORD=yourpassword

Give proper permissions:

bash

sudo chown -R www-data:www-data /var/www/swrd
sudo chmod -R 775 /var/www/swrd/storage /var/www/swrd/bootstrap/cache

---

## 🌐 STEP 4: CONFIGURE NGINX

bash

sudo nano /etc/nginx/sites-available/swrd

Paste:

nginx

server {
    listen 80;
    server_name yourdomain.com; # or your VPS IP

    root /var/www/swrd/public;
    index index.php index.html;

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php8.1-fpm.sock; # adjust version if needed
    }

    location ~ /\.ht {
        deny all;
    }
}

bash

sudo ln -s /etc/nginx/sites-available/swrd /etc/nginx/sites-enabled/
sudo nginx -t
sudo systemctl reload nginx

---

## 💡 STEP 5: INSTALL LARAVEL BREEZE (or Jetstream)

bash

CopyEdit

`composer require laravel/breeze --dev php artisan breeze:install npm install && npm run dev php artisan migrate`

This gives you:

- Auth
    
- Layout
    
- Tailwind
    
- Base scaffolding
    

---

## 🤖 STEP 6: SET UP CURSOR AI INTEGRATION

If you want to code with Cursor on your local machine but **deploy remotely**:

- Clone your Laravel project locally
    
- Connect it to your VPS via Git
    
- Push/pull as needed
    

If you want to **run Cursor directly on the server** (headless), that’s a bit trickier — usually it’s best to **develop locally and deploy remotely** until you're ready to expose an AI endpoint.

You _can_ eventually run a self-hosted agent or LLM service on the VPS (or adjacent one) to handle translations if you want full sovereignty.