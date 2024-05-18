# Установка Kubernetes, тестирование различных сценариев, заметки

---

## Установка kubernetus 1.29.4 на ubuntu 22.0 

knode1 - 172.17.50.122 - мастер нода

knode2 - 172.17.50.128 - воркер 1

knode3 - 172.17.50.12- воркер 2


<details>
  <summary>Подготовительная часть</summary>

Добавляем запись в hosts т.к. не используем dns

 ```
printf "\n172.17.50.122 knode1\n172.17.50.128 knode2\n172.17.50.129 knode3\n\n" >> /etc/hosts
 ```

Отключаем  swap - vim /etc/fstab/ и комментируем строку

 ```
#/swap.img      none    swap    sw      0       0
 ```

обновляем репозитории, ставим обновления, ставим необходимые пакеты

 ```
apt update && apt -y upgrade && apt -y install apt-transport-https ca-certificates curl gnupg2 software-properties-common
```

Загружаем сетевые модули из ядра и создаем конфигурационный файл k8s.conf с указанными модулями.
```
cat <<EOF | tee /etc/modules-load.d/k8s.conf
overlay
br_netfilter
EOF
```
```
modprobe overlay
modprobe br_netfilter
```

проверяем что модули активированы

```
lsmod | egrep "br_netfilter|overlay"
```

![TCP_Handshake](img/tcp-connection.png)     Картинка !


включаем сетевые параметры отвечающие за маршрутизация трафика через сетевой мост, нужно для работы сетевых (CNI) плагинов кубера работающих через iptables.

```
cat <<EOF | tee /etc/sysctl.d/k8s.conf
net.bridge.bridge-nf-call-iptables  = 1
net.bridge.bridge-nf-call-ip6tables = 1
net.ipv4.ip_forward                 = 1
EOF
```

Перезапускаем параметры ядра

```
sysctl --system
```
Выключаем firewalld:

```
systemctl stop ufw && systemctl disable ufw
```

</details>


<details>
  <summary>Часть установки</summary>

  </details>
