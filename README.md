# Руководство по созданию мини приложений Gets One App на сайте [gets.one](https://www.gets.one)
**Gets One App** — это платформа встраиваемых приложений. Они создаются на базе стандартных веб-технологий: HTML, JS, CSS.

Приложения используються для разширения функциональности страниц. Технически приложение - это сайт, который открываеться во фрейме на вашей странице.

## Создание приложения
1) Перейдите по адресу [gets.one/console/apps](https://www.gets.one/console/apps) и нажмите кнопку Создать приложение.

![Альтернативный текст](https://www.gets.one/public/images/hPfs21BkXl0mKK7EsZVF7kTeQ.png)

2) Напишите название приложения, загрузите иконку и кажмите кнопку Создать.

3) После создания приложения оно появиться в списке Ваших приложений. Нажмите на кнопку Редактор кода.

![Альтернативный текст](https://www.gets.one/public/images/ODUkvQUC8JuGgYyM7IqlX8UHj.png)

4) Вам откроется редактор кода приложения

![Альтернативный текст](https://www.gets.one/public/images/jpdWdp4HxFkw0Zorex5b1JB8E.png)

Мы предоставляем платформу только для клиентской части приложения(HTML, JS, CSS)

## Технические особености приложений

Приложение состоит из **одного** html блока c идентификатором app

`<div id="app"></div>`
>Весь html код должен быть внутри этого блока

и **одного** JS объекта, фреймворка Vue

    new Vue({
       el : '#app',
       data : {
          title : '',
       },
       methods : {
          init () {
            this.title = 'Привет мир!!!' 
          }
       },
       created () {
           this.init();
       }
    });
>Вся клиентская логика должна быть в этом объекте

Сборка приложения, с подключением необходимых библиотек происходит автоматически

## Подключаемые библиотеки
* bootstrap 4.5.3

* jquery-3.1.1

* vue 2.x

* getsoneApi 1.0

## User View и Admin View
В редакторе кода Вы создаете две версии приложения

![Альтернативный текст](https://www.gets.one/public/images/6nPqTPkN6tJ9iMHiFiNDKqdv0.png)

**User View** - приложение, которое открываеться на Вашей странице

**Admin View** - приложение для администратора, которое доступно в App Admin

## Gets One API
Внутри приложения Вам доступен глобальный объект `API`, для взаимодействия с сайтом

>В данный момент api очень ограничены, но мы добавляем новые

**getCurrentData(result)**

**result** - callback функция, в которую прийдет результат

Возвращает объект

    { 
      user : идентификатор пользователя или null,
      app : идентификатор приложения
    }
Способ вызова метода

    API.getCurrentData((d) => {
        console.log(d)
    });
    
**post(url, data, result)**

Отправляет post запрос

`url` - адрес сайта, на который нужно отправить запрос

`data` - данные, которые будут переданы методом `post`

`result` - callback функция, в которую прийдет результат

Способ вызова метода

    API.post('https://ipwhois.app/json/',null,(r)=>{
        console.log(r)
    });
    
## Технические ограничения
В приложениях запрещается:

* Подключать сторонние библиотеки, фреймворки
* Писать html вне `<div id="app"></div>`, `js` вне объекта `Vue`
* Использовать тег ссылки `<a>` и любым другим способом перенаправлять приложение на другой адрес. Это касается и форм `<form>`. Для отправки/получения данных используйте метод `post` из `API`
* Использовать функцию `alert()`
* Реализовывать систему авторирации/регистрации. Если для работы приложения необходима авторизация пользователей используйте `API.getCurentData`
