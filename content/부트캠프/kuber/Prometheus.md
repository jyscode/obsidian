
오픈소스 모니터링 시스템
메트릭을 수집하고 저장하여 모니터링을 할 수 있는 환경 제공
수집된 데이터를 기반으로 알람을 발생시켜 빠른 장애 혹은 이슈를 인지


### 특징

메트릭 이름과 값, 레이블이라고 불리는 키값의 쌍으로 이루어진 다차원 모델의 데이터
다차원 데이터 모델의 사용을 위한 PromQL 쿼리 언어 사용
PULL 방식의 메트릭 수집

### 구성요소

**Prometheus**: 메트릭 수집 및 규칙 확인
**Grafana**: Prometheus로부터 받은 값을 토대로 데이터 시각화
**Alertmanager**: Prometheus로 부터 규칙에 해당하는 메트릭 정보를 받아 알람 발생
**Exporter**: 내부적으로 필요한 데이터 수집 및 수집 된 데이터 접근을 위한 포트 오픈
**Pushgateway**: Push방식으로 데이터가 수집되어야 할 경우 사용

### Prometheus 실행 옵션

```
--config.file: 프로메테우스 설정 위치
--storage.tsdb.path: 메트릭 데이터가 저장될 경로
--web.enable-lifecycle: http 요청을 통해 Prometheus를 제어
--storage.tsdb.retention.time: 데이터 저장에 대한 최소 보장 시간
--storage.tsdb.retention.size: Prometheus의 블록이 저장될 수 있는 최대 바이트 수
```

### Prometheus 설정

```
global: 전역으로 사용되는 설정 값
	scrap_interval: 메트릭 수집 주기(1m)
	scrap_timeout: 수집 요청 시에 timeout 시간(10s)
	evaluation_interval: rule_files에 명시된 규칙 확인 주기(1m)
```

```
alerting: Alertmanager에 관한 설정 명시
	alertmanager: 알람을 받을 Alertmanager 관련 설정
		follow_redirects: 수집 시 Redirection을 따를지 여부(기본 true)
		schema: 요청시 사용될 프로토콜 (http)
		timeout: Alertmanager가 알람을 받을 시 timeout 시간(10s)
		static_configs: Alertmanager로 사용할 서버 설정
			targets: Alertmanager로 사용될 대상 서버 목록
	rule_files: 메트릭 알람 조건
```


```
scrape_configs: 수집할 방법 및 대상 설정
	job_name: 수집된 메트릭에 할당할 그룹 이름
	scrape_interval: 메트릭 수집 주기
	scrape_timeout: 수집 요청시 timeout 시간
	metrics_path: 메트릭을 가져올 요청 경로(/metrics)
	schema: 요청 시 사용될 프로토콜(http)
	follow_redirects: 수집 시, redirection을 따를 지 여부(true)
	static_configs: 수집될 대상 서버 설정
	targets: 대상 서버 목록 
```

---
### 설치

Prometheus-community가 제공하는 helm chart 사용

Prometheus + Grafana + Prometheus Rules

```bash
k create ns monitoring
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update
helm install prometheus prometheus-community/kube-prometheus-stack -n monitoring
```

Prometheus, Grafana를 연결해주는 ingress 생성

vi prometheus-ingress.yaml
```
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: prometheus-ingress
  namespace: monitoring
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  ingressClassName: "nginx"
  rules:
    - host: prometheus.example.com
      http:
        paths:
          - path: /
            pathType: Prefix
            backend:
              service:
                name: prometheus-kube-prometheus-prometheus
                port:
                  number: 9090
```


vi grafana-ingress.yaml
```
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: grafana-ingress
  namespace: monitoring
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  ingressClassName: "nginx"
  rules:
  - host: grafana.example.com
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: prometheus-grafana
            port:
              number: 3000
```

k apply -f prometheus-ingress.yaml
k apply -f grafana-ingress.yaml


기존 IP 를 사용한 접근은 3 Tier App 이 차지 하고 있으므로 domain을 사용하여 접근한다!

/etc/hosts에 라우팅 설정
```
External-IP prometheus.example.com
External-IP grafana.example.com
```

---

시간 동기화 오류 - 중요!!!!

```
sudo systemctl stop chronyd
sudo chronyd -q 'server pool.ntp.org iburst'
sudo systemctl start chronyd

```


접속하기
LocalPC에서
`prometheus.example.com`
`grafana.example.com`



grafana ID
`admin`
grafana PW
`prom-operator`



