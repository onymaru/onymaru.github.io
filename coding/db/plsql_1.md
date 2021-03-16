---
title: Задача по PL/SQL
layout: single-copy
classes: wide
author_profile: true
author: Pavel Shiryaev
---

Время выполнения: **30 минут**

## Исходные данные

Есть таблица с ценами на услуги, живущими во времени.

```
create table tariff (
  service_id number, -- id услуги
  amount     number, -- стоимость
  start_dt   date    -- дата начала действия стоимости
);

alter table tariff add constraint uk_tariff unique (service_id, start_dt);
```

Пример данных

```
 service_id  | amount |  start_dt
-----------------------------------
          1  |     10 | 01.02.2021
          5  |      9 | 01.12.2020
          5  |     10 | 01.02.2021
          5  |     12 | 01.05.2021
          1  |     14 | 01.05.2021        
```

## Задача

Нужно написать реализацию пакета по приведенному ниже шаблону и pl/doc

```
create or replace package serv_tariff as

/**
 * Получение тарифа для услуги на дату
 * @param p_serice_id id услуги
 * @param p_dt дата, на которую нас интересует цена
 * @return тарифф
 */
function get_service_tariff ...

/**
 * Вставка цены за услугу.
 * Если в таблице уже есть запись с service_id = p_service_id и start_dt = p_start_dt, то цену нужно просто измененить на p_amount. 
 * Иначе произвести вставку, но есть условие: Нельзя вставлять цену раньше чем через 10 дней от предыдущей цены и позже чем за 10 дней до следующей цены. 
 * Т.е. если у вас с 01.01.21 действует цена 10, а с 01.02.21 действует цена 15, то вы можете вставить цену только в промежуток с 11.01 по 22.01. 
 * При нарушении условия нужно выбросить ошибку.
 * @param p_service_id id услуги
 * @param p_amount цена
 * @param p_start_dt дата, с которой будет действовать цена
 * @raise "Дата %1 не может быть вставлена"
 */
procedure set_service_tariff ...

end;
/
```

```
create or replace package body serv_tariff as

function get_service_tariff ...

procedure set_service_tariff ...

end;
/
```
