# HTB/Starting Point/Redemmer
---
Starting with an NMAP Scan of my target ip `nmap -sV {IP}` I got no responce by default nmap scans 1000 of the most common ports, we need to scan the rest. `$ nmap -p- -sV -v {Target-IP}` will scan all ports it might take a minute so I added -v for verbose so I can follow the scan status. That returned with an open TCP port (6379) [Task #1].
![Screenshot from 2023-11-08 03-25-41](https://github.com/Elusive-Enigma/Hacking-CTFs/assets/149143123/e33dd1bc-7c75-4db7-9d52-5463028552a7)
From our scan we can also see the service is Redis [Task #2].

---

[Task #3] is askes what kind of database is Redis after a quick google search Redis lables its self as a (In-memory
non-relational database) compared to our two options (In-memory Database) is the correct option.
In order to connect to the server lets use redis-cli [Task #4] The Command to connect is `$ redis-cli -h {Target-IP} -p 6379`as you can see -h <hostname> and -p <port> [Task #5]

![Screenshot from 2023-11-08 03-43-44](https://github.com/Elusive-Enigma/Hacking-CTFs/assets/149143123/78afb3f8-5923-4fe0-86f5-da777cfc357f)


---

Once Connected i typed help to see what options I had. Out of the list "help <tab>' seemed the best
tabbing through my options i saw @server `help @server` listed a lot of options and reading them i found Since [Task #6] asks (Once connected to a Redis server, which command is used to obtain the information and statistics about the Redis server?) `info` fits that criteria

![Screenshot from 2023-11-08 03-56-45](https://github.com/Elusive-Enigma/Hacking-CTFs/assets/149143123/0fdf016a-d45b-4cdd-be20-4b564ad31ee9)

---

In the info section it states the version 5.0.7 multple times [Task # 7]
under `help @connection` select will allow us to "change the selected database for the current connection" [Task #8] That shows up their are 4 keys [Task #9]
![Screenshot from 2023-11-08 04-04-22](https://github.com/Elusive-Enigma/Hacking-CTFs/assets/149143123/9a134aaf-e95e-4502-aa82-76e22ad2e4b1)


---

Lets `select 0` to select the database and `keys *` [Task #10] to show all keys within the database  followed by `get flag` and it will show our flag!

![Screenshot from 2023-11-08 04-07-54](https://github.com/Elusive-Enigma/Hacking-CTFs/assets/149143123/b9bd1baf-a3f3-4978-aaef-044422a8ef4c)

