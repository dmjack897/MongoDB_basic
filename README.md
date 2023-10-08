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
