# TIL

## ✅ 실습 시나리오 요약 (1번 ~ 5번)

### 1. 기본 웹 이중화 (Load Balancer + Web 서버 2대)

- **구성**:
    - LB → Web1, Web2
- **목표**:
    - 리눅스에서 Nginx 또는 HAProxy로 로드밸런서 설정
    - Apache/Nginx 설치하여 웹서버 구성
- **실습 포인트**:
    - 네트워크 설정
    - 서비스 설정
    - 방화벽(포트 개방: 80, 443)
    - 사용자 및 sudo 설정

---

### 2. DB 이중화 구성

- **구성**:
    - LB → DB1, DB2
- **목표**:
    - MariaDB or MySQL 서버 2대 구성
    - Master-Slave 또는 Master-Master 복제 실습
- **실습 포인트**:
    - DB 설치 및 replication 설정
    - 사용자 권한 설정
    - 네트워크 방화벽: 포트 3306 오픈

---

### 3. LAMP 구성 또는 Web-WAS-DB 3계층

- **구성 예시**:
    - Web → LB → WAS → DB
- **목표**:
    - LAMP (Linux + Apache + MySQL + PHP) 구성
    - 또는 Web 서버와 WAS를 분리한 구조 구성
- **실습 포인트**:
    - 아파치 + PHP 연동
    - PHPMyAdmin 설치 (옵션)
    - DB 연결 확인

---

### 4. 웹 + NFS 공유 + 이중화

- **구성**:
    - LB → W1, W2 → NFS 공유 → DB
- **목표**:
    - 웹 서버 간 파일 공유 (예: 이미지 업로드 디렉토리)
    - NFS 서버 구축 및 마운트 실습
- **실습 포인트**:
    - NFS 설치 및 export 설정
    - 마운트 자동화 (/etc/fstab)
    - 퍼미션 및 SELinux 확인

---

### 5. DHCP + iscsi + LB

- **구성**:
    - LB + Web + DB + iscsi storage
    - DHCP 서버와 iscsi target 구성
- **목표**:
    - DHCP 서버 구축 → 클라이언트 자동 IP 할당
    - iSCSI 서버/클라이언트 실습 → 원격 디스크 마운트
- **실습 포인트**:
    - iscsi-target, iscsi-initiator 설치
    - LVM으로 디스크 추가 구성

---

## 🎯 사이드 실습 항목과 매핑

| 항목 | 설명 | 연결 시나리오 |
| --- | --- | --- |
| 6. 네트워크 | NIC 설정, IP 할당, DHCP 사용 | 5번 DHCP 실습 |
| 7. 방화벽 | firewalld, iptables 실습 | 1~3번 포트 개방 |
| 8. 서비스 | systemctl enable/disable/start | 모든 서버 구성 |
| 9. 편집기 | vim, nano 사용법 | 설정 파일 수정 (httpd.conf, my.cnf 등) |
| 10. 사용자(SUDO) | sudoers 설정, 사용자 추가 | 웹/DB 운영계정 분리 |
| 11. 디스크(LVM) | 디스크 추가, 파티셔닝, LVM 구성 | 5번 iSCSI + LVM |

---

## 🔧 추가 제안 (리눅스 연습 팁)

- 각 서버를 VirtualBox로 VM 만들고 내부 네트워크로 구성
- Ansible이나 Shell Script로 반복작업 자동화 연습
- /etc/hosts로 간단한 DNS 흉내 가능

---

## ✅ 추천 리눅스 배포판 (2025년 기준)

| 배포판 | 버전 | 특징 |
| --- | --- | --- |
| **Rocky Linux** | **9.x (최신 안정버전)** | CentOS 후속, RHEL과 100% 호환, 서버 실습에 강력 추천 |
| **AlmaLinux** | 9.x | Rocky와 유사, RHEL 클론 |
| **Ubuntu Server** | **22.04 LTS (장기지원)** | 가장 친숙한 리눅스, 자료 많고 초보자 친화적 |
| **Debian** | 12 | 안정성 중시 시 추천 |
| **CentOS Stream** | X | 비추 – 더 이상 전통적 CentOS가 아님 (업스트림 테스트용) |

---

## 🥇 **가장 추천하는 조합**

### ✔ Rocky Linux 9 (혹은 AlmaLinux 9)

- 실무 환경과 유사한 RHEL 구조
- systemd, firewalld, SELinux, LVM 등 학습에 최적
- 보안 및 성능 실습 포함 가능

> ✅ ISO 다운로드:
> 
> 
> https://rockylinux.org/download
> 

---

## 🧰 가상머신 생성 기본 설정 (공통)

| 항목 | 추천값 |
| --- | --- |
| 이름 | rocky9-web1 / rocky9-db1 등 |
| OS 종류 | Linux / Red Hat (64-bit) |
| 메모리 | 최소 1024MB, 권장 2048MB |
| CPU | 1~2개 |
| 디스크 | 최소 20GB (동적 할당) |
| 네트워크 | 내부 네트워크 or NAT(Network Address Translation) + 포트포워딩 |
