FROM python:3.9-alpine3.22 AS builder
RUN apk add --no-cache python3-dev build-base linux-headers pcre-dev musl-dev
WORKDIR /opt/server
COPY payment.ini .
COPY *.py .
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt uwsgi


FROM python:3.9.23-alpine3.22
EXPOSE 8080
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop
WORKDIR /opt/server
COPY --from=builder /opt/server /opt/server
COPY --from=builder /usr/local /usr/local
USER roboshop
CMD ["uwsgi", "--ini", "payment.ini"]


# FROM python:3.9
# WORKDIR /opt/server
# COPY payment.ini .
# COPY *.py .
# COPY requirements.txt .
# RUN pip3 install -r requirements.txt
# CMD ["uwsgi", "--ini", "payment.ini"]
