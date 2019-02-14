# 개요
ORM(Object-Relational Mapping or Object-Relational modeling) Framework for NodeJS

여러 type의 db 에 대해 코드를 통해 schema define, validation, association 등을 정의하고 CRUD 등의 DB 작업을 할 수 있다.


## 이점
 * DB Type 의 상관없이 동일한 코드로 db 작업을 진행 할 수 있다
 * sequelizejs 에 비해 단순한 문법과 쉬운 사용 


## 예제
   
### Schema define
``` javascript
const cormo = require('cormo');
const connection = new cormo.Connection('mysql', { database: 'test' });

// this will create two tables - users, posts - in the database.

const User = connection.model('User', {
  name: { type: String },
  age: { type: cormo.types.Integer }
});

const Post = connection.model('Post', {
  title: String, // `String` is the same as `type: String`
  body: 'string', // you can also use `string` to specify a string type
  date: Date
});

const User = connection.model('User', {
  name: { type: String, required: true },
  age: { type: Number, required: true },
  email: { type: String, unique: true, required: true }
});
```

### Validation
```javascript
User.addValidator((record) => {
  if (record.age<18) {
    return 'too young';
  }
});
```

### Callback
```javascript
User.beforeSave(() => {
  this.name = this.name.trim();
});
```
   
### Association   
```javascript
var User = connection.model('User', {
  name: String,
  age: Number
});

var Post = connection.model('Post', {
  title: String,
  body: String
});

User.hasMany(Post);
Post.belongsTo(User);
```
     
### CRUD
```javascript
//Create
const user1 = new User({ name: 'John Doe', age: 27 });
await user1.save();

const user2 = await User.create({ name: 'John Doe', age: 27 });

//Read
const user = await User.find(1);

const users = await User.where({name: 'John Doe'});

const users = await User.where({age: 27})
  .select(['name'])
  .order('name')
  .limit(5)
  .skip(100);

const users = await User.where({$or: [ { age: { $lt: 20 } }, { age: { $gt: 60 } } ]})
  .where({name: { $contains: 'smi' }});

//Update
const user = await User.find(1);
user.age = 30;
await user.save();

const count = await User.find(1).update({age: 10});

const count = await User.where({age: 27}).update({age: 10});

const count = await User.where({age: 35}).update({age: {$inc: 3}});

// Delete
const count = await User.delete({age: 27});

```

### 기타
 - 좌표 타입 제공
 - Aggregation
 - 지원하는 디비 종류: MySQL, MongoDB, PostgreSQL

### 참고
* http://croquiscom.github.io/cormo/index.html