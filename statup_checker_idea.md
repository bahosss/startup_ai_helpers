Telegram-бот для первичного стресс-теста продуктовых идей
Пользователь кидает сырую идею в 1–10 предложениях, бот:


нормализует формулировку,


оценивает по фиксированным критериям,


дает короткий вердикт,


в платной версии строит развернутый разбор: ICP, риски, GTM, MVP, монетизацию, гипотезы для теста.


JTBD
“У меня есть сырая идея. Я хочу быстро понять, стоит ли ее вообще тестировать, в каком виде, и что делать дальше, не тратя 2 дня на размышления.”
Для кого
Первая аудитория:


founders / indie hackers,


PM / marketers / devs, у которых много сырых идей,


Telegram-native аудитория,


люди, которые хотят “быстрый sanity check”, а не консалтинг на 2 часа.


Ценность
Не “истина о бизнесе”, а быстрый структурированный фильтр.

2) Лучший формат запуска
Рекомендованный старт
Telegram bot only + минимальная admin-панель + платный deep report.
Почему это лучший формат:


не нужен фронтенд для пользователя;


низкий time-to-market;


привычный UX: “скинул идею → получил ответ”;


легко запустить freemium;


легко измерять конверсию free → paid.


Не лучший формат на старте
Не надо сейчас:


полноценный веб-сервис;


личный кабинет;


маркетплейс идей;


комьюнити/соцсеть;


автопоиск конкурентов по интернету;


pitch-deck generator;


multi-agent систему.


Сначала нужен один кейс:
“ввел идею → получил полезный разбор → захотел платить за глубину”

3) MVP scope / not scope
MVP scope


Прием идеи текстом в Telegram.


Free-ответ:


вердикт,


score,


3 сильных стороны,


3 слабых места,


1 следующий шаг.




Paid-ответ:


нормализованная идея,


ICP,


pain / value,


MVP scope,


GTM-гипотеза,


монетизация,


риски,


3 быстрых теста,


итоговый recommendation.




История последних запросов пользователя.


Простая оплата / разблокировка deep report.


Admin-панель:


пользователи,


запросы,


статусы,


usage / cost,


ручная разблокировка paid.




Логи, rate limit, basic moderation.


Not scope


Голосовые сообщения.


Фото / файлы / презентации.


Автоматический web-research.


Настоящий TAM/SAM/SOM.


Генерация бизнес-плана на 40 страниц.


CRM / email / Notion integration.


Командные аккаунты.


Marketplace of ideas.


Auto competitor monitoring.


Fine-tuning / RAG / vector DB.



4) Как должен выглядеть продуктовый output
Free version
Формат должен быть очень коротким и Telegram-friendly:


Вердикт: “Можно тестить” / “Сыровато” / “Плохая ставка”


Оценка: 6.4/10


Почему да


Почему нет


Что сделать следующим шагом


Категории вердикта
Лучше не “норм/не норм”, а 4 статуса:


Сильная гипотеза


Можно тестить


Сыровато


Не стоит так запускать


Это продает лучше и выглядит умнее.
Paid version
Структура:


Нормализация идеи


Для кого продукт


Какую боль решает


Почему это может взлететь


Почему это может не взлететь


MVP в 1-й версии


Что не делать в MVP


Как монетизировать


Как привлечь первых пользователей


Какие 3 теста сделать за 7 дней


Итоговая рекомендация



5) User flow
Основной user flow


Пользователь открывает бота.


Жмет “Оценить идею”.


Бот просит отправить идею одним сообщением.


Пользователь отправляет текст.


Бот делает:


нормализацию,


scoring,


short verdict.




Пользователь получает free result.


Бот предлагает:


“Получить глубокий разбор”


“Оценить еще одну идею”


“Мои последние идеи”




Если пользователь платит:


создается paid report,


бот присылает расширенный анализ.




Пользователь может сохранить / переслать / вернуться к истории.


Alternative flows
Слишком короткий ввод
“Сделай маркетплейс для всего”
→ бот не анализирует глубоко, а просит минимум структуры:


для кого,


какая проблема,


как пользователь это делает сейчас.


Спам / мусор
→ вежливый reject.
Повторный пользователь
→ бот показывает прошлые идеи и предлагает сравнить.

6) Модули системы
1. Telegram Bot Interface
Отвечает за:


команды,


inline buttons,


прием текста,


выдачу результатов,


платежный UX.


2. Analysis Orchestrator
Сценарий анализа:


preprocessing,


validation,


prompt assembly,


model call,


parsing structured JSON,


formatting ответа.


3. Scoring Engine
Не отдельный ML, а простой слой логики:


6–8 критериев,


вес каждого критерия,


итоговый score,


вердикт по диапазонам.


4. Report Generator
Собирает:


short report,


deep report.


5. Payments / Access Control


free quotas,


paid unlock,


purchase status,


manual override.


6. Persistence Layer
Хранит:


users,


ideas,


reports,


payments,


events,


costs.


7. Admin Panel
Минимум:


список пользователей,


список запросов,


цена / себестоимость,


ошибки,


ручное открытие paid report.


8. Moderation / Safety


лимиты,


антиспам,


блок мусорного контента,


disclaimer.



7) Рекомендуемый стек
Самый прагматичный вариант:
Backend


Python 3.12


FastAPI


aiogram для Telegram


SQLAlchemy 2 + Alembic


PostgreSQL


Pydantic


httpx


Admin


FastAPI + Jinja2 / HTMX
Не надо React на старте.


Infra


Docker


docker-compose


Nginx


VPS


Observability


structured logging


Sentry optional, но не обязателен в v1


cost logging per request


LLM layer


abstraction over provider


2 режима:


cheap model for free verdict


better model for paid deep report




Почему не надо сложнее
Не надо сейчас:


Kafka


Celery cluster


Kubernetes


Redis как обязательную зависимость


microservices


vector DB


Один монолитный сервис здесь нормален.

8) Архитектура
High-level
Telegram User   ↓Telegram Bot Webhook   ↓FastAPI App   ├─ Auth / User lookup   ├─ Idea Validation   ├─ Analysis Orchestrator   │    ├─ Prompt Builder   │    ├─ LLM Provider   │    ├─ JSON Parser   │    └─ Scoring Mapper   ├─ Payment / Access Control   ├─ Report Formatter   └─ Admin UI        ↓PostgreSQL
Принцип
Один сервис, одна БД, одна кодовая база.
Async
Можно сделать без отдельной очереди:


короткие операции синхронно,


deep report через background task + polling status в БД.


Если нагрузка вырастет — потом добавить Redis/RQ.

9) Data model
users


id


telegram_user_id


username


first_name


language_code


created_at


last_seen_at


is_blocked


free_quota_remaining


paid_credits


ideas


id


user_id


raw_text


normalized_text


status (received, processing, done, failed)


created_at


reports


id


idea_id


report_type (free, paid)


verdict


score_total


score_market


score_distribution


score_monetization


score_execution


score_clarity


strengths_json


weaknesses_json


next_steps_json


full_report_markdown


llm_model


input_tokens


output_tokens


estimated_cost


created_at


payments


id


user_id


provider


external_payment_id


amount


currency


status


credits_granted


created_at


events


id


user_id


idea_id nullable


event_type


payload_json


created_at


admin_actions


id


admin_name


action_type


target_type


target_id


payload_json


created_at



10) Scoring logic
Нужна не магия, а понятная рубрика.
Критерии
Оцениваем по шкале 1–10:


Clarity — понятно ли, что это вообще за продукт


Pain intensity — есть ли реальная боль


Audience specificity — понятна ли ЦА


Distribution feasibility — можно ли дешево достучаться до первых юзеров


Monetization potential — есть ли понятный путь к деньгам


Execution simplicity — можно ли сделать MVP быстро


Differentiation — есть ли угол атаки, кроме “еще один AI-tool”


Validation speed — можно ли проверить гипотезу за 1–2 недели


Вес
Пример:


Pain intensity — 20%


Distribution feasibility — 20%


Monetization potential — 15%


Execution simplicity — 15%


Audience specificity — 10%


Clarity — 10%


Differentiation — 5%


Validation speed — 5%


Mapping to verdict


8.0–10.0 → Сильная гипотеза


6.5–7.9 → Можно тестить


4.5–6.4 → Сыровато


0–4.4 → Не стоит так запускать



11) AI-часть
Что реально делает AI
Не “угадывает успех бизнеса”, а:


нормализует текст идеи;


оценивает по рубрике;


объясняет причины;


строит следующий action plan.


Как делать правильно
Шаг 1. Normalize
Из сырого текста собрать структуру:


что за продукт,


для кого,


какую боль решает,


что получает пользователь.


Шаг 2. Structured evaluation
Модель должна вернуть строго JSON:


normalized_idea


scores


verdict


strengths


weaknesses


next_steps


Шаг 3. Deep expansion
Только для paid:


MVP,


GTM,


monetization,


risks,


7-day validation plan.


Что нельзя делать


Не просить модель “предскажи успех стартапа”.


Не давать модели свободу писать длинную воду.


Не пускать free-версию в длинные essay-ответы.


Не верить модели в market sizing без внешних данных.


Практичный prompt strategy
Два промпта:


Prompt A — short evaluator


Prompt B — deep business breakdown


Плюс жесткий JSON schema parser.

12) API design
Внутренний backend API.
Public-ish endpoints
POST /webhooks/telegram
Принимает webhook update.
POST /api/v1/ideas
Создает новую идею.
Request:
{  "telegram_user_id": 12345,  "text": "бот-оценщик идей..."}
GET /api/v1/ideas/{idea_id}
Статус идеи.
POST /api/v1/reports/{idea_id}/free
Создает free report.
POST /api/v1/reports/{idea_id}/paid
Создает paid report, если есть доступ.
GET /api/v1/users/{user_id}/history
История последних идей.
POST /api/v1/payments/create
Создает платеж / ссылку.
POST /api/v1/payments/webhook
Подтверждение оплаты.
Admin endpoints
GET /admin/users
GET /admin/ideas
GET /admin/reports
POST /admin/reports/{id}/unlock
POST /admin/users/{id}/grant-credits

13) Экраны
У пользователя веб-экрана может не быть. Основной UI — Telegram.
Telegram screens
1. Welcome
Кнопки:


Оценить идею


Как это работает


Мои идеи


Получить глубокий разбор


2. Submit Idea
Текст:
“Отправь идею одним сообщением. Чем конкретнее — тем полезнее ответ.”
3. Free Result
Показывает:


verdict


score


3 плюса


3 минуса


next step


Кнопки:


Глубокий разбор


Новая идея


Мои идеи


4. Paid Offer
Что входит:


MVP


риски


монетизация


GTM


тесты на 7 дней


5. Paid Result
Полный markdown-отчет.
6. History
Список последних N идей.
Admin screens
1. Dashboard


DAU


ideas/day


free→paid conversion


average AI cost


revenue


2. Ideas table


user


short text


verdict


score


status


created_at


3. Payments


amount


status


provider


4. User card


total ideas


paid credits


last activity



14) Что можно сделать руками
Это важно. На старте не надо автоматизировать всё.
Руками можно оставить


Разблокировку paid report


Саппорт


Обработку edge cases


Проверку мусорных запросов


Подбор pricing


Анализ лучших / худших кейсов


Коррекцию prompt’ов


Разметку хороших примеров для few-shot


Полуручной режим старта
Вообще можно стартовать так:


бот принимает идею,


free report — автоматически,


paid report — полуавтомат:


генерируется AI draft,


ты руками чуть правишь,


отправляешь пользователю.




Это хороший pre-MVP, если хочешь сперва проверить willingness to pay.

15) Риски
Продуктовые


Ответы выглядят как generic AI-water


лечится структурой и коротким output




Пользователь ждет “оракула”, а получает просто умный разбор


нужен честный positioning




Слишком много одинаковых идей


нужно few-shot и rubric, а не “свободное эссе”




Низкая ценность paid


paid должен давать конкретику, а не длиннее тот же текст




Технические


Telegram retries / duplicate webhook


LLM output ломает JSON


Long response formatting in Telegram


Billing/access mismatch


Юнит-экономические


Слишком дорогой deep report


Маленький ARPPU


Free users жрут токены без конверсии


Юридические / репутационные


Пользователи боятся сливать идеи


Могут трактовать вывод как инвестиционный совет


Жалобы на “AI чушь”


Что делать


дисклеймер,


не обещать truth,


дать delete history,


не хранить лишнее,


paid делать реально полезнее.



16) Монетизация
Лучший старт
Freemium


1–3 free idea checks


paid deep report per idea


later пакет кредитов


Рекомендуемая схема
Вариант A


Free: короткий verdict


Paid: deep report за фиксированную сумму


Вариант B


Free: 1 идея/день


Pro: N deep reports в месяц


Вариант C


Pay-per-report + subscription
На старте можно, но лучше сначала один понятный paid action.


Мой выбор для запуска
Free short verdict + paid deep report per idea
Потому что:


очень понятный paywall;


легко мерить конверсию;


не надо сразу продавать подписку в пустоту.



17) GTM
Каналы


Telegram-каналы про стартапы, AI, no-code, indie hacking


Контент “разбираем безумные идеи”


UGC: пользователи шарят свои разборы


Short-form контент:


“проверили 10 стартап-идей”


“почему идея звучит круто, но не полетит”




Партнерки с каналами / чатами founders


Первые growth hooks


Разбор популярных идей


Серия “скинь идею — получи verdict”


Leaderboard лучших/худших идей — позже, опционально


Referral: “пригласи друга — получи deep report”


Самый реалистичный early GTM
Контент-машина + Telegram-native distribution.

18) Unit economics
Ниже — не рыночная истина, а рабочая модель для MVP.
Допущения
Free report


AI cost: $0.005–0.02


infra + logging: $0.001–0.005


total: $0.006–0.025


Paid report


AI cost: $0.03–0.12


infra + formatting + retries: $0.01


total: $0.04–0.13


Pricing hypothesis
Starter


Free: 1–3 оценки


Paid deep report


$3.99–9.99 per report
Для старта я бы тестировал:


low-ticket: $4.99


mid-ticket: $7.99


Gross margin
Даже при себестоимости $0.10 и цене $4.99 маржа очень жирная.
Проблема будет не в cost, а в конверсии.
Пример модели
Если за месяц:


3,000 free users


8% нажали на paywall


3% от всех free купили deep report


это 90 paid reports


Выручка


90 × $4.99 = $449.1


Себестоимость AI


90 × $0.10 = $9


Даже если добавить free cost и прочее, проблема не в юнит-экономике вычислений.
Проблема только в:


acquisition,


retention,


value perception.


Главный вывод
Это продукт с очень дешевой себестоимостью ответа.
Значит ключевой вопрос:
сможешь ли ты продавать ощущение “полезного интеллектуального фильтра”, а не просто очередной AI-output.

19) Метрики успеха
North star
Количество paid deep reports на 100 активных пользователей.
Основные метрики


ideas submitted / day


free completion rate


free → paid conversion


repeat users %


paid repurchase rate


average AI cost / report


refund / complaint rate


share rate (пересылки)


Good enough first signals
Через 2–3 недели после запуска:


25%+ пользователей доходят до free result


5%+ от получивших free result покупают deep report


15%+ пользователей возвращаются с новой идеей


средняя себестоимость ответа под контролем



20) Roadmap
Phase 0 — pre-MVP


bot shell


manual report drafting


20–50 пользователей


проверка willingness to pay


Phase 1 — MVP


free short report


paid deep report


history


admin


payment unlock


Phase 2


compare two ideas


niche-specific templates


founder mode / agency mode


export to Notion / PDF


Phase 3


web app


team workspace


optional web enrichment


benchmarks по типам идей



21) Дерево /project-docs
/project-docs  /00-product    vision.md    positioning.md    target-audience.md    jobs-to-be-done.md  /01-strategy    launch-format.md    mvp-scope.md    not-scope.md    pricing.md    gtm.md    risks.md    success-metrics.md  /02-ux    user-flow.md    telegram-screens.md    admin-screens.md    copy-deck.md  /03-ai    evaluation-rubric.md    prompt-free-evaluator.md    prompt-paid-report.md    json-schema.md    output-formatting.md    safety-rules.md  /04-architecture    system-overview.md    tech-stack.md    modules.md    sequence-flow.md    infra.md  /05-data    data-model.md    db-schema.md    events.md  /06-api    api-spec.md    webhook-contracts.md    error-handling.md  /07-delivery    backlog-mvp.md    milestones.md    acceptance-criteria.md    qa-checklist.md    ops-runbook.md  /08-business    unit-economics.md    monetization.md    experiments.md  /09-claude    master-prompt.md    implementation-rules.md

22) Что должно быть в каждом doc-файле
vision.md


что за продукт


для кого


какую задачу решает


чем не является


positioning.md


“не бизнес-оракул, а быстрый фильтр идеи”


ценность free


ценность paid


mvp-scope.md


точный feature list v1


evaluation-rubric.md


критерии


вес


verdict mapping


prompt-free-evaluator.md


системный prompt для free


примеры input/output


prompt-paid-report.md


системный prompt для paid


строгая структура ответа


system-overview.md


high-level архитектура


data-model.md


сущности и связи


api-spec.md


endpoints


request/response schema


backlog-mvp.md


что делать сначала


что делать потом


что не делать



23) Master-prompt для Claude Code
Ниже готовый мастер-промпт. Его можно вставлять в Claude Code как стартовую постановку.
You are my pragmatic CTO/product engineer.Build a lean MVP for a Telegram bot that evaluates startup/product ideas.Product concept:A user sends a raw idea in Telegram. The bot returns:1) a short free verdict,2) a paid deep breakdown.The product is NOT an oracle that predicts startup success.It is a structured idea stress-test assistant.Main audience:- founders- indie hackers- PMs / marketers / developers with many raw ideas- Telegram-native usersMain JTBD:“I have a rough idea and want a fast sanity check: is it worth testing, what is wrong with it, and what should I do next?”Your task:Create a production-lean but launchable MVP package and codebase.No overengineering.Optimize for fastest launch and hypothesis validation.Core constraints:- Telegram-first, no user web app in v1- Minimal admin panel is allowed- Monolith architecture- Python stack preferred- Simple, explicit, maintainable code- Cost-aware AI usage- Good UX in Telegram- Avoid generic AI-water responses- Strong structured outputs- Free and paid flows must be clearly different in valueUse this tech stack unless there is a strong reason not to:- Python 3.12- FastAPI- aiogram- PostgreSQL- SQLAlchemy 2- Alembic- Pydantic- Jinja2 or HTMX for minimal admin UI- Docker / docker-compose- NginxArchitecture rules:- Single backend service- Telegram webhook handled by FastAPI- Store users, ideas, reports, payments, events in PostgreSQL- No microservices- No Kubernetes- No vector DB- No RAG- No React frontend for MVP- No Redis unless truly necessary- Background generation can be done with simple async/background task patternProduct behavior:Free report must include:- verdict- total score- 3 strengths- 3 weaknesses- 1 next stepPaid report must include:- normalized idea- audience / ICP- pain/value proposition- why it may work- why it may fail- MVP scope- what should NOT be in MVP- monetization options- GTM hypothesis- 3 fast validation tests- final recommendationVerdict buckets:- Strong hypothesis- Worth testing- Raw / undercooked- Do not launch it like thisScoring dimensions:- clarity- pain intensity- audience specificity- distribution feasibility- monetization potential- execution simplicity- differentiation- validation speedExpected AI design:- Prompt A: short evaluator with strict JSON output- Prompt B: deep report with strict structure- deterministic parsing layer- token/cost logging per request- model abstraction to support a cheap model for free and a better model for paidNeed anti-garbage behavior:- if user sends vague nonsense, bot should ask for slightly more structure- if text is too short, bot should request clarification template- basic abuse/rate-limit protectionPayment approach:Design a generic payment abstraction.Manual unlock must also be supported via admin panel.Do not hardwire to one provider too deeply.Build the following deliverables:1. /project-docs folder with:- product docs- scope docs- UX docs- AI docs- architecture docs- data model docs- API docs- backlog and acceptance criteria- business docs- operational notes2. Codebase with:- FastAPI app- Telegram webhook handling- report generation pipeline- DB models and migrations- admin panel- environment config- logging- basic tests3. Prompt files:- free evaluator prompt- paid report prompt- output schemas4. Clear README with:- setup- env vars- local run- webhook setup- migrations- deployment notes5. MVP backlog and launch checklistProduct decisions to follow:- Telegram bot is the main UI- free-to-paid conversion is the main monetization path- paid value must be concrete, not just “more text”- all copy should be concise and sharp- avoid fake precision- do not claim to know real market size without external data- be honest in outputsImportant:When unsure, choose the simpler implementation.Prefer “working and launchable this week” over “architecturally beautiful”.Write code and docs as if a solo founder will maintain it.Now execute in this order:STEP 1 — define product docsCreate /project-docs structure and fill all docs with pragmatic content.STEP 2 — define architectureDesign modules, data model, API contracts, and Telegram flows.STEP 3 — implement backendGenerate the monolith app structure and code.STEP 4 — implement AI layerCreate prompt templates, schemas, report builders, and parsing logic.STEP 5 — implement adminMinimal admin pages for users, ideas, reports, and manual unlock.STEP 6 — delivery layerAdd Docker, env config, migrations, README, and launch checklist.STEP 7 — final auditReview for overengineering and remove anything not needed for MVP.Non-goals:- no mobile app- no web user cabinet- no multi-agent architecture- no vector search- no competitor scraping- no fancy dashboards- no overbuilt auth systemAcceptance criteria:- a Telegram user can send an idea and receive a free result- paid result can be unlocked and generated- reports are saved in DB- admin can inspect and unlock reports- prompts are structured and maintainable- docs are usable by a solo founder- local run and deploy are documentedStart by generating the /project-docs tree and filling the docs with useful content, then scaffold the codebase.

24) Самое важное продуктовое решение
Если сжать всё до одного тезиса:
Ты не продаешь “оценку идеи”.
Ты продаешь быстрый переход от сырой мысли к тестируемому плану.
Именно поэтому paid-версия должна отвечать не на вопрос “норм или нет”, а на вопрос:
“Окей, что конкретно делать с этой идеей дальше?”

25) Мой финальный вердикт по самой идее
Идея сама по себе
Нормальная для быстрого запуска.
Почему


очень простой вход;


понятный Telegram UX;


дешевая себестоимость;


легко делать контент-маркетинг;


легко тестировать платный upgrade.


Главный риск
Это легко скатить в очередной “AI говорит умные слова”.
Значит вся игра — в:


хороший rubric,


короткий sharp output,


реальную полезность paid-части.


Как бы я запускал


Telegram-only


Free short verdict


Paid deep report


Полуручной режим первую неделю


Потом автоматизация


Контент через “разбор идей подписчиков”



Могу следующим сообщением сразу дать тебе готовое содержимое всех md-файлов из /project-docs, чтобы это можно было почти без правок скормить в Claude Code.
