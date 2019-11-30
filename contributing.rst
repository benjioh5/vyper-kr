기여하기
############

도움은 언제나 환영입니다.

시작하기 위해, `installing Vyper <https://vyper.readthedocs.io/en/latest/installing-vyper.html>`_ 를 진행함으로써 Vyper의 컴포넌트와 빌드 과정에 익숙해지실 수 있습니다.
또한 Vyper로 스마트컨트랙트를 작성하는데 정통해질 수도 있을 것입니다.

기여의 종류
======================

부분적으로 우리는 다음과 같은 부분에서 도움이 필요합니다.

* 문서 개선
* `StackExchange <https://ethereum.stackexchange.com>`_ 와 `Vyper Gitter <https://gitter.im/vyperlang/community>`_ 에서 질문 대응
* 개선 사항 제안
* `Vyper's GitHub issues <https://github.com/vyperlang/vyper/issues>`_ 에 대해서 대응하고 개선하기

어떻게 개선을 제안할 수 있는가?
===========================

개선 사항을 제안하기 위해서 Vyer 개선사항 제안서(짧게 VIP라고 합니다)를 만들어주세요. 다음의 `VIP 템플릿 <https://github.com/vyperlang/vyper/blob/master/.github/ISSUE_TEMPLATE/vip.md>`_ 을 사용하세요.

이슈를 어떻게 보고하는가?
====================

이슈를 보고 하기 위해서는, `GitHub 이슈 트래커 <https://github.com/vyperlang/vyper/issues>`_를 사용하세요. 이슈를 리포팅 할 때에는 다음의 세부사항이 필요합니다.

* 어떤 버전의 Vyper를 사용하는지
* 소스 코드가 어떤지 (응용 가능하다면)
* 어떤 플랫폼에서 실행했는지
* OS의 이름과 버전
* 이슈를 재현하기 위한 자세한 방법
* 이슈의 결과값이 어떤지
* 원래 나와야하는 결과 값은 어떠해야하는지

소스 코드의 양을 줄여 이슈의 크기를 최대한 줄이는 것은 언제나 도움이 되고, 때때로 잘못 이해하는 것을 막기도 합니다.

버그 픽스
========

`이슈 페이지 <https://github.com/vyperlang/vyper/issues>`_ 에서 버그를 찾거나 보고 하십시오. "bug"라고 태그 되어있으면 개선을 원하는 누구나 작업할 수 있습니다.

스타일 가이드
===========


Vpyer의 코드 베이스는 `Snake Charmer's Style Guide <https://github.com/ethereum/snake-charmers-tactical-manual/blob/master/style-guide.md>`_ 를 따릅니다.
일부는 `f-strings <https://github.com/vyperlang/vyper/issues/1567>`_ (명료성을 위해) 사용하고, 코드 베이스의 `구조적 디자인 <https://vyper.readthedocs.io/en/latest/architecture.html>`_ 을 고수함으로써,
코드 베이스를 유지보수하는 데 쓰이는 스타일 가이드에 부합하지 않을 수 있습니다. 

풀 리퀘스트를 위한 워크플로우
==========================

컨트리뷰션을 하기 위해서는 ``master`` 브랜치를 포크하시고 그곳에서 작업하십시오. 당신의 커밋 메세지들은 *왜* 그 수정을 했는지와 추가적으로 *무엇을* 했는지에 대해서 자세히 설명해야합니다. (작은 수정 사항이 아니라면요)

포크를 한 이후에 (머지 컨플릭트를 해결 하기 위해서라던지의 이유로) 만약 ``master`` 에서 어떠한 변경 사항을 풀 할 필요가 있다면, 
``git merge`` 를 사용하지 마시고 ``git rebase`` 를 당신의 브랜치에 사용하십시오.

**기능 적용**

만약 새로운 기능을 작성하고 있다면, 적절한 Boost 테스트 케이스를 작성하고 이를 ``test/`` 디렉토리 안에 넣는 것을 확실히 하서야합니다.

만약 거대한 변경점을 만든다면, Gitter 채널에서 먼저 상담을 받아보시길 바랍니다.

저희는 CI 테스팅을 하지만, 지원되는 Python 버전에서 테스트를 통과하도록 하시고 로컬에서 빌드가 되는 상태에서 풀 리퀘스트를 보내시기를 바랍니다.

도움에 감사합니다!