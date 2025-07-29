### **🧪 문제 1: 특정 IP 차단 상태 확인 후 차단 설정**

#### **✅ 실행 예시**

$ sudo ./problem1.sh

\[INFO\] 현재 rich rule 목록에 192.168.0.100 차단 룰이 존재하지 않습니다.

\[INFO\] 차단 룰을 추가합니다...

success

또는

$ sudo ./problem1.sh

\[INFO\] 192.168.0.100은 이미 차단되어 있습니다.

\[SKIP\] 추가 작업을 수행하지 않습니다.
```
#!/bin/bash

Blocked_IP=$1
Check=$(sudo firewall-cmd --permanent --list-rich-rule | grep "$Blocked_IP")

if [ -z "$Check" ]; then
  echo "[INFO] 현재 rich rule 목록에 "$Blocked_IP" 차단 룰이 존재하지 않습니다."

  sudo firewall-cmd --permanent --add-rich-rule="rule family='ipv4' source address='$Blocked_IP' reject" &> /dev/null
  echo "[INFO] 차단 룰을 추가합니다..."  
  echo "Success"
else
  echo "[INFO] '$Blocked_IP'은 이미 차단되어 있습니다."
fi
~                                                                                    
~                                                                                    
~                     
```
---

### **🔒 문제 2: 포트 8080이 열려 있다면 닫기**

#### **✅ 실행 예시**

$ sudo ./problem2.sh

\[INFO\] 포트 8080/tcp 이 열려 있습니다. 제거합니다...

success

또는

$ sudo ./problem2.sh

\[INFO\] 포트 8080/tcp 이 열려 있지 않습니다. 아무 작업도 수행하지 않습니다.

```
#!/bin/bash

PORT=$1
Check=$(sudo firewall-cmd --list-ports | grep "$PORT"/tcp)

if [ -n "$Check" ]; then
  echo "[INFO] 포트 '$PORT'/tcp 이 열려 있습니다. 제거합니다..."        
  sudo firewall-cmd --permanent --remove-"$PORT"=["$PORT"/tcp] &> /dev/null

else
  echo "[INFO] 포트 '$PORT'/tcp 이 열려 있지 않습니다. 아무 작업도 수행하지 않습니다.
"
fi
~                       
```


---

### **🧩 문제 3: SSH 서비스 제거 후 특정 IP만 허용**

#### **✅ 실행 예시**

$ sudo ./problem3.sh

\[INFO\] SSH 서비스가 열려 있습니다. 제거합니다...

success

\[INFO\] 192.168.0.10 IP에만 포트 22 허용 규칙을 추가합니다...

success

또는

$ sudo ./problem3.sh

\[INFO\] SSH 서비스가 이미 제거되어 있습니다.

\[INFO\] 포트 22 허용 규칙만 추가합니다...

success

---

