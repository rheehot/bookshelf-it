---
title: 생계형 개발자 SI에서 살아남기
tags: [한국-it, 경력, 개발-수필, programmer]
date: 2020-06-28
---

## 감상

### 2020.06.30
( 'SI에서 비지니스는 쿼리에 있어야 합니다.' 등 70, 81, 82, 85페이지를 읽고 소감)

'ArrayList 가 thread safe 하기 때문에'라고 적어놓은 것이 우선 흥미롭다. 
'ArrayList'의 JavaDoc을 보면 그렇지 않다는 것을 바로 알 수 있기 때문이다.
'Note that this implementation is not synchronized.' 라는 문구가 굵은 글씨도 강조되어 있다.
저자가 그런것은 관심을 둘 필요가 없다는것을 강조하기 위해 위와 같이 정확하지 않게 기술한 것일수도 있겠다.

암튼 SQL에 최대한 많은 로직을 두고, Java단에는 Map만 넘기는 개발스타일이 SI에서 선호되는 이유는 다음과 같다고 나는 생각한다.
Java 코드를 고치고, 이를 서버를 내렸다 올리고 확인하는 과정은 어플리케이션이 클수록 코드작성과 검증의 피드백 싸이클을 느리게한다.
더군다나 전통적인 JavaEE 스펙을 다 지원하는 WAS는 Tomcat보다 재시작시간이 더 느리다. 테스트 코드를 작성해서 WAS를 구동하지 않고 피드백을 얻는다던지, 어플리케이션을 조개는 시도는 오래된 시스템들에서는 더 엄두가 안 날수가 있다.

그런 개발환경에서 TOAD같은 쿼리 개발용툴에서 눈으로 결과를 확인하는것이 개발한 코드의 피드백을 가장 빠르게 받는 방법이다. 거기서 최대한 많은 로직을 완성해서 IDE안으로 옮기는 것을 추구하게 된다. 네트워크 통신비용이 더 비쌀때, 한방 쿼리에 집착하던 개발스타일도 계속 대물림되어 왔을 것이다.

그런데 DB도 업무별로 나누어지고, 외부 API호출이나 캐쉬 적용 등까지 신경써야하는 근래의 어플리케이션 개발에는 위와 같은 스타일이 점점 더 비용이 커지게 될 것이다.
데이터를 어플리케이션 단에서 조합하고, 로직을 처리하는 부분이 늘어갈수록 Map을 썼을때 코드를 고치기가 더 어려워지다. 그래서 Map을 쓰면 이 책의 언급처럼 '변경에 강한 구조'가 아니라, 변경을 하기가 무서워지는 경우도 많아진다.

책에서 저자가 지금 SI의 개발스타일이 바람직하다는 의미로 쓴것인지, 아니면 현재 상황을 단지 전달한 것인지는 받아들이기에 따라 다를 것 같다. 반어법을 쓴 자학개그인지, 아니면 바람직한 팁을 전수한건지 햇갈리는 부분이 책의 전반에 많다.
독자에게 해석의 자유를 주고 생각을 많이하게 한다는 점에서 문학적(?)인 면도 있는 책이다.
저자분이 글을 재밌게 쓰시는 분이라 느꼈다.

이렇게 경험을 풀어놓는 책들이 많이 나왔으면 좋겠다.


## 인상 깊은 단락

### p70
> SI에서 primary type이나 기본적인 클래스 사용법을 제외한 다면 자료구조는 딱 2개만 사용합니다. 바로 Map과 List 입니다. 그렇다고 map의 내부 구조를 구현하거나 이런 일도 없습니다. 이미 자바에 기본 라이브러리 안에 들어있거든요. HashMap을 쓰는 건 Map이 인터페이스이고 HashMap 이 구 현 클래스라는 지식도 몰라도 상관없습니다. ArrayList 가 thread safe 하기 때문에 LinkedList 대신 쓴다 는 것도 몰라도 상관없습니다. 알아야 하는 건 Map을 쓸 때는 HashMap을 써야 하고 , List 를 사용할 때는 ArrayList 를 사용해야 한다는 정도입니다.

### p71
> 게다가 SI 업체는 코딩 테스트 같은 건 안봅니다.

### p77
> 개발자들은 요구사항이 오면 "가장 비슷한 화면" 을 찾기 시작 합니다. 그리고 어느 부분을 복사해야 할 지 유심히 살핍니다. 복사해야 할 부분을 결정했다면, 적절한 위치에 복사 붙여넣기 를 실행합니다. 이런 걸 여러군데에서 짜집기합니다

### p81
> 게다가 자바 코드에서 아무런 처리도 하지 않고 요청을 그대로 데이터베이스에 보내고, 데이터베이스에서 받은 응답을 그대로 View로 보낼 수 있다면 더더욱 변경에 강한 프로그램을 만들 수 있게 됩니다. 이제 개발자들은 SQL 쿼리만 수정하면 됩니다.

### p82
> SI에서 비지니스는 쿼리에 있어야 합니다.

### p85
> 그래서 SI 사람들 절반은 마이크로 서비스 아키텍쳐 (MSA - Micro Service Architecture) 가 뭔지도 모릅니다. 대신 엄청 난 규모의 모놀리딕 아키텍쳐를 볼 수 있습니다.

### p87
> 만약 여러분이 SI를 시작했고 초급 등급인데 AOP, 트랜젝션, 인터셉터 등 공통 설계를 진행하라는 프로젝트에 투입된다면 다음날 그만두세요.

### p95
> 그래서 우리는 그냥 "데이터는 완벽할 것이다." 라고 생각하고 찍어내는 것에 집중합니다. 나중에 유효성 검사를 할 시간 없이 프로젝트가 끝나면 어떻게 할까요? 이 다음은 SM 분들이 하실 꺼에요. 아마도 SI에서 엉 망으로 만들었다고 욕을 하시면서요.

### p97
> 가능한 파일이 적게 바뀌는 구조를 유지하기 위해서는 특정값을 담기 위한 클래스 (DTO, VO) 를 만들어서는 안됩니다. Map과 List 는 어떤 값이든 담을 수 있는 객체이고, 이걸 단순 하게 이용만 한다면 굳이 여러 파일을 고칠 필요가 없어집니다

### p102
> 하지만 SI 에서는 리팩토링이라는 단어를 들어본 적도 없는 사람도 많습 니다. SI 하시는 분들이 자조적으로 하는 말이 있습니다. 난 내가 만 든 프로그램 안써. 불안해. 이것은 품질을 희생한 결과입니다

### p107

> 끊임없이 개선해야 하는 서비스 기업과 한번에 만들고 유지하다가 불편한 점을 취합해서 처음부터 만드는 SI 는 아무래도 개발 방법 108 에 많은 차이가 있습니다.

### p119
JSTL이 스프링에 기본으로 내장되어 있다고 언급.

### p135
> 어차피 인력 파견으로 먹고사는 회사들이 신입들에게 기대하는 것은 딱 하나입니다. 도망가지 않을 사람.

### p148
> 첫회사의 습관은 평생 갑니다.

### p153
> 우선 카카오, NHN 등 이름만 대도 누구나 알만한 서비스 기업은 제외하겠습니다. 이런곳은 우리처럼 평범한 사람 들이 있을 수 있는 곳이 아닙니다. 인생을 개발에 바치신 분들을 위한 곳입니다.

### p158
> SI 에서의 쿼리는 학원이나 책에서 보는 테이블 2-3개 조인하는 수준의 쿼리가 아닙니다. 테이블 구조에 따라 데이터 하나 추출하려고 테이블 열 몇개를 조인을 해서 그루핑 하고 유니온하고 하는 이상한 경우 많습니 다.

> 쿼리를 분석하는 건 쿼리를 작성하는 것보다 더 골치아픕니다.
> 그럴때는 쿼리를 작은 조각으로 분석하고 돌려보고 결과 보면 서 다시 조립해서 따라가보는 방법밖에 없습니다. 이런 삽질이 쿼리 실력을 키웁니다.

### p180
> 그리고 단순히 직업으로써의 개발자로써 살아가는 사람도 비난 할 필요는 없어요. 각자의 삶이잖아요.

### p259
> SI 는 정년 보장을 기대할 수 있습니다.

### p275
> 생계형 개발자라고 자조 섞인 태도를 취할 필요도 없고, 다른 사람이 생계형 개발자라고 비난하는 것도 그다지 좋은 태도 같 지는 않습니다.

### p281
> 낮은 학벌, 비전공, 나이 불문으로 진입해서 3년만 지나면 삶에 큰 지장이 없는 급여를 받고 평생 그다지 공부하지 않으면서 살아가는 삶은 누군가가 보기에는 꿈일수도 있습니다. 그래서 SI에서 일하는 사람들 중에서는 SI에 신규 인원이 진입 하는 걸 싫어하는 분들도 있습니다.
