#### Wireshark

* search parameters
```
filter: http.request.method == GET
filter: http.request.method == POST
filter: udp.port==53
filter: ftp (follow tcp-stream)
filter: ftp-data (line-based text data)
```
