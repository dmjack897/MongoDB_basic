# MongoDB_basic

MongoDB를 공부하며 기본 개념들을 메모하겠습니다.


|MySQL|MongoDB|
|:----:|:----:|
|Database|Databases|
|Table|Collection|
|Row|Document|
|Column|Field|

MongoDB실행
- MongoDB 기본 포트번호 : 27017
```
mongo
```
DB생성 및 선택
```
use DB명
```
DB리스트 확인
- 최소 한개의 Document가 있어야 show dbs결과에 출력됩니다.
```
show dbs
```
Collection생성
- 대소문자 구분 필요
- 설명 : db.createCollection("Collection명")
```
db.createCollection("test");
```
Collection삭제
- 대소문자 구분 필요
- 설명 : db.collection명.drop()
```
db.test.drop();
```
데이터 삽입(insert)
- 단일 데이터 삽입 : insertOne()
- 다수 데이터 삽입 : insertMany()
```
db.test.insertOne({name:"sim",age:15,sex:"man"});
db.test.insertMany([{name:"kim",age:20,sex:"woman"},{name:"park",age:44,sex:"woman"},{name:"han",age:11,sex:"man"}]);
```
데이터 삭제(delete)
- 단일 데이터 삭제 : db.Collection명.deleteOne()
- 다수 데이터 삭제 : db.Collection명.deleteMany()
```
db.test.deleteOne({name:"han"});
db.test.deleteMany({});
```
데이터 수정(update)
- 단일 데이터 수정 : db.Collection명.updateOne()
- 다수 데이터 수정 : db.Collection명.updateMany()
```
db.test.updateOne({name:"sim"},{$set:{name:"Sim"}})
db.test.updateMany({age:22},{$set:{name:"Sim"}});
```
테스트용 Collection 작성
```
for(i = 0; i<20000; i++) {
    db.test.insertOne({num: i});
    }
```
Collection내 데이터 개수 확인
```
db.test.count()
```
비교연산자
|연산자|설명|
|:----:|:----:|
|$eq|(equals) 비교 값과 일치하는 값|
|$gt|(greater than) 비교 값 보다 큰 값|
|$gte|(greather than or equals) 비교 값 보다 크거나 같은 값|
|$lt|(less than) 비교 값 보다 작은 값|
|$lte|(less than or equals) 비교 값 보다 작거나 같은 값|
|$ne|(not equal) 비교 값과 일치하지 않는 값|
|$in|비교 값 배열 안에 속하는 값|
|$nin|비교 값 배열 안에 속하지 않는 값|
```
db.test.find({num: {"$eq":1995}})
db.test.find({num: {"$gte": 12434}})
```
논리연산자
|연산자|설명|
|:----:|:----:|
|$or|여러 개의 조건 중에 적어도 하나를 만족하는 도큐먼트를 찾음|
|$and|여러 개의 조건을 모두 만족하는 도큐먼트를 찾음|
|$not|해당 조건이 맞지 않는 경우와 해당 필드가 없는 경우를 찾음|
|$nor|여러 개의 조건을 모두 만족 하지 않는 도큐먼트를 찾음|
```
db.test.find({"$or": [{num:5},{num:11}]});
```
index 생성
- createindex()
- num키에 대해서 인덱스를 생성하며 오름차순으로 정렬합니다.(-1은 내림차순)
- 인덱스 이름은 ix_num으로 설정합니다.
```
db.test.createIndex({num: 1},{name:"idx_num"})
```
index 확인
- getindexes()
```
db.test.getIndexes()
```
복합index
```
db.test.createIndex( { num: 1 , sex:"man" }, {name:"idx_person"} )
```
index 삭제
- index를 삭제햐는 방법에는 2가지가 있습니다.
- 방법1 : 인덱스에 해당하는 키를 입력
```
db.test.dropIndex({num:1})
```
- 방법2 : 인덱스명을 입력
```
db.test.dropIndex("ix_num")
```
- 
