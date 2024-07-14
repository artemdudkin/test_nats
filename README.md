# test_nats

Тест получения данных из [NATS](https://nats.io/)

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

2.3 Результат - запущенный сервер
![nats-started](https://github.com/artemdudkin/test_nats/blob/b235c71b53c839f292be07f37be04b1b37af732d/docs/img/nats.png)

2.4 Количество соединений и прочую статистику можно посмотреть на [странице мониторинга](http://localhost:8222/varz)
![varz](https://github.com/artemdudkin/test_nats/blob/b235c71b53c839f292be07f37be04b1b37af732d/docs/img/varz.png)


## Publish data at subject and check it published

3.1 Создать подписчика на сабджект xyz

```
nats -s ws://localhost:8080 sub xyz
```
![cli-create-sub](https://github.com/artemdudkin/test_nats/blob/b235c71b53c839f292be07f37be04b1b37af732d/docs/img/nats-cli.png)


3.2 Публикация данных в сабджект xyz

```
nats --server localhost:4223 pub xyz "{\"a\":2}"
```
![cli-pub](https://github.com/artemdudkin/test_nats/blob/b235c71b53c839f292be07f37be04b1b37af732d/docs/img/nats-cli-2.png)

3.3 данные пришли в подписчика
![cli-sub-data](https://github.com/artemdudkin/test_nats/blob/b235c71b53c839f292be07f37be04b1b37af732d/docs/img/nats-cli-3.png)

## Получение данных в веб-приложении

4.1 Необходимо открыть файл index.html в браузере (все сообщения выводятся в консоль)

4.2 Отправить данные в сабджект xyz (см п 3.2)

4.3 Убедиться, что данные пришли (в консоли браузера)
![web](https://github.com/artemdudkin/test_nats/blob/b235c71b53c839f292be07f37be04b1b37af732d/docs/img/web.png)

4.4 Обрабатываются кейсы - (1) обрыв связи с сервером и последующее восстановление, (2) старт в момент отсутствия связи с сервером и ее восстановление, (3) продолжение работы после получения не-json данных

## License

MIT
