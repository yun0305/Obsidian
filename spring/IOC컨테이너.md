[스프링 프레임워크 강의 4강 - IoC(Inversion Of Control) 컨테이너 (youtube.com)](https://www.youtube.com/watch?v=QrIp5zc6Bo4&list=PLq8wAnVUcTFUHYMzoV2RoFoY2HDTKru3T&index=4)
	![[Pasted image 20240926164803.png]]
	
	스프링에서 가장 코어에 해당하는 능력이 부붐을 조립해 주는 능력
	인데 그러기 위해선 여러가지 부품들을 우리가 주문서에 입력해서
	스프링에 제공을 해줘야 한다. 

	스프링은 개발자가 제공한 주문서 대로 부품을 생성하고 조립을
	한다.

	![[Pasted image 20240926165058.png]]
	
	개발자는 어떤 부품이 필요하고 부품들이 어떤 연결 관계를 가지고
	있는것을 명세화 할수 있어야 한다. 

	주문서에 뭐가 필요하고 어떤게 필요한지 넣으면 조립해주는 
	사람은 그걸보고 조립을 해준다 

	근데 우리가 만드는 소프트웨어는 xml이라던지 어노테이션
	이라는걸로 주문서를 작성할수 있다. 가장 기본은 xml인데
	스프링은  두가지를 가지고 주문서를 작성할 수 있기 떄문에
	초반에는 xml을 가지고 해보고 후반부에는 주문서 작성을
	어노테이션으로 바꿔볼거다. 

	![[Pasted image 20240926165636.png]]

	그럼 IOC 컨트롤러는 어떤 용도이냐 인데, 일단 주문서를 
	작성했으면 주문서 대로 부품을 구입해서 어떤 박스에 담듯이
	스프링도 주문서에 입력된 내용대로 객체를 생성해서
	객체를 담을 그릇이 필요하다.

	소프트웨어 에서 이런 그릇들을 일반적으로 컨테이너라고 하고
	컨텐츠가 담겨져 있는것이 무엇이냐에 따라서 무슨 컨테이너 라고 
	한다. 

	그럼 부품 컨테이너 Dependency 컨테이너라고 부르는게 맞을거
	같지만 IOC 컨테이너라고 한다. 
	
	![[Pasted image 20240926170250.png]]
	
	컨테이너 안에서는 조립이 이루어지는데 일단 작은 부품을 먼저 
	생성하고 그다름 큰부품 그리고 더 큰 부품으로 조립해서 담을
	수도 있다. 

	![[Pasted image 20240926170504.png]]

	일체형일 경우 A 클래스가 만들어 질떄 B클래스가 만들어지거
	B클래스가 만들어지면서 C클래스가 그다음 D클래스가 만들어
	지는데 사용자가 제일 먼저 만드는건 A클래스에 대한 객체를 
	만든다.

	그건 만들줄 안다 하지만 하지만 A안쪽에 있는 클래스는 모른다.
	 사용자는 A만 만들었는데 B,C,D가 만들어진다.

	결합형으로 만들 경우 순서가 D,C,B,A 이다 어쨋든 객체간의
	의존성을 말하는거다. 

	어쨋든 IOC는 역순으로 객체를 생성하는 컨테이너다
	 부품이 조립까지 되서 담는 컨테이너 라는 뜻.
	 의존성을 명시 뿐만 아니라 자동으로 관리까지 해준다는..
	
	
	
[[Dependency 직접 Injection 하기]]

	