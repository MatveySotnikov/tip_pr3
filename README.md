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

