![Backend CD](https://github.com/JohnLi1999/closet/workflows/Backend%20CD/badge.svg)
![Node.js CI](https://github.com/JohnLi1999/closet/workflows/Node.js%20CI/badge.svg)
![Android CI](https://github.com/JohnLi1999/closet/workflows/Android%20CI/badge.svg)

# Azure Server
- VM Name: `closet`
- Public IP: `138.91.146.226`
- DNS: `closet-cpen321.westus.cloudapp.azure.com`
- User `closet`
- Password: (feel free to save your ssh keys)
- **Auto-shutdown**: 1:01:00 AM PST
- Is the server up and running? `curl http://closet-cpen321.westus.cloudapp.azure.com/version`

# Backend deployment
### Pull backend code
```sh
cd /home/closet/closet/backend    # change directory
git fetch --all                   # fetch all
git reset --hard origin/master    # remove all local chanegs!!!
npm install                       # if not installed
npm run test                      # feel free to run test to check
```

### Run as service `closet-backend`
- Service is set to restart on fail or on reboot
- Partial environemnt variable is set already in the service file
```sh
sudo systemctl status closet-backend    # check status (partial log)
sudo systemctl start closet-backend     # start service
sudo systemctl stop closet-backend      # stop service
sudo systemctl restart closet-backend   # restart service
sudo systemctl enable                   # enable to run on boot
```

### Service log
- Should also put into another location so we can have a clean log for each start of backend
```sh
journalctl -u closet-backend          # all logs (use SHIFT-G to go to the bottom)
journalctl -u closet-backend -f       # follow low
```

### Modify service
- A copy of service file is in this repository `closet/backend/closet-backend.service`
```sh
sudo vim /lib/systemd/system/closet-backend.service   # edit service file
sudo systemctl daemon-reload                          # reload service file
sudo systemctl start closet-backend                   # start service

sudo chmod +x /home/closet/closet/backend/index.js    # add exceutable permissions to express app
sudo chmod go+w /home/closet/closet/backend           # allows any users to write the app folder (for using fs)
```



