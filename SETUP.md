# 환경 설정 가이드

K8s-Windows-WSL2 프로젝트를 위한 개발 환경 설정 가이드입니다.

---

## 필수 요구사항

- Windows 11 (WSL2 지원)
- 최소 8GB RAM
- 20GB 이상 여유 디스크 공간

---

## 설치 단계

### 1. WSL2 설치

#### Windows PowerShell (관리자 권한)
```powershell
# WSL2 설치
wsl --install

# 재부팅 후 Ubuntu 설치 확인
wsl --list --verbose
```

#### Ubuntu 22.04 설정
```bash
# 업데이트
sudo apt update && sudo apt upgrade -y
```

---

### 2. Docker Desktop 설치

1. [Docker Desktop for Windows](https://www.docker.com/products/docker-desktop/) 다운로드
2. 설치 후 Docker Desktop 실행
3. **Settings → Resources → WSL Integration**
   - Enable integration with additional distros
   - Ubuntu 체크

#### 설치 확인
```bash
docker --version
docker run hello-world
```

---

### 3. kubectl 설치
```bash
# 최신 안정 버전 다운로드
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"

# 실행 권한 부여 및 설치
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl

# 설치 확인
kubectl version --client
```

#### 자동 완성 설정 (선택사항)
```bash
echo 'source <(kubectl completion bash)' >>~/.bashrc
echo 'alias k=kubectl' >>~/.bashrc
echo 'complete -o default -F __start_kubectl k' >>~/.bashrc
source ~/.bashrc
```

---

### 4. Minikube 설치
```bash
# Minikube 다운로드
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64

# 설치
sudo install minikube-linux-amd64 /usr/local/bin/minikube

# 설치 확인
minikube version
```

#### Minikube 시작
```bash
# Docker 드라이버로 시작
minikube start --driver=docker

# 상태 확인
minikube status
```

#### Minikube 유용한 명령어
```bash
# 중지
minikube stop

# 재시작
minikube start

# 삭제 (완전 초기화)
minikube delete

# 대시보드 열기
minikube dashboard
```

---

### 5. Node.js 설치 (Flask-K8s용)
```bash
# NodeSource 저장소 추가
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -

# Node.js 설치
sudo apt install -y nodejs

# 설치 확인
node --version  # v18.x.x
npm --version   # 9.x.x
```

---

### 6. Python 설치 (Flask-K8s용)
```bash
# Python 및 pip 설치
sudo apt update
sudo apt install -y python3.10 python3-pip python3-venv

# 설치 확인
python3 --version  # Python 3.10.x
pip3 --version
```

---

## 설치 확인

모든 도구가 제대로 설치되었는지 확인:
```bash
# 버전 확인
docker --version
kubectl version --client
minikube version
node --version
npm --version
python3 --version

# Minikube 상태 확인
minikube status
```

---

## Docker 환경 설정

Minikube의 Docker 데몬 사용하기:
```bash
# Minikube Docker 환경 설정
eval $(minikube docker-env)

# 확인
docker ps

# 원래 환경으로 돌아가기
eval $(minikube docker-env -u)
```

**중요:** 새 터미널을 열 때마다 `eval $(minikube docker-env)` 실행 필요

---

## 🐛 트러블슈팅

### WSL2 메모리 제한 설정

WSL2가 너무 많은 메모리를 사용하면:

**Windows 사용자 폴더에 `.wslconfig` 파일 생성**
```ini
[wsl2]
memory=4GB
processors=2
swap=2GB
```

설정 후 WSL2 재시작:
```powershell
wsl --shutdown
```

### Docker Desktop이 시작되지 않을 때

1. Docker Desktop 완전 종료
2. `%LOCALAPPDATA%\Docker` 폴더 삭제
3. Docker Desktop 재설치

### Minikube 시작 실패
```bash
# 기존 Minikube 삭제
minikube delete

# 재시작
minikube start --driver=docker --force
```

---

## 참고 자료

- [WSL2 공식 문서](https://docs.microsoft.com/en-us/windows/wsl/)
- [Docker Desktop 문서](https://docs.docker.com/desktop/windows/wsl/)
- [Kubernetes 공식 문서](https://kubernetes.io/docs/)
- [Minikube 공식 문서](https://minikube.sigs.k8s.io/docs/)

---

## 다음 단계

환경 설정이 완료되었다면:

1. [Flask-K8s 프로젝트](./labs/Flask-K8s/README.md) 실행해보기
2. [K8s-Troubleshooting](./labs/K8s-Troubleshooting) 사례 학습

---

## 팁

- `alias k=kubectl` 설정으로 타이핑 절약
- VS Code의 Kubernetes 확장 프로그램 사용 권장
- Minikube 대시보드로 시각적 관리 가능

---
