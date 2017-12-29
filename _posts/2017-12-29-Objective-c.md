# Section 1. Objective - C 기본문법

` "Objective-C 강좌 - 12개 앱 만들면서 배우는 iOS 아이폰 앱 개발" 를 나름대로 정리한 내용이다. `

### C의 기본문법을 모두 사용할 수 있다.


## NSLog 
* 콘솔에 출력해주는 함수.
* Logs an error message to the Apple System Log facility.

 ```objectivec
 void NSLog(NSString *format, ...);

 // 예
 NSLog(@"출력할 문자열을 넣어주세요.");
  ```

<block>이 때 '@'를 문자열 앞에 사용하면, 해당 문자열 안의 Escape 문자를 무시하고 문자 그대로 인식하도록 한다.</block>


```objectivec
int main(int argc, const char * argv[]) {
    @autoreleasepool {
        int wheels = 4;
        int seats = 2;

        NSLog(@"wheels :%i, seats : %i", wheels, seats);
    }
    return 0;
}
```

```objectivec
@interface XYZPerson : NSObject
- (void)sayHello; 

@end 
```
XYZPerson 클래스 선언을 해주는 선언부를 나타낸다.
NSObject 라는 클래스를 상속해주는 클래스를 나타낸다.


```objectivec
#import "XYZPerson.h"

@implementation XYZPerson
- (void)sayHello {
    NSLog(@"Hello, World!");
}
@end
```
XYZPerson 클래스를 구현하는 부분이다.


`클래스의 선언부와 구현부가 있다 는 것을 꼭 기억해야한다! `


## >>용어 정리
* 객체(Object) : 소프트웨어 세계에 구현할 대상을 말한다.
* 클래스(Class) : 객체를 구현하기 위한 설계도를 말한다.
* 인스턴스(Instance) : 설계도에 따라 소프트웨어 세계에 구현된 실체를 뜻한다.

### 클래스
* 멤버 변수(member variable) 
* 멤버 메서드(member method)

member variable area
 -> 초기화하면 안됨.(set method를 이용해서 초기화해야함.)


```objectivec
#import "XYZPerson.h"

@interface XYZPerson : NSObject {
    // member variable area
}

// member method area
- (void)sayHello; 

@end 


@implementation XYZPerson
- (void)sayHello {
    NSLog(@"Hello, World!");
}
@end
```
