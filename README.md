# วิธี เชื่อมต่อ Database ด้วยวิธี remote ผ่าน ssh tunnel ใน MacOS

## วิธีที่ 1.
```bash
ssh -N -L localhost:[local port]:[host หรือ IP ของ DB]:[DB Port] [username ของเครื่องที่ต้องการ remote]@[host/ip ของเครื่องที่จะ ssh]
```

### ตัวอย่างการเชื่อมต่อ PostgreSQL
```bash
ssh -N -L localhost:54321:192.168.1.100:5432 root@203.19.202.111
```
- localhost คือเครื่อง local ตามด้วย :54321 เป็น port ที่ใช้ในเครื่อง local จะเป็น port ใดก็ได้ที่ไม่ซ้ำกับ port อื่นๆบนเครื่อง
- :192.168.1.100 คือ IP ของ DB Server ตามด้วย :5432 เป็น port เริ่มต้นของ PostgreSQL
- root@203.19.202.111 คือ username ตามด้วย IP ของเครื่องที่ต้องการทะลุ tunnel ไปบางครั้งอาจเป็นคนละเครื่องกับ DB Server แต่เครื่องนั้นอยู่ใน local เดียวกันก็สามารถทำได้

## วิธีที่สอง 2.
กรณีที่ต้องการเชื่อมต่อแบบนานๆ
```bash
ssh -f -N -M -S /tmp/sshtunnel -L localhost:[local port]:[host หรือ IP ของ DB]:[DB Port] [username ของเครื่องที่ต้องการ remote]@[host/ip ของเครื่องที่จะ ssh]
```

### ตัวอย่างการเชื่อมต่อ
```bash
 ssh -f -N -M -S /tmp/sshtunnel -L localhost:54321:192.168.1.100:5432 root@203.19.202.111
```
- localhost คือเครื่อง local ตามด้วย :54321 เป็น port ที่ใช้ในเครื่อง local จะเป็น port ใดก็ได้ที่ไม่ซ้ำกับ port อื่นๆบนเครื่อง
- :192.168.1.100 คือ IP ของ DB Server ตามด้วย :5432 เป็น port เริ่มต้นของ PostgreSQL
- root@203.19.202.111 คือ username ตามด้วย IP ของเครื่องที่ต้องการทะลุ tunnel ไปบางครั้งอาจเป็นคนละเครื่องกับ DB Server แต่เครื่องนั้นอยู่ใน local เดียวกันก็สามารถทำได้

### ตั้งค่า SSH บนเครื่อง Mac
สามารถตั้งค่าให้ local เชื่อมต่ออยู่ตลอดเวลาโดยการสั่งให้เครื่องทำการ Interval ตลอดทุกช่วงเวลาดังนี้
```bash
nano ~/.ssh/config
```
...
```
Host *
    ServerAliveInterval 120
    TCPKeepAlive no
```

