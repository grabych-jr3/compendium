# Spring Security
## Автентифікація
### Flow:
1. Клієнт відправляє HTTP request
2. SecurityFilterChain витягує із запиту username і password, створює Authentication request (наприклад UsernamePasswordAuthenticationToken) і передає до AuthenticationManager
3. AuthenticationManager(зазвичай ProviderManager) перебирає AuthenticationProviders і якщо AuthenticationProvider підтримує тип Authentication - він виконує аутентифікацію
4. AuthenticationProvider викликає UserDetailsService, завантажує користувача з БД і перевіряє пароль
5. Якщо пароль правильний, то повертається ауторизований Authentication
6. Authentication записується в SecurityContext, а context в SecurityContextHolder
