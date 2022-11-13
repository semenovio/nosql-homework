# Базовые возможности mongodb 
Используемаю коллекция: https://www.kaggle.com/datasets/shwetabh123/mall-customers?datasetId=7721
#### Получить колличество клиентов старше 35 лет
    db.customers.find({"Age" : {$gt: '35'}}).count()
#### Результат
    102
    
#### Получить список, первых пяти клиентов от 25 до 50 лет, отсортировать по доходу
    db.customers.aggregate([{$match : {"Age" :{$gt:'25', $lt:'50'}}}, {'$sort':{'Annual Income (k$)':1}}, {'$limit':5}])
#### Результат
    
    [
    {
      _id: ObjectId("6370c80e9f4dc0f710d70c17"),
      CustomerID: '0188',
      Genre: 'Male',
      Age: '28',
      'Annual Income (k$)': '101',
      'Spending Score (1-100)': '68'
    },
    {
      _id: ObjectId("6370c80e9f4dc0f710d70c19"),
      CustomerID: '0190',
      Genre: 'Female',
      Age: '36',
      'Annual Income (k$)': '103',
      'Spending Score (1-100)': '85'
    },
    {
      _id: ObjectId("6370c80e9f4dc0f710d70c1b"),
      CustomerID: '0192',
      Genre: 'Female',
      Age: '32',
      'Annual Income (k$)': '103',
      'Spending Score (1-100)': '69'
    },
    {
      _id: ObjectId("6370c80e9f4dc0f710d70c1a"),
      CustomerID: '0191',
      Genre: 'Female',
      Age: '34',
      'Annual Income (k$)': '103',
      'Spending Score (1-100)': '23'
    },
    {
      _id: ObjectId("6370c80e9f4dc0f710d70c18"),
      CustomerID: '0189',
      Genre: 'Female',
      Age: '41',
      'Annual Income (k$)': '103',
      'Spending Score (1-100)': '17'
    }
    ]
 
#### Добавить нового клиента с новым полем name
    customers> db.customers.insert({ "CustomerID": "500", "Genre": "Male", "Age": "37", "Annual Income (k$)": "20", "Spending Score (1-100)": "13", "name": "John" })
    {
    acknowledged: true,
    insertedIds: { '0': ObjectId("6370e044cf46247177c1357e") }
    }
    customers> db.customers.find({"name" : "John"})
    [
    {
        _id: ObjectId("6370e044cf46247177c1357e"),
        CustomerID: '500',
        Genre: 'Male',
        Age: '37',
        'Annual Income (k$)': '20',
        'Spending Score (1-100)': '13',
        name: 'John'
    }
    ]
    
#### Добавить всем мужчинам старше 35 имя John
    customers> db.customers.updateMany({$and: [{"Age" : {$gt:"35"}}, {"Genre" : "Male"}]}, {$set: {"name": "John"}})
    {
    acknowledged: true,
    insertedId: null,
    matchedCount: 48,
    modifiedCount: 46,
    upsertedCount: 0
    }
    customers> db.customers.find({"name": "John"}).limit(5)
    [
    {
        _id: ObjectId("6370c80e9f4dc0f710d70b64"),
        CustomerID: '0009',
        Genre: 'Male',
        Age: '64',
        'Annual Income (k$)': '19',
        'Spending Score (1-100)': '3',
        name: 'John'
    },
    {
        _id: ObjectId("6370c80e9f4dc0f710d70b66"),
        CustomerID: '0011',
        Genre: 'Male',
        Age: '67',
        'Annual Income (k$)': '19',
        'Spending Score (1-100)': '14',
        name: 'John'
    },
    {
        _id: ObjectId("6370c80e9f4dc0f710d70b6a"),
        CustomerID: '0015',
        Genre: 'Male',
        Age: '37',
        'Annual Income (k$)': '20',
        'Spending Score (1-100)': '13',
        name: 'John'
    },
    {
        _id: ObjectId("6370c80e9f4dc0f710d70b6e"),
        CustomerID: '0019',
        Genre: 'Male',
        Age: '52',
        'Annual Income (k$)': '23',
        'Spending Score (1-100)': '29',
        name: 'John'
    },
    {
        _id: ObjectId("6370c80e9f4dc0f710d70b7a"),
        CustomerID: '0031',
        Genre: 'Male',
        Age: '60',
        'Annual Income (k$)': '30',
        'Spending Score (1-100)': '4',
        name: 'John'
    }
    ]
    
#### Удальть всех клиентов с оценкой расходов меньше 50
    customers> db.customers.deleteMany({"Spending Score (1-100)" : {$lt: "50"}})
    { acknowledged: true, deletedCount: 94 }
    customers> db.customers.find({"Spending Score (1-100)" : {$lt: "50"}})

    customers> 
