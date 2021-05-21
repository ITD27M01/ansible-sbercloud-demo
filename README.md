# Ansible демо для SberCloud

Пример использования openstacksdk и Ansible для работы с SberCloud.

## Аутентификация

OpenStackSDK использует стандартизированный способ аутентификации в
совместимых облаках и это файл `clouds.yaml`:
https://docs.openstack.org/openstacksdk/latest/user/config/configuration.html

Используемый по умолчанию плагин `password` требует создания IAM пользователя
(`ansible` в примере) и указания идентифкатора домена.

## Идентификатор домена

Идентификатор домена мне удалось найти по следующему пути в Web-интерфейсе
(https://console.hc.sbercloud.ru):
1. Перейти на страницу IAM: https://console.hc.sbercloud.ru/iam
2. Там в левом списке выбрать "Identity Providers"
3. Выбрать провайдера, который позволяет вход по SberID
   (SAML с описанием `auth.sbercloud.ru`)
4. Нажать на нем view и в строке Login Link найти `domain_id=<id>`
5. Собственно, вот этот `<id>` и нужен.
