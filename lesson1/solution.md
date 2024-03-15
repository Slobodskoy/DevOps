## Сгенерируйте новый ssh ключ

```sh
ssh-keygen -t rsa -b 4096 -C "myemail@server.com"
```

## Создайте нового персонального пользователя на ВМ

```sh
sudo adduser userName
```

## Добавьте к новому пользователю публичную часть ключа

```sh
sudo mkdir -p /home/userName/.ssh
sudo cp ~/.ssh/id_rsa.pub /home/userName/.ssh/authorized_keys
```

## Добавите пользователя в группу wheel, sudo

```
sudo gpasswd -a userName wheel
sudo gpasswd -a userName sudo
```

## Добавьте политику использования sudo без пароля

Открыть файл sudoers через

```
sudo visudo
```

Добавить строку:

```
userName    ALL=(ALL) NOPASWD: ALL

```
