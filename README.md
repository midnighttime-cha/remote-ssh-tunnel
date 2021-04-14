# Remote ssh tunnel in MacOS

## Solution 1.
```bash
ssh -N -L localhost:[localport]:[APPLICATION ADDRESS]:[PORT] [SSH USERNAME]@[SSH ADDRESS]
```

### Example
```bash
ssh -N -L localhost:5432:192.168.1.100:5432 root@203.19.202.111
```

## Solution 2.
```bash
ssh -f -N -M -S /tmp/sshtunnel -L localhost:[localport]:[APPLICATION ADDRESS]:[PORT] [SSH USERNAME]@[SSH ADDRESS]
```

### Example
```bash
 ssh -f -N -M -S /tmp/sshtunnel -L localhost:5432:192.168.1.100:5432 root@203.19.202.111
```
make a temp file for ssh tunnel all time.

