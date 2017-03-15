# Keynote David Beazley - Topics of Interest (Python Asyncio)

Those example code was original from Python Brasil 2015 Keynote. It's all about whether interface of asyncio is necessary or not.

Source: [Keynote David Beazley - Topics of Interest (Python Asyncio)](https://www.youtube.com/watch?v=ZzfHjytDceU)

---

## Background Knowledge

1.yield

    $ python yield.py
    5
    4
    3
    2
    1

2.coroutine

    $ python coroutine.py 
    >>>> send1
    somevalue

    >>>> send2
    The result is None
    Traceback (most recent call last):
      File "background_knowledge_coroutine.py", line 13, in <module>
        print(f.send(None))
    StopIteration

3.coroutine + async

    $ python coroutine_async.py
    >>>> send1
    Start foo()
    somevalue

    >>>> send2
    The result is None
    End foo()
    Traceback (most recent call last):
      File "background_knowledge_coroutine_async.py", line 17, in <module>
        print(f.send(None))
    StopIteration

4.coroutine + async + async

    $ python coroutine_async2.py
    >>>> send1
    Start bar()
    Start foo()
    somevalue

    >>>> send2
    The result is None
    End foo()
    End bar()
    Traceback (most recent call last):
      File "background_knowledge_coroutine_async2.py", line 22, in <module>
        print(f.send(None))
    StopIteration

5.examples of invalid syntax

    $ python background_knowledge_invalid_syntax.py

---

## Echo server

Here are three echo servers:

- aecho.py: asyncio + interface
- mecho.py: asyncio with your own interface - myasyncio.py
- gecho.py: gevent

## Run echo server

    *Must install requirement.txt while using gecho.py
    $ pip install -r requirement.txt

    > Terminal 1: Run server first
    $ python [aecho.py|mecho.py|gecho.py]
    
    > Terminal 2: Connect to server by netcat
    $ nc localhost 50000

    > Terminal 1: Check the reaction of server
    Connection from:  ('127.0.0.1', XXXXX)

    > Terminal 2: Check the function of echo server
    asd
    Got: asd
    Ctrl+C
    
    > Terminal 1: Check the reaction of server
    Connection closed

## Run benchmark

    > Terminal 1: Run server first
    $ python [aecho.py|mecho.py|gecho.py]

    > Terminal 2: Run benchmark
    $ python bench.py

## Result of benchmark

- aecho.py: (12638.540409225803, 'messages/sec')
- mecho.py: (19400.764281054424, 'messages/sec')
- gecho.py: (21307.778045333405, 'messages/sec') 

gevent had the best performance. However, asyncio with its interface had the worst performance.
