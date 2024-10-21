---
theme: ../../../../themes/black
titleTemplate: '%s'
author: Minjae Gwon
keywords: Clean Code,Collaboration
presenter: false
download: true
exportFilename: /clean-code/talks/clean-code/dist
export:
  format: pdf
  timeout: 30000
  dark: false
  withClicks: true
  withToc: true
remoteAssets: true
selectable: true
themeConfig:
  header: Clean Code
  brandImage: "/clean-code/wordmark-postech.svg"
  brandText: "POSTECH"
htmlAttrs:
  dir: ltr
  lang: ko
layout: cover
---

# Clean Code

> 틀린 코드 찾기

- Minjae Gwon
  - <minjae.gwon@postech.ac.kr>
  - <https://bxta.kr>
- CompSec Lab / ML Lab
  - <https://compsec.postech.ac.kr>
  - <https://ml.postech.ac.kr>
- PLUS
  - <https://plus.or.kr>

---

```yaml
layout: toc
```

- Introduction
  - What is Clean Code?
  - Why Clean Code?
- Code
  - Rules
- Collaboration
  - Rules
- Conclusion
  - Summary: Clean Code
  - Summary: Collaboration

---

```yaml
layout: leaflet
```

## Introduction

> 들어가며

---

### What is Clean Code?

- 주요 로직을 간결하게 한 줄로 작성한 코드
- 다른 사람들이 쉽게 읽을 수 있도록 주석을 자세하게 작성한 코드
- 구현하고자 하는 개념 각각에 일치하는 클래스를 모두 작성한 코드
- 테스트 커버리지를 100% 유지하며 코드를 작성한 코드

---

### That's Not Clean Code

- ~~주요 로직을 간결하게 한 줄로 작성한 코드~~
  - 주요한 로직일수록 풀어서 **읽기 쉽게 작성**해야 **유지보수성**을 높일 수 있다.
- ~~다른 사람들이 쉽게 읽을 수 있도록 주석을 자세하게 작성한 코드~~
  - 주석은 코드의 해석을 해칠 수 있다. **코드 자체로 설명할 수 있도록 작성**하는 것이 좋다.
- ~~구현하고자 하는 개념 각각에 일치하는 클래스를 모두 작성한 코드~~
  - 클래스는 프로젝트의 복잡성을 무조건 증가시킨다. **복잡도가 낮은 코드**가 세상을 구한다.
- ~~테스트 커버리지를 100% 유지하며 코드를 작성한 코드~~
  - 높은 테스트 커버리지가 과연 좋은 코드를 의미하는가?

---

### What is Really Clean Code?

- **Readability. Readability. Readability.**
  - 유지보수성이 높은 코드, 버그가 적은 코드, 복잡도가 낮은 코드, ...
  - 모두 **읽기 쉬운 코드**를 의미한다.

---

### Why Clean Code?

- **읽기 좋은 코드는 유지보수성을 높인다.**
  - 서로의 작업을 더 쉽게 이해할 수 있다.
- **읽기 좋은 코드는 버그를 줄인다.**
  - Logical 버그를 훨씬 빠르게 찾을 수 있다.
- **읽기 좋은 코드는 작업 속도를 높인다.**
  - 의사소통 비용은 협업에 드는 비용 중 가장 큰 비용이다.
  - 우리는 코드로 대화한다.
  - 코드가 읽기 좋으면 의사소통 비용이 줄어든다.

---

```yaml
layout: leaflet
```

## Code

> 코드

---

### Rule: 짧은 이름보다 긴 이름이 좋다 (1)

- 변수나 함수 스스로를 충분히 설명할 수 있을 만큼 긴 이름이 좋다.
  - 특히 줄임말을 지양해야한다.
  - 자동 완성이 되는 시대인데 긴 이름을 두려워 할 필요가 없다.
- Clean Code (Martin, Robert C, 2008)
  - 이름이 길어져도 괜찮으니 서술적인 이름을 택해라.
  - 긴 이름이 짧고 이해하기 어려운 이름보다 좋다.
  - 서술적인 이름은 설계를 뚜렷하게 만들어주며, 코드를 개선하기도 쉽게 만든다.

---

### Rule: 짧은 이름보다 긴 이름이 좋다 (3)

- **Clean Code (Martin, Robert C, 2008)**
  - 이름의 길이는 코드의 단순성에 영향을 미치지 않는다.
  - 오직 컴파일러의 불평 불만을 피하기 위해 이름을 짓거나, noise words를 추가하는 방식으로 이름을 짓는 것은 적절하지 않다.
    - 예시로, 같은 namespace에서의 변수 중복을 막기 위해 연속된 숫자를 뒤에 붙이는 방식은 코드의 의도를 전혀 전달하지 못한다.
  - 또한, variable이나 string 같은 불용어를 이름에 포함하는 것은 도움이 되지 못한다.
    - 그러므로 읽는 사람이 차이를 알도록 이름을 지어야 한다.
  - 발음하기 쉬운 단어가 두뇌에서 처리하기 쉬우며, 발음하기 어려운 이름은 토론하기도 어렵다.
  
---

### Rule: 짧은 이름보다 긴 이름이 좋다 (4)

```python
def some_function(a, cfg):
    # a가 b가 무엇을 의미하는지 명확하지 않다.
    # cfg? configuration? context free grammar?
```

```python
def to_number(data: bytes) -> int:
    # 무엇을 변환하는지 명확하지 않다. `bytes_to_int`는 어떨까?
    # ...
    return result
```

---

### Rule: 짧은 이름보다 긴 이름이 좋다 (5)

```python
def select_variable_or_empty(...): # 무엇을 선택하는 함수인지 명확하지 않다.
  # 잘 지은 이름은 로직을 보지 않아도 함수의 역할을 알 수 있게 만든다.
  for send_variable in send_variables:
    min_difference = 0x100000000 
    min_variable = None
    for recv_variable in recv_variables:
        difference = send_variable.value - recv_variable.value
        if abs(difference) < min_difference:
            min_difference = abs(difference)
            min_variable = recv_variable
```

---

### Rule: 주석보다 스스로 설명하는 코드가 좋다 (1)

- **주석은 오히려 코드의 해석을 해친다.**
  - 주석은 코드의 의도를 왜곡할 수 있다.
  - 코드와 일치하지 않는 주석은 코드를 읽는 사람을 속이는 것과 같다.
- **주석이 필요하다면 "스스로 설명할 수 있는 이름의 함수"로 분리해야할 때가 되지 않았는지 고민해보자.**
  - 함수의 이름이 주석의 역할을 대신할 수 있다.
- **Clean Code (Martin, Robert C, 2008)**
  - 코드로 충분히 설명하지 못한 부분을 주석으로 설명하려고 하기 보다 코드를 깔끔하게 만드는 것이 좋다.
  - 대부분의 경우에 코드만으로 의도를 표현할 수 있다.

---

### Rule: 주석보다 스스로 설명하는 코드가 좋다 (2)

```python
def calculate_total(order):
    total = 0
    for item in order:
        if item.type == "food": # 음식 항목의 경우 수량을 곱한 값을 더한다
            total += item.price * item.quantity 
        else: # 음료 항목의 경우 그냥 가격을 더한다
            total += item.price * 2 
    tax = total * 0.2  # 세금을 계산한다 (10%)
    return total + tax # 총 금액에 세금을 더한다
```

---

### Rule: 주석보다 스스로 설명하는 코드가 좋다 (3)

```python
def calculate_item_cost(item):
    if item.type == "food":
        return calculate_food_item_cost(item)
    else:
        return calculate_drink_item_cost(item)
def calculate_food_item_cost(item):
    return ...
def calculate_drink_item_cost(item):
    return ...
```

---

### Rule: Null을 주고 받지 마라

- **Clean Code (Martin, Robert C, 2008)**
  - *Don't Return Null*
    - `null`을 반환하는 코드는 작성해야할 코드를 증가시킬 뿐만 아니라 호출자에게 책임을 맡긴다.
    - 외부 라이브러리가 `null`을 반환한다면 감싸서 예외를 던지거나 특수 사례 객체를 반환하자.
  - *Don't Pass Null*
    - `null`을 인수로 받을 수 있도록 설계된 언어가 아니라면 `null`의 전달은 최대한 피해야한다.

---

### Rule: 에러 코드는 Caller를 골치 아프게 한다

- **Clean Code (Martin, Robert C, 2008)**
  - 오류 코드를 반환하기보다 예외를 발생시키는 편이 호출자 코드를 더 깔끔하게 만든다.
  - 즉, 비즈니스 로직과 예외를 처리하는 로직을 분리할 수 있다.
  - 예외에 전후 상황을 담아서 함께 던지는 것이 코드의 의도를 파악하는데 도움이 된다.

---

### Rule: Assert를 적절히 많이 사용하는 것이 좋다 (1)

- **코드 리전의 pre-condition과 post-condition을 assert로 나타내자.**
  - 실수를 줄이고 가독성을 높인다.
- **스스로 설명하는 코드를 만들어낸다.**
  - 코드를 읽는 사람에게 코드의 의도를 알려준다.
- **테스트 코드를 작성하는 것과 같은 효과를 낸다.**
  - 코드의 품질을 높인다.

---

### Rule: Assert를 적절히 많이 사용하는 것이 좋다 (2)

```python
def apply_discount(order, discount_rate):
    assert 0 <= discount_rate <= 1, "Discount rate should be between 0 and 1"
    discounted_order = []
    for item in order:
        discounted_price = item.price * (1 - discount_rate)
        assert discounted_price >= 0, "Discounted price should be non-negative"
        discounted_order.append(item._replace(price=discounted_price))
    return discounted_order
```

---

### Rule: 이름을 재사용하지 말자 (1)

- **이름을 재사용하면 코드를 읽는 사람을 속이는 것과 같다.**
  - 이름이 같다고 해서 같은 역할을 하는 것은 아니다.
  - 이름이 같다고 해서 같은 역할을 하는 것이라고 가정하는 것은 위험하다.
- **재사용된 이름은 코드 작성자에게도 위험하다.**
  - 버그를 찾기 어렵게 만든다.

---

### Rule: 이름을 재사용하지 말자 (2)

```python
tmp_pcap = FileCapture(...)
for packet in tmp_pcap:
    # ...
tmp_pcap.close()
for stream_number in suspicious_stream_numbers:
    tmp_pcap = FileCapture(...)
    # ...
tmp_pcap.close()

```

---

### Rule: 같은 이름은 같은 개념을 가리켜야한다 (1)

- **같은 이름은 같은 개념을 가리켜야한다.**
  - 같은 이름이 다른 개념을 가리키면 코드를 읽는 사람을 속이는 것과 같다.
  - 가독성을 심각하게 해친다.
    - 유지보수성의 저하를 초래한다.

---

### Rule: 같은 이름은 같은 개념을 가리켜야한다 (2)

- **Clean Code (Martin, Robert C, 2008)**
  - 추상적인 개념 하나에 단어 하나를 고수하자.
    - 예를 들어, `get`, `fetch`, `retreive`를 섞어 쓰는 것은 혼란을 야기한다.
  - 일관성 있는 어휘가 읽기 쉬운 코드를 만든다.
  - 한 단어를 두 가지 목적으로 사용하는 것은 말장난에 불과하다.
  - 같은 맥락이 아닌데도 일관성을 고려하여 앞서 사용한 단어를 채택하는 것은 혼란을 야기한다.

---

### Rule: 같은 이름은 같은 개념을 가리켜야한다 (3)

```python
for send_variable in send_variables:
    min_difference = 0x100000000 # `difference`가 `절댓값`을 나타냄
    min_variable = None
    for recv_variable in recv_variables:
        difference = send_variable.value - recv_variable.value
        # `difference`가 `차이`를 나타냄
        if abs(difference) < min_difference:
            min_difference = abs(difference)
            min_variable = recv_variable
```

---

### Rule: 거짓말을 하지 않는 것이 좋다 (1)

- **잘못 붙여진 이름은 거짓말이다.**
  - 변수나 함수의 이름이 잘못 붙여지면 코드를 읽는 사람을 속이는 것과 같다.
  - 가독성을 심각하게 해친다.
    - 유지보수성의 저하를 초래한다.
- **Clean Code (Martin, Robert C, 2008)**
  - 잘못된 단서는 코드의 이해를 어렵게 만든다.
  - 예시로, 널리 쓰이는 단어를 다른 의미로 사용할 경우 독자는 이를 잘못 이해할 수 있다.
  - 또한, 서로 흡사한 이름을 사용할 경우 독자는 읽기에 어려움을 느낀다.

---

### Rule: 거짓말을 하지 않는 것이 좋다 (2)

```python
def try_decode_hex(payload: bytes) -> list[bytes]:
    # `try`라는 이름은 보통 예외를 일으킬 수도 있는 함수에 붙이는 이름이다.
    pattern = re.compile(rb"([0-9a-fA-F]+)")

    decoded_payloads: list[bytes] = []
    for hex_string in pattern.findall(payload):
        decoded_payloads.append(bytes.fromhex(hex_string.decode()))

    return decoded_payloads
```

---

### Rule: 함수의 인자는 가능한 한 적어야 한다

- **Clean Code (Martin, Robert C, 2008)**
  - 인수의 개수가 적을수록 좋다.
  - 인수에 대한 질문을 던지거나, 인수를 변환해 결과를 반환하거나, 이벤트를 쓸 때가 아니라면 단항 함수는 피하는 것이 좋다.
  - 상황에 따라서 가변 인수를 취하는 함수를 단항, 이항, 삼항 함수로 생각할 수 있으며, 이를 넘어서 인수를 사용하는 것은 좋지 않다.
    - 이항 함수는 단항 함수보다 이해하기 어렵지만, 더 적절한 경우도 있다.
    - 삼항 함수는 이항 함수보다 이해하기 어렵다.
    - 인수가 여러개 필요하다면 객체로 묶어서 패스해보는 방법도 있다.

---

### Rule: 하나의 함수는 한가지 역할만 수행해야한다 (1)

- **하나의 함수가 여러 기능을 수행하는 것은 거짓말을 하는 것과 같다.**
  - 여러 기능을 수행하는 함수는 분리되어야할 필요가 있음을 스스로 증명한다.
  - 여러 기능을 수행하는 함수는 너무 많은 책임을 가지고 있다는 것을 의미한다.
- **Clean Code (Martin, Robert C, 2008)**
  - 함수는 한 가지만 해야하며, 그 한 가지를 잘 해야한다.
  - 의미 있는 이름으로 다른 함수를 추출할 수 있다면 그 함수는 여러 작업을 수행하고 있다고 생각할 수 있다.
  - 플래그 인수는 해당 함수가 여러 일을 처리하는 것을 암시하기에 좋지 않다.
  - 상태를 변경하거나 정보를 반환하는 행위를 하나의 함수가 하는 것은 혼란을 야기한다.
    - 명령과 조회를 분리해 혼란을 없애는 것이 좋다.

---

### Rule: 하나의 함수는 한가지 역할만 수행해야한다 (2)

```python
def process_order(order): # 재사용성이 떨어진다.
    total_with_tax = total + tax
    
    # 주문 내역 출력
    print("Order Details:")
    print(f"Total: {total_with_tax}")
    
    # 이메일 전송
    send_order_confirmation_email(order, total_with_tax)
```

---

### Rule: 사이드 이펙트는 만악의 근원이다

- **Clean Code (Martin, Robert C, 2008)**
  - 사이드 이펙트는 함수가 시간에 종속되는 문제를 초래하며, 순서에 종속되게 만든다.
  - 시간에 종속되는 함수는 함수 이름에 이를 분명히 명시해야 한다.
  - 출력을 위한 인수는 피하는 것이 좋다.

---

### Rule: 변하지 않는 변수가 좋다 (1)

- **변수의 값이 변경되지 않는 로직을 구성하는 것이 버그를 줄일 수 있는 지름길이다.**
  - 변경이 필요하다면 새로운 변수로 복사 및 할당을 동시에 하는 것이 좋다.
    - 과거와 같이 메모리가 부족한 시대가 아니다.

---

### Rule: 변하지 않는 변수가 좋다 (2)

```python
def get_unused_offsets_or_empty(
    used_offsets: List[Tuple[int, int]], total_range: range
) -> List[Tuple[int, int]]:
    used_offsets.sort()
    # .sort()는 원본 리스트를 변경한다.
    # 이는 Caller에게 예상치 못한 Side Effect를 초래한다.
    # 따라서, .sort()를 사용하지 않고 새로운 리스트를 생성해서 이용하는 것이 좋다.
```

---

### Rule: 전역변수는 코드를 죽인다

- **코드의 확장성을 낮춘다.**
  - 비즈니스 로직이 전역변수의 컨텍스트에 갇히게 된다..
  - 특정 컨텍스트에 갇힌 갇힌 비즈니스 로직은 재사용이 어렵다.
- **조그만 변경이 눈사태처럼 커진다.**
  - 변수가 어디서 어떻게 사용되는지 추적하기 어려워진다.
  - 코드 의존성을 파악하기 어려워진다.
  - 언제 어디서 변경될지 모르는 값에 의존하게 만든다.

---

### Rule: 클래스를 만들기 전에 한 번 더 생각해보자 (1)

- **클래스는 코드의 확장성을 낮춘다.**
  - 클래스는 근본적으로 **비즈니스 로직을 컨텍스트에 가두는 장치**이다.
  - 클래스에 갇힌 비즈니스 로직은 재사용이 어렵다.
- **비즈니스 로직을 클래스의 메서드로 구현하기보다 일반적인 함수로 구현해보자.**
  - 일반적인 함수는 어디서든 이용될 수 있다.
    - 전역변수를 사용하지 않는다면.

---

### Rule: 클래스를 만들기 전에 한 번 더 생각해보자 (2)

```python
class ShoppingCart:
    def __init__(self, items: Item[], tax_rate: float):
        self.items = items
        self.tax_rate = tax_rate

    def calculate_total_price(self): # 이 로직을 굳이 메서드로 만들어야할까?
        total = sum(item.price for item in self.items)
        tax = total * self.tax_rate
        return total + tax
```

---

### Rule: 상속을 하기 전에 두 번 더 생각해보자 (1)

- **상속은 사실 전역변수를 쓰는 것과 같다.**
  - 상속을 받은 클래스는 부모 클래스의 자원을 이용한다.
  - 즉, 부모 클래스의 변경이 자식 클래스에 영향을 미친다.
    - 이는 전역변수를 사용하는 것과 비슷한 효과를 초래한다.
  - 코드 수정이 어디까지 영향을 미칠지 추적하기 어렵다.
- **상속이 깊어질수록 복잡성은 증가하고 확장성은 낮아진다.**
  - 코드를 이해하기 어려워진다.
  - 코드를 변경하기 어려워진다.

---

### Rule: 함수는 적절한 길이를 유지해야한다 (1)

- **긴 함수는 코드의 가독성을 낮춘다**.
  - 함수가 길어지기 전에 함수를 분리하자.
  - 클래스와 달리, 함수가 많아지는 것을 기피할 필요가 없다.
    - 확장성에 큰 영향을 미치지 않는다.
- **Clean Code (Martin, Robert C, 2008)**
  - 함수를 만드는 첫번째 규칙은 작아야만 한다는 것이다.
  - 중첩 구조가 생길 만큼 커진 함수는 읽고 이해하기 어렵다.
  - 더 나아가, `if`나 `else` 그리고 `while` 등에 들어가는 블록도 작아야한다.

---

### Rule: 함수는 적절한 길이를 유지해야한다 (2)

```python
def calculate_total_price(items, tax_rate):
    total = 0
    for item in items:
        if item["type"] == "food":
            price = item["price"]
            quantity = item["quantity"]
            total += price * quantity
        elif item["type"] == "drink":
            price = item["price"]
            total += price
    tax = total * tax_rate
    return total + tax
```

---

### Rule: 함수는 적절한 길이를 유지해야한다 (3)

```python
def calculate_total_price(items, tax_rate):
    total = sum(get_item_total(item) for item in items)
    tax = total * tax_rate
    return total + tax
def get_item_total(item):
    if item["type"] == "food":
        return get_food_item_total(item)
    elif item["type"] == "drink":
        return get_drink_item_total(item)
```

---

### Rule: 코드는 위로 자란다 (1)

- **사람은 코드를 위에서 아래로 읽는다.**
- **그러므로 위로 갈수록 추상화 단계가 높은 코드를 배치하는 것이 맞다.**
  - 코드를 읽는 사람은 코드의 추상화 단계가 높은 코드를 먼저 읽게 된다.
    - 코드의 의도를 더 잘 파악할 수 있다.
  - 코드의 추상화 단계가 높은 코드는 코드의 의도를 더 잘 나타낸다.
- **Clean Code (Martin, Robert C, 2008)**
  - 함수 내 모든 문장의 추상화 수준은 동일해야 한다.
  - 한 함수 내에 추상화 수준을 섞으면 이해하기 어렵다.
  - 위에서 아래로 갈 수록 함수의 추상화 수준이 한 단계씩 낮아지는 것이 좋다.

---

### Rule: 코드는 위로 자란다 (2)

```python
def sum_item_costs(order):
    return sum(calculate_item_cost(item) for item in order)

def calculate_total_cost(order, tax_rate):
    total_price = sum_item_costs(order)
    tax = calculate_tax(total_price, tax_rate)
    return total_price + tax

def calculate_tax(total_price, tax_rate):
    return total_price * tax_rate
```

---

### Rule: 관련된 코드를 뭉치자 (1)

- **변수나 함수의 정의와 사용을 가까이 배치하자.**
  - 정의와 참조가 멀리 떨어져 있으면 코드를 이해하기 어렵다.
- **함수는 호출하는 함수와 호출되는 함수를 가까이 배치하자.**
  - 함수가 호출되는 곳이 멀리 떨어져 있으면 코드를 이해하기 어렵다.

---

### Rule: 관련된 코드를 뭉치자 (2)

```python
        suspicious_stream_numbers: Set[int] = set()
        suspicious_pcaps: List[str] = list() # suspicious_pcaps는 어디서 사용되는가?

        for packet in tmp_pcap:
            # ... 100줄 이상의 코드

        # suspicious_stream_numbers를 사용하는 코드가 너무 멀리 떨어져 있다.
        for stream_number in suspicious_stream_numbers:
            # ...
```

---

```yaml
layout: leaflet
```

## Collaboration

> 협업

---

### Rule: 낙천주의는 금물이다

<!-- header: Collaboration -->
- **The Mythical Man-Month (Fred Brooks, 1975)**
  - **모든 문제는 낙천적인 일정 산정에서 비롯된다.**
    - 모든 작업이 예정 시간 내에 완료될 것이라는 착각은 프로그래밍 일정 관리를 망치는 지름길이다.
    - 프로그래밍의 재료는 다루기가 무척이나 쉽기 때문에 프로그래머는 어려움이 없을 것이라고 쉽게 착각한다.
    - 수많은 작업으로 이뤄진 대형 프로그래밍 프로젝트가 예정대로 진행될 확률은 매우 낮다.

---

### Rule: The Mythical Man-Month (1)

- **The Mythical Man-Month (Fred Brooks, 1975)**
  - **맨먼스 단위로 투입된 프로젝트 비용과 작업 진척도는 연관되어 있지 않다.**
    - 여러 사람이 동시에 소통 없이 작업할 수 있는 경우에만 맨먼스와 작업 진척도 사이에 연관성이 존재한다.
    - 작업들 사이에 의존성이 있다면 어떤 노력을 더 하더라도 일정에 영향을 미치지 못한다.
    - 작업을 나눌 수 있지만 커뮤니케이션을 해야하는 경우 그 비용도 고려해야 한다.
    - 늘어난 인원 수에 따른 과중된 의사소통 비용은 소요 시간을 오히려 증대시키는 결과를 초래한다.

---

### Rule: The Mythical Man-Month (2)

- **The Mythical Man-Month (Fred Brooks, 1975)**
  - **더 많은 사람과 더 짧은 시간으로는 건강한 일정을 만들 수 없다.**
    - 프로젝트에 소요되는 기간은 의존성이 있는 내부 작업들에 의해 결정된다.
    - 프로젝트에 필요한 최대 인원수는 독립된 작업들의 개수에 의해 정해진다.
    - 마일스톤을 제시간 안에 끝내지 못했다면,
      - 인원을 추가하거나 일정을 재수립하거나 작업 범위를 축소할 수 있을 것이다.
    - 일정은 그대로 두면서 인원을 추가하는 경우,
      - 훈련과 의사소통 비용으로 인해 프로젝트의 완료는 오히려 더 늦어진다.

---

### Rule: The Surgical Team (1)

- **The Mythical Man-Month (Fred Brooks, 1975)**
  - **프로그래머들의 실력에 따라서 생산성은 10배까지, 효율성은 5배까지 차이가 난다.**
    - *다양한 실력의 프로그래머들로 이루어진 큰 팀*
      - i.e. The Mythical Man-Month
    - *베테랑 프로그래머들로만 이루어진 작은 팀*
      - 큰 프로젝트를 수행하기에 너무 오랜 시간을 필요로 한다.

---

### Rule: The Surgical Team (2)

- **Mills's Proposal: The Surgical Team**
  - 외과 팀처럼 작은 팀들로 나눠서 프로젝트를 수행하자.
    - 베테랑 프로그래머 한 명과 이를 보조하는 프로그래머 여러 명으로 이루어진 팀
    - Surgeon, Assistant Surgeon, Anesthetist, Nurses, etc.
- **Advantages**
  - Surgeon과 copilot이 모든 코드의 디자인을 인식하고 있기에 일관성을 유지할 수 있다.
  - 의견 충돌이 발생할 경우에는 surgeon이 결정을 내릴 수 있기 때문에 의사 결정이 빠르다.
  - Surgeon들의 의견만 모으면 되므로 생산성이 높아진다.
    - 수 백명이 투입되는 큰 프로젝트라 하더라도.

---

### Rule: The Surgical Team (3)

- **Note: 소프트웨어 개발은 민주적인 활동이 아니다.**
  - 모든 개발자들의 의견을 수렴한 코드는 일관성이 떨어진다.
  - 의견 충돌이 발생할 경우에는 결정을 내릴 수 있는 사람이 필요하다.
  - 즉, 팀원들은 surgeon의 결정을 따라야만 하며 surgeon은 그 결정에 책임을 져야 한다.

---

### Rule: 컨벤션은 초석이다

- **일관된 스타일과 규칙은 협업을 쉽게 만든다.**
  - 동일한 컨벤션을 따르는 코드는 대화하기 쉽다.
  - Merge Conflict를 줄일 수 있다.
  - 코드를 수정하거나 기능을 추가할 때 이해하기 쉬워진다.
- **Examples**
  - Conventional Commits, Semi-linear History, PEP8, Google Python Style Guide, Airbnb JavaScript Style Guide, etc.
- **Tools**
  - Black, Prettier, ESLint, etc.

---

```yaml
layout: leaflet
```

## Conclusion

> 결론

---

### Summary: Clean Code

- **좋은 코드는 읽기 좋은 코드이다.**
- **읽기 좋은 코드는 거짓말을 하지 않는 코드이다.**
  - 변수나 함수의 이름은 기능을 정확하게 나타내야한다.
  - 함수는 하나의 역할만 수행해야한다.
- **읽기 좋은 코드는 특정 컨텍스트에 갇히지 않는 코드이다.**
  - 전역변수나 클래스는 코드의 확장성을 낮춘다.

---

### Summary: Collaboration

- **낙천주의는 금물이다.**
  - 모든 문제는 낙천적인 일정 산정에서 비롯된다.
- **The Mythical Man-Month**
  - 맨먼스 단위로 투입된 프로젝트 비용과 작업 진척도는 연관되어 있지 않다.
- **The Surgical Team**
  - 외과 팀처럼 작은 팀들로 나눠서 프로젝트를 수행하되 Surgeon의 결정을 따르자.
- **컨벤션은 초석이다.**
  - 일관된 스타일과 규칙을 따르자.

---

```yaml
layout: disclaimer
```

# Clean Code

<!-- _class: disclaimer -->
<!-- header: "" -->
<!-- footer: "" -->
<!-- paginate: false -->

> 틀린 코드 찾기

**Disclaimer** This document is intended solely for seminar series within the POSTECH PLUS. Any use of its contents outside of this context is not endorsed or supported by us. We explicitly disclaim any responsibility for the application or interpretation of the information contained herein beyond our organization's boundaries.

- <img src="./public/wordmark-postech.svg" style="height:1rem; margin-top:8px;" />
- Minjae Gwon
  - <minjae.gwon@postech.ac.kr>
  - <https://bxta.kr>
- PLUS
  - <https://plus.or.kr>
