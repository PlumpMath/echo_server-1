#Keynote David Beazley - Topics of Interest (Python Asyncio)

Those example code was original from Python Brasil 2015 Keynote. It's all about whether interface of asyncio is necessary or not.

Source: ![Keynote David Beazley - Topics of Interest (Python Asyncio)](https://www.youtube.com/watch?v=ZzfHjytDceU)

---

##Background Knowledge

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

##echo server

    - aecho.py: asyncio + interface
    - mecho.py: asyncio with your own interface - myasyncio.py
    - gecho.py: gevent

    *Must install requirement.txt while using gecho.py
    $ pip install -r requirement.txt

    > Terminal 1
    $ python [aecho.py|mecho.py|gecho.py]
    
    > Terminal 2
    $ nc localhost 50000

    > Terminal 1
    Connection from:  ('127.0.0.1', XXXXX)

    > Terminal 2
    asd
    Got: asd

##Benchmark of echo server

    > Terminal 1
    $ python [aecho.py|mecho.py|gecho.py]

    > Terminal 2
    $ python bench.py

    - aecho.py: (12638.540409225803, 'messages/sec')
    - mecho.py: (19400.764281054424, 'messages/sec')
    - gecho.py: (21307.778045333405, 'messages/sec') 

    gevent had the best performance. However, asyncio with its interface had the worst performance.
