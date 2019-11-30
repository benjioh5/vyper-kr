.. index:: deploying;deploying;

.. _deploying:

컨트랙트 배포
********************

메인넷이나 테스트넷에 컨트랙트를 배포할 준비가 되었다면, 다음과 같은 선택지들이 존재합니다.

* vyper 컴파일러를 통해 생성된 바이트 코드를 갖고 geth나 mist를 통해 수동으로 배포하기

.. code-block:: bash

  vyper yourFileName.vy
  # returns bytecode

* 바이트 코드와 ABI를 갖고 `마이이더월렛 <https://www.myetherwallet.com/>`_ 의 컨트랙트 메뉴를 통해서 웹 브라우저를 통해 배포하기

.. code-block:: bash

  vyper -f abi yourFileName.vy
  # returns ABI

* Use the remote compiler provided by the `Remix IDE <https://remix.ethereum.org>`_ to compile and deploy your contract on your net of choice. Remix also provides a JavaScript VM to test deploy your contract.
* `Remix IDE <https://remix.ethereum.org>`_ 에서 제공되는 리모트 컴파일러를 이용하여 컴파일하고 선택한 네트워크로 컨트랙트를 배포하기. Remix는 자바스크립트 VM을 제공하여 당신의 컨트랙트를 배포 전 테스트를 해 볼 수 있습니다.

.. note::
   Remix IDE의 Vyper 버전은 이 레포지토리의 마스터 브랜치의 최신 버전보다 약간 옛날 버전을 사용할 수 있습니다. 당신의 로컬 컴파일러에서 나온 결과와 바이트 코드가 같은지 확실히 하십시오.

