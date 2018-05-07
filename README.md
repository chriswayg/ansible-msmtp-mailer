[![Build Status](https://travis-ci.org/chriswayg/ansible-msmtp.svg?branch=master)](https://travis-ci.org/chriswayg/ansible-msmtp)

# chriswayg.msmtp-mailer

This ansible role deploys msmtp for Debian / Ubuntu.

## Prerequisite
* Having ansible installed on your workstation.
* Having an SMTP server

## How to install
* Use github to clone/fork into your role directory
* ansible galaxy ```ansible-galaxy install chriswayg.msmtp-mailer```

## Variables
  All the default variables are located **defaults/main.yml**. Mostly you would need to configure the following variables.
  - *msmtp_accounts:* You can define one or more smtp accounts:

      ```
      msmtp_accounts:
      - account  : gmail
        host     : smtp.gmail.com
        port     : 587
        auth     : "on"
        from     : example@gmail.example
        user     : example@gmail.example
        password : "some password"
      - account  : mysmtp
        host     : smtp.example
        port     : 587
        auth     : "on"
        from     : admin@example.org
        user     : myuser@example.org
        password : plain-text-password2
      ```
  - *msmtp_default_account:* Default smtp account to use

    ```msmtp_default_account: "gmail"```

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

## Configure
You can configure your variables in ansible with one of the following

 * Create a variable in host/group variables directory. (recommended)
 * Editing var/main.yml
 * Run ansible-playbook with -e
 * Edit the default/main.yml (not recommended)

## Run
**By default mstmp will work as the configuration uses a real smtp server (for testing only!)**

  ```ansible-playbook -l hostname msmtp.yml```

## Test
  You should get a test mail if it works on the root mail

## Documentation
[msmtp manual](http://msmtp.sourceforge.net/doc/msmtp.html)
