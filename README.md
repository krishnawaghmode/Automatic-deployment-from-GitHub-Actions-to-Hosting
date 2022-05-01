# Automatic Deployment from GitHub Actions To Hosting Server (PHP ,Laravel ,VueJs & NuxtJs Websites)

<img src="https://raw.githubusercontent.com/krishnawaghmode/attendance_task/main/screenshots/Screenshot1.png" width="800">

## Setup PHP Website in GitHub Actions
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
