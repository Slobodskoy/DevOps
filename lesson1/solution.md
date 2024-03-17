## Сгенерируйте новый ssh ключ

На локальной машине генерируем пару ключей
```sh
ssh-keygen -t rsa -b 4096 -C "myemail@server.com"
```
В диалоге задаем имя для файла с ключом ```userName_rsa```
## Создайте нового персонального пользователя на ВМ

```sh
sudo adduser userName
```

## Добавьте к новому пользователю публичную часть ключа
Ручной способ:
- заходим новым пользователем по ssh с паролем
```sh
sudo mkdir -p /home/userName/.ssh
sudo nano /home/userName/.ssh/authorized_keys
```
- копируем в файл строку с публичным ключом
- настраиваем права на файл
1. удаляем все разрешения  «group» и «other» для директории ~/.ssh/
```sh
chmod -R go= ~/.ssh
```
2. устанавливем владельцем директории своего пользователя вместо root:
```sh
chown -R userName:userName ~/.ssh
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
