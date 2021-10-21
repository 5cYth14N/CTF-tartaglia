# Tartaglia
### Scripting challenge
Pascal Triangle, is a numerical triangle formed by binomials. In a visual way, the triangle is something like this:

                                     1
                                 1       1
                             1       2       1
                         1       3       3       1
                     1       4       6       4       1

Each number is equal to the sum of the two previous numbers above in the triangle.
Challenge is to calculate the sum of all numbers from the line 1 to N. For example, for the line 3, the sum of all numbers is 7. For the line 5, the sum of all those numbers is 31.
The server ask a line number and we need to answer with the sum.

After we type ```help```, the server send us the python code.


```python
#!/usr/bin/python
# -*- coding: UTF-8 -*-

import re, socket, time

def solution(N):
    
    return str(sum)

sock = socket.socket(socket.AF_INET,socket.SOCK_STREAM)
sock.connect((‘localhost’, 14004))
data = sock.recv(100).decode('utf-8')
data = sock.recv(2048).decode('utf-8')
print(f'Data: {data}')
sock.send(b'start')
data = sock.recv(20).decode('utf-8')
print(f'Data: {data}')
time.sleep(1)

while True:
    try:
        data = sock.recv(2048).decode('utf-8')
        N = int(re.findall(r'N: (\d+)', data)[0])
    except IndexError:
        print(data)
        break

    print(data)
    answer = solution(N)
    print(f'Challenge: {N}')
    print(f'Solution: {answer}')

    sock.send(answer)
    data = sock.recv(32).decode('utf-8')
    print(data)
```

I do not wish to explain all lines in the program, just the main things.
1.	The server send the data which contains the line number (N).
2.	Then, the ```solution``` function calculate the answer.
3.	The program sends it to the server.
4.	If the answer correct we get the next question, otherwise the server terminates the connection.

Simple mathematical solution is, the sum of all numbers is equal of the power of two minus one. ```N^2 - 1```




#### *My programming solution is:*

First we need to change our address from localhost to the Tartaglia server:
```python
sock.connect((‘address of the tartaglia server’, 14004))
```

Then we write the simple mathematical formula:
```python
def solution(N):
    sum = (2 ** N) - 1
    return str(sum)
```

However, the server expect utf-8 encoding (as the hint mentions in the beginning of the code). Just simply send a number will not work. So:
```python
sock.send(answer.encode('utf-8'))
```

After 25 questions, we get the flag.

[+] Cong
ratz! The flag is: flag_{¬--------------------}
