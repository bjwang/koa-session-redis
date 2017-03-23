# koa-session-redis-01
koa-session-redis-01

## How to use
`koa@2`基于koa2.0的session处理

`npm install koa-session-redis-01 --save`

## Notice
原本生成session是基于客户端cookies的，并存于redis中，但app端无cookies机制，所以原代码就不适用了，

所以在原来的基础上做了修改，同样可以适用于pc和app两端来存储用户session,

并且对原来的thunkify方式改为了Promise方式处理。

## Example

      #### app.js
      const koa = require('koa')
      const app = new koa()
      const convert = require('koa-convert')
      const session = require('koa-session-redis-01')

      app.keys = ['session keys']

      app.use(convert(session({
       host: process.env.SESSION_PORT_6379_TCP_ADDR || '127.0.0.1',
       port: process.env.SESSION_PORT_6379_TCP_PORT || 6379,
        db: 1,
        ttl: 24 * 60 * 60
      })))

      app.use(function *(){
        var n = this.session.views || 0
        this.session.views = ++n
        this.body = n + ' views'
      })

      app.listen(3000)

## Contributors
Chilledheart [koa-session-redis](https://github.com/Chilledheart/koa-session-redis "koa-session-redis" )
