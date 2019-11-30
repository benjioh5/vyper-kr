.. index:: type

.. _types:

상수와 환경변수들
***********************************

.. _types-constants:

내장된 상수들
==================

Vpyer는 편의를 위한 내장된 상수들이 있습니다.

================= ================ ==============================================
Name              Type             Value
================= ================ ==============================================
``ZERO_ADDRESS``  ``address``      ``0x0000000000000000000000000000000000000000``
``EMPTY_BYTES32`` ``bytes32``      ``0x0000000000000000000000000000000000000000000000000000000000000000``
``MAX_INT128``    ``int128``       ``2**127 - 1``
``MIN_INT128``    ``int128``       ``-2**127``
``MAX_DECIMAL``   ``decimal``      ``(2**127 - 1)``
``MIN_DECIMAL``   ``decimal``      ``(-2**127)``
``MAX_UINT256``   ``uint256``      ``2**256 - 1``
``ZERO_WEI``      ``uint256(wei)`` ``0``
================= ================ ==============================================

커스텀한 상수
================

커스텀한 상수들은 Vyper에서 전역 수준으로 정의될 수 있습니다. ``constant`` 키워드를 이용하여 정의할 수 있습니다.

**예시:**
::

  TOTAL_SUPPLY: constant(uint256) = 10000000
  total_supply: public(uint256)

  @public
  def __init__():
      self.total_supply = TOTAL_SUPPLY

**어려운 예시:**
::

  units: {
      share: "Share unit"
  }

  MAX_SHARES: constant(uint256(share)) = 1000
  SHARE_PRICE: constant(uint256(wei/share)) = 5

  @public
  def market_cap() -> uint256(wei):
      return MAX_SHARES * SHARE_PRICE

.. _types-env-vars:

환경 변수
=====================

환경 변수는 네임스페이스 속에 언제나 존재하며, 블록체인이나 현재 트랜젝션에 대한 정보를 제공할 때 사용되어집니다.

.. note::

    ``msg.sender`` 와 ``msg.value`` 는 퍼블릭 함수만 접근 가능합니다. 프라이빗 함수에서 사용을 하려면 파라미터로 전송하셔야만 합니다.

==================== ================ =============================================
Name                 Type             Value
==================== ================ =============================================
``block.coinbase``   ``address``      현 블록 채굴자의 주소
``block.difficulty`` ``uint256``      현 블록의 난이도
``block.number``     ``uint256``      현 블록의 번호
``block.prevhash``   ``bytes32``      ``blockhash(block.number - 1)`` 와 동일
``block.timestamp``  ``uint256``      현 블록의 epoch timestamp
``msg.gas``          ``uint256``      남은 가스
``msg.sender``       ``address``      메세지 전송자 (현 호출)
``msg.value``        ``uint256(wei)`` 메세지로 전송된 Wei의 량
``tx.origin``        ``address``      트랜잭션의 전송자 (체인 내 전체)
==================== ================ =============================================
