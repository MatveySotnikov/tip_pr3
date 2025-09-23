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

## Ошибка кодировки

Так как файлы изначально были созданы через PowerShell (```echo```) их кодировка была неподходящей для Go, что привело к следующей ошибке:    
<img width="954" height="57" alt="Ошибка кодировки" src="https://github.com/user-attachments/assets/6df8f837-8447-4207-ae62-449e000715e3" />   

Решением данной проблемы стало изменение кодировки файлов прямиком в VSCode:    
<img width="625" height="421" alt="Изменение кодировки" src="https://github.com/user-attachments/assets/958a07b2-5798-40aa-af04-8d4e2ba24a2a" />    
Все файлы были перезаписаны в UTF-8, и сервер смог запуститься с новыми зависимостями:   
<img width="507" height="61" alt="успешный успех" src="https://github.com/user-attachments/assets/a0e41936-84d3-4309-b89b-640ebb22df9a" />    






