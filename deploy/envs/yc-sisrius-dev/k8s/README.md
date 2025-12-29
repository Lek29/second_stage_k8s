## Как задеплоить тестовый веб-сервер

1. Перейдите в корень проекта.
2. Примените манифест пода:
   `kubectl apply -f deploy/envs/yc-sirius-dev/k8s/test-pod.yaml`
3. Примените манифест сервиса:
   `kubectl apply -f deploy/envs/yc-sirius-dev/k8s/test-service.yaml`
4. Для проверки используйте Port Forwarding в Lens на сервис `test-nginx-service`.
---
## как подготовит dev окружение
1. Скачайте SSL-сертификат Яндекс Облака: Invoke-WebRequest -Uri "https://storage.yandexcloud.net/cloud-certs/CA.pem" -OutFile "CA.pem"

2. Создайте секрет в кластере: kubectl create secret generic postgres-ca-cert --from-file=root.crt=CA.pem -n edu-stanislav-hatylev