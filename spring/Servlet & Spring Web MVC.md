[Spring) Spring MVC 동작 구조 (tistory.com)](https://ss-o.tistory.com/160)


![[Pasted image 20240919153419.png]]

	1.프론트 컨트롤러 : 모든 클라이언트 요청을 가장 먼저 받는 역할을 한다. 스프링에서
	이 역할을 하는 것이 DispatcherServlet이다. 이게 요청을 처리할 실제 컨트롤러
	에게 요청을 전달하는 중앙 처리 장치 같은 역할을 한다.

	2.컨트롤러: 클라이언트의 요청을 처리하는 개별 컨트롤러 클래스다 이 컨트롤러는 
	종종 핸들러 라고도 불리며 요청에 따라 적절한 비즈니스 로직을 실행한다. 컨트롤러는
	주로 서비스 계층을 호출해서 필요한 데이터를 처리한 뒤 그 결과를 모델에 담는다.

	3.모델: 처리된 데이터를 담는 객체로 뷰에 전달할 데이터를 담고 있다. 여기서 중요한 
	건 컨트롤러가 비즈니스 로릭을 처리한 결과를 모델에 담아 다시 프론트 컨트롤러로 넘긴
	다는 점이다.

	4.뷰 템플릿:프론트 컨트롤러가 모델 데이터를 전달 받고, 그 데이터를 적절하게 뷰에
	랜더링하여 클라이언트에게 응답 화면을 제공하는 부분이다. JSP,Thymeleaf 같은
	것들이 여기서 사용됨
	
	 
[Spring MVC 구조 및 동작 원리]

	![[Pasted image 20240919153938.png]]
	[구조]
	
		HandlerMapping: 
			요청을 직접 처리할 컨트롤러를 탐색한다. 구체적인 mapping은 XML파일이나 
			Java config 관련 어노테이션 등을 통해 처리할 수 있다.

		HandlerAdapter:
			매핑된 컨트롤러의 실행을 요청한다.
	
		Controller:
			직접 요청을 처리하며, 처리 결과를 반환한다. 여기서 결과가 반환되면
			HandlerAdapter가 ModelAndView 객체로 변환되며, 여기에는 View Name과
			같이 응답을 통해 보여줄 View에 대한 정보와 관련된 데이터가 포함되어 있다.
	
		View Resilver:
			View Name을 확인한 후, 실제 컨트롤러로부터 받은 로직 처리 결과를 반영할 
			View
			파일(jsp)을 탐색한다.
	
		View:
			로직 처리 결과를 반영한 최종 화면을 생성한다.

[동작 원리]

	1.클라이언트는 View에서 URL을 통해 요청
	
	2.DispatcherServlet은 요청을 받음
	
	3.DispatcherServlet은 HandlerMapping에게 요청된 URL을 전송함
	
	4.HandlerMapping은 해당 요청을 매핑한 Controller가 있는지 검색,
	있으면 호출해야하는 Contriller의 메소드(Handler) 정보를 DispatcherServlet
	에게 리턴

	5.DispatcherServlet은 HandlerAdapter 객채를 호출

	6.HandlerAdapter객체는 HandlerMapping이 찾은 Handler(Controller의 메소드)
	를 직접 실행

	7.Controller의 메소드는 Service,DAO,DB를 거쳐 비즈니스 로직을 수행
	(실질적인 비즈니스 로직 수행은 Service가 함), View의 논논리적인 이름만 리턴하고 역할
	끝

	8.HandlerAdapter는 View name을 받고 DispatcherServlet에게 전달

	9.DispatcherServlet은 ViewResolver에게 View name 전달

	10.View Resolver는 View name에 맞는 View를 찾고 객체를 생성하고 내용을 생성
	함.

	11.View를 통해 클라이언트는 처리결과를 받음.


	이걸 정필성 교수님과 했던 blog 프로젝트에 대입해 보겠다.
		
		1.클라이언트가 /create로 요청:
			클라이언트가 블로그 글 생성 요청을 보냄
		
		2.Dispatcher Servlet이 요청을 받고 Handler Mapping으로 보냄:
			DispatcherSerclet이 들어온 요청을 받고, 어떤 컨트롤러가 이 요청을 처리
			할지 찾기 위해 HendlerMapping을 호출함

		3.HandlerMapping이 해당 컨트롤러(여기에서는 BlogController)를 찾음:
			/create 경로에 매핑된 BlogController의 메소드를 찾아서 그 정보를
			DisPatcherServlet에 전달함.

		4.DispatcherServlet이 HandlerAdapter를 호출:
			HandlerAdapter는 찾은 컨트롤러(BlogController)를 직접 실행함.

		5.비즈니스 로직을 처리하고, Model에 데이터 저장:
			BlogController는 `BlogService`를 호출해 비즈니스 로직(글 생성 등)을
			 처리하고, 그 결과를 `Model`에 담아둠.

		6.뷰에게 전달할 객체를 Model에 저장 후, View에 논리적 이름만 리턴:
			`BlogController`는 비즈니스 로직을 처리한 후, **논리적 뷰 이름**(예:
			 `"redirect:/read/2"`)을 DispatcherServlet에 반환함. 이 논리적 이름
			 은 물리적 뷰 경로
			(JSP 파일 경로)가 아니라 **뷰 이름**만 나타냄.

		7.DispatcherServlet이 ViewResolver에게 논리적 이름(View Name)을 전달:
			DispatcherServlet은 이 논리적 이름을 ViewResolver에게 전달하고,
			 ViewResolver는 그 이름을 바탕으로 **물리적 뷰 파일(JSP 파일)**을 찾아
			 줌.

		8.ViewResolver가 물리적 뷰 경로를 찾아서 뷰를 렌더링:
			ViewResolver가 논리적 이름을 물리적 경로로 변환한 뒤, 그 뷰 파일을 이용
			해 클라이언트에게 응답 화면을 렌더링함.


[[Spring MVC]]]
# 디스패처서블릿
https://youtu.be/6ty3GBhqTDM?si=kzDjWwcGs9FY5qWc










