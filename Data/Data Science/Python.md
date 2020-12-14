# Python

* [How to Install Python 3 on Mac](https://www.saintlad.com/install-python-3-on-mac/)
* [Installing Python 3 and Python Packages](https://www.codecademy.com/articles/install-python3)
* [How to set up virtual environments for Python on a Mac](https://opensource.com/article/19/6/python-virtual-environments-mac)

```
▶ conda init fish
```

## Str

```
"Python" in name
```

## Data classes

https://realpython.com/python-data-classes/

## Tuple

```python
hearts = ("Q", "Hearts")

# Unpacking
a, b = (1, 2)
```

## Dic

```python
hearts = {"rank": "Q", "suit": "Hearts"}

for key, value in hearts.items():
  print(key, value)
```

## List and Map

```python
squares = list(map(lambda x: x**2, numbers))
```

## Tips

```python
x = 1 if condition else 0
num = 10_000_000
print(f"{num:,}")

names = ["Peter Parker", "Clark Kent"]
heroes = ["Spiderman", "Superman"]

for index, name in enumerate(names, start=1):
    print(index, name)
    
for name, hero in zip(names, heroes):
    print(f"{name} is actually {hero}")
```

## Read file

```python
with open("test.txt", "r") as f:
    file_content = f.read()
    
with open("countries.json") as f:
    COUNTRIES = json.loads(f.read())
    
import gzip

for line in gzip.open("data.gz", "rt"):
    line.strip().split()
```

