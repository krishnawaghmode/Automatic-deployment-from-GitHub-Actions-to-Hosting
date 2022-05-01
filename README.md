# Automatic Deployment from GitHub Actions To Hosting Server (PHP,Laravel,NuxtJs Websites deploy)

<img src="https://raw.githubusercontent.com/krishnawaghmode/Automatic-deployment-from-GitHub-Actions-to-Hosting/main/CI_CD.png" width="800" height="400"> 

## PHP Website in GitHub Actions
### cPanelDepolyment.yml
```bash
name: sms reminder system
on:
  push:
    branches:
      - main
jobs:
  FTP-Deploy-Action:
    name: FTP-Deploy-Action
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v2.1.0
      with:
        fetch-depth: 2
    - name: FTP-Deploy-Action
      uses: SamKirkland/FTP-Deploy-Action@3.1.1
      with:
        ftp-server: ${{ secrets.FTP_SERVER }}
        ftp-username: ${{ secrets.FTP_USERNAME }}
        ftp-password: ${{ secrets.FTP_PASSWORD }}
```
## Laravel Website in GitHub Actions
### LaravelDepolyment.yml
```bash
on: push
name: 🚀 Deploy website on push
jobs:
  web-deploy:
    name: 🎉 Deploy
    runs-on: ubuntu-latest
    steps:
    - name: 🚚 Get latest code
      uses: actions/checkout@v2

    - name: Use php 8.0
      uses: shivammathur/setup-php@master
      with:
        php-version: '8.0'
        
    - name: Copy .env
      run: php -r "file_exists('.env') || copy('.env.example', '.env');"
    - name: 🔨 Install Dependencies
      run: composer install
      
    - name: Generate key
      run: php artisan key:generate
    
    - name: Upload ftp
      uses: sebastianpopp/ftp-action@releases/v2
      with:
        host: ${{ secrets.FTP_SERVER }}
        user: ${{ secrets.FTP_USERNAME }}
        password: ${{ secrets.FTP_PASSWORD }}
```
## NuxtJs Website in GitHub Actions
### NuxtJs.yml
```bash
on: push
name: 🚀 Deploy website on push
jobs:
  web-deploy:
    name: 🎉 Deploy
    runs-on: ubuntu-latest
    steps:
    - name: 🚚 Get latest code
      uses: actions/checkout@v2

    - name: Use Node.js 14
      uses: actions/setup-node@v2
      with:
        node-version: '14'
      
    - name: 🔨 Build Project
      run: |
        npm install
        npm run generate
    
    - name: 📂 Sync files
        #uses: SamKirkland/FTP-Deploy-Action@4.2.0
      uses: sebastianpopp/ftp-action@releases/v2
      with:
        host: ${{ secrets.FTP_SERVER }}
        user: ${{ secrets.FTP_USERNAME }}
        password: ${{ secrets.FTP_PASSWORD }}
        localDir: ./dist/ 
```

