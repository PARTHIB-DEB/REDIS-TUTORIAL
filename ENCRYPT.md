# SECURE YOUR SERVER 

❗**I have applied these steps on redis-server only . I hope it will be same for valkey-servers**

When we are using redis in any production based application, we definitely need to take care about the data that is stored inside it. Keeping its importance for caching , 
we can apply security mechanisms by ACL . The steps to encrypt **redis-cli** under the hood ACL are -

## STEPS

- **Start The Redis Server**

(```redis-server``` or ```valkey-server``` won't work here because , these commands are running servers without ```sudo``` priviledges which causes to not access the ```redis.conf``` file )
```bash
  sudo service <redis or valkey>-server start
# or
  sudo systemctl start <redis or valkey>
```

- **See active users**

```bash
   127.0.0.1:6379> ACL LIST
   1) "user default on nopass sanitize-payload ~* &* +@all"
```

- **Create a new user (with privileges like ```default```**)

```bash
   127.0.0.1:6379> ACL SETUSER myuser on >mypassword allcommands allkeys
   OK
```

- **Save the information of new user**

```bash
   127.0.0.1:6379> ACL SAVE
   # or
   127.0.0.1:6379> CONFIG REWRITE  (If error occurs in ACL SAVE , then this command will save this info in /etc/redis/redis.conf)
   OK
```
🔦 **_Check if the new user's data is inserted or not by ➡️ ```nano /etc/redis/redis.conf``` and go at the end of the file_**

- **Login by new user's credentials**
  I am showing 3 ways to login here .


  - **From ```default``` user , inside ```redis-cli```**


  ```bash
     127.0.0.1:6379> AUTH myuser mypassword
     OK
     127.0.0.1:6379> ACL WHOAMI
     "myuser"
  ```
  
  - **Using an Url , directly to ```redis-cli```**
    (can use **localhost** , instead of **127.0.0.1**)


  ```bash
     root@rootuser:~$ redis-cli -u redis://myuser:mypassword@127.0.0.1:6379
     Warning: Using a password with '-a' or '-u' option on the command line interface may not be safe.
     127.0.0.1:6379> ACL WHOAMI
     "myuser"
  ```

  - **Using username and password , directly to ```redis-cli```**


  ```bash
     root@rootuser:~$ redis-cli --user myuser --pass mypassword
     Warning: Using a password with '-a' or '-u' option on the command line interface may not be safe.
     127.0.0.1:6379> ACL WHOAMI
     "myuser"
  ```

- **Make Defaultuser off**

  Why its necessary ? because the default user is the default admin user who has access see and apply change to any database , key-value pairs of any user even before the authentication.
  so its necessary to keep it off and make this user a new admin user.
  
  The difference willbe , now redis-cli will always seek authentication by showing ```NOAUTH authentication required``` message , if authentication is not done

  ```bash
    127.0.0.1:6379> ACL SETUSER default off
    OK
    127.0.0.1:6379> CONFIG REWRITE  # Make it permanent (BEFORE THIS STEP , NOT YOUR ADMIN USERNAME AND PASSWORD SOMEWHERE)

    # Restart your redis-server the same way you started , you can even kill the process to begin at a fresh pace , after restarting the server it will look like this -
    root@rootuser:~$ redis-cli
    127.0.0.1:6379> ACL LIST
    (error) NOAUTH Authentication required.  # Now Do the Login using the admin username and password
  ```
