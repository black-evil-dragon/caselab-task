Мы создадим простой REST API, который умеет отдавать список книг и информацию по конкретной книге. Это как маленький backend для книжного магазина или библиотеки

### Создай ветку со своей фамилией
Например: `feature/golgan-task`

### Создай класс `Book` со следующими полями:
```java
public class Book {
	private Long id;
	private String title;
	private String author;
	private Integer year;

	// ...
}
```
## API-эндпоинты

Реализуй следующие пути:

| Метод | Путь | Описание                                                   |
|-------|------|------------------------------------------------------------|
| POST | `/api/users` | создать пользователя                                       |
| GET | `/api/users/{id}` | получить пользователя по ID                                |
| POST | `/api/users/{userId}/tasks` | создать задачу для пользователя                            |
| GET | `/api/users/{userId}/tasks` | получить все задачи пользователя (с пагинацией `Pageable`) |
| PATCH | `/api/tasks/{taskId}` | отметить задачу выполненной                                |
| DELETE | `/api/tasks/{taskId}` | удалить задачу (только если она принадлежит пользователю)  |

---
### Подсказка контроллера в проекте
```java
@GetMapping("/{id}")
public ResponseEntity<Book> getBookById(@PathVariable Long id) {
    Book book = bookService.findById(id);
    if (book == null) {
        return ResponseEntity.notFound().build();
    }
    return ResponseEntity.ok(book);
}
```
## Пример структуры ответа

```http
GET /api/users/1
{
  "id": 1,
  "name": "Иван Петров",
  "email": "ivan@example.com"
}
```
```http
GET /api/users/1/tasks?page=0&size=10
{
  "content": [
    {
      "id": 101,
      "title": "Изучить JPA",
      "completed": false,
      "deadline": "2025-12-31T23:59:59"
    }
  ],
  "pageable": {
    "pageNumber": 0,
    "pageSize": 10,
    "sort": {
      "empty": true,
      "sorted": false,
      "unsorted": true
    },
    "offset": 0,
    "paged": true,
    "unpaged": false
  },
  "totalPages": 1,
  "totalElements": 1,
  "last": true,
  "size": 10,
  "number": 0,
  "sort": {
    "empty": true,
    "sorted": false,
    "unsorted": true
  },
  "numberOfElements": 1,
  "first": true,
  "empty": false
}

```
### Завершение работы.
Отправь **Pull request** из своей ветки в ветку основного репозитория