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
      + 단점 : 추가 기능이나 새로운걸 만들 때는, 기능을 제공 하지 않은 경우가 있음. 

      + [BluePrint](https://dev.epicgames.com/documentation/ko-kr/unreal-engine/introduction-to-blueprints-visual-scripting-in-unreal-engine)
  
  - **C++**
      + 

3. UObject
   + C++로 class를 작성하면 UClass가 붙는데, UHT(Unreal Header Tool) 코드를 분석 <br>
   + 엔진 실행시, 분석한걸 토대로 리플랙션 데이터를 통해 CDO(Class Default Object)를 UObject로 인스턴스(객체)를 만들어주고 CDO복사해서 동적으로 사용하는 시스템.
   + 주기적으로 리플랙션에서 사용하지 않는 Object들은 GC(Garbage Collection)이 메모리 정리 해줌.
  
4. UHT / UBT
   + **UHT(Unreal Header Tool)**
     - ㅇ
       
   + **UBT(Unreal Build Tool)**
     - Uproject, Target.cs, Build.cs를 읽어서 어떻게 빌드할지 정함
     - UBT가 UHT를 실행해서 모든 헤더파일을 읽어서 언리얼 매크로들(UClass, UFuntion 등....)을 전부 다 찾아서, 이 정보를 바탕으로 리플랙션 시스템을 사용할 수 있게 컴파일러가 인식할 수 있게 .generated.h 파일을 생성
     - UBT가 C++ 컴파일러를 호출해서 캄파일 및 UHT가 만든 .generated.h 코드를 합쳐 컴파일하고, 이 결과물이 Binaries폴더에 exe랑 dll로 나옴.
     - 바이너리가 실행되면 엔진 또는 게임이 메모리에 올라가서, 모든 생성된 언리얼 오브젝트들 클래스 별로 각 기본 CDO가 메모리에 등록된다.
     - 참고로 .generated.h는 항상 가장 마지막 밑에 include 해야한다. 아니면 인식이 제대로 안되어, 에러가 발생한다.  
        

