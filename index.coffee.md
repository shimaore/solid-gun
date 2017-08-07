Ref IDs

    Base = require 'base-p'
    base62 = new Base 62

## Time

- Year, base 62 (2+)
- Month, base 12 (1)
- Day, base 32 (1)
- Hour, base 12 (1)
- Minute, base 60 (1)

    Moment = require 'moment'

    @time = ->
      date = Moment()
      [
        base62.encode date.year()            # 2
        base62.encode date.month()+1         # 1
        base62.encode date.date()            # 1
        base62.encode date.hours()           # 1
        base62.encode date.minutes()         # 1
      ].join ''

      # total length: 6

## Uniqueness

    crypto = require 'crypto'
    dic64 = '0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz._'

    @uniqueness = ->
      r = crypto.randomBytes(3)
      p = ((r[0]>>6)<<0) + ((r[1]>>6)<<2) + ((r[2]>>6)<<4)
      console.log p
      [
        dic64[r[0] & 63]
        dic64[r[1] & 63]
        dic64[r[2] & 63]
        dic64[p]
        # base62.encode date.seconds()         # 1
        # base62.encode date.milliseconds()    # 2
        # process.env.SYSTEM_ID ? ''           # 1+
      ].join ''

      # total length: 4
