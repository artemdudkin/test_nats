# test_nats

> Тест получения данных из [NATS](https://nats.io/)

## Installation

1.1 Необходимо установить NATS (см https://github.com/nats-io/nats-server/releases) <br/>
1.2 Необходимо установить NATS CLI (см https://github.com/nats-io/natscli/releases)

## Start NATS

2.1 В папке где лежит NATS необходимо создать файл my.cfg

```
host: 0.0.0.0
port: 4223

websocket: {
 port: 8080
 no_tls: true
}

http: localhost:8222
```

2.2 Запускать NATS необходимо так:

```
nats-server -config my.cfg
```

## Publish data at subject and check it published


3.1 Публикация данных в сабджект xyz

```
nats --server localhost:4223 pub xyz "{\"a\":2}"
```

3.2 Если перед этим сделать подписчикана этот сабджект, то эти данные придут в него

```
nats -s ws://localhost:8080 sub xyz
```

## Получение данных в веб-приложении

4.1 Необходимо открыть файл index.html в браузере (все сообщения выводятся в консоль)

4.2 Отправить данные в сабждект xyz (см п 3.1)

4.3 Убедиться, что данные пришли (в консоли браузера)

4.4 Реализованы тестовые случаи - обрыв связи с сервером и последующее восстановление, старт в момент отсутствия связи с сервером и ее восстановление, продолжение работы после получения не-json данных

## License

MIT
