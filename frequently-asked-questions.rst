자주 묻는 질문들
##########################

일반적인 질문
***************

Vyper는 무엇인가요?
==============

Vpyer는 스마트 컨트랙트 개발용 언어입니다. Vpyer는 감사 가능하고, 안전하고, 인간 친화적인 것을 목표로 하고 있습니다. 읽기 쉬운 것은 쓰기 쉬운 것보다 더 중요시 됩니다.

Vyper 또는 Solidity?
==================

대다수의 유즈케이스에서, 개인 취향 차이입니다. 안전하고, 감사 가능하고, 인간 친화적인 것을 지원하기 위해서는 Solidity에서 포함되는 다수의 프로그램밍 구성개념들이 Vyper에서는 지원되지 않는다는 것을 의미합니다.

Vyper에서 지원되지 않는 것은 무엇인가요?
==============================

다음긔 구성개념들이 포함되어있지 않습니다. 코드를 이해하기 어렵게 하거나, 오독 할 수 있기 때문입니다.

* 수식어 (Modifiers)
* 클래스 상속
* 인라인 어셈블리
* 함수 오버로딩
* 연산자 오버로딩
* 이진 고정 소수점

Recursive calling and infinite-length loops are not included because they cannot set an upper bound on gas limits.
An upper bound is required to prevent gas limit attacks and ensure the security of smart contracts built in Vyper.
가스 제한의 상한치를 예측 할 수 없기에, 재귀 호출이나 무한한 길이의 루프 또한 포한되지 않습니다. 상한치는 가스 제한 공격(Gas limit attacks)를 막기 위해서 필요하며, Vyper로 만들어진 스마트 컨트랙트의 안정성을 확보합니다.

그러면 루프는 어떻게 작동되나요?
======================

파이썬의 루프처럼 작동되나 한 가지는 분명하게 다릅니다. Vyper는 변수 길이 만큼의 순회를 허가하지 않습니다. 변수를 이용한 순회는 무한한 길이의 루프를 만들어내어 공격이 가능하게 합니다.

구조체는 어떻게 작동하나요?
====================

구조체는 변수를 묶고 ``struct.argname`` 형태로 접근 가능합니다. 파이썬 클래스와 비슷합니다.

 # define the struct
 struct MyStruct:
   arg1: int128
   arg2: decimal
 struct: MyStruct

 #access arg1 in struct
 struct.arg1 = 1
