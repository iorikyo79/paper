https://devinlife.com/python/pythonic-code/
페이지의 내용을 정리중.

### 1-1. range는 enumerate()를 사용하자
len과 range를 조합한 for 문법은 사용하지 말자.

```bash
animals = ['cat', 'dog', 'moose']

# Unpythonic Example
for i in range(len(animals)):
   print(i, animals[i])

--- output ---
0 cat
1 dog
2 moose

# enumerate()
for i, animal in enumerate(animals):
   print(i, animal)

--- output ---
0 cat
1 dog
2 moose

# index가 필요 없는 경우는 직접 리스트를 순환
for animal in animals:
   print(animal)
--- output ---
cat
dog
moose
```

### 1-2. open, close는 with을 사용하자
open, close를 이용해 file 접근시 with ... as Obj 방식 사용.
```bash

# Unpythonic Example
try:
    fileObj = open('spam.txt', 'w')
    eggs = 42 / 0    # A zero divide error happens here.
    fileObj.close()  # This line never runs.
except:
    print('Some error occurred.')

# 예외처리가 불편함. except에 close가 누락될 경우 문제 될수 있음.

# with
with open('spam.txt', 'w') as fileObj:
   fileObj.write('hello')
```

### 1-3. None과의 비교는 is를 사용하자.
None객체와 비교시 == 를 사용할 경우 오류가 발생할 가능성이 있음. is를 사용하자.
```bash
# Unpythonic Example
if spam == None:
   print('Not pythonic.')

# Pythonic Example
if spam is None:
   print('Pythonic.')
```

### 1-4. Boolean 비교는 ==나 is를 사용하지 말자.
if문에 직접 넣어서 사용하자.
```bash
# Unpythonic Example
if spam is True:
   print('Not pythonic.')

#Pythonic example
if isSpam:
   print('good')
elif not isSpam:
   print('no')
```

## 2. 문자열 포맷팅
### 2.1 문자열에 백슬래시가(\) 많은 경우 원시문자열을 사용하자
원시문자열(raw string)은 r 접두사가 붙운 문자열 리터럴. 백슬래시를 문자열로 취급안함
```bash
# Unpythonic Example
print('The file is in C:\\Users\\Al\\Desktop\\Info\\Archive\\Spam')
--- output ---
The file is in C:\Users\Al\Desktop\Info\Archive\Spam

# Pythonic Example
print(r'The file is in C:\Users\Al\Desktop\Info\Archive\Spam')
--- output ---
The file is in C:\Users\Al\Desktop\Info\Archive\Spam
```
