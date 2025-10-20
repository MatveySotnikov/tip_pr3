# Практическая работа 3 - Реализация простого HTTP-сервера на стандартной библиотеке net/http. Обработка запросов GET/POST

## Цели занятия:   
* Освоить базовую работу со стандартной библиотекой net/http без сторонних фреймворков.   
*	Научиться поднимать HTTP-сервер, настраивать маршрутизацию через http.ServeMux.   
* Научиться обрабатывать параметры запроса (query, path), тело запроса (JSON/form-data) и формировать корректные ответы (код статуса, заголовки, JSON).   
* Научиться базовому логированию запросов и обработке ошибок.
  
## Запуск сервера

Напишем изначальный код для сервера и запустим:

```
package main

import (
	"log"
	"net/http"
)

func main() {
	mux := http.NewServeMux()
	mux.HandleFunc("GET /health", func(w http.ResponseWriter, r *http.Request) {
		w.Header().Set("Content-Type", "application/json")
		w.WriteHeader(http.StatusOK)
		w.Write([]byte(`{"status":"ok"}`))
	})

	addr := ":8080"
	log.Println("listening on", addr)
	if err := http.ListenAndServe(addr, mux); err != nil {
		log.Fatal(err)
	}
}
```

<img width="952" height="357" alt="Проверка сервера 1" src="https://github.com/user-attachments/assets/89cb9dcc-df80-4d3a-808a-e799c0914224" />  

Сервер запущен и успешно работает (код 200)    
Проверка через POSTMAN:

<img width="615" height="716" alt="HealthPostman" src="https://github.com/user-attachments/assets/d9901a19-c002-4515-97ca-e1c3ea45e01a" /> 

## Проверка GET и POST
Сделаем POST для двух задач
<img width="834" height="679" alt="POSTPostman" src="https://github.com/user-attachments/assets/bed5c3e1-b9dd-45e3-81e3-6456daf0801c" />

<em>Добавили задачу №1</em>
<br>


<img width="818" height="688" alt="POST2Postman" src="https://github.com/user-attachments/assets/331ba7c6-1805-4578-893a-eafeff1ef9eb" />

<em>Добавили задачу №2</em> 
<br>   

Далее проверим GET


<img width="628" height="489" alt="GETtasks" src="https://github.com/user-attachments/assets/0bafe561-31d5-446a-92ba-d67d1625f2c3" />

<em>Проверяем список задач GET /tasks</em> 

<br>


<img width="447" height="379" alt="GETtasksID" src="https://github.com/user-attachments/assets/b4a71e7f-927e-4c8d-814b-9637b375101a" />

<em>Получаем задачу по id GET /tasks/[id]</em> 


<br>
<img width="825" height="460" alt="GETtasks?q=" src="https://github.com/user-attachments/assets/7eb9ad44-d27e-4663-91b4-5fe9aa3d582b" />    

<em>Проверка фильтрации</em> 
<br>

Настроим ошибку, при обращении к несуществующему id

<img width="481" height="364" alt="Ошибка ID (неверная)" src="https://github.com/user-attachments/assets/f2f5824a-6271-4b30-9a20-9cf5fa86033e" />

<em></em> 

<img width="811" height="379" alt="Фикс ошибки GET tasks/{несуществующий id}" src="https://github.com/user-attachments/assets/72814be2-c993-442e-b1a2-f8d9ed2ae699" />

<img width="1379" height="780" alt="Отсутствие валдиации" src="https://github.com/user-attachments/assets/463382d3-3b8a-450b-bba3-6a2f15a1e3c4" />

```
if len(req.Title) > MaxTitleLength {
		BadRequest(w, "title is too long (max 140 characters)")
		return
	}
```

<img width="796" height="630" alt="Добавленная валидация" src="https://github.com/user-attachments/assets/82afb99d-19da-4870-a942-7489fed2d6b4" />

<img width="787" height="659" alt="Валидация 2" src="https://github.com/user-attachments/assets/69d0cc08-9611-473c-9029-42a604d22228" />








