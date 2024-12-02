Это шаблон для решения **первой части** проектной работы. Структура этого файла повторяет структуру заданий. Заполняйте его по мере работы над решением.

# Задание 1. Анализ и планирование

Чтобы составить документ с описанием текущей архитектуры приложения, можно часть информации взять из описания компании условия задания. Это нормально.

### 1. Описание функциональности монолитного приложения

**Управление отоплением:**

- Пользователи могут удалённо включать/выключать отопление в своих домах
- Система поддерживает удалённое включение/отключение датчиков температуры, установленных в домах

**Мониторинг температуры:**

- Пользователи могут просматривать текущую температуру в своих домах через веб-интерфейс. 
- Система поддерживает получение данных о температуре с датчиков, установленных в домах

### 2. Анализ архитектуры монолитного приложения

Перечислите здесь основные особенности текущего приложения: какой язык программирования используется, какая база данных, как организовано взаимодействие между компонентами и так далее.

Язык программирования: Java
База данных: PostgreSQL
Архитектура: Монолитная, все компоненты системы (обработка запросов, бизнес-логика, работа с данными) находятся в рамках одного приложения.
Взаимодействие: Синхронное, запросы обрабатываются последовательно.
Масштабируемость: Ограничена, так как монолит сложно масштабировать по частям.
Развёртывание: Требует остановки всего приложения.

### 3. Определение доменов и границы контекстов

Архитектура монолитного решения (AS IS)

```markdown
@startuml Basic Sample
!include https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/master/C4_Container.puml

Header Архитектура существующей системы
Title Система "Теплый дом" (As Is)

skinparam BackgroundColor SeaShell

Person(user, "User")
System_Boundary(c1, "Система Теплый дом") {
    Container(web_app, "Web Application", "React, Java, PostgreSQL", "Система управления температурой с датчиков")
}
System_Ext(iot, "IoT")

Rel(user, web_app, "Uses", "HTTPS")
Rel(web_app, iot, "Передача температуры на устройство", "HTTPS")
Rel(iot, web_app, "Получение температуры с устройства", "HTTPS")

footer Рябчиков Владимир, 2024

@enduml
```
Опишите здесь домены, которые вы выделили.

Архитектура MSA решения (To Be)

В монолитном приложении можно выделить 2 основных домена:
1. Управление устройствами
2. Мониторинг устройств

Дополнительно я выделил бы домены:
- Авторизации и аутентификации
- Управления домами
- Управления учетными данными пользователей
- Мониторинг / логирование

### **4. Проблемы монолитного решения**

- сложность системы будет расти;
- поддерживать и масштабировать ее будет все сложнее и сложнее;
- разобраться в ней трудно — особенно если система переходила из поколения в поколение, логика забывалась, люди уходили и приходили, а комментариев и тестов нет);
- возможно, множество ошибок, которые тяжело мониторить и устранять;
- мало тестов — монолит не разобрать и не протестировать, поэтому обычно есть только UI-тесты, поддержка которых обычно занимает много времени;
- дорого вносить изменения;
- застревание на технологиях. Стоит учитывать, что компания планирует подключать видео-наблюдение, что, возможно,  потребует использование отличного от монолитного решения стека.

### 5. Визуализация контекста системы — диаграмма С4

```markdown
[Context diagram С4 монолита](www.plantuml.com/plantuml/png/TLBTQXD15BwVfnZtAe4qqT8hhze6ePKAiKdnCansnsJfximoCsij8iGKAHAmuWluymGnT24sCNc5Cs_aEKrifCQzsTdlx7U-7sRNEc5SdYRiGQp298yaxpcNsSUrcX5drMxiUdadjzA4MZcfN3NKQIrBX2BEbdLH4dTgzPsj1a4dpuvggR1E6eJQTMI8M4bJpMW_Ev0YaeR39z_txs7Y1r30ZH_u2z-74VVlyF012dmFO8pdZ_G5Ft404mBnO-Q7h1MxH7BujWQH7C1tF2rWweV8W6kOmopWfJtB3ssPCNiQgqmOaV9z4PvsZSvLLDU9DhmfHRCd4tJNaCPgLQAe5HwSu2iei-OvXadR-qGGvhmKFiBPFUrDqcN-Xd5yxYeedSbEMsGPqb_83j_BiYGEXOkr2X0wbY9q5VvKl18Ltj3MTOriFZyA_XNp5x2Wkc0CKuH-uV2AhwOBA6YqQdH-MnqP8kGI9d23s1X3lVqJwybhLugrGvL3tS81EvR9ge2rNMp2af63LglHn9_edxlfaWrVRfKBqaAbqKP3ViZHBYMWE4k3TC8ay_lxQUtQ0ksVmnI9byl8KFn70GDlsZ_wUpzxgRMZQ_ZLNy6FTJ4SFcEb8xX6O8QrzYjy--7s3jkLAiBh-ni0)
```

# Задание 2. Проектирование микросервисной архитектуры

В этом задании вам нужно предоставить только диаграммы в модели C4. Мы не просим вас отдельно описывать получившиеся микросервисы и то, как вы определили взаимодействия между компонентами To-Be системы. Если вы правильно подготовите диаграммы C4, они и так это покажут.

**Диаграмма контейнеров (Containers)**

Добавьте диаграмму.

**Диаграмма компонентов (Components)**

Добавьте диаграмму для каждого из выделенных микросервисов.

**Диаграмма кода (Code)**

Добавьте одну диаграмму или несколько.

# Задание 3. Разработка ER-диаграммы

ER-диаграмма

```markdown
[ER диаграмма](www.plantuml.com/plantuml/png/lLPHJnj747xVNx4vHSBGsY6eVJaX545BAwML44HzFQrzWzbcRzVPsoEo0XAX3rHALQgehrMgz0yuQIWa0VCNzlvHP_VkiCzsQNZ1ak7kcszcPxwPNU-3r31jiaHGq76KTdOWOMJElhGd-K7-t9xbno6ztrf4w3VxDZ-qm_mWfFRF_DY-oO_icVrWX_OjjIzRzeyM8NUsCzanN4bwbsL6TK62PWRYnbqsJ-veC9cMD5ZkAA5qkAdwJAoA35O2-Xawu9-0BY_N7Ed6mvMLvNlUOIKWTq36rHArrJB9dsGmSvarpPDKoVeY1V-JGgTWLfMOBA5TYtUlFHKXVSnbZscMq5NMUTpLAfFncbkBRW7RsW4XnYZVGHUT9udVyzJqDrKAqqobOz05QuC9-84h0MOJuYdckf9c5c-Ck2POcj9dXEBdMs0Ok9P8wVgD1f1adv2vaQVW4ao_1rHfiwF6GZxYHi1ewIqEKZ92YkZKlieFS7JEtOpHhpURzXs-3UpVY0uGFSzV41zWbiqEQ61VsnDxQJ_cB-nxYeIXFGy80McuwTFWgc61VMM7oFh5dheXjGCStnFtJXjP2de-c0yeIwbxBgjVc1pRWCSqf5d6us3UCrgjYbXEN21KbqiafKPpsMtSNrp4m2MfXy8-nLQDp5ykLZR94XZXI-X6vWfBckd_Ckuep3RoIN5fS8uzq49W7VT96HaInaKz8s_XQSHmE7TTvBPI0fZ4235iiqmOQdG6POWsntP6CJEEwVvvjAF1QH8n4rB34qWDItgJ-xMCaFNYJ-BkpspRxwwZjE5hgxhaNwvl4oeosINNs-YgXvY00rfPLWbMAGvwbtTgmfPGQv9fcCdI6j4Za9QLr_fwG_5lMUQ_ykVvONw0OhztJxX3XhGHWokxKhruk_7kc2r2gJHd8f9PqWOzmLYu6k_PqxrGfXFXaJFEAj172DOtWjCS96kB_zTSoMtUZRJAZEF-c2evZhjVHSbAmoqtwRKzivSq_scgLmFQ61LUxnSYDzegrxSiKJ68QKjDjCX0qXFi6lNgZDkNqPty-CNV7AyZtcjemu2018pkVyKCgoIiWJTKiPnF7b-TDmKoEd4yRPU93DARw-1g8tvFX65rikshPgoUokRU7dLG6FAOr4e8mpAhEha0FRrwhE-kQJAELTt1fJ99zPXdpLNvqBszfdf6DJp1gaqQXbKhstqK4UVxrBN5NkJ7hZbrF_pKVKkfq9UGkH6CBZEAB56q-txPIt_lkB03-yvFmpyu1uUrCDNnxg9aFH_3GqMCSIepXk5anz4s5n0LsMhUtJ5DjKSHApq84VuUHhsDr8zV-z5VJ2xm8dD2yV4DVazTVlcH4yJVlWDtC3Qz5GKw7TrYq3vqRfTsw8eX6myTxT9TgZ3c6OQuA2v87v3zQtv4rZq1bqFApoxwkD6bM6HAoBPI1lIiMpukXDeXS8uB77nEbnQNlY3a0NfbYVWN)
```
