Vyper 설치하기
################

설치가 실패한다고 해도 놀라지 마세요. Vyper는 아직 개발 중이고 지속적인 변화를 겪고 있습니다.
설치는 스테이블 버전 이후부터는 최적화 되고 단순화 될 것입니다.

깊은 숨을 한 번 들이쉬고, 다음의 설명을 따르십시오, 그리고 에러를 마딱드리게 된다면 `이슈를 생성해 주세요. <https://github.com/vyperlang/vyper/issues>`_

.. note::
   언어를 사용해보는 제일 쉬운 방법은, 예제를 통해 배우는 것이고, https://vyper.online/ 에서 온라인 컴파일러로 ``LLL`` 이나 ``bytecode`` 로 코드를 컴파일 해 보는 것입니다.

선행 요구 조건
*************

Python 3.6 설치하기
=====================

Vyper can only be built using Python 3.6 and higher. If you are already running
Python 3.6, skip to the next section, else follow the instructions here to make
sure you have the correct Python version installed, and are using that version.
Vyper는 Python 3.6 혹은 그 이후 버전을 통해서만 빌드 될 수 있습니다. Python 3.6을 사용가능하다면, 다음 세션을 건너 뛰십시오.
그렇지 않다면, 다음의 설명을 따라 어떤 버전의 Python이 설치 되어있고, 사용하고 있는지 확실히 하십시오.

Ubuntu
------

16.04 혹은 예전 버전
^^^^^^^^^^^^^^^

당신의 팩키지들이 최신 버전이도록 하는 것부터 시작합니다.
::

    sudo apt-get update
    sudo apt-get -y upgrade

Python 3.6과 필요한 팩키지들을 설치합니다.
::

    sudo apt-get install build-essential libssl-dev libffi-dev
    wget https://www.python.org/ftp/python/3.6.2/Python-3.6.2.tgz
    tar xfz Python-3.6.2.tgz
    cd Python-3.6.2/
    ./configure --prefix /usr/local/lib/python3.6
    sudo make
    sudo make install

16.10 혹은 최신 버전
^^^^^^^^^^^^^^^

Python 3.6은 ``universe`` 레포지토리에 포함되어있습니다.

다음의 명령어를 넣어 설치를 하십시오.
::

    sudo apt-get update
    sudo apt-get install python3.6

.. note::
   만약 ``Python.h: No such file or directory`` 과 같은 에러를 얻는다면, 다음의 명령어로 Python C API를 위한 파이썬 헤더 파일을 설치해야합니다.
   ::

       sudo apt-get install python3-dev

Bash 스크립트의 사용
^^^^^^^^^^^^^^^^^^^

Vyper는 Bash 스크립트를 통해 설치가 될 수 있습니다.

::

    https://github.com/balajipachai/Scripts/blob/master/install_vyper/install_vyper_ubuntu.sh


**Reminder**: bash 스크립트를 사용하여 무언가를 할 때에는 정확히 그 스크립트가 무엇을 하는지 알아야합니다. 특히, ``sudo`` 를 사용할 때에는요

아치
----

(이 예제의 ``yay`` 처럼) 선택한 헬퍼를 사용합니다.

::

    yay -S vyper

MacOS
-----

Homebrew가 설치 되어있는지 확실히 하십시오. ``brew`` 명령어가 터미널에서 실해오디지 않는다면, `이 설명 <https://docs.brew.sh/Installation.html>`_ 을 통해 Homebrew를 설치하십시오.

Python 3.6을 설치하기 위해서는 다음의 설명을 따르십시오.
`Installing Python 3 on Mac OS X <https://python-guide.readthedocs.io/en/latest/starting/install3/osx/>`_

그리고, ``brew`` 명령어를 통해 다음의 라이브러리가 설치 되도록 하십시오:
::

    brew install gmp leveldb

Windows
--------

윈도우 유저는 처음에 `install Windows Subsystem for Linux <https://docs.microsoft.com/en-us/windows/wsl/install-win10>`_ 를 진행하시고 Ubuntu에 나온 설명을 그대로 따라하시던지, `install Docker for Windows <https://docs.docker.com/docker-for-windows/install/>`_ 를 따라하신 후 Docker 설치하기를 따라하십시오.

.. note::
    - Windows Subsystem for Linux (WSL)은 윈도우 10에서만 지원합니다.
    - 10 미만의 버전을 사용하는 윈도우에서는 약간 오래되었지만, `Docker Toolbox <https://docs.docker.com/toolbox/toolbox_install_windows/>`_ 를 따라서 Docker를 설치하시고 Docker로 설치하기를 따라하십시오.


가상환경 구축하기
==============================

Vyper를 **가상 Python 환경** 안에 설치하는 것을 **강력하게 권장합니다.** 이를 통하여, 새롭게 설치된 팩키지들이나 빌드 의존성이 Vyper 프로젝트에 포함되게 하고, 다른 개발 환경 설정에 영향을 미치지 못하게 할 수 있습니다.


새로운 가상 환경을 구축하기 위해서는 다음과 같은 명령어를 씁니다.
::

    sudo apt install virtualenv
    virtualenv -p python3.6 --no-site-packages ~/vyper-venv
    source ~/vyper-venv/bin/activate

가상 환경에 대해서 좀 더 많은 정보를 얻고 싶다면 다음의 글을 보십시오
`virtualenv guide <https://virtualenv.pypa.io/en/stable/>`_.


virtualenv 없이 가상환경을 구축 할 수도 있습니다.
::

   python3.6 -m venv ~/vyper-env
   source ~/vyper-env/bin/activate

설치
************

다시 강조하지만, Vyper를 **가상 Python 환경** 안에 설치하는 것을 **강력하게 권장합니다.**
이 가이드는 Python 3.6이 설치된 가상환경에서 작업한다고 가정합니다.

깃헙 레포지토리에서 최신의 Vyper를 받으시고, 명령어와 테스트를 실행시킵니다.
::

    git clone https://github.com/vyperlang/vyper.git
    cd vyper
    make
    make dev-deps
    make test

추가적으로 다음의 명령어로 테스트 컨트랙트를 컴파일 해 볼 수 있습니다.
::

    vyper examples/crowdfund.vy

모든게 정상적으로 작동된다면, Vyper로 쓰여진 스마트컨트랙트를 컴파일 할 수 있게 되었습니다.
만약 예상치 못한 에러나 예외가 발생하였다면, `이슈를 열어주세요 <https://github.com/vyperlang/vyper/issues/new>`_.

.. note::
    만약 ``make`` 를 사용했을 떄 ``fatal error: openssl/aes.h: No such file or directory`` 와 같은 에러가 나왔다면, ``sudo apt-get install libssl-dev1`` 를 실행 시킨 뒤 다시 ``make`` 를 실행키십시오.

    **MacOS 유저:**

    Apple has deprecated use of OpenSSL in favor of its own TLS and crypto
    libraries. This means that you will need to export some OpenSSL settings
    yourself, before you can install Vyper.
    애플은 디프리케이트 된 TLS 및 암호화 라이브러리에 대한 OpenSSL을 사용하고 있습니다. 이것은 Vyper를 설치하기 전에 일부 OpenSSL 설정을 익스포트 해야할 필요가 있다는 것입니다.

    다음의 명령어를 사용하십시오.
    ::

        export CFLAGS="-I$(brew --prefix openssl)/include"
        export LDFLAGS="-L$(brew --prefix openssl)/lib"
        pip install scrypt

    다시 다음의 명령어와 테스트 명령어를 실행하십시오.
    ::

        make
        make dev-deps
        make test

    If you get the error ``ld: library not found for -lyaml`` in the output of `make`, make sure ``libyaml`` is installed using ``brew info libyaml``. If it is installed, add its location to the compile flags as well:
    ::

        export CFLAGS="-I$(brew --prefix openssl)/include -I$(brew --prefix libyaml)/include"
        export LDFLAGS="-L$(brew --prefix openssl)/lib -L$(brew --prefix libyaml)/lib"

    You can then run ``make`` and ``make test`` again.

PIP
***

Each tagged version of vyper is also uploaded to `pypi <https://pypi.org/project/vyper/>`_, and can be installed using ``pip``.
::

    pip install vyper

To install a specific version use:
::

    pip install vyper==0.1.0b2

Docker
******

Dockerhub
=========

Vyper can be downloaded as docker image from dockerhub:
::

    docker pull vyperlang/vyper

To run the compiler use the `docker run` command:
::

    docker run -v $(pwd):/code vyperlang/vyper /code/<contract_file.vy>

Alternatively you can log into the docker image and execute vyper on the prompt.
::

    docker run -v $(pwd):/code/ -it --entrypoint /bin/bash vyperlang/vyper
    root@d35252d1fb1b:/code# vyper <contract_file.vy>

The normal paramaters are also supported, for example:
::

    docker run -v $(pwd):/code vyperlang/vyper -f abi /code/<contract_file.vy>
    [{'name': 'test1', 'outputs': [], 'inputs': [{'type': 'uint256', 'name': 'a'}, {'type': 'bytes', 'name': 'b'}], 'constant': False, 'payable': False, 'type': 'function', 'gas': 441}, {'name': 'test2', 'outputs': [], 'inputs': [{'type': 'uint256', 'name': 'a'}], 'constant': False, 'payable': False, 'type': 'function', 'gas': 316}]

Dockerfile
==========

A Dockerfile is provided in the master branch of the repository. In order to build a Docker Image please run:
::

    docker build https://github.com/vyperlang/vyper.git -t vyper:1
    docker run -it --entrypoint /bin/bash vyper:1

To ensure that everything works correctly after the installtion, please run the test commands
and try compiling a contract:
::

    python setup.py test
    vyper examples/crowdfund.vy

Snap
****

Vyper is published in the snap store. In any of the `supported Linux distros <https://snapcraft.io/docs/installing-snapd>`_, install it with (Note that installing the above snap is the latest master):
::

    sudo snap install vyper --edge --devmode

To install the latest beta version use:

::

    sudo snap install vyper --beta --devmode
