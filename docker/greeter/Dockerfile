FROM ubuntu:24.04
WORKDIR /app
COPY ./greet /app/greet
RUN chmod +x ./greet

ENV GREETING="Hi!" NAME="CJ"

CMD ["./greet"]
