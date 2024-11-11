# Домашнее задание к занятию «Системы мониторинга»   

---

### Обязательные задания

### 1) Вас пригласили настроить мониторинг на проект. На онбординге вам рассказали, что проект представляет из себя платформу для вычислений с выдачей текстовых отчетов, которые сохраняются на диск.   
Взаимодействие с платформой осуществляется по протоколу http. Также вам отметили, что вычисления загружают ЦПУ. Какой минимальный набор метрик вы выведите в мониторинг и почему?**

Настройка мониторинга для проекта, который представляет собой платформу для вычислений и взаимодействует через HTTP, требует учета нескольких ключевых аспектов. Основываясь на описанном сценарии, ниже привел набор метрик, которые как я считаю стоит применить:

1) **Загрузка ЦПУ (CPU Usage):**  
- Поскольку вычисления загружают ЦПУ, важно отслеживать его использование, чтобы убедиться, что серверы справляются с нагрузкой и не перегреваются. Высокая загрузка ЦПУ может привести к снижению производительности и увеличению времени обработки запросов.  
2) **Использование памяти (Memory Usage):**  
- Чтобы убедиться, что приложению хватает оперативной памяти для выполнения вычислений. Недостаток памяти может вызвать замедление работы и даже аварийное завершение процессов.  
3) **Использование диска (Disk Usage):**  
- Поскольку отчеты сохраняются на диск, важно следить за доступным дисковым пространством, чтобы избежать переполнения и потери данных.  
4) **Скорость чтения/записи на диск (Disk I/O):**  
- Высокая нагрузка на диск может замедлить операции чтения/записи, что повлияет на генерацию и сохранение отчетов.  
5) **Время отклика HTTP (HTTP Response Time):**  
- Поскольку взаимодействие происходит по HTTP, важно отслеживать время отклика сервера, чтобы определить, насколько быстро обрабатываются запросы пользователей.  
6) **Коды состояния HTTP (HTTP Status Codes):**  
- Анализ кодов состояния (например, 200, 404, 500) помогает выявить успешные и неуспешные запросы, а также обнаружить возможные ошибки в работе системы.
7) **Число входящих запросов (Request Rate):**
- Позволяет оценить нагрузку на систему и понять, как изменяется количество пользователей или запросов к платформе.  
8) **Ошибки приложения (Application Errors):**  
- Отслеживание ошибок в приложении поможет выявить проблемы в логике работы платформы и своевременно их исправить.  
9) **Время выполнения вычислений (Computation Time):**  
- lПозволяет контролировать, сколько времени уходит на выполнение задач, и выявить «узкие» места в производительности.  

Эти метрики помогут вам получить общее представление о производительности и состоянии системы, а также своевременно выявить потенциальные проблемы. Для отслеживания этих метрик можно использовать инструменты мониторинга, такие как Prometheus, Grafana, Zabbix или другие, которые соответствуют вашим требованиям и возможностям.  

---
### 2) Менеджер продукта посмотрев на ваши метрики сказал, что ему непонятно что такое RAM/inodes/CPUla. Также он сказал, что хочет понимать, насколько мы выполняем свои обязанности перед клиентами и какое качество обслуживания. Что вы можете ему предложить?

Вот как это можно сделать (нагуглил и насобирал отовсюду):

1) **Перевод технических метрик в бизнес-метрики:**
- RAM (оперативная память): Можно представить метрики, связанные с производительностью сервиса. Например, "Среднее время ответа сервиса" или "Процент запросов, выполненных без задержек".
- Inodes (индексы файловой системы): Рассказать о "Доступности сервиса для загрузки и сохранения отчетов" или показать "Процент успешно обработанных файловых запросов".
- CPUla (нагрузка на ЦПУ): Вместо загрузки процессора, сфокусироваться на "Среднем времени обработки задач" и "Проценте задач, выполненных в срок".
2) **Ключевые показатели производительности (KPI) и качества обслуживания:**
- Доступность сервиса (Uptime): Процент времени, когда сервис доступен для клиентов.
- Среднее время ответа: Среднее время, которое требуется для обработки запроса клиента.
- Уровень ошибок: Процент ошибок или неуспешных операций в системе.
3) **Service Level Agreements (SLA) и цели (SLO):**
- Определите конкретные цели обслуживания, такие как "99.9% запросов обрабатываются менее чем за 2 секунды" или "Сервис доступен 99.95% времени".
- Отчетность по выполнению этих целей позволит менеджеру видеть, насколько компания выполняет свои обязательства.
4) **Отчеты и дашборды:**
- Создать дашборды, которые показывают эти бизнес-ориентированные метрики в простом и наглядном виде.
- Использовать графики, диаграммы и цветовые индикаторы для иллюстрации текущего состояния и трендов.
5) **Регулярные отчеты и обсуждения:**
- Проводить регулярные встречи для обсуждения текущего состояния метрик и их влияния на бизнес.
- Предоставлять отчеты, которые показывают успехи и области для улучшения.

Таким образом можно помочь менеджеру продукта получить четкое представление о том, как технические аспекты работы системы влияют на качество обслуживания клиентов. Это также позволит лучше оценивать эффективность работы команды и определять приоритеты для улучшений.

---
### 3) Вашей DevOps команде в этом году не выделили финансирование на построение системы сбора логов. Разработчики в свою очередь хотят видеть все ошибки, которые выдают их приложения. Какое решение вы можете предпринять в этой ситуации, чтобы разработчики получали ошибки приложения?

1) **Использование существующих инструментов с открытым исходным кодом:**
- Можно рассмотреть использование бесплатных инструментов с открытым исходным кодом, таких как ELK Stack (Elasticsearch, Logstash, Kibana) или Graylog. Они могут быть развернуты на имеющихся серверах или виртуальных машинах.

2) **Локальный сбор логов:**
- Настройка приложений на запись логов в файлы на диске, с последующей периодической отправкой этих файлов разработчикам. Конечно мера временная, но мне кажется тоже разработчикам анализировать ошибки.

3) **Облачные решения с бесплатным форматом:**
- Можно использовать облачные решения с бесплатными тарифными планами, такие как AWS CloudWatch, Google Cloud Logging или Azure Monitor, чтобы собирать и анализировать логи. Бесплатные уровни имеют ограничения, но могут быть полезны для небольших объемов данных. В силу непростого времени думаю не все так просто будет, но как вариант нашел и такой.

4) **Уведомления об ошибках:**
- Настройка приложений на отправку уведомлений об ошибках напрямую разработчикам через электронную почту или другие средства коммуникации. Это может быть сделано путем интеграции с существующими сервисами уведомлений.

5)  **Локальные решения для анализа и обеспечение совместной работы:**
- Разработчики могут использовать локальные инструменты, такие как Splunk Free или даже простые скрипты для анализа логов, которые они получают от серверов.
- Также организовывать регулярные встречи между DevOps и разработчиками для обсуждения вопросов, связанных с логами и ошибками. Это позволит оперативно решать возникающие проблемы и поддерживать взаимодействие между командами.

---  
### 4) Вы, как опытный SRE, сделали мониторинг, куда вывели отображения выполнения SLA=99% по http кодам ответов. Вычисляете этот параметр по следующей формуле: summ_2xx_requests/summ_all_requests. Данный параметр не поднимается выше 70%, но при этом в вашей системе нет кодов ответа 5xx и 4xx. Где у вас ошибка?

1) **Коды 1xx и 3xx:**
- Коды ответа 1xx (информационные) и 3xx (перенаправление) могут составлять оставшиеся 30%. Например, коды 301, 302, 304 (перенаправления) могут использоваться в системе, и они не считаются успешными (2xx), но и не являются ошибочными (4xx или 5xx).

2) **Неполные или неверные данные:**
- Возможно, в расчетах участвуют неполные данные.

3) **Проблемы в логике вычисления:**
- Можно перепроверить формулу и убедиться, что summ_all_requests действительно включает все запросы, а не только 2xx и 5xx/4xx.

---
### 5) Опишите основные плюсы и минусы pull и push систем мониторинга.

### Pull-системы мониторинга:

**Плюсы:**

1) Централизованное управление:
- Центральный сервер запрашивает данные, что позволяет лучше контролировать частоту и объем запросов.
2) Безопасность:
- Сервер инициирует соединение, что может уменьшить риск несанкционированного доступа, так как агенты не открыты для входящих соединений.
3) Упрощенная конфигурация агентов:
- Агенты имеют простую конфигурацию, так как им не нужно знать, куда отправлять данные.
4) Легкость в управлении изменениями:
- Обновления и изменения в мониторинге можно централизованно управлять с сервера.

**Минусы:**

1) Масштабируемость:
- При большом количестве узлов нагрузка на центральный сервер может стать узким местом, так как ему нужно опрашивать множество агентов.
2) Задержка данных:
- Поскольку сервер опрашивает агенты по расписанию, могут возникать задержки в получении данных.
3) Непрерывное подключение:
- Требуется постоянная доступность сетевого соединения между сервером и агентами.

### Push-системы мониторинга:

**Плюсы:**

1) Масштабируемость:
- Устройства отправляют данные самостоятельно, что позволяет легко масштабировать систему, добавляя новые узлы без значительной нагрузки на центральный сервер.
2) Снижение задержки:
- Данные отправляются в реальном времени, что позволяет быстрее обнаруживать и реагировать на события.
3) Гибкость в настройке агентов:
- Каждый агент может быть настроен на отправку данных в разные системы мониторинга или аналитики, что добавляет гибкости.

**Минусы:**

1) Безопасность:
- Агенты должны знать, куда отправлять данные, и быть настроены на открытие исходящих соединений, что может создать дополнительные риски безопасности.
2) Управление конфигурацией:
- Нужно управлять конфигурацией каждого агента, что может быть сложно при большом количестве узлов.
3) Потеря данных:
- В случае недоступности центрального сервера данные могут быть потеряны, если не предусмотрена возможность буферизации и повторной отправки.


---
### 6) Какие из ниже перечисленных систем относятся к push модели, а какие к pull? А может есть гибридные?

**Prometheus**  
**TICK**  
**Zabbix**  
**VictoriaMetrics**  
**Nagios**  

1) **Prometheus:**
- Pull модель:
  Prometheus в основном использует pull модель, где он сам опрашивает целевые узлы или экспортеры для получения метрик. Однако, с помощью pushgateway Prometheus может также поддерживать push модель, что делает его частично гибридным.
2) **TICK (Telegraf, InfluxDB, Chronograf, Kapacitor):**
- Push модель:
  В этой системе Telegraf, агент сбора метрик, использует push модель, отправляя данные в InfluxDB.
3) **Zabbix:**
- Гибридная модель:
  Zabbix поддерживает оба подхода. В Zabbix сервер может опрашивать агенты (pull), а также агенты могут отправлять данные на сервер (push).
4) **VictoriaMetrics:**
- Гибридная модель:
  VictoriaMetrics поддерживает оба подхода. Она может собирать данные как путем опроса (pull) совместимых источников данных, так и принимать данные, отправленные в push режиме.
5) **Nagios:**
- Pull модель:
  В основном, Nagios использует pull модель, где центральный сервер опрашивает удаленные хосты и сервисы. Однако, с помощью плагинов и сторонних решений можно реализовать push модель.




























