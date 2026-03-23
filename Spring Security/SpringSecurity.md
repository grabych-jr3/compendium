<img width="1408" height="568" alt="image" src="https://github.com/user-attachments/assets/b4e6fd41-8af1-410f-bdd2-95ff9b422780" /># Spring Security
## Автентифікація
### Basic Authentication
#### Flow
1. Клієнт робить HTTP request
2. Сервер відповідає 401(Unauthorzied) + Header: WWW-Authenticate: Basic
3. Клієнт відправляє свої Credentials: Authorization: Basic Base64(username:password)
4. Сервер перевіряє Credentials

### UsernamePasswordAuthentication
#### Flow:
1. Клієнт відправляє HTTP request
2. SecurityFilterChain витягує із запиту username і password, створює Authentication request (наприклад UsernamePasswordAuthenticationToken) і передає до AuthenticationManager
3. AuthenticationManager(зазвичай ProviderManager) перебирає AuthenticationProviders і якщо AuthenticationProvider підтримує тип Authentication - він виконує аутентифікацію
4. AuthenticationProvider викликає UserDetailsService, завантажує користувача з БД і перевіряє пароль
5. Якщо пароль правильний, то повертається ауторизований Authentication
6. Authentication записується в SecurityContext, а context в SecurityContextHolder

### JWT
#### How JWT works:
<img width="1408" height="568" alt="image" src="https://github.com/user-attachments/assets/990a4316-284e-473d-bd8a-2b6f433d8a65" />

**Header** - тип токена та алгоритм шифрування
**Payload** - корисне навантаження. Тут лежить claims - інформація про користувача(id, username, roles) та службова інформація
**Signature** - хеш від заголовка, payload і секретного ключа
**!!!НІКОЛИ НЕ КЛАСТИ В JWT ПАРОЛІ ТА СЕКРЕТНІ ДАНІ**
