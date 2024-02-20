# niknav83_infra

## Таблица адресов

| Имя машины     |  Внутренний IPv4 | Публичный IPv4  |
|---------       |-----------       |--------------   |
|bastion         | 10.128.0.9/24    | 130.193.48.211  |
|someinternalhost| 10.128.0.6/24    |       —         |

## Адреса для проверки:

 bastion_IP = 130.193.48.211

 someinternalhost_IP = 10.128.0.6

## Подключение к someinternalhost в одну команду:

```
 ssh -i ~/.ssh/niknav83 -J niknav83@130.193.48.211 niknav83@10.128.0.6

```

130.193.48.211  - публичный IP jump-сервера

niknav83        - имя ключа

Публичный ключ прописан в настройках каждой виртуальной машины.

## Вариант решения для подключения из консоли при помощи команды вида ssh someinternalhost

Чтобы подключиться к серверу за jump сервером используя короткую команду нужно создать alias в файле ~/.ssh/config следующего содержания:

```
Host bastion
        HostName 130.193.48.211
        IdentityFile  ~/.ssh/niknav83 
        User niknav83

Host someinternalhost
        HostName someinternalhost
        IdentityFile  ~/.ssh/niknav83 
        Port 22
        User niknav83
        ProxyJump bastion

```

После этого можно подключаться командой ssh someinternalhost

## Дополнительное задание

### Реализуйте использование валидного сертификата для панели управления VPN-сервера

Задание с созданием валидного SSL сертификата выполнил взяв свой домен.

https://pritunl.niknav.ru/
