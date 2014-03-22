[![Build Status](https://travis-ci.org/ahelal/ansible-msmtp.svg?branch=master)](https://travis-ci.org/ahelal/ansible-msmtp)
#Readme

This ansible role deploys msmtp for Ubuntu 12.04 (tested on vagrant)

##Prerequisite
* Having ansible installed on your workstation. 
* Having an SMTP server 

##How to install
* Use github to clone/fork in your role directory
* ansible galaxy ```ansible-galaxy install adham.helal.msmtp```

##Variables 
  All the default variables are located **defaults/main.yml**. Mostly you would need to configure the following variables. 
  - *msmtp_accounts:* You can define one or more smtp account 
 
      ```
      msmtp_accounts:
      - account  : "gmail"
        host     : "smtp.gmail.com"
        port     : 587
        auth     : "on"
        user     : "example@gmail.example"
        password : "some password"
      - account  : "mysmtp"
        host     : "smtp.example"
        port     : 587
        auth     : "on"
        user     : "myuser"
        password : "123456"
      ```
  - *msmtp_default_account:* Default smtp account to use 

    ```msmtp_default_account: "gmail"```

  - *msmtp_from:* From field

    ```msmtp_from : "No Reply"```
  
  - Logging 
     - Option A (syslog)
     
       ```
        msmtp_log : "syslog"
       ```

     - Option B (file logging)
     
       ```
        msmtp_log     : "file"
        msmtp_logfile : /var/log/msmtp.log
       ```

     - Option C (No logging)

       ```
        msmtp_log     : "no"
       ```

  - Mail aliases 
     - *msmtp_alias_default:* default email this required 

       ```msmtp_alias_default : ops@example.com```

     - *msmtp_alias_root:* root email this is optional

       ```msmtp_alias_root : root@example.com```

     - *msmtp_alias_cron:* cron email this optional

       ```msmtp_alias_cron : cron@example.com``` 

##Configure
You can configure your variables in ansible with one of the following

 * Create a variable in host/group variables directory. (recommended)
 * Editing var/main.yml
 * Run ansible-playbook with -e
 * Edit the default/main.yml (not recommended)

##Run
**By default the mstmp will fail because the configuration uses a bogus smtp server you need to use a valid smtp server**
    
  ```ansible-playbook -l hostname msmtp.yml```

##Test
  You should get a test mail if it works on the root mail

##Possible issues
 From field requires more work 
[http://msmtp.sourceforge.net/doc/msmtp.html#Envelope_002dfrom-address](http://msmtp.sourceforge.net/doc/msmtp.html#Envelope_002dfrom-address) 
