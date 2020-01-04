# CSA
# Cloud solution architect

1st day

Цели занятия
- Перестаем угадывать наши потребности к ресурсам

Resources Auto-scaling (увеличение/уменьшение) в зависимости от нагрузки
* для ресурсов которыми мы сами управляем (например EC2)
* для ресурсов которые нам предоставляются облачным провайдером (например DynamoDB, API Gw
– контроль/запрос на изменение лимитов сервиса)
* Horizontal Auto-scaling (например количество EC2)
* Vertical Auto-Scaling (например EC2 производительность - CPU / network interface / HD)
* Serverless Functions (вызываются/поднимаются только по запросу на выполнение, затем умирают)
* Увеличение ресурса AWS Shield Advance (traffic absorption) в случае DDoS атаки

- Тестируем системы на требуемую производительность

Можем протестировать наш стек на производительность:
1. Создать на короткий промежуток времени Production-scale Test Environment
2. Протестировать Test Environment под предполагаемой нагрузкой, убедиться что
* Auto-Scaling работает
* Лимиты сервисов облачного провайдера выставлены правильно
* Стек генерирует косты согласно предварительным прогнозам и расчётам
3. Удалить Production-scale Test Environment
* Создание Production-scale Test Environment реализовано с помощью Infrastructure as Code,
является репликой кода Production Environment, может быть протестировано в любое время

- Автоматизируем, чтобы облегчить архитектурные эксперименты

Cloud Infrastructure Stack + Application Stack реализовано с помощью Infrastructure as Code
* Можем (и должны) проводить эксперименты по оптимизации стека посредством небольших,
инкрементальных экспериментов
* Подход аналогичен разработке фич в приложении с использованием Git
* Feature ticket in Jira, create feature branch
* Small code change -> Git Commit/push upstream to feature branch
* Pull-Request
* Review, Blame/Approval
* Merge in feature branch
* Deploy & Test in Test Env
* Merge in master branch
* Deploy & Test in PROD Env

- Допускаем и приветствуем эволюцию архитектуры

Традиционный подход - Waterfall, TOGAF/ITIL, собственный ЦОД
* Архитектурные решения - редкие и большие
* Изменения - несколько раз за время жизни решения
Pubic Cloud - Agile DevOps
* Архитектурные решения - частые и небольшие
* Изменения – регулярные, вплоть до несколько раз за день
Можем (и должны) эволюционировать архитектуру Cloud Infra + App Stack посредством
небольших, инкрементальных изменений с помощью Infrastructure as Code

- Ведем дизайн архитектуры используя данные о нагрузке

Дизайн решения в Public Cloud должен обеспечивать возможность сбора детальных данных о
работе сервиса
* Данные которые мы собираем, должны предоставлять срезы для анализа по основным
направлениям Public Cloud архитектуры:
* Performance Efficiency - Service SLA
* Reliability - End-user KPI
* Security – SIEM events
* Operational Excellence - Number of Support Tickets, Auto-scaling events
* Cost Optimization - Cost break down structure
* Мы должны постоянно анализировать собираемые данные с целью дальнейшей оптимизации
работы решения
* Эволюция архитектуры на основе собираемых данных с помощью Infrastructure as Code

- Улучшаем архитектуру через тестирование в Game-days

Проверяем как решение и команда справляются с непредвиденными ситуациями
* Регулярно проводим Game-days (как минимум раз в квартал) для проверки:
* У нас есть Run-book (пошаговая инструкция с описанием что делать в данной ситуации)
* Команда может использовать Run-book для успешного решения проблемы
* Команда имеет достаточную компетенцию для успешного решения проблемы
* Время затрачиваемое на решения проблемы не нарушает SLA
* Game-day должны аккуратно планироваться и к ним необходимо готовиться, обычная практика:
* День 1 – подготовка сценария, описания, проверка валидности Run-book (коррекция)
* День 2 – проведение Game-day
* День 3 – анализ результатов Game-day, составление плана по улучшению / коррекции

HW 1st

На основе заданного шаблона разработать описание Game-day для тестирования собственного решения (если имеется) или предложенного преподавателем примера

## Пример описания GameDay
  Scenario:

    A Hacker has gained access to you AWS account and executed a clean up script which wiped the account clean.

  Goal:

    Separate production workloads from non production workloads by doing a disaster recovery into a "fresh" AWS account

    This GameDay will focus on:
      * Get the needed infrastructure up and running in a new account
      * Restore application data from the backup account

  Rational:

    1. Separation of concern:

      a. Increase development speed since there will be no risk of destroying the live environment when doing changes to non production environments
      b. By having one AWS account per environment we can more easily limit the access to live environment for new employees.

    2. Test a full disaster recovery

      a. Do we have all the needed data under version control?
      b. Do we have all data backed up and restorable in our Backup Account?
      c. How long time does a full restore take?
      d. Practice makes perfect...

    3. Verification

      a. Prepared list of what to verify that systems runs normally (API, Mobile apps, 3:rd party integration, synchronisation...)

## Пример шаблона описания GameDay

Status:
  * GameDay run ... yes/no
  * All services up and running ... yes/no
  * Using account for normal development work ... yes/no
  * Removed old Dev-env from Live account ... yes/no

Take contact with squad before GameDay and get an innovatory over what they run.
Squad runs:
  * Service one
  * Service two
  * Service three

Make a list of matching backup solution that are provided and documentation on that backup solution:
  * Backup solution one, confluence page: here
  * Backup solution two, confluence page: here
  * Backup solution three, confluence page: here

Make a list of solution /things that gets to be done before we are ready for the GameDay:
  * Need to create solution for.
  * This we need to fix before GameDay

Goals and measure points:

Squads internal documentation:

Environments & accounts

## Runbook
