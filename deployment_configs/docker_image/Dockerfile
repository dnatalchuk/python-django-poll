FROM python:3.7

RUN wget https://github.com/dnatalchuk/python-django-poll/archive/master/challenge.tar.gz && \
    tar xf ./challenge.tar.gz && \
    chmod -R 755 python-django-poll-master

WORKDIR python-django-poll-master

RUN pip install -r requirements.txt

EXPOSE 8000

CMD ["python3", "manage.py", "runserver", "0.0.0.0:8000"]