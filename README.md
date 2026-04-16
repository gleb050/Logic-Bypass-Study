# Business Logic Vulnerability Research

### Description
This project documents a case study of a quantity manipulation vulnerability (Insecure Logic) discovered in a live e-commerce environment.

### The Vulnerability
The server-side implementation failed to validate the data type of the `quantity` field. While the frontend restricted input to integers, the backend accepted floating-point numbers via direct API manipulation.

### Steps to Reproduce
1. Intercepted the "Add to Cart" request via Browser DevTools.
2. Modified the payload from `{"quantity": 1}` to `{"quantity": 0.2}`.
3. The backend calculated the price proportionally (20% of original price).
4. Order was successfully placed and paid via legal payment gateway.

### Impact
Critical financial loss risk. An attacker could purchase high-value items for a fraction of their cost.

### Mitigation
Implemented server-side validation to ensure `quantity` is a positive integer and meets the minimum threshold.

# Исследование уязвимости бизнес-логики (Write-up)

### Описание
В данном репозитории задокументирован кейс обхода проверки количества товара (Insecure Logic), обнаруженный в действующем интернет-магазине.

### Суть уязвимости
Серверная часть приложения не проверяла тип данных в поле `quantity` (количество). В то время как фронтенд ограничивал ввод целыми числами, бэкенд принимал дробные числа через прямую манипуляцию API-запросом.

### Шаги для воспроизведения
1. Перехват запроса "Добавить в корзину" через DevTools браузера.
2. Изменение полезной нагрузки (payload) с `{"quantity": 1}` на `{"quantity": 0.2}`.
3. Сервер рассчитал цену пропорционально (20% от исходной стоимости).
4. Заказ был успешно размещен и оплачен, сформирован реальный фискальный чек.

### Последствия
Критический финансовый риск. Злоумышленник может покупать дорогостоящие товары за долю их стоимости.

### Рекомендация по исправлению
Внедрить проверку на стороне сервера, чтобы количество товара было строго положительным целым числом.
