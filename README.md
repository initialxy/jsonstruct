typedjson
=========

typedjson is a library for two way conversion of typed Python object and JSON. This project is originally a fork of [jsonpickle](jsonpickle.github.com) (Thanks guys!).

The key difference between this library and jsonpickle is that during deserialization, jsonpickle requires Python types to be specified as part of the JSON. This library intend to remove this requirement, and instead, allows you to specify the class that it will be deserialized into. It will exam the class definiton and create a typed Python object as a result. This approach is similar to how [Jackson](https://github.com/FasterXML/jackson) works.

    # Create sample types
    class Test(object):
        name = ""
        title = ""
        address = Address()

    class Address(object):
        city = ""
        province = ""

    t = Test()
    t.name = "Alice"
    t.title = "Developer"
    t.address = Address()
    t.address.city = "Toronto"
    t.address.province = "Ontario"

    j = typedjson.encode(t)
    print j         # '{"title": "Developer", "name": "Alice", "address": {"province": "Ontario", "city": "Toronto"}}'

    u = typedjson.decode(j, Test)

    print u.name    # 'Alice'
    print u.title   # 'Developer'
    print u.address.city    # 'Toronto'

The purpose of this library is that you can use it to create typed RESTful web services or clients, where data structures need to be defined and shared between client and server. It is also not ideal to expect incoming or outgoing JSON request or response to contain Python types as part of the JSON. Data types needed for services could sometimes grow very complex, making schema/type definition much more important and easier to understand.

This project is licensed under BSD License. Please see COPYING

**I Haven't really started working on this project yet, so right now it's mostly just jsonpickle. I will remove this line when it's ready to be used.**
