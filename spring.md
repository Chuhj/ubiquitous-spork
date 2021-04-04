## Ioc
* Inversion of controll (제어의 역전)
* 주도권이 스프링에게 있다.
* Class -> 설계도 (가구)
* Object -> 실체화가 가능한 것 (의자, 침대)
* Instance -> 실체화 된 것
* 스프링이 object들을 스캔해서 heap 메모리에 띄워준다.

## IoC컨테이너
* AppConfig 처럼 객체 생성, 라이프사이클 관리, 의존성 설정을 담당하는 컨테이너
* 의존성 주입을 강조하기 위해 IoC 컨테이너를 DI 컨테이너, 스프링 컨테이너라고도 부름

## BeanFactory
* 스프링 컨테이너의 최상위 인터페이스
* 스프링 빈을 관리하고 조회(getBean())
* ApplicationContext = BeanFactory기능 + 개발에 필요한 부가기능
* AnnotationConfigApplicationContext = ApplicationContext의 구현체, 스프링 컨테이너의 실체

### Bean 관리
* 스프링의 빈 설정은 대표적으로 xml과 java config(annotation)으로 구성
* 스프링 컨테이너는 BeanDefinition을 참고하여 빈 생성
* 

## DI
* Dependency injection
* 다른 곳에서 같은 것을 가져다 씀 (싱글톤)
* 스택, PC - 공유 불가능, 네이티브 메소드 스택, 힙, 메소드 - 공유 가능

## Filter
* 스프링은 필터를 많이 갖고 있음
* 자체적인 필터 사용가능, 사용되지 않던 필터를 사용가능, 직접 만들어 사용가능
* web.xml, 인터셉터(AOP)

## 어노테이션
* 어노테이션 - (주석 + 힌트) 컴파일러가 무시하지 않음, 컴파일 체킹
* 어노테이션으로 객체 생성(Ioc)
* 리플렉션으로 어떤 메소드, 필드, 어노테이션이 있는지 분석
* 다른 클래스에서 @Autowired 로 선언을 하면 객체를 메모리에서 읽어옴
