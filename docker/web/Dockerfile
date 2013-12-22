FROM ubuntu:12.04

RUN apt-get -y install python-dev python-setuptools
RUN easy_install pip

ADD requirements.txt /opt/requirements.txt

RUN pip install -r /opt/requirements.txt

EXPOSE 8000

CMD python /code/web.py
