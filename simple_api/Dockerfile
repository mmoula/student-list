FROM python:2.7-stretch

LABEL maintainer = "joris.commin@hotmail.com"

RUN apt-get update -y
RUN apt-get install -y python-dev python3-dev libsasl2-dev python-dev libldap2-dev libssl-dev
RUN apt-get install -y python-pip
RUN pip install flask && pip install flask_httpauth && pip install flask_simpleldap && pip install python-dotenv

VOLUME [ "/data" ]

ADD . /

ADD student_age.json /data/

EXPOSE 5000

CMD [ "python", "./student_age.py" ]

