```python
import socket
import threading

# 포트 스캔 함수
def scan_port(ip, port):
    with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
        s.settimeout(1)
        if s.connect_ex((ip, port)) == 0:
            print(f"열려 있는 포트 발견: {port}")

# 메인 실행 함수
def main():
    ip = input("스캔할 IP 주소를 입력하세요: ")
    start_port = int(input("시작 포트를 입력하세요: "))
    end_port = int(input("끝 포트를 입력하세요: "))

    print(f"{ip}의 포트 {start_port} ~ {end_port} 스캔 시작...")

    threads = []
    for port in range(start_port, end_port + 1):
        thread = threading.Thread(target=scan_port, args=(ip, port))
        threads.append(thread)
        thread.start()

    for thread in threads:
        thread.join()

    print("스캔 완료!")

if __name__ == "__main__":
    main()
```
scanner.py 로 저장하고
```
python scanner.py
``` 실행
