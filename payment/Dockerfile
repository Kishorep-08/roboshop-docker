FROM python:3 AS builder
WORKDIR /opt/server
COPY files .
RUN pip3 install -r --prefix=/python-install files/requirements.txt

FROM python:3.9.25-alpine3.22
WORKDIR /opt/server
RUN addgroup --system roboshop && adduser --system --group roboshop
EXPOSE 8080
LABEL created_by="Kishore" \
      component="payment" \
      project="roboshop"
ENV CART_HOST="cart" \
    CART_PORT="8080" \
    USER_HOST="user" \
    USER_PORT="8080" \
    AMQP_HOST="rabbitmq" \
    AMQP_USER="roboshop" \
    AMQP_PASS="roboshop123"
# Copying application files from builder stage
COPY --from=builder --chown=roboshop:roboshop /opt/server/python-install /usr/local/bin
COPY --chown=roboshop:roboshop files .
USER roboshop
ENTRYPOINT ["uwsgi", "--ini"]
CMD ["payment.ini"]


# FROM python:3
# WORKDIR /opt/server
# COPY files .
# RUN pip3 install -r requirements.txt
# EXPOSE 8080
# ENV CART_HOST="cart" \
#     CART_PORT="8080" \
#     USER_HOST="user" \
#     USER_PORT="8080" \
#     AMQP_HOST="rabbitmq" \
#     AMQP_USER="roboshop" \
#     AMQP_PASS="roboshop123"
# CMD ["uwsgi", "--ini", "payment.ini"]
