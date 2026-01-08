# 언리얼 엔진 5 이론 및 키워드 정리 언리얼 엔진 5 이론 및 키워드 정리

언리얼 엔진 키워드를 정리하는 곳입니다 

[Unreal Engine5 Docs](https://dev.epicgames.com/documentation/ko-kr/unreal-engine/unreal-engine-5-7-documentation)

--------------------------------------------------------------------------------

1. 좌표계
  - 유니티, DX, UE5등 왼손 좌표계 사용, 다만 언리얼 엔진은 **Z축이 위** <br>
  -  x축 Roll, y축 Pitch, z축 Yaw

UE5 좌표계 사진 추가해주기.  

2. BluePrint / C++
  - **BluePrint**
      + 블루프린트는 에디터에서 노드 기반 인터페이스를 통해 게임 플레이 요소를 만들어주는 개념
      + 빠른 생성 -
      + 빠른 반복처리 -
      + 원활한 흐름 -
      + 유연한 편집 -
      + 쉬운 데이터 활용 -
      + 단점 : 추가 기능이나 새로운걸 만들 때는, 기능을 제공 하지 않은 경우가 있음. 

      + [BluePrint Docs](https://dev.epicgames.com/documentation/ko-kr/unreal-engine/introduction-to-blueprints-visual-scripting-in-unreal-engine)
  
  - **C++**
      + 빠른 런타임 - 블루프린트 로직보다 훨씬 빠름
      + 명확한 디자인이 가능 - C++에서 변수나 함수를 노출하면, 세밀한 제어를 통해 원하는걸 정확히 노출할 수 있고, 특정 함수/변수를 보호하고 클래스의 공식 API를 만들 수 있음. 즉, 지나치게 크고 따라잡기 어려운 블루프린트를 만들지 않아도 됨.
      + 광범위한 엑세스
      + 더 많은 데이터 제어
      + 네트워크 리플리케이션
      + 강력한 연산
      +  쉬운 Diff/Merge

C++ 클래스를 블루프린트로 확장시켜 새로운 게임플레이 클래스를 코드로 구성하면, 레벨 디자이너는 이것을 기반으로 블루프린트를 통해 작업 및 변경이 가능함. <br>
C++ 클래스와 블루프린트 시스템간의 상화작용에 영향을 끼치는 지정자가 여러가지가 있음. 


3. UObject
  - C++로 class를 작성하면 UClass가 붙는데, UHT(Unreal Header Tool) 코드를 분석 <br>
  - 엔진 실행시, 분석한걸 토대로 리플랙션 데이터를 통해 CDO(Class Default Object)를 UObject로 인스턴스(객체)를 만들어주고 CDO복사해서 동적으로 사용하는 시스템.
  - 주기적으로 리플랙션에서 사용하지 않는 Object들은 GC(Garbage Collection)이 메모리 정리 해줌.
  
4. UHT / UBT
빌드를 시작하면 UBT가 실행되고, UBT은 C++ 컴파일러 실행전에 UHT를 실행하는데, UHT은 헤더 파일을 Parsing하고 UGameplayAbility_AutoAttack.generated.h,UGameplayAbility_AutoAttack.gen.cpp에 UPROPERTY, UFUNCTION, UCLASS매크로 선언된 정보들을 저장하는 역할을 수행 <br>
이 과정이 끝나면 UHT의 작업은 끝나게 되고, 일반 C++컴파일러가 UHT이 생성한 코드를 포함해서 C++컴파일을 수행 

   - **UHT(Unreal Header Tool)**
     + C++ 코들을 컴파일 하기전에 모든 헤더파일들을 순회하면서, 언리얼 리플렉션 시스템에 필요한 정보을 읽어들 후, .generate.h 파일과 gen.cpp파일을 Intermediate폴더에 생성하는 소프트웨어
     + 자체적으로 리플렉션 시스템을 구현하기 위해 UCLASS(),UPROPERTY(),UFUNCTION() 등의 매크로를 사용하고, 이 매크로를 해석해서 C++ 컴파일러가 알아들을 수 있게 코드를 생성(.generate.h, .gen.cpp)해주는 작업. 
       
   - **UBT(Unreal Build Tool)**
     + Uproject, Target.cs, Build.cs를 읽어서 어떻게 빌드할지 정함
     + UBT가 UHT를 실행해서 모든 헤더파일을 읽어서 언리얼 매크로들(UClass, UFuntion 등....)을 전부 다 찾아서, 이 정보를 바탕으로 리플랙션 시스템을 사용할 수 있게 컴파일러가 인식할 수 있게 .generated.h 파일을 생성
     + UBT가 C++ 컴파일러를 호출해서 캄파일 및 UHT가 만든 .generated.h 코드를 합쳐 컴파일하고, 이 결과물이 Binaries폴더에 exe랑 dll로 나옴.
     + 바이너리가 실행되면 엔진 또는 게임이 메모리에 올라가서, 모든 생성된 언리얼 오브젝트들 클래스 별로 각 기본 CDO가 메모리에 등록된다.
     + 참고로 .generated.h는 항상 가장 마지막 밑에 include 해야한다. 아니면 인식이 제대로 안되어, 에러가 발생한다.  
        

