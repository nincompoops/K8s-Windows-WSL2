# K8s-Windows-WSL2

Windows WSL2 환경에서 Kubernetes를 학습하고 실습하는 프로젝트 모음입니다.

---

## Labs

### [Flask-K8s](./labs/Flask-K8s)
Flask + React + Kubernetes 풀스택 이미지 갤러리 애플리케이션

**기술 스택:**
- Backend: Flask (Python)
- Frontend: React
- Container: Docker
- Orchestration: Kubernetes (Minikube)

**주요 기능:**
- 사용자 정보 API
- 카테고리별 이미지 업로드 (Colleague, Family, Etc)
- 이미지 갤러리 뷰어

[자세한 실행 방법 보기](./labs/Flask-K8s/README.md)

---

## 환경 설정

### 필수 요구사항
- Windows 11 with WSL2
- Docker Desktop
- Minikube
- kubectl
- Node.js 18+
- Python 3.10+

### 설치 가이드

#### 1. WSL2 설치 (Windows)
```powershell
# PowerShell 관리자 권한으로 실행
wsl --install
```

#### 2. Docker Desktop 설치
- [Docker Desktop for Windows](https://www.docker.com/products/docker-desktop/) 다운로드 및 설치
- WSL2 통합 활성화

#### 3. kubectl 설치 (WSL2 Ubuntu)
```bash
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
kubectl version --client
```

#### 4. Minikube 설치 (WSL2 Ubuntu)
```bash
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
minikube version
```

#### 5. Node.js 설치 (WSL2 Ubuntu)
```bash
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
sudo apt install -y nodejs
node --version
npm --version
```

#### 6. Python 설치 (WSL2 Ubuntu)
```bash
sudo apt update
sudo apt install -y python3.10 python3-pip
python3 --version
```

### 초기 설정

#### Minikube 시작
```bash
minikube start --driver=docker
minikube status
```

#### Docker 환경 연결
```bash
eval $(minikube docker-env)
```

---

## 학습 내용

- Kubernetes 기본 개념 (Pod, Service, Deployment)
- Docker 컨테이너화 및 이미지 빌드
- 마이크로서비스 아키텍처
- Frontend-Backend 분리 및 API 통신
- Kubernetes 네트워킹 (ClusterIP, NodePort, 포트 포워딩)
- CORS 설정 및 처리

---

## 빠른 시작
```bash
# 1. 저장소 클론
git clone <repository-url>
cd K8s-Windows-WSL2

# 2. Minikube 시작
minikube start

# 3. 원하는 Lab으로 이동
cd labs/Flask-K8s

# 4. 각 Lab의 README.md 참고하여 실행
```

---
