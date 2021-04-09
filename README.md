This is a stydy project where I set up ELK (Filebeat, Elasticsearch, Kibana) with Kafka broker to analyze system logs from remote server with filebeat.

It contains:

- docker-compose file to set up containers with  ELK and kafka on main server.
- filebeat config file - to configure kafka server IP [you need to change the server IP to correctly configure connection].
- .env file with variables for docker-compose [which is unnecessary, but I thought it is useful to have all variables in one place].

I didn't add the SSL connection yet, try to figure it out in different branch.


My dashboard:
![dash](https://user-images.githubusercontent.com/78160022/114172296-24d6a180-993e-11eb-8aa5-36820db986db.png)
