# 개요
비동기 문제를 해결하기 위한 지시어로 기존 Callback 또는 Promise 를 대체하며

비동기 코드를 동기코드 처럼보이도록 만들어 준다

Node8 부터 완전히 지원한다 (7.6에서 일부 지원)

# 사용
 - `async` 키워드를 사용하여 함수를 선언한다
 - `await` 키워드는 `async` 로 정의된 함수내에서 사용한다
 - `then().error()` 구문을 처리하기 위해서는 `try / catch` 를 사용한다
   

# 예제

```javascript
//before 
function handler (req, res) {
  return request('https://user-handler-service')
    .catch((err) => {
      logger.error('Http error', err)
      error.logged = true
      throw err
    })
    .then((response) => Mongo.findOne({ user: response.body.user }))
    .catch((err) => {
      !error.logged && logger.error('Mongo error', err)
      error.logged = true
      throw err
    })
    .then((document) => executeLogic(req, res, document))
    .catch((err) => {
      !error.logged && console.error(err)
      res.status(500).send()
    })
}

//after
async function handler (req, res) {
  let response
  try {
    response = await request('https://user-handler-service')  
  } catch (err) {
    logger.error('Http error', err)
    return res.status(500).send()
  }

  let document
  try {
    document = await Mongo.findOne({ user: response.body.user })
  } catch (err) {
    logger.error('Mongo error', err)
    return res.status(500).send()
  }

  executeLogic(document, req, res)
}
```

```javascript
//before
function executeAsyncTask () {
  return functionA()
    .then((valueA) => {
      return functionB(valueA)
        .then((valueB) => {          
          return functionC(valueA, valueB)
        })
    })
}

//after
async function executeAsyncTask () {
  const valueA = await functionA()
  const valueB = await functionB(valueA)
  return function3(valueA, valueB)
}

```


참고 * https://blog.risingstack.com/mastering-async-await-in-nodejs/