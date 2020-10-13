<a href="https://play.google.com/store/apps/details?id=app.witwork.vpn"><img alt="Get it on Google Play" src="https://play.google.com/intl/en_us/badges/images/generic/en-play-badge.png" height=60px /></a>

# WitVPN - High Speed Free VPN Proxy
### Why you should install WitVPN now:

► Unblock Websites and Apps

► Unlimited access, 500+ fast proxy servers

► Secure Your Device anywhere

► Surf anonymously at Fast Speed & stably

► Shield WiFi Hotspot and Privacy Protection


WitVPN free version shows ads. Upgrade to premium to enjoy unlimited and ad-free VPN!


Contact us

If you have any questions or suggestions, feel free to reach us on hello@witwork.app for more information.

By the way, don’t forget to follow our Facebook https://www.facebook.com/witworkapp to stay tuned.

# DOCUMENT
When installing a VPN, I need you to prepare the following:
* [Server] - Linux/ Centos, Debian 
* [Firebase] -  Authenticate, Cloud Firestore
* [Onesginal] 
## !!! --- SERVER --- !!!
`**Note: We recommend that you use Google VM Instance or AWS EC2`
#### ► Install OpenVPN Server:
##### Copy file `openvpn.sh` from `server` folder and upload to your server
- Upgrade `apt`
```sh
$ sudo apt-get update
```
- Install `wget`  
```sh
$ sudo apt-get install wget
```
- Make excute with `openvpn.sh` 
```sh
$ sudo chmod +x openvpn.sh
```
- Install OpenVPN 
```sh
$ sudo ./openvpn.sh
```
- Start OpenVPN Service
```sh
$ sudo service openvpn start
```
Make  sure OpenVPN service is running
#### ► Create OpenVPN User:
- Show menu 
```sh
$ sudo ./openvpn.sh
```

```sh
Select an option:
   1) Add a new client
   2) Revoke an existing client
   3) Remove OpenVPN
   4) Exit
'Option: 1' <-- choose option 1

Provide a name for the client:
Name: withworkvpn
```
- After entering the name and enter, Terminal will export the log as shown below and the ovpn file is located in the path : `/root/withworkvpn.ovpn`
```sh
--> Last line
'withworkvpn added. Configuration available in: /root/withworkvpn.ovpn'
```
`**Note: The server you need to allow access to port 1194 from outside`

## !!! --- FIREBASE --- !!!
*** Setup Firebase CLI for deploy CMS Admin. See [Document](https://firebase.google.com/docs/cli)
#### ► Setup CMS Admin
* Go to the `admin` directory and install firebase cli
* Init Firebase `hosting`
```sh
$ cd admin
$ firebase init hosting
----
'❯ Create a new project' <-- choose this line
```
* Enter name of project
```sh
? Please specify a unique project id (warning: cannot be modified afterward) [6-30 characters]:
 () 'WitVPN' 
```
`Note: The name of projectId is unique, you must not enter an existing name or if the same, Google will return an error and you have to look in the firebase-debug file for more details.`
* Enter for default Id (leave it empty)
```sh
? What would you like to call your project? (defaults to your project ID) () 'Enter'
```
*  Enter (leave it empty)
```sh
? What do you want to use as your public directory? (public) 'Enter'
Configure as a single-page app (rewrite all urls to /index.html)? (y/N) 'N'
```
* Final: Congratulations on having successfully set up a project
 ```sh
✔  Firebase initialization complete!
```
* Build Webpacke , If you can't build it, check out the section  `Note: NVM Install`
```sh
$ cd admin & yarn install & yarn build 
```
* Edit file `firebase.json` bellow:
```sh
{
  "hosting": {
    "public": "build",
    "ignore": [
      "firebase.json",
      "**/.*",
      "**/node_modules/**"
    ],
    "rewrites": [ {
      "source": "**",
      "destination": "/index.html"
    }]
  }
}
```
* Copy Firebase Config from `Firebase -> Project Settings -> Tab General -> Under Your App` and edit file `src/configs/index.js` 

* Final step: Deploy your package to firesbase hosting
```sh
$ firebase deploy
```
* Here are the results after you deploy successfully
```sh
=== Deploying to 'wit-vpn'...
...
✔  Deploy complete!
Project Console: https://console.firebase.google.com/project/wit-vpn/overview
Hosting URL: https://wit-vpn.****
```
`Note: Note that when you build using node version 12.10.0, you can customize the node version using nvm`
#### ► NVM Install: [Document](https://github.com/nvm-sh/nvm) 
1. curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.36.0/install.sh | bash
2. command -v nvm
3. nvm install node
4. nvm use node 12.10.0

#### ► Cloud Function For Admin:
1. Remove User
2. Edit User

`Coming soon: Create server, limit bandwith, create specific server for special users`
* Go to the `admin` folder and install firebase cloud functions
```sh
$ firebase init functions
```
* Deploy function 
```sh
$ firebase deploy --only functions
```
* Final
```sh
✔  Deploy complete!
```

## !!! --- ANDROID --- !!!
- Change Package Id
- Change Google Admob ID (ADMOB_ID) in `app/build.gradle`
- Change Onesignal Id (onesignal_app_id) in `app/build.gradle`
- Download google-service.json from Firebase 

