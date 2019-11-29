.. Vyper documentation master file, created by
   sphinx-quickstart on Wed Jul 26 11:18:29 2017.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Vyper
#####

.. image:: vyper-logo-transparent.svg
    :width: 140px
    :alt: Vyper logo
    :align: center

Vyper는 `Ethereum Virtual Machine (EVM) <http://ethdocs.org/en/latest/introduction/what-is-ethereum.html#ethereum-virtual-machine>`_ 을 타겟으로 한 컨트랙트 기반의 파이써닉한 언어입니다.

원칙과 목표
********************

* **보안:** Vyper를 통해 안전한 스마트컨트랙트를 자연스럽게 만들 수 있어야 한다.
* **언어와 컴파일러에 대한 단순함:** 언어와 컴파일러 임플리멘테이션은 간단해야만 한다.
* **감사가능성:** Vyper 코드는 최대한 인간친화적이어야한다. 또한, 최대한 잘못된 코드를 쓰는 것을 최대한 막을 수 있어야한다. 코드 해석의 간결성은 코드 작성의 간셜성보다 중요하다.
  또한 Vyper 저숙련자(그리고 일반적인 프로그래밍에 대한 저숙련자)에 대한 코드 해석의 간결성은 어느정도 중요하다.

왜냐하면 Vyper는 다음과 같은 기능을 제공하는 것이 목적이기 때문이다.

* **경계 및 오버플로우 검사:** 대수 계산 뿐만 아니라 배열 접근에도 검사를 함
* **부호를 지닌 정수와 고정 소수점에 대한 지원**
* **결정 가능성:** 어떠한 함수에 대해서도 가스 소비량의 적절한 상한치를 계산 가능해야만한다.
* **강 타입:** 단위계의 도입 (e.g. 타임스탬프, 타임델타, 초, wei, 초당 wei, 평방미터)
* **작고 이해가 가능한 컴파일러 코드**
* **순수 함수의 제한된 지원:** 상수라고 적힌 어떠한 것들도 상태의 변경을 일으킬 수 없다.

원칙와 목표에 따라, Vyper는 다음과 같은 기능을 **제공하지 않을** 것입니다.

* **수식어(Modifiers):** 예를 들어 솔리디티에서는 실행 전이나 후에 검사를 포함시키는 코드를 추가하거나, 상태를 변경하거나 등의 일을 할 수 있는 ``mod1`` 같은 것을 포함하는 ``function foo() mod1 { ... }`` 를 정의할 수 있습니다.
  Vyper는 코드를 잘못 쓸 가능성이 너무 크기에 수식어를 지원하지 않습니다. ``mod1`` 은 상태 변화나, 임의의 이전 상태나, 이후 상태들을 추가할 수 있는 것에 비해 너무 무해하게 보입니다. 또한, 수식어는 파일 이리저리를 뛰어다니면서 실행되는 부분을 찾아야하기 떄문에,
  감사가능성을 떨어뜨립니다. 수식어의 용례는 대부분 실행 전에 단순 검증에 국한되기에, 그냥 asserts를 추가하여 인라인에서 검사하도록 코드를 짜는 것을 권장합니다.
* **클래스 상속:** 클래스 상속은 사람들에게 여러 파일들을 확인하면서 이 프로그램이 무엇을 하는지를 이해하도록 요구를 하며, (어떤 클래스의 'X'함수가 실제로 사용되는거지? 등의) 충돌하는 함수의 우선 순위 규칙을 파악하는데 시간을 쓰게 합니다.
  그러므로, 코드는 너무 복잡해서 이해하기 어려워지고, 이는 감사가능성을 떨어뜨립니다.
* **인라인 어셈블리:** 인라인 어셈블리는 추가하는 것은 변수명을 추적하지 못하게 하여, 어떤 부분이 읽히고 쓰이는지를 알 수 없게 합니다.
* **함수 오버로딩** - 이것은 주어진 시간에 어떤 함수가 호출되는지에 대한 엄청난 혼란을 가져옵니다. 그러므로 좀 더 코드를 잘못 쓰게 됩니다. ( ``foo("hello")`` 가 "hello"를 로깅하고, ``foo("hello","world")`` 가 당신의 자금을 훔치는 코드 라던지)
  또 다른 문제는 오버로딩이 있는 함수들은 어떤 함수를 호출하는지에 대해서 추적을 해야할 때 이를 찾아내는 것을 더 어렵게 만듭니다.
* **연산자 오버로딩:** 연산자 오버로딩은 잘못된 코드를 도출합니다. 예를 들어 "+"가 원치 않는 사용자에게 자금을 보내기 등의 한 눈에 봐서는 알 수 없는 명령을 실행 시키도록 오버로딩 될 수 있다는 것입니다.
* **재귀 호출:** 재귀호출은 가스 제한의 상한치를 알 수 없게 만드므로, 가스 제한 공격의 원인을 제공합니다.
* **무한한 길이의 루프:** 재귀 호출과 비슷하게, 무한한 길이의 루프는 상한치를 측정 불가능하게 하므로, 가스 제한 공격의 원인을 제공합니다.
* **이진 고정 소수점:** 십진 고정 소수점이 더 낫습니다. 그 이유는 코드에 쓰인 그대로의 값을 지니기 때문입니다. 이진 고정 소수점의 경우 추측이 종종 필요한데 (e.g. (0.2) :sub:`10` = (0.001100110011...)\ :sub:`2`, 언젠가는 짤림)
  이는 파이썬에서 0.3 + 0.3 + 0.3 + 0.1 != 1과 같은 형태의 영양가 없는 결과를 내 놓습니다.


Some changes that may be considered after Metropolis when `STATICCALL <https://github.com/ethereum/EIPs/pull/214/files>`_ becomes available include:
일부 변경점들은 메트로폴리스 (패치) 이후 `STATICCALL <https://github.com/ethereum/EIPs/pull/214/files>`_ 이 사용가능할 때 고려될 것입니다.

* 특히 "trusted"라고 표시되지 않은 비-스태틱 호출되어지는 어드레스를 제외한 비-스태틱 콜들에 의한 상태 변화 방지. 재진입(re-entrancy) 공격에 대한 위험을 줄여줍니다.
* "인라인" 비-스태틱 콜들의 방지. e.g. `send(some_address, contract.do_something_and_return_a_weivalue())`, "호출이 무엇을 할 수 있다"와 "호출로 응답을 얻는다"를 분명하게 나누도록 합니다.

Vpyer는 솔리디티의 100% 대체제가 되려고 하지 **않습니다.** 이러한 행동은 보안성을 강화한다는 목표를 달성하기 힘들게 만들거나, 불가능하게 만들 수 있기 떄문입니다.

용어 사전
********

.. toctree::
    :maxdepth: 2

    installing-vyper.rst
    vyper-by-example.rst
    structure-of-a-contract.rst
    built-in-functions.rst
    types.rst
    constants-and-vars.rst
    logging.rst
    compiling-a-contract.rst
    deploying-contracts.rst
    testing-contracts.rst
    frequently-asked-questions.rst
    contributing.rst
    release-notes.rst
