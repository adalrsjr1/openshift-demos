FROM alpine:latest

RUN apk --no-cache add --update \
    python \
    py-pip && \
    pip install flask

COPY app.py /opt/


ENTRYPOINT FLASK_RUN_PORT=8080 FLASK_APP=/opt/app.py flask run --host=0.0.0.0
