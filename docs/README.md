# DAC_test
# TS - Список Договоров

## Назначение документа
В документе описано поведение системы на странице просмотра списка договоров.

## Версионность документа

| Версия | Изменения           | Дата       | Автор                     | Связи                         | Согласующие |
|--------|---------------------|------------|---------------------------|-------------------------------|-------------|
| 1.0    | Создание документа  | 21.10.2024 | Глик Виталий Игоревич     | NCRM-1661 TS список договоров | DONE        |

## Предусловия
- Осуществлён вход в систему.
- Пользователь находится на главной странице NCRM.

## Процессные роли
- Специалист CV
- Руководитель в Регионе
- Начальник БКЗ регион
- Сотрудник БКЗ регион
- Сотрудник БКЗ КЦ
- Система NCRM

## Результат
- На странице отображается список необходимых договоров.
- Осуществляется переход на детальную карточку договора.

## Ограничения
- Пользователь имеет соответствующие полномочия для просмотра списка КА.
- Все поля: **«Только для чтения»** (недоступны для редактирования).

---

## Описание
### Действия пользователя
1. Пользователь переходит на страницу «Договоры».  
   **Запрос:** `GET /contracts`.

### Доступные быстрые фильтры:
- **«Мои»** — система отображает список договоров, в команде которых текущий пользователь является основным.  
  **Запрос:** `GET /contracts?_filter.field.primaryTeamMemberId.equals`.
- **«Моего отделения»** — система отображает список договоров, которые обслуживаются в отделении пользователя.  
  **Запрос:** `GET /contracts?_filter.field.followOrganizationId.equals`.
- **«Все»** — система отображает список всех договоров ГПН-РП.  
  **Запрос:** `GET /contracts`.

### Отображаемые данные (по умолчанию):
- № договора `(contract_number)`
- Наименование (гиперссылка на детальную карточку договора) `(contract_name)`
- Тип `(contract_type)`
- Этап продаж `(sale_stage)`
- Статус `(status_approval)`
- Краткое наименование КА (гиперссылка на детальную карточку КА) `(t_client_short_name)`
- ИНН `(inn)`
- Синхронизация с АСКУ `(asku_status)`
- Текст ошибки синхронизации с АСКУ (отображается при наведении) `(asku_error)`
- Синхронизация с процессингом `(w4_status)`
- Ошибка синхронизации с процессингом (отображается при наведении) `(w4_error)`
- Офис (основной офис сопровождения) `(primary_follow_division)`
- Отделение (основное отделение сопровождения) `(primary_follow_organization)`

### Настройка дополнительных полей
Пользователь может настроить отображение дополнительных полей, нажав на иконку шестерёнки.  
Доступные поля:
- Условия оплаты `(payment_terms)`
- Схема оплаты `(invoicing_scheme)`
- Ожидает согласования `(waiting_agreement)`
- Дата заключения `(conclusion_date)`
- Дата вступления в силу `(effective_date)`
- Дата окончания `(end_date)`
- Дата закрытия `(closure_date)`
- ЭДО `(edo_flag)`

### Поиск записи
1. **Глобальный поиск** (по одному из четырёх параметров):
    - Номер договора
    - ИНН
    - Краткое наименование КА
2. **Детальный поиск по столбцам**:
    - Номер договора
    - Наименование
    - Краткое наименование КА
    - Дата заключения
    - Дата вступления в силу
    - Дата окончания
    - Дата закрытия
    - Офис
    - Отделение
3. **Фильтр по уникальным значениям столбца**:
    - Тип
    - Этап продаж
    - Статус
    - Условия оплаты
    - Схема оплаты
    - Ожидает согласования
    - ЭДО

Если запись не найдена, отображается экран неудачного поиска.

### Действие при переходе
Пользователь нажимает на гиперссылку в поле **«Наименование»**.  
**Запрос:** `GET /contracts/{contract-id}`.  
Пользователь переходит на детальную карточку договора.

---

## Альтернативный сценарий №1
1. После шага №6 основного сценария пользователь нажимает на гиперссылку в поле **«Краткое наименование КА»**.  
   **Запрос:** `GET /client?_filter.field.id.equals`.
2. Пользователь переходит на детальную карточку КА.
3. Пользователь выбирает вкладку **«Договоры»**.  
   **Запрос:** `GET /contracts?_filter.field.clientId.equals`.
4. Система NCRM отображает список договоров текущего контрагента.
5. Пользователь переходит на детальную карточку договора.  
   **Запрос:** `GET /contracts/{contract-id}`.

---

[Ссылка на Confluence](https://doc.dev.gazprom-neft.ru/display/~Glik.VI)  
[Ссылка на задачу](https://task.dev.gazprom-neft.ru/browse/NCRM-1661)
