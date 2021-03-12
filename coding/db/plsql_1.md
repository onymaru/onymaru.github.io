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
 * Вставка цены на услугу. 
 * Если в таблице уже есть запись с service_id = p_service_id и start_dt = p_start_dt, то цена будет изменена на p_amount
 * Иначе произойдет вставка
 * Если в таблице есть запись с service_id = p_service_id и start_dt > p_start_dt, то цена в таких записях будет также изменена на p_amount 
 * @param p_service_id id услуги
 * @param p_amount цена
 * @param p_start_dt дата, с которой будет действовать цена
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
