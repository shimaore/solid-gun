Ref IDs

    Base = require 'base-p'
    base62 = new Base 62

## Time

    Moment = require 'moment'

    @time = (date) ->
      unixstamp = if date? then Moment(date).unix() else Moment().unix()
      base62.encode unixstamp // 6
      # total length: 5, encodes 10 times per minute

## Uniqueness

    crypto = require 'crypto'
    dic64 = '0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz._'

    @uniqueness = ->
      r = crypto.randomBytes(3)
      p = ((r[0]>>6)<<0) + ((r[1]>>6)<<2) + ((r[2]>>6)<<4)
      [
        dic64[r[0] & 63]
        dic64[r[1] & 63]
        dic64[r[2] & 63]
        dic64[p]
      ].join ''

      # total length: 4, 24 bits of randomness
