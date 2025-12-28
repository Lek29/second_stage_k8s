## Как задеплоить тестовый веб-сервер

1. Перейдите в корень проекта.
2. Примените манифест пода:
   `kubectl apply -f deploy/envs/yc-sirius-dev/k8s/test-pod.yaml`
3. Примените манифест сервиса:
   `kubectl apply -f deploy/envs/yc-sirius-dev/k8s/test-service.yaml`
4. Для проверки используйте Port Forwarding в Lens на сервис `test-nginx-service`.