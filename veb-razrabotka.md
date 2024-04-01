# 🌐 Веб-разработка

## **Написание веб-приложения:**

Мы разработаем простое веб-приложение, которое будет работать с абстрактными элементами (назовем их items). Наше приложение сможет хранить items, также по запросу пользователя приложение сможет добавлять новые items, изменять их и удалять. В item будут лежать данные о его названии, цене и наличии.

### 1. Создать файл main.pу и запустить его

как создать main.py файл вы сможете прочитать тут

### 2. Далее импортируем классы FastAPI, HTTPException, status для дальнейшей работы с ними



<pre class="language-python"><code class="lang-python"><strong>from fastapi import FastAPI, HTTPException, status
</strong></code></pre>

### 3. Создаем экземпляр класса FastAPI для создания нашего приложения. Также нам потребуется создать список items для хранения данных и переменную items\_id для идентификации items

```python
app = FastAPI()
items = []
items_id = 1
```

### 4.  Создадим первый endpoint, который будет возвращать сообщение "Hello World"

\*endpoint - это часть URL-адреса, указывающая, какой ресурс мы хотим получить

```python
@app.get('/')
def root():
    return {'message': 'Hello World'}
```

### 5.  Далее создадим endpoint '/items', который будет обрабатывать GET-запросы и возвращать требуемый item, если он существует

```python
@app.get('/items')
def get_item(item_id: int):
    try:
        return items[item_id - 1]
    except IndexError:
        raise HTTPException(status_code=status.HTTP_404_NOT_FOUND, detail='item does not exists')
```

Проверка существования item происходит за счёт блока try except. Если элемента с переданным id не существует, будет вызвано исключение IndexError, так как мы выйдем за границы нашего списка. Если элемента не существует, мы оповещаем об этом пользователя статус-кодом 400 и сообщением "item does not exists"

### 6. Теперь создадим endpoint '/items', который будет обрабатывать POST-запросы, создавать item и добавлять его в список items

