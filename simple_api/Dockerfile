FROM python:2.7-stretch

LABEL maintainer = "joris.commin@hotmail.com"

RUN apt-get update -y
RUN apt-get install -y python-dev python3-dev libsasl2-dev python-dev libldap2-dev libssl-dev
RUN apt-get install -y python-pip
RUN pip install flask==1.1.2  && pip install flask_httpauth==4.1.0 && pip install flask_simpleldap && pip install python-dotenv==0.14.0


VOLUME [ "/data" ]

ADD . /

ADD student_age.json /data/

EXPOSE 5000

CMD [ "python", "./student_age.py" ]

