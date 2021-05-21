# Ansible демо для SberCloud

Пример использования openstacksdk и Ansible для работы с SberCloud.

## Аутентификация

OpenStackSDK использует стандартизированный способ аутентификации в
совместимых облаках и это файл `clouds.yaml`:
https://docs.openstack.org/openstacksdk/latest/user/config/configuration.html

Используемый по умолчанию плагин `password` требует создания IAM пользователя
(`ansible` в примере) и указания идентифкатора домена:

```yaml
---
clouds:
  sbercloud:
    auth:
      auth_url: "https://iam.ru-moscow-1.hc.sbercloud.ru/v3"
      project_name: "ru-moscow-1"
      username: "ansible"
      password: "sEcr@t"
      user_domain_id: "some_id"
      project_domain_name: "some_id"
    region_name: "ru-moscow-1"
    interface: "public"
    identity_api_version: 3
```

## Идентификатор домена

Идентификатор домена мне удалось найти по следующему пути в Web-интерфейсе
(https://console.hc.sbercloud.ru):
1. Перейти на страницу IAM: https://console.hc.sbercloud.ru/iam
2. Там в левом списке выбрать "Identity Providers"
3. Выбрать провайдера, который позволяет вход по SberID
   (SAML с описанием `auth.sbercloud.ru`)
4. Нажать на нем view и в строке Login Link найти `domain_id=<id>`
5. Собственно, вот этот `<id>` и нужен.

## Пример запуска

```shell
> ansible-playbook playbook.yml

PLAY [Demo Play for all SBC hosts] **************************************************************

TASK [ping] *************************************************************************************
ok: [ecs-7a69]

PLAY RECAP **************************************************************************************
ecs-7a69  : ok=1    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```