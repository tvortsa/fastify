<div align="center">
<img src="https://github.com/fastify/graphics/raw/master/full-logo.png" width="650" height="auto"/>
</div>

Enter Fastify. Fastify это веб-фреймворк, ориентированный на обеспечение наилучшего опыта разработчика с минимальными издержками и мощной архитектурой плагинов. Он вдохновлен Hapi и Express, и, насколько нам известно, это одна из самых быстрых веб-платформ в городе.

### Установка

установка с npm:

```
npm i fastify --save
```

установка с yarn:

```
yarn add fastify
```

### Пример

```js
// Require фрэймворк и инстанцируем его
const fastify = require('fastify')({
  logger: true
})

// объявляем роуты
fastify.get('/', (request, reply) => {
  reply.send({ hello: 'world' })
})

// Запускаем сервер
fastify.listen(3000, (err, address) => {
  if (err) throw err
  fastify.log.info(`server listening on ${address}`)
})
```

with async-await:

```js
const fastify = require('fastify')({
  logger: true
})

fastify.get('/', async (request, reply) => {
  reply.type('application/json').code(200)
  return { hello: 'world' }
})

fastify.listen(3000, (err, address) => {
  if (err) throw err
  fastify.log.info(`server listening on ${address}`)
})
```

Хотите узнать больше? Идите в <a href="https://github.com/fastify/fastify/blob/master/docs/Getting-Started.md"><code><b>Getting Started</b></code></a>.

### Быстрый старт с Fastify CLI

Хорошие инструменты делают разработку API быстрее и проще в обслуживании, чем все вручную.

[Fastify CLI](https://github.com/fastify/fastify-cli) является инструментом интерфейса командной строки, который может создавать новые проекты, управлять плагинами, а также выполнять различные задачи разработки, тестирование и запуск приложения.

Целью данного руководства является создание и запуск простого проекта Fastify с использованием интерфейса командной строки Fastify, при этом следуя рекомендациям руководства по стилю, которые полезны для каждого проекта Fastify.

### Пример

Откройте окно терминала.

```
npm install fastify-cli --global
```

Сгенерируйте новый проект и дефолтное приложение, выполнив следующую команду:

```
fastify generate
```

За подробностями идите к [Fastify CLI documentation](https://github.com/fastify/fastify-cli).

### Fastify v1.x

Код для Fastify's **v1.x** лежит в [Branch 1.x](https://github.com/fastify/fastify/tree/1.x), так все Fastify 1.x изменения этой версии лежат в **`branch 1.x`**.

> ## Note
> 
> `.listen` binds to the local host, `localhost`, interface by default (`127.0.0.1` or `::1`, depending on the operating system configuration). If you are running Fastify in a container (Docker, [GCP](https://cloud.google.com/), etc.), you may need to bind to `0.0.0.0`. Be careful when deciding to listen on all interfaces; it comes with inherent [security risks](https://web.archive.org/web/20170711105010/https://snyk.io/blog/mongodb-hack-and-secure-defaults/).
> See [the documentation](https://github.com/fastify/fastify/blob/master/docs/Server.md#listen) for more information.

### Основные особенности

-   **Производительность:** as far as we know, Fastify is one of the fastest web frameworks in town, depending on the code complexity we can serve up to 30 thousand requests per second.
-   **РАсширяемость:** Fastify is fully extensible via its hooks, plugins and decorators.
-   **Основан на схемах:** даже если это не является обязательным, мы рекомендуем использовать [схему JSON](http://json-schema.org/) для проверки ваших маршрутов и сериализации выходных данных, внутренне Fastify компилирует схему в высокопроизводительную функцию..
-   **Логирование:** logs are extremely important but are costly; we chose the best logger to almost remove this cost, [Pino](https://github.com/pinojs/pino)!
-   **Дружественный к разработчику:** the framework is built to be very expressive and help the developer in their daily use, without sacrificing performance and security.

### Benchmarks

__Machine:__ EX41S-SSD, Intel Core i7, 4Ghz, 64GB RAM, 4C/8T, SSD.

__Method:__: `autocannon -c 100 -d 40 -p 10 localhost:3000` * 2, taking the second average

| Framework | Version | Router? | Requests/sec |
| --- | --- | --- | --- |
| hapi | 18.1.0 | &#10003; | 29,998 |
| Express | 4.16.4 | &#10003; | 38,510 |
| Restify | 8.0.0 | &#10003; | 39,331 |
| Koa | 2.7.0 | &#10007; | 50,933 |
| **Fastify** | **2.0.0** | **&#10003;** | **76,835** |
| - |  |  |  |
| `http.Server` | 10.15.2 | &#10007; | 71,768 |

Benchmarks taken using https://github.com/fastify/benchmarks. This is a
synthetic, "hello world" benchmark that aims to evaluate the framework
overhead. The overhead that each framework has on your application
depends on your application, you should __always__ benchmark if performance
matters to you.

## Documentation

-   <a href="https://github.com/fastify/fastify/blob/master/docs/Getting-Started.md"><code><b>Getting Started</b></code></a>
-   <a href="https://github.com/fastify/fastify/blob/master/docs/Server.md"><code><b>Server</b></code></a>
-   <a href="https://github.com/fastify/fastify/blob/master/docs/Routes.md"><code><b>Routes</b></code></a>
-   <a href="https://github.com/fastify/fastify/blob/master/docs/Logging.md"><code><b>Logging</b></code></a>
-   <a href="https://github.com/fastify/fastify/blob/master/docs/Middleware.md"><code><b>Middleware</b></code></a>
-   <a href="https://github.com/fastify/fastify/blob/master/docs/Hooks.md"><code><b>Hooks</b></code></a>
-   <a href="https://github.com/fastify/fastify/blob/master/docs/Decorators.md"><code><b>Decorators</b></code></a>
-   <a href="https://github.com/fastify/fastify/blob/master/docs/Validation-and-Serialization.md"><code><b>Validation and Serialization</b></code></a>
-   <a href="https://github.com/fastify/fastify/blob/master/docs/Lifecycle.md"><code><b>Lifecycle</b></code></a>
-   <a href="https://github.com/fastify/fastify/blob/master/docs/Reply.md"><code><b>Reply</b></code></a>
-   <a href="https://github.com/fastify/fastify/blob/master/docs/Request.md"><code><b>Request</b></code></a>
-   <a href="https://github.com/fastify/fastify/blob/master/docs/Errors.md"><code><b>Errors</b></code></a>
-   <a href="https://github.com/fastify/fastify/blob/master/docs/ContentTypeParser.md"><code><b>Content Type Parser</b></code></a>
-   <a href="https://github.com/fastify/fastify/blob/master/docs/Plugins.md"><code><b>Plugins</b></code></a>
-   <a href="https://github.com/fastify/fastify/blob/master/docs/Testing.md"><code><b>Testing</b></code></a>
-   <a href="https://github.com/fastify/fastify/blob/master/docs/Benchmarking.md"><code><b>Benchmarking</b></code></a>
-   <a href="https://github.com/fastify/fastify/blob/master/docs/Write-Plugin.md"><code><b>How to write a good plugin</b></code></a>
-   <a href="https://github.com/fastify/fastify/blob/master/docs/Plugins-Guide.md"><code><b>Plugins Guide</b></code></a>
-   <a href="https://github.com/fastify/fastify/blob/master/docs/HTTP2.md"><code><b>HTTP2</b></code></a>
-   <a href="https://github.com/fastify/fastify/blob/master/docs/LTS.md"><code><b>Long Term Support</b></code></a>
-   <a href="https://github.com/fastify/fastify/blob/master/docs/TypeScript.md"><code><b>TypeScript and types support</b></code></a>
-   <a href="https://github.com/fastify/fastify/blob/master/docs/Serverless.md"><code><b>Serverless</b></code></a>

中文文档[地址](https://github.com/fastify/docs-chinese/blob/master/README.md)

## Ecosystem

-   [Core](https://github.com/fastify/fastify/blob/master/docs/Ecosystem.md#core) - Core plugins maintained by the _Fastify_ [team](#team).
-   [Community](https://github.com/fastify/fastify/blob/master/docs/Ecosystem.md#community) - Community supported plugins.
-   [Live Examples](https://github.com/fastify/example) - Multirepo with a broad set of real working examples.

## Support

-   [Fastify help](https://github.com/fastify/help)
-   [Gitter Chat](https://gitter.im/fastify)

## Team

_Fastify_ is the result of the work of a great community.
Team members are listed in alphabetical order.

**Lead Maintainers:**

-   [__Matteo Collina__](https://github.com/mcollina), <https://twitter.com/matteocollina>, <https://www.npmjs.com/~matteo.collina>
-   [__Tomas Della Vedova__](https://github.com/delvedor), <https://twitter.com/delvedor>, <https://www.npmjs.com/~delvedor>

### Fastify Core team

-   [__Tommaso Allevi__](https://github.com/allevo), <https://twitter.com/allevitommaso>, <https://www.npmjs.com/~allevo>
-   [__Ethan Arrowood__](https://github.com/Ethan-Arrowood/), <https://twitter.com/arrowoodtech>, <https://www.npmjs.com/~ethan_arrowood>
-   [__Matteo Collina__](https://github.com/mcollina), <https://twitter.com/matteocollina>, <https://www.npmjs.com/~matteo.collina>
-   [__Tomas Della Vedova__](https://github.com/delvedor), <https://twitter.com/delvedor>, <https://www.npmjs.com/~delvedor>
-   [__Dustin Deus__](https://github.com/StarpTech), <https://twitter.com/dustindeus>, <https://www.npmjs.com/~starptech>
-   [__Denis Fäcke__](https://github.com/SerayaEryn), <https://twitter.com/serayaeryn>, <https://www.npmjs.com/~serayaeryn>
-   [__Luciano Mammino__](https://github.com/lmammino), <https://twitter.com/loige>, <https://www.npmjs.com/~lmammino>
-   [__Cemre Mengu__](https://github.com/cemremengu), <https://twitter.com/cemremengu>, <https://www.npmjs.com/~cemremengu>
-   [__Manuel Spigolon__](https://github.com/eomm), <https://twitter.com/manueomm>, <https://www.npmjs.com/~eomm>
-   [__James Sumners__](https://github.com/jsumners), <https://twitter.com/jsumners79>, <https://www.npmjs.com/~jsumners>

### Fastify Plugins team

-   [__Matteo Collina__](https://github.com/mcollina), <https://twitter.com/matteocollina>, <https://www.npmjs.com/~matteo.collina>
-   [__Tomas Della Vedova__](https://github.com/delvedor), <https://twitter.com/delvedor>, <https://www.npmjs.com/~delvedor>
-   [__Manuel Spigolon__](https://github.com/eomm), <https://twitter.com/manueomm>, <https://www.npmjs.com/~eomm>

### Collaborators

Great contributors on a specific area in the Fastify ecosystem will be invited to join this group by Lead Maintainers.

-   [__Luciano Mammino__](https://github.com/lmammino), <https://twitter.com/loige>, <https://www.npmjs.com/~lmammino>
-   [__Evan Shortiss__](https://github.com/evanshortiss), <https://twitter.com/evanshortiss>, <https://www.npmjs.com/~evanshortiss>

**Past Collaborators**

-   [__Çağatay Çalı__](https://github.com/cagataycali), <https://twitter.com/cagataycali>, <https://www.npmjs.com/~cagataycali>
-   [__Trivikram Kamat__](https://github.com/trivikr), <https://twitter.com/trivikram>, <https://www.npmjs.com/~trivikr>
-   [__Nathan Woltman__](https://github.com/nwoltman), <https://twitter.com/NathanWoltman>, <https://www.npmjs.com/~nwoltman>

## Acknowledgements

This project is kindly sponsored by:

-   [nearForm](http://nearform.com)

Past Sponsors:

-   [LetzDoIt](http://www.letzdoitapp.com/)

## License

Licensed under [MIT](./LICENSE).

For your convenience, here is a list of all the licenses of our production dependencies:

-   MIT
-   ISC
-   BSD-3-Clause
-   BSD-2-Clause
