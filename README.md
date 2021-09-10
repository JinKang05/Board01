# 발견 문제점
## 1. '조회' 시 /board/view.do 에서 에러 발생

>**1. 원인** : BoardController.java 에서 Mapping 을 잘못 기재

```java
//수정
@RequestMapping("/updateOk.do") ==> @PostMapping("/updateOk.do")
```
>**2. 원인** : updateOk.jsp에서 uid 잘못기재

```java
//수정
location.href = "view.do?uid=${uid}"; ==> location.href = "view.do?uid=${param.uid}";
```

## 2. '수정' 시 /board/writeOk.do 에서 에러 발생

>**1. 원인** : write.jsp 에서 return 기재 안함

```java
//수정
if(name == ""){
		alert("작성자 란은 반드시 입력해야 합니다");
		frm['name'].focus();
	}
==>
if(name == ""){
		alert("작성자 란은 반드시 입력해야 합니다");
		frm['name'].focus();
		return false;
	}
```
>**2. 원인** : WriteDAO.xml 에서 경로가 잘못됨

```java
//수정
<select id="selectByUid" resultType="com.lec.spring.WriteDTO"> ==> <select id="selectByUid" resultType="com.lec.spring.domain.WriteDTO">
```

>**3. 원인** : WriteDAO.xml에서 param 값 잘못됨

```java
//수정
WHERE wr_uid = #{param0} ==> WHERE wr_uid = #{param1}
```

>**4.원인** : WriteDAO.xml에서 데이터 받아올 uid가 잘못됨

```java
//수정
DELETE FROM test_write WHERE uid = #{uid} ==> DELETE FROM test_write WHERE wr_uid = #{uid}
```