# Client-Server-Architecture-with-MySQL

Client-Server is an architecture in which two or more computers are connected together over a network to send and receive requests between one another.

1. Create and configure two linux based virtual servers (EC2 instances in AWS) ``` mysql-server```
and ``` mysql-client```

![AWS](https://github.com/user-attachments/assets/21ac0420-a545-4c06-b760-0a87a24d2a46)

![instances](https://github.com/user-attachments/assets/a4d30b23-5084-4689-9782-3229fd7c4457)

2. Install MySQL on both servers

On ```mysql server ``` install MySQL server software
```sh
sudo apt-get update
sudo apt-get install mysql-server
```
On ```mysql client ``` install MySQL client software
```sh
sudo apt-get update
sudo apt-get install mysql-client
```

3. Confirm that the both servers are runing
```sh
sudo systemctl status mysql
```

![mysql-server](https://github.com/user-attachments/assets/b0cc13e4-a380-49aa-b80e-c6c456411608)

![mysql-client](https://github.com/user-attachments/assets/71f55ae3-dbb0-47ed-a838-918a8eb20e9d)

4. Use mysql server's local IP address to connect from mysql client. MySQL sever uses TCP PORT 3306  by default. Hence, add a new in Inbound rule in mysql server.

5. Configure MySQL server to allow. Replace ```127.0.0.1``` to ```0.0.0.0```
![bind-address](https://github.com/user-attachments/assets/84c9f4af-9db0-4ac3-9b0f-ae2cbac24162)

6. Restart ```mysql-server```

```sh
sudo systemctl restart mysql
```

7. From mysql client Linux Server connect remotely to mysql server Database Engine without using ssh. The mysql utility must be use to perform this action by:

Login to ```mysql-server```
  ```sh
  sudo mysql
  ```
![mysql-login](https://github.com/user-attachments/assets/b5b6883e-5e5a-4be8-ae67-4e962802647e)

Create a new user with remote access privileges
```sh
CREATE USER '<user-name>'@'<Client-server-ip>' IDENTIFIED WITH mysql_native_password BY '<password>';
```

Grant privileges to the remote user
```sh
GRANT <permissions> ON <database>.* TO 'remote_user'@'client_ip' WITH GRANT OPTION;
```

After creating the user and granting privileges, flush the privileges to ensure the changes take effect
```sh
FLUSH PRIVILEGES;
```
Exit ```mysql-server``` shell 
```sh
exit
```

8. Connect to ```mysql-server``` from ```mysql-cient``` and check that the remote MySQL server is successfully connected.
```sh
mysql -u client -p -h <mysql-server-ip>
```
```sh
SHOW DATABASES;
```
![connect](https://github.com/user-attachments/assets/9487032c-dea7-46e6-bff9-75d7c5eeaf53)

# Conclusion
This is a successfull implementation of a Client Server Architecture using MySQL Database Management System System  

