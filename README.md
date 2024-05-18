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




</details>