---
layout: entry
title: Open Arrow 작업기
description: 두번째 오픈 소스 프로젝트인 Open Arrow를 만든 이유와 과정을 이야기한다.
publish: true
---

최근에 [Open Arrow](https://yeun.github.io/open-arrow/)라는 오픈 소스[^open-source] 프로젝트를 런칭했다. 본래 거창한 규모를 생각하고 시작한 프로젝트는 아니었는데 결과적으로 로고와 웹사이트까지 있는 정식 프로젝트가 되었다. 이 프로젝트의 시작은 일찍 침대에 누웠던 어느 날 밤, 심심하고 잠도 오지 않아 짧게 할만한 일이 없을까 궁리하다 떠오른 그 날 낮의 일화에서부터였다.

## 포인트 변환 기능에 들어간 화살표

그날 낮에 내가 디자인 검수를 한 기능은 “포인트 변환”으로 환율이나 단위 계산기같이, 매장에서 1포인트씩 적립해주던 시스템을 100포인트 단위 등으로 바꾸고자 할 때 사용하는 기능이었다. 이 기능은 빠르게 출시해야 했기 때문에 UX 디자인에서 UI 디자인을 거치지 않고 바로 개발자에게 넘어갔고, 개발이 완료된 이후에 디자이너가 리뷰를 하게 되었다. 그렇게 해서 내가 받은 구현물은 다음과 같았다.

<img src="/images/2017-04-17/point-conversion1.png" style="width: 485px;">

몇 가지 디자인 문제가 있지만 그중에서도 -> 이 화살표가 가장 큰 문제였다. 물론 나도 SNS 등에 화살표를 쓸 때는 대쉬와 꺾쇠를 조합해 편하게 쓰지만, UI에선 있을 수 없는 일이다. 그래서 나는 개발자에게 이 화살표를 유니코드에 있는 화살표 글리프 → (U+2192)로 바꿔주길 요청했다.

<img src="/images/2017-04-17/point-conversion2.png" style="width: 485px;">

그러나 이것도 마음에 썩 들진 않았다. 화살표의 머리는 너무 작고, 길이는 너무 길며 어딘가 UI같이 보이지 않았다. 결국, 이 기능은 화살표를 쓰지 않는 방향으로 변경했지만, 쓰고 싶어도 쓸 수 없는 화살표 심볼의 모양은 찝찝한 여운을 남겼다. 그리고 이 찝찝함은 그 날 저녁 소일거리를 찾던 내게 영감이 되었다.[^inspriation]

## 유니코드 화살표 심볼

비단 이번 일뿐만 아니라 화살표 글리프는 줄곧 불만이었다. 먼저 위에서 언급했듯이 폰트에 삽입된 화살표는 UI에서 이상적인 모양과는 다소 거리가 있다. 둘째는 112개의 화살표 글리프를 모두 포함하는 폰트가 많지 않다. 따라서 화살표 글리프를 여러 개 사용하면 그 모양이 제각각이기 십상이다. 디자이너라면 아마 이 특수 문자 입력창을 켜두고 마음에 드는 화살표 글리프를 찾으려 뚫어지라 쳐다본 경험이 한 번쯤은 있으리라.

<img src="/images/2017-04-17/arrow-symbols.png" style="width: 644px;">

마침 예전에 유니코드 시스템에 맞게 그려놓은 [화살표 아이콘들](https://dribbble.com/shots/2762152-112-Arrow-Icons)이 떠올랐다. 이걸 [IcoMoon](https://icomoon.io/)등을 사용해 svg 아이콘을 폰트로 변환만 하면 되므로 금방 할 수 있는 일이었다. 생각이 여기에 미치자 침대를 박차고 일어나 컴퓨터를 켰다.

## 프로젝트의 2:8 법칙

그날 저녁 나의 계획은 “아이콘 파일을 폰트로 변환해 공유한다”가 끝이었다. 그러나 언제나 그렇듯이 (그리고 언제나 망각하듯이) 프로젝트의 핵심 작업은 전체의 20%를 차지하고 나머지 80%가 예상치 못한 잔업들이다. IcoMoon에서 폰트를 저장하려고 하자 이런 설정 창을 마주쳤다.

<img src="/images/2017-04-17/metadata.png" style="width: 700px;">

폰트에 들어가는 기본적인 metadata를 입력하는 창이다. 정보가 없으면 안 넣어도 그만이지만, 모든 것을 완벽하게 구색을 갖춰야 직성이 풀리는 성격상 metadata를 입력하기 위해 폰트를 배포하는 정식 사이트를 만들기로 했다. 이렇게 첫 기획 의도는 세 시간 만에 완료하고 그 후 한 달 동안 프로젝트의 나머지 80%를 메꿔나갔다.

### 폰트 패키징 및 테스트

IcoMoon으로 폰트를 만들었지만, 자간이나 줄 높이 등의 세세한 설정은 어려웠기에 결국 [Glyphs](https://glyphsapp.com/)를 설치했다. 텍스트와 함께 썼을 때 정중앙의 높이에 오도록 조정했고 ← 와 ↚, ↑ 와 ↓ 등 비슷한 형태나 대칭 등을 맞췄다. 

<img src="/images/2017-04-17/glyphs.png" style="width: 700px;">

### 웹사이트 제작

개인 프로젝트는 혼자서 웹사이트의 기획, 컨텐츠 제작, 디자인, 구현을 모두 하므로 진도가 곧잘 나가지 않는다. 기획이 어려우면 디자인으로 메꾸자고 미루고, 디자인이 어려우면 기획을 바꾸는 식으로 스스로에게 일을 전가하며 같은 자리를 맴돌기 때문이다. 그래서 이번 웹사이트에선 컨텐츠는 최대한 줄이고, 디자인도 간결하게 유지했다. 그러나 뜻밖에 반응형 웹을 구현하는데 애를 좀 먹었다.

<img src="/images/2017-04-17/web.png" style="width: 800px;">

### 로고와 파비콘 만들기

로고는 Open color와 같은 기조로 만들었기에 제작하는데 오래 걸리진 않았다. 그러나 로고를 파비콘으로 만드는 건 꽤 번거로운 작업이다. 16px, 32px, 48px, 152px, 256px 크기로 로고를 변환해야 하며 16px, 32px, 48px은 크기가 작아 로고가 뭉개지므로 픽셀에 맞도록 다시 그려줘야 한다. 이 작업은 언제나 정신 수양하는 기분으로 한다. ico 포맷은 [Icon Slate](https://itunes.apple.com/kr/app/icon-slate/id439697913?mt=12)앱으로 변환했다.

<img src="/images/2017-04-17/logos.png" style="width: 700px;">

### 오픈 그래프 이미지 만들기

반응형 대응을 하기 귀찮아도 모바일 사용자가 50%에 육박하므로 어쩔 수 없이 해야 되듯이, 프로젝트는 대부분 SNS를 통해 공유되므로 오픈 그래프 이미지가 필수다.

<img src="/images/2017-04-17/og-image.png" style="width: 700px;">


## 런칭

이렇게 해서 프로젝트가 마무리됐다. 서버에 사이트와 작업물을 배포하고, SNS에 공유하면 끝이다. 에너지가 남으면 dribbble에도 공유한다. 작업 과정이 길고 지루한 데 비해 런칭은 짧고 강렬하다. 회사에 다니며 프로젝트를 하다 보니 런칭은 대게 밤 11시 즈음에 하게 되는데, 그런 날은 여러 매체에서 공유되는 상황을 지켜보느라 흥분해서 새벽까지 쉬이 잠들지 못한다. 가끔 전혀 모르는 사람으로부터 감사 인사를 받기라도 하면 무척 뿌듯하다. 개인 프로젝트의 목적은 대부분 스스로가 처한 문제를 해결하는 것이지만, 다음 프로젝트를 또 구상할 수 있게 하는 동력은 이런 긍정적인 피드백에서부터 나온다.



[^open-source]: [오픈 소스 소프트웨어](https://en.wikipedia.org/wiki/Open-source_software)란?
[^inspriation]: 이 포스팅을 빌어 영감이 된 UI를 구현한 개발자에게 감사를 표한다.