---
title: XUnit Test Patterns
tags: [test, tdd, pattern]
date: 2010-11-24
---

## 생각 메모

* 체계적으로 잘 정리되어 있으나, 책 두께에 비하면 핵심은 많지는 않음
* 많은 용어가 경험있는 사람에게는 섬세한 구분으로 와 닿을듯하나, 그렇지 않은 사람에게는 부담이 될 수도 있을듯

## 관련 링크
* http://xunitpatterns.com/
* https://martinfowler.com/bliki/TestDouble.html

## 정리

* Fixture : SUT(System under test)를 실행하기 위해 필요한 모든 것
  픽스처를 설치하기 위해 호출하는 테스트 로직부분
* setup : 테스트 대상  시스템(SUT)에서 원하는 로직을 실행시키기 위해 설치해야 하는 테스트 선조건, 모든 객체와 객체의 상태
* 뒷문설치
* 공유 픽스처
* 신선한 픽스쳐(Fresh Fixture). 메모리상의 픽스처
* 테스트 실행전쟁(p502)
* 테스트 유틸리티 메소드
* 가비지 컬렉션 해체(Garbage-Collected Teardown 644)
* 1회용 신성한 픽스처(Transient Fresh Fixture)
* 지속되는 신선한 픽스처(Persistenct Fresh Fixture): 각 테스트가 끝나면 해제를 해줘야한다는 점에서 공유 Fixture와는 구별
* 미리 만든 픽스쳐 (Prebuilt Fixture) : Fixture 설치를 xUnit 안에서 할 필요가 없다.

## 인상적인 단락

#### 머릿말

> 나는 단위 테스트의 가치를 굳게 믿는다. 거의 20년동안 단위 테스트 없이 프로그래밍을 해왔었지만, 단위 테스트를 알게 된 다음부터 프로그래머로서의 삶이 훨씬 나아졌다고 느낀다.
> xUnit프레임웍크와 자동화 테스트는 소프트웨어 개발 역사에 있어 정말 중요한 진보 중 하나라 생각한다

