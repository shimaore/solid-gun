    require('chai').should()

    describe 'The module', ->
      it 'should load', -> require '..'
      m = require '..'
      it 'should have a time() function', ->
        m.should.have.property 'time'
        m.time.should.be.a 'function'
      it 'should have a uniqueness() function', ->
        m.should.have.property 'uniqueness'
        m.uniqueness.should.be.a 'function'

    describe 'time()', ->
      m = require '..'
      it 'should return a string', ->
        m.time().should.be.a 'string'
        m.time().should.have.length 5

    describe 'uniqueness()', ->
      m = require '..'
      it 'should return a string', ->
        m.uniqueness().should.be.a 'string'
        m.uniqueness().should.have.length 4

