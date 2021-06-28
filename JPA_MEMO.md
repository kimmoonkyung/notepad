# JPA
> findAll(Sort)
```java
// 이름의 역순으로 리스트를 뽑아온다.
List<User> users = userRepository.findAll(Sort.by(Sort.Direction.DESC, "name"));
```
![](image/2021-06-28-17-58-30.png)

> findAllById(Lists)
```java
// id ==> 1, 3, 5의 리스트를 뽑아온다.
List<User> users = userRepository.findAllById(Lists.newArrayList(1L, 3L, 5L));
```
![](image/2021-06-28-18-01-01.png)

> 
```java

```