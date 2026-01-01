## Как задеплоить тестовый веб-сервер

1. Перейдите в корень проекта.
2. Примените манифест пода:
   `kubectl apply -f deploy/envs/yc-sirius-dev/k8s/test-pod.yaml`
3. Примените манифест сервиса:
   `kubectl apply -f deploy/envs/yc-sirius-dev/k8s/test-service.yaml`
4. Для проверки используйте Port Forwarding в Lens на сервис `test-nginx-service`.
---
## Как подготовит dev окружение
1. Скачайте SSL-сертификат Яндекс Облака: Invoke-WebRequest -Uri "https://storage.yandexcloud.net/cloud-certs/CA.pem" -OutFile "CA.pem"

2. Создайте секрет в кластере: kubectl create secret generic postgres-ca-cert --from-file=root.crt=CA.pem -n edu-stanislav-hatylev
---
## Сборка и публикация образов
Для деплоя приложения используется версионирование образов по хэшу `Git-коммита`. Это позволяет избежать конфликтов версий и обеспечивает возможность быстрого отката.

### 1. Подготовка окружения
Убедитесь, что вы авторизованы в Docker Hub:

```Bash

docker login
```
### 2. Сборка образа
Сборка производится из корня папки приложения. В качестве тега используется короткий хэш текущего коммита:

```Bash

# Узнаем хэш
$TAG = git rev-parse --short HEAD
# Собираем
docker build -t lekan29/django-app:$TAG ./backend_main_django
```

### 3. Публикация
Отправьте собранный образ в удаленный репозиторий:

```Bash

docker push username/django-app:$TAG
```