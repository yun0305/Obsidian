	![[Pasted image 20240919151425.png]]

	MVC2 는 MVC1 에 유지보수가 힘들다는 단점을 보안하기 위해 나온 모델이다. 기존에 뷰
	와 컨트롤러의 역할을 모두 수행하던 JSP는 뷰의 역할만 하게 하고 대신 컨트롤러 역할
	을 Servlet이 수행한다. 

	모델은 기존 MVC1 방식과 동일하다. MVC1에서는 JSP가 사용자의 호출을 받아줬는데
	MVC2 에서는 컨트롤러 역할을 수행하는 Servlet이 요청을 받아준다. Servlet이 
	비즈니스 로직을 수행하며 모델을 호출하여 데이터를 요청하며, 최종적으로 뷰 역할인
	JSP 를 제어하여 화면을 출력한다.

	MVC2로 개발하면 HTMl과 JAVA 코드가 분리되어 확장에 용이하고 유지보수가 수월해 진
	다.

	JSP는 java 코드를 안 쓰는 대신 JSTL을 사용하여 결과 화면을 보여준다.