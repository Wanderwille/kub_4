# Домашнее задание к занятию «Сетевое взаимодействие в K8S. Часть 1» - Подус Сергей

### Задание 1. Создать Deployment и обеспечить доступ к контейнерам приложения по разным портам из другого Pod внутри кластера

1. Создать Deployment приложения, состоящего из двух контейнеров (nginx и multitool), с количеством реплик 3 шт.
2. Создать Service, который обеспечит доступ внутри кластера до контейнеров приложения из п.1 по порту 9001 — nginx 80, по 9002 — multitool 8080.
3. Создать отдельный Pod с приложением multitool и убедиться с помощью `curl`, что из пода есть доступ до приложения из п.1 по разным портам в разные контейнеры.
4. Продемонстрировать доступ с помощью `curl` по доменному имени сервиса.
5. Предоставить манифесты Deployment и Service в решении, а также скриншоты или вывод команды п.4.

------

### Задание 2. Создать Service и обеспечить доступ к приложениям снаружи кластера

1. Создать отдельный Service приложения из Задания 1 с возможностью доступа снаружи кластера к nginx, используя тип NodePort.
2. Продемонстрировать доступ с помощью браузера или `curl` с локального компьютера.
3. Предоставить манифест и Service в решении, а также скриншоты или вывод команды п.2.

## Ответ:

### Задание 1

1. 

Манифест находиться в папке src:

![Scrin 1](https://github.com/Wanderwille/scrinshot/blob/scrin2/kube4/namespaces.png)

![Scrin 2](https://github.com/Wanderwille/scrinshot/blob/scrin2/kube4/deploy.png)

2. 

Манифест находиться в папке src:

![Scrin 2](https://github.com/Wanderwille/scrinshot/blob/scrin2/kube4/service.png)

3. 

Манифест находиться в папке src:

![Scrin 3](https://github.com/Wanderwille/scrinshot/blob/scrin2/kube4/multitool.png)

``` bash

root@User:/mnt/c/Users/serpo/OneDrive/Документы/DZ_docker/kubik/kub_4/src# kubectl exec -n homework-4 test-multitool -- curl 10.1.38.71:80
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   612  100   612    0     0   138k      0 --:--:-- --:--:-- --:--:--  149k
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
    body {
        width: 35em;
        margin: 0 auto;
        font-family: Tahoma, Verdana, Arial, sans-serif;
    }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
```

```bash
root@User:/mnt/c/Users/serpo/OneDrive/Документы/DZ_docker/kubik/kub_4/src# kubectl exec -n homework-4 test-multitool -- curl 10.1.38.71:8080
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   149  100   149    0     0  72860      0 --:--:-- --:--:-- --:--:--  145k
WBITT Network MultiTool (with NGINX) - test-deployment-5fb59cd8fc-574f4 - 10.1.38.71 - HTTP: 8080 , HTTPS: 443 . (Formerly praqma/network-multitool)
```

```bash
root@User:/mnt/c/Users/serpo/OneDrive/Документы/DZ_docker/kubik/kub_4/src# kubectl exec -n homework-4 test-multitool -- curl 10.1.38.125:80
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   612  100   612    0     0   348k      0 --:--:-- --:--:-- --:--:--  597k
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
    body {
        width: 35em;
        margin: 0 auto;
        font-family: Tahoma, Verdana, Arial, sans-serif;
    }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
```

```bash
root@User:/mnt/c/Users/serpo/OneDrive/Документы/DZ_docker/kubik/kub_4/src# kubectl exec -n homework-4 test-multitool -- curl 10.1.38.125:8080
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   150  100   150    0     0  89179      0 --:--:-- --:--:-- --:--:--  146k
WBITT Network MultiTool (with NGINX) - test-deployment-5fb59cd8fc-ngcbm - 10.1.38.125 - HTTP: 8080 , HTTPS: 443 . (Formerly praqma/network-multitool)
```

```bash
root@User:/mnt/c/Users/serpo/OneDrive/Документы/DZ_docker/kubik/kub_4/src# kubectl exec -n homework-4 test-multitool -- curl 10.1.38.126:80
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   612  100   612    0     0   350k      0 --:--:-- --:--:-- --:--:--  597k
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
    body {
        width: 35em;
        margin: 0 auto;
        font-family: Tahoma, Verdana, Arial, sans-serif;
    }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
```

```bash
root@User:/mnt/c/Users/serpo/OneDrive/Документы/DZ_docker/kubik/kub_4/src# kubectl exec -n homework-4 test-multitool -- curl 10.1.38.126:8080
WBITT Network MultiTool (with NGINX) - test-deployment-5fb59cd8fc-wvz8h - 10.1.38.126 - HTTP: 8080 , HTTPS: 443 . (Formerly praqma/network-multitool)
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   150  100   150    0     0  90525      0 --:--:-- --:--:-- --:--:--  146k
```

```bash
root@User:/mnt/c/Users/serpo/OneDrive/Документы/DZ_docker/kubik/kub_4/src# kubectl exec -n homework-4 test-multitool -- curl 10.1.38.126:8080
WBITT Network MultiTool (with NGINX) - test-deployment-5fb59cd8fc-wvz8h - 10.1.38.126 - HTTP: 8080 , HTTPS: 443 . (Formerly praqma/network-multitool)
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   150  100   150    0     0  90525      0 --:--:-- --:--:-- --:--:--  146k
```

4. 

![Scrin 4](https://github.com/Wanderwille/scrinshot/blob/scrin2/kube4/curl.png)

### Задание 2

1. Манифест находится в папке src:

2. 

![Scrin 5](https://github.com/Wanderwille/scrinshot/blob/scrin2/kube4/nginx.png)

![Scrin 6](https://github.com/Wanderwille/scrinshot/blob/scrin2/kube4/multitiiol.png)