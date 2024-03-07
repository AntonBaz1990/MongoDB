**Задание 1:**
```javascript
db.posts.find({ 
    topics: "as",
    author_id: /example\.ru/,
    score: { $gt: 100 }
})
```

**Задание 2:**
```javascript
db.posts.insertMany([
    {
        creation_date: new Date(),
        author: "skbx@example.com",
        topics: ["mongodb"]
    },
    {
        creation_date: new Date("2021-12-31"),
        author: "skbx@example.ru"
    }
])
```

**Задание 3:**
```javascript
db.users.createIndex({ first_name: 1, last_name: 1 })
```
Для проверки использования индекса можно воспользоваться методом explain:
```javascript
db.users.find({ first_name: "Имя", last_name: "Фамилия" }).explain("executionStats")
```

**Задание 4:**
```javascript
db.users.aggregate([
    { $match: { visits: { $gt: 300 } } },
    { 
        $group: {
            _id: { $substr: ["$first_name", 0, 1] },
            total_karma: { $sum: "$karma" }
        }
    }
])
```

**Задание 5:**  
MongoDB не поддерживает явно хранимые процедуры.  Можете создать JavaScript-функцию и использовать ее в запросах функции shuffle:
```javascript
var shuffle = function(str) {
    var arr = str.split('');
    for (var i = arr.length - 1; i > 0; i--) {
        var j = Math.floor(Math.random() * (i + 1));
        var temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }
    return arr.join('');
}