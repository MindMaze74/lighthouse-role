# Ansible Роль: lighthouse-role

[![License](https://img.shields.io/badge/license-MIT%20License-brightgreen.svg)](https://opensource.org/licenses/MIT)
[![Ansible Role](https://img.shields.io/badge/ansible%20role-MindMaze74.lighthouse--role-blue.svg)](https://galaxy.ansible.com/MindMaze74/lighthouse-role)
[![GitHub tag](https://img.shields.io/github/tag/MindMaze74/lighthouse-role.svg)](https://github.com/MindMaze74/lighthouse-role/tags)

Роль устанавливает веб-интерфейс [LightHouse](https://github.com/VKCOM/lighthouse) для работы с ClickHouse. LightHouse — это лёгкий веб-клиент, который позволяет просматривать базы данных, таблицы и выполнять SQL-запросы прямо из браузера.

## Требования

- Ansible >= 2.10
- Managed node на базе RHEL/CentOS 7
- Доступ к репозиторию EPEL (для установки Nginx)
- Доступ в интернет для клонирования репозитория LightHouse с GitHub

## Переменные роли

Все переменные, которые можно переопределить, хранятся в файле [defaults/main.yml](defaults/main.yml), а также в таблице ниже.

| Имя | Значение по умолчанию | Описание |
| --- | --- | --- |
| `lighthouse_dir` | `/usr/share/nginx/lighthouse` | Директория, в которую будет склонирован репозиторий LightHouse и из которой Nginx будет отдавать статику. |

## Пример использования

```yaml
- hosts: lighthouse
  roles:
    - lighthouse-role
```
Если нужно изменить директорию со статикой:
```yaml
- hosts: lighthouse
  roles:
    - role: lighthouse-role
      vars:
        lighthouse_dir: "/var/www/lighthouse"
```
## Что делает роль

1. Устанавливает EPEL-репозиторий (нужен для дополнительных пакетов).
2. Устанавливает git и nginx.
3. Клонирует репозиторий LightHouse с GitHub в {{ lighthouse_dir }}.
4. Деплоит конфиг Nginx /etc/nginx/conf.d/lighthouse.conf для отдачи статики.
5. Запускает и включает сервис Nginx.

## Зависимости
Нет.

## Лицензия
MIT

## Информация об авторе
Эта роль была создана в рамках домашнего задания по Ansible.




