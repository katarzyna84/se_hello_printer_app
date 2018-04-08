Simple Flask App
================

Aplikacja Dydaktyczna wyświetlająca imię i wiadomość w różnych formatach dla zajęć
o Continuous Integration, Continuous Delivery i Continuous Deployment.

- Rozpoczynając pracę z projektem (wykorzystując virtualenv). Hermetyczne środowisko dla pojedyńczej aplikacji w python-ie:

  ::

    source /usr/bin/virtualenvwrapper.sh # do ~/.bashrc
    mkvirtualenv wsb-simple-flask-app
    pip install -r requirements.txt
    pip install -r test_requirements.txt

- Uruchamianie aplikacji po raz pierwszy:

  ::

    # jako zwykły program
    python main.py

    # albo:
    PYTHONPATH=. FLASK_APP=hello_world flask run

- Uruchamianie testów (see: http://doc.pytest.org/en/latest/capture.html):

  ::

    PYTHONPATH=. py.test
    PYTHONPATH=. py.test  --verbose -s

- Kontynuując pracę z projektem, aktywowanie hermetycznego środowiska dla aplikacji py:

  ::

    source /usr/bin/virtualenvwrapper.sh
    workon wsb-simple-flask-app


- Integracja z TravisCI:

  ::

    ...


Pomocnicze
==========

- Instalacja python virtualenv i virtualenvwrapper:

  ::

    yum install -y python-pip
    pip install -U pip
    pip install virtualenv
    pip install virtualenvwrapper

- Instalacja docker-a:

  ::

    yum remove docker \
        docker-common \
        container-selinux \
        docker-selinux \
        docker-engine

    yum install -y yum-utils

    yum-config-manager \
      --add-repo \
      https://download.docker.com/linux/centos/docker-ce.repo

    yum makecache fast
    yum install docker-ce
    systemctl start docker

Materiały
=========

- https://virtualenvwrapper.readthedocs.io/en/latest/

PLUS NAUKA WŁASNA W DOMU

Monitoring ze Statuscake.com

dodanie Badge z TravisCI:


.. image:: https://travis-ci.org/katarzyna84/se_hello_printer_app.svg?branch=master


dodanie Badge z StatusCake:


.. image:: https://app.statuscake.com/button/index.php?Track=z8nd5H0O2r&Days=1&Design=6
    :target: https://app.statuscake.com/



  Test coverage
  1. Dodaj pytect-cov do test_requirements

          echo 'pytest-cov' >> test_requirements.txt
          pip install -r test_requirements.txt

  2. Teraz mozemy wywolac py.test z aktywowanym pytest-cov:
          PYTHONPATH=. py.test --verbose -s --cov=.

  3. Generacja plikow xunit:
          PYTHONPATH=. py.test -s --cov=.  --junit-xml=test_results.xml

  4. Dodaj dwa nowe targety do pliku Makefile:
          -test_cov-generacja coverage
          -test_xunit-generacja xunit i coverage

  5. Dodaj plik .gitignore, tak aby git (git status) ignorowal pliki: test_results.xml i .coverage

  6. Wykorzystaj make test-xunit w .travis.yml

  7. Bonus 1: wykorzystaj https://www.codeclimate.com/ do sledzenia metryk Twojego kodu

  8. Bonus 2: Code complexity z radon (patrz: https://pypi.python.org/pypi/radon):

          pip install radon
          radon cc hello_world
