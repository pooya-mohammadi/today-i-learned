# OOP

## What is a Singleton pattern?

The singleton pattern is a design pattern that restricts the instantiation of a class to one object. It is used in cases
where exactly one object is needed.

```python
class Singleton(type):
    _instances = {}

    def __call__(cls, *args, **kwargs):
        if cls not in cls._instances:
            cls._instances[cls] = super(Singleton, cls).__call__(*args, **kwargs)
        return cls._instances[cls]


class Logger(metaclass=Singleton):
    def __init__(self, var=10):
        self.var = var


if __name__ == '__main__':
    logger_1 = Logger(var=1)
    logger_2 = Logger(var=2)
    print(logger_1.var)  # returns 1
    print(logger_2.var)  # returns 1
    print(logger_2 == logger_1)  # returns True

```
References:</br>
https://stackoverflow.com/questions/6760685/creating-a-singleton-in-python </br>
https://python-course.eu/oop/metaclasses.php