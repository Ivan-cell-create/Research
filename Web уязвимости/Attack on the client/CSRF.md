# Cross-Site Request Forgery (CSRF)

## Что такое CSRF?

**CSRF** (Cross-Site Request Forgery) — это тип атаки, при которой злоумышленник заставляет браузер жертвы выполнить нежелательное действие на доверенном сайте, где жертва уже авторизована. :contentReference[oaicite:0]{index=0}

Пример: если пользователь вошёл в свой интернет-банк, злоумышленник может отправить запрос на перевод средств от имени пользователя без его ведома.

## Как это работает?

1. Пользователь авторизуется на сайте, получая сессионный cookie.
2. Злоумышленник создаёт поддельный запрос (например, через скрытую форму или изображение) на тот же сайт.
3. Браузер пользователя автоматически отправляет этот запрос с действующим cookie.
4. Сервер принимает запрос как легитимный, так как он содержит действительные учетные данные пользователя.

## Примеры уязвимости

- **Скрытая форма**:

  ```html
  <form action="https://example.com/transfer" method="POST">
    <input type="hidden" name="recipient" value="attacker" />
    <input type="hidden" name="amount" value="1000" />
  </form>
  <script>
    document.forms[0].submit();
  </script>
  ```

Ссылка с GET-запросом:

 ```html
<img src="https://example.com/transfer?recipient=attacker&amount=1000" />
 ```

 При загрузке изображения браузер отправляет запрос на сервер, выполняя действие без ведома пользователя.

 # Как защититься от CSRF?

1. **Использование CSRF-токенов**  
Включение уникального токена в каждую форму и проверка его на сервере помогает убедиться, что запрос был отправлен с вашего сайта.  
*Источник: [Sapphire](https://www.sapphire.net/blogs-press-releases/xsrf-attack/)*

2. **Заголовки Referer и Origin**  
Проверка этих заголовков позволяет убедиться, что запрос исходит с вашего домена.  
*Источник: [MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/Security/CSRF)*

3. **Метод HTTP**  
Использование методов, изменяющих состояние (например, POST), вместо GET для операций, которые изменяют данные.

4. **SameSite Cookies**  
Установка флага `SameSite` в cookie на значение `Strict` или `Lax` ограничивает отправку cookie только с вашего сайта.  
*Источник: [Sapphire](https://www.sapphire.net/blogs-press-releases/xsrf-attack/)*

5. **Разделение API**  
Использование отдельных API для браузера и мобильных приложений помогает избежать уязвимостей, связанных с CSRF.  
*Источник: [EITCA Academy](https://eitca.org/cybersecurity/eitc-is-wasf-web-applications-security-fundamentals/same-origin-policy/cross-site-request-forgery/examination-review-cross-site-request-forgery/how-can-web-developers-prevent-csrf-attacks/)*

---

# Заключение

CSRF — это серьёзная угроза для веб-приложений, особенно тех, которые используют cookie для аутентификации. Важно применять комплексный подход к защите, включая использование CSRF-токенов, проверку заголовков и настройку cookie.

---

# Полезные ссылки

- [OWASP: Cross-Site Request Forgery (CSRF)](https://owasp.org/www-community/attacks/csrf)
- [MDN: Cross-Site Request Forgery (CSRF)](https://developer.mozilla.org/en-US/docs/Glossary/CSRF)

---

> Вся информация предоставлена исключительно в учебных целях. Используйте её для повышения безопасности, а не для нанесения вреда.
