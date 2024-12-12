[[_TOC_]]

# CMDB

## Baremetal

1. **Владелец**
   - Контакт ответственного за продукт (CPO, PO, PM, Team Lead, QA Lead, Architect...)
   - Профиль сотрудника на team.wb.ru - EID

2. **Команда сопровождения**
   - (Обязательно для инфраструктурного сервиса) Указывается ID команды, которая будет поддерживать/администрировать данный сервис.

3. **Окружение**
   - dev
   - stage
   - prod

4. **Список согласующих**
   - Профиль WB Team 
   - Employee ID
   - Контакт WB Band

5. **Метки телепорта**
   - `env`
   - `team`
   - `owner`
   - `product`
   - и остальные при наличии

6. **Описание**
   - Для каких целей используется данный ресурс.
   - В особенности:
     - Является ли машина гипервизором (Proxmox/Cloud).
     - К какому кластеру принадлежит.
     - Размещена ли на машине СУБД и к какому кластеру относится (по global_inventory).

7. **Serial Number**
   - Для Bare Metal серверов – серийный номер оборудования.

8. **Сетевые адаптеры**
   - Установленные сетевые адаптеры.
   - Их MAC-адреса.

9. **Операционная система**
   - Версия ОС/ядра, установленной на bare metal сервере или виртуальной машине.

10. **Название**
    - Укажите название КЕ, не используя точки. Максимальная длина названия — 100 символов.

11. **Модель**

12. **UUID**

13. **Device Height**

14. **Netbox Device ID**

15. **Vendor**

---

## VM Cloud

1. **Название проекта**

2. **Имя и версия образа**

3. **IP-адреса**
   - Внутренний IP-адрес.
   - Внешний IP-адрес (если имеется).

4. **FQDN и IP**
   - IP-адреса и FQDN, принадлежащие ресурсу.

5. **Зона доступности**

6. **Дата-центр размещения ресурса**

7. **Netbox Device ID**

8. **TPM2 Endorsement Certificate**
   - Описание версии TPM и модели материнской платы:
     - Сертификат модуля безопасности, подписанный CA производителя. 
     - Получение на Debian/Ubuntu:
       ```bash
       sudo apt install tpm2-tools openssl && openssl x509 -in <(tpm2_nvread 0x1c00002) -text
       ```
     - Если сертификат недоступен:
       ```bash
       # Версия TPM
       cat /sys/class/tpm/tpm*/tpm_version_major
       # Модель материнской платы
       sudo dmidecode -t 2
       ```

9. **[Статус](https://cmdb-ingress-controller.cmdb.svc.k8s.dldevel/docs/kef/statuseske.html)**

10. **Описание**

11. **Модель**

12. **UUID**

13. **Тип виртуализации**

14. **ПО виртуализации**

---

## Namespaces

Поля (данные), необходимые в новом типе КЕ в CMDB:

1. **ID**
   - Тянуть уникальный UID из кластера k8s.

2. **Имя NS**
   - Имя K8s namespace = имя подгруппы GitLab = имя каталога Vault.

3. **Статус**
   - Если namespace существует в кластере: **"В эксплуатации"**.
   - Если namespace отсутствует в кластере, но ранее был: **"Выключен"**.

4. **Дата создания NS**
   - В кластере k8s.

5. **Лимиты**
   - **PODS**
   - **CPU**
   - **RAM**

6. **CMDB ID**
   - Каждому уникальному UID присваивается свой CMDB ID.

7. **Комментарий/Описание**

8. **Owner**

9. **Тег/пометка**
   - Объединяющее поле.