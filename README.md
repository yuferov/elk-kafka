This is a stydy project where I set up ELK (Filebeat, Elasticsearch, Kibana) with Kafka broker (plus Zookeep) to analyze system logs from remote server with filebeat.

It contains:

- docker-compose file to set up containers with  ELK and kafka on main server.
- filebeat config file - to configure kafka server IP [you need to change the server IP to correctly configure connection].
- .env file with variables for docker-compose [which is unnecessary, but I thought it is useful to have all variables in one place].

I didn't add the SSL connection yet, I will try to figure it out in different branch.


My dashboard:
![dash](https://user-images.githubusercontent.com/78160022/114172296-24d6a180-993e-11eb-8aa5-36820db986db.png)

To convert log messages to JSON I used default Node Pipeline (I tuned it up a little - to parse messages that contain "Started" and "Starting" words to visualize number of restarted services).
My additional grok pattern:

%{SYSLOGTIMESTAMP:system.syslog.timestamp} %{SYSLOGHOST:host.hostname} %{DATA:process.name} %{WORD:system.status} %{WORD:system.service} %{GREEDYMULTILINE:system.syslog.message}.

The upper left Lens contains the list of services that has been launched numerous times (filters: system.status: Started; process.name: exists).

The upper right Lens contains the list of services that run on the system (filters: system.service).

The bottom left Lens contains the number of services that has been logging the message beginning with "Starting" (filters: system.status: Starting).

The bottom right Lens contains the number of services that has been logging the message beginning with "Started" (filters: system.status: Started).

The result is inprecise and I think I need to either change the pattern or I need to somehow filter data using processors in filebeat, or maybe chage logging template in rsyslog.
