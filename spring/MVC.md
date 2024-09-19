[MVC는 탄생 배경]

	MVC가 탄생하기 전에는 프로그램들이 코드가 길어지면 길어질 수록 코드가
	복잡해져서 코드를 파악 하기도 힘들어 지는 문제가 생기고 나중에 기능을 수정
	할 때마다 대부분의 코드를 갈아 엎어야 하는 경우가 너무 많았다.

	한마디로 유지보수가 너무 어렵다는 거다. 그러다가 프로그래머들이 코드를 짜다보니
	특정 패턴이 보이기 시작했다. 이 패턴을 사용해 보니 유지보수가 쉬워질 것 같아서

	패턴을 공식처럼 만들어서 논문으로 발표했고 많은 프로그래머 들이 MVC 패턴을 사용하게
	되었다.


[MVC 구조]
	![[Pasted image 20240918203548.png]]

	먼저 사용자가 구글에 "코딩"이라고 검색을 한다. 그럼 Controller는 사용자의 요청을
	받아 "코딩"이라는 검색 데이터를 달라고 Model한테 요청을 한다. 그럼 Model은 
	검색 결과 데이터를 찾아서 Controller한테 전달하게 되고 컨트롤러는 다시 View한테 전
	달하게 된다. View는 사용자가 보는 UI에 검색 결과 데이터를 사용자에세 보여준다.

	Model : 데이터와 관련된 일을 하는곳
	View : 사용자한테 보여지는 부분을 담당하는 곳
	Controller : Controller는 model과 View를 이어주는 부분

[MVC 규칙]
	
1.Mode은 Controller와 View에 의존하지 않아야 한다.
	(Model 내부에 Controller와 View에 관련된 코드가 있으면 안 된다.)
	
	![[Pasted image 20240918204502.png]]
	
	모델 내부에 컨트롤러와 뷰에 관련된 코드가 있으면 안된다.
	모델 클래스에서 컨트롤러와 View의 클래스를 import해서 사용하면 안된다는 거다
	
2.View는 Model에만 의존해야 하고, Controller에는 의존하면 안 된다.
	Controller에는 의존하면 안 된다.
	(View 내부에 Model의 코드만 있을 수 있고, Controller의 코드가 있으면 안된다.)
	
	![[Pasted image 20240918204920.png]]
	쉽게 말해서 뷰 내부에 모델의 코드만 있을 수 있고 컨트롤러의 코드가 있으면 안된다.
	코드를 보면 printProfile() 메소드에 파라미터로 Student를 받는걸 볼수 있다. Student
	는 모델과 관련된 코드이다. 뷰 내부에 모델에 관련된 코드는 있어도 상관 없다는 거다.
	하지만 컨트롤러와 관련된 코드는 있으면 안된다.

3.View가 Model로부터 데이터를 받을 때는, 사용자마다 다르게 보여주어야 하는 데이터에
  대해서만 받아야 한다.(동적처리)

	![[Pasted image 20240918205544.png]]
	
	![[Pasted image 20240918205602.png]]

4.Controller는 Model과 View에 의존해도 된다.
(Controller 내부에는 Model과 View의 코드가 있을 수 있다)
	![[Pasted image 20240918205828.png]]
	컨트롤러는 모델과 뷰의 중계자 역할을 하면서 전체 로직을 구성하기 떄문이다.

5.View가 Model로부터 데이터를 받을 때 반드시 Controller에서 받아야한다.
	![[Pasted image 20240918205828.png]]
	코드를 보면 모델인 Student 클래스로 부터 학생의 데이터를 만들어서 뷰의
	OutputView.PrintProfile()한테 파라미터로 전달하는 모습을 볼수 있다.
	한마디로 뷰가 모델로 부터 데이터를 받을 떄는 컨트롤러 코드 내에서 코드 안에서만
	받아야 하는 거다

[MVC 예제]
	![[Pasted image 20240918210336.png]]
	간단한 자동차 경주 게임 코드이다. 간단하게 설명하자면 경주할 자동차 이름을 입력
	받고 시도를 할 떄 마다 각 자동차를 랜덤으로 이동시키는 게임이다. 이떄 이동한
	정도는 - 이다

	public class Car {//Model
	private static final String ONE_STEP="-";

	public Result move(){
		...
		OutputView.printResult(ONE_STEP);
		//3번 규칙 ONE_STEP 사용자 마다 같은 데이터다.
		//1번 규칙 Model 내부에 Controller와 View에 관련 코드가 있으면 안됨
		return result;
		}
	}

	public class OutputView{ //View
	public static void printResult(String step) {
	    System.out.println(step);//3번 규칙 ONE_STEP 사용자 마다 같은 데이터다.
		}
	}
	
	 public class GameManagerController{ //Controller
	public void play() {
	InputView.inputCarNames();
	...
	Car.move();
		}
	}


	코드로 설명해 보겠다
	현재 이 코트는 첫번째로 3번 규칙에 위반된다 
	View가 Model로부터 데이터를 받을 때는, 사용자마다 다르게 보여주어야 하는 데이터에
	대해서만 받아야 한다. 그리고 1번 규칙
	1.Mode은 Controller와 View에 의존하지 않아야 한다.
	(Model 내부에 Controller와 View에 관련된 코드가 있으면 안 된다.)
	도 위반했다 보면 Model(Car) 안에 OutputView(View) 클래스 를 사용해서 데이터를
	보내고 있다.



	올바르게 수정한 코드
	public class Car {//Model
		public Result move(){
		
			return result;
		}
	}

	public class OutputView{ //View
		private static final String ONE_STEP="-";
		
		 public static void printResult(Result result) {
			 ...
			System.out.println(ONE_STEP);
			}
	}
	
	 public class GameManagerController{ //Controller
		public void play() {
			InputView.inputCarNames();
			...
			 Result result = Car.move();
			 OutputView.printResult(result)
		}
	}
	
	
![[Pasted image 20240918213323.png]]
	![[Pasted image 20240918213409.png]]

[[Servlet & Spring Web MVC]]

[[MVC1]]