# 05-1. 클래스
## 클래스와 객체
- 클래스(class): 무언가 똑같은 것을 계속 만들어낼 수 있는 설계도면(과자 틀)
- 객체(object): 클래스로 만든 실직적인 물체/피조물 (과자 틀로 찍어낸 과자). 각각의 객체는 고유한 성격을 가지며, 동일한 클래스들로 만든 객체들은 서로 전혀 영향을 주지 않음.

```python
#클래스 선언 및 객체 생성 방법

class Cookie: #Cookie라는 클래스 생성
    pass

a = Cookie() #a라는 변수에 Cookie 객체 생성해서 주소값 저장
```

## 클래스
- 클래스 구조:
    > class 클래스명:
    ```python
        class Cookie:
        pass

    a = Cookie() #객체 생성
    ```

- 메소드(method): 클래스 내에 구현하는 함수를 다르게 부르는 말.
    > def 함수이름 (매개변수):
    ```python
    def add(self, num1, num2):
        return num1+num2
    ```

- 매개변수: 일반 함수와 달리 메소드의 첫 번째 매개변수에는 **반드시** **self**가 와야함. 그리고 self는 특별한 의미를 가짐.

    ```python
    a.add(2,3)
    ```
    > 메소드에 매개변수를 3개로 적었지만, 실제 메소드 사용할 때는 2개의 매개변수만 적는 이유? <br> 이유: self에 호출한 객체 a가 자동으로 전달됨. (이 부분은 파이썬만의 특징으로 자바는 이렇지 않음!)
<br>

- 객체에 생성되는 객체만의 변수를 `객체변수` 또는  `속성`이라함.

## 생성자(constructor)
생성자란 객체가 생성될 때, 실행되는 특별한 메소드. 보통 인스턴스 변수값을 초기화하는 등의 작업을 위해 사용됨.

> def __init__ 메소드가 생성자 메소드!

```python
class Calc:
    def __init__(self, first, second):
        self.first = first
        self.second = second
```
객체가 생성될 때 위의 생성자가 호출되며, first, second를 매개변수로 받아, 값 초기화 진행. **init 메소드에도 self가 첫 매개변수로 자동으로 전달됨!**

## 클래스의 상속
상속(inheritance)의 개념은 클래스에도 적용되는데, 어떤 클래스가 하나의 클래스를 상속받으면, 해당 클래스의 기능들을 물려받아 쓸 수 있음.

### 상속 선언
> class 클래스명 (상위클래스(상속해주는클래스))
하위 클래스는 상위 클래스의 기능을 모두 사용할 수 있음.

```python
class AdditionalCalc(Calc):
    def pow(self):
        result = self.first **self.second
        return result
```

### 메소드 오버라이딩 (method overriding)
상속한 상위클래스에 있는 메소드를 동일한 이름으로 다시 만드는 것.
이렇게 메소드를 오버라이딩하면, 상위클래스의 메소드 대신, 하위 클래스에서 새로 만든 메소드가 호출되어 실행됨.

## 클래스 변수
- 객체변수(인스턴스 변수): 다른 객체들에 영향을 받지 않고, 각 객체마다 독립적으로 존재

```python
class Family:
    lastname = "김"
```
이렇게 선언한 lastname은 클래스변수. 즉, 모든 객체에 동일하게 적용되는 변수. (/자바의 static 변수와 동일한 기능!)

클래스 변수는 `클래스명.클래스변수명`으로 사용할 수 있음.

<br>

# 05-2. 모듈
모듈: 함수/변수/클래스들을 모아 놓은 파이썬 파일. 즉, 다른 파이썬 프로그램에서 불러와 사용할 수 있도록 만든 파이썬 파일.

### 모듈 선언
```python
# mod1.py
def add(a,b):
    return a+b

def sub(a,b):
    return a-b
```
지금까지 만든 파이썬 파일과 다르지 않음.

### 모듈 불러오기
> import 모듈명

```python
import mod1

print(mod1.add(3,4))
print(mod1.add(4,6))
```
import는 이미 만들어 놓은 파이썬 모듈을 이용할 수 있게 해주는 명령어.
이용을 위해서는 `모듈명.사용할함수명`으로 이용.

> 주의:
    - import는 현재 디렉토리에 있는 파일/파이썬 라이브러리가 저장된 디렉토리에 있는 모듈만 불러올 수 있음
    - 파이썬 라이브러리는 파이썬을 설치할 때 자동으로 설치되는 파이썬 모듈을 말함.

모듈 내의 함수를 도트 연산자(.)를 사용하지 않고, 함수 이름만 사용하려고 할 때는 아래처럼 사용.
> from 모듈명 import 사용하려는_함수명

```python
from mod1 import add
print(add(3,4))
```

## `if__name__=="__main__":`의 의미
```python
#mod1.py
def add(a,b):
    return a+b

def sub(a,b):
    return a-b


if __name__ == "__main__":
    print("if__main문 실행됨")
    print(add(1,4))
    print(sub(4,2))
```
이렇게 if문을 넣어놓으면, mod1.py를 실행하면, 위의 조건문 안의 코드가 실행되고, test.py(메인함수)를 실행하면 실행되지 않음. 이는 `import mod1`을 실행했을 때, mod1.py가 실행되는 것을 막기 위해서임.

> __name__ 변수란?
    파이썬의 __name__ 변수는 내부적으로 사용하는 특별한 변수 이름. 만약, python의 mod1.py에서 직접 해당 파일을 실행하면, mod1.py의 __name__변수에 __main__의 값이 저장됨. 하지만, 파이썬 셸/다른 파이썬 모듈에서 mod1을 import할 경우에는 mod1.py의 __name__ 변수에는 mod1.py의 모듈 이름이 저장됨


## 클래스/변수를 포함한 모듈
모듈 내에 클래스/변수를 포함하고 있다면, 해당 모듈을 import하면 해당 클래스와 변수들을 사용할 수 있음

## 다른 디렉토리에 있는 모듈을 불러오는 방법
### 1. sys 모듈 사용하기
- sys 모듈 가져오기
    ```python
    import sys
    ```
    sys 모듈은 파이썬의 기본 라이브러리 모듈. 해당 모듈을 이용하면, 파이썬 라이브러리가 설치되어있는 디렉토리들을 확인할 수 있음. 따라서 sys.path에 import하려는 디렉토리를 추가하면, 다른 디렉토리에 있어도 불러올 수 있음. sys.path는 리스트이므로, .append()를 통해서 추가가능.

- sys.path에 디렉토리 경로 추가
    ```python
    sys.path.append("C:/doit/mymod")
    ```

### 2. PYTHONPATH 환경변수 사용하기
```cmd
set PYTHONPATH = "C:\doit\mymod"
```

위의 명령어를 통해, PYTHONPATH 환경변수에 사용하려는 모듈이 있는 파일 디렉토리를 설정하면, 별도의 디렉토리 이동 혹은 모듈 추가 작업 없이 불러와서 사용할 수 있음.
맥/유닉스에서는 `set`이 아니라 `export` 사용하기.

```bash
export PYTHONPATH=C:\doit\mymod
```
<br>

# 05-3. 패키지
패키지(package): 관련 있는 모듈들의 집합으로, 파이썬 모듈을 계층적(디렉토리 구조)로 관리할 수 있게 해줌
> 파이썬에서 모듈은 하나의 .py 파일을 말함

에: game 패키지
```python
game/
    __init__.py
    sound/
        __init__.py
        echo.py
        wav.py
    graphic/
        __init__.py
        screen.py
        render.py
    play/
        __init__.py
        run.py
        test.py
```

## 패키지 만들기
필요한 서브 디렉토리들을 생성하고, 해당 디렉토리 안에 `__init__.py`파일을 생성.

## `__init__.py`의 용도
`__init__.py` 파일은 해당 디렉토리가 패키지의 일부임을 알려주는 역할. 만약, game, sound, graphic 등 패키지에 포함된 디렉토리에 `__init__.py` 파일이 없다면, 패키지로 인식되지 않음.

또한, `__init__.py` 파일은 패키지와 관련된 설정/초기화 코드를 포함할 수 있음.

> 하지만, python3.3부터는 없어도 패키지로 인식

## 패키지 변수 및 함수 정의
패키지 수준에서의 변수와 함수를 정의하려면, 가장 상위(여기서는 game 패키지)패키지 내의 `__init__.py` 파일에 공통 변수나 함수를 정의아면됨.

```python
#C:/game/__init__.py
VERSION = 3.5
def print_version_info():
    print(f"The version of this game is {VERSION}.")
```

이렇게 정의된 변수와 함수는 아래처럼 사용가능
```python
import game
print(game.VERSION)
```

## 패키지 내의 모듈을 미리 import
`__init__.py` 파일에 같은 패키지 내의 다른 모듈을 미리 import해 패키지를 사용하는 코드에서 간편하게 접근할 수 있게함.

## 패키지 초기화
`__init__.py` 파일에 패키지를 처음 불러올 때 실행되어야하는 코드를 작성. 해당 코드는 패키지를 처음 import할 때 초기화하는 코드가 실행됨. 상위 패키지의 초기화 코드는, 하위 모듈의 함수를 import할 경우에도 실행됨. 단, 초기화 코드는 한 번 실행된 후에는 다시 import를 수행하더라도 실행되지 않음.

예: 데이터베이스 연결/ 설정 파일 로드

## `__all__`
특정 디렉토리의 모듈을 `*`을 사용하여 import할 때는 다음과 같이 해당 디렉토리의 `__init__.py` 파일에 `__all__` 변수를 설정하고 import할 수 있는 모듈을 정의해주어야함

```python
#C:/game/sound/__init.py
__all__ = ['echo']
```

`__all__`의 의미는 sound 디렉토리에서 `*`를 사용해 import할 경우, 이곳에서 정의된 echo 모듈만 import 된다는 의미.

## relative 패키지
전체 경로를 사용하지 않고 상대경로를 사용해 import 사용 가능
```python
#render.py
from ..sound.echo import echo_test

def render_test():
    print("render")
    echo_test()
```
`..`은 render.py의 부모 디렉토리를 의미.

### 상대 경로에 사용되는 접근자
| 접근자 | 설명 |
|:---:|:---:|
|..| 부모 디렉토리 |
|.| 현재 디렉토리 |