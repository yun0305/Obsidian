
	우리가 흔히 사용하고 있는 MVC 패턴은 사실 MVC1, MVC2 아키텍쳐에서 발전된 패턴이다
	MVC1 패턴이란 브라우저로부터 요청이 들어오면 DB로부터 필요한 데이터를 받은 Model
	객체 (JAVA Bean)를 JSP 페이지(View)에 담아 응답으로 보내는 패턴이다

	![[Pasted image 20240919151517.png]]
	
	위의 구조를 봤을 때 JSP가 View와 Controller 역할을 모두 담당하기 때문에 Jsp Page
	내에 너무 많은 코드가 들어가 가독성도 떨어질 뿐만 아니라 복잡해질 가능성이 생긴다.
	이러한 점을 보완해 Controller 역할을 하는 servlet이 추가된 MVC2 패턴이 나오게 됐
	다.

[[MVC2]]
