---
theme: ../../../../themes/blue
titleTemplate: '%s'
author: Minjae Gwon
keywords: Clean Code,Collaboration
presenter: false
download: true
exportFilename: /clean-code-english/talks/clean-code-english/dist
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
  brandImage: "/clean-code-english/wordmark-postech.svg"
  brandImageWhite: "/clean-code-english/wordmark-postech-white.svg"
  brandText: "POSTECH"
htmlAttrs:
  dir: ltr
  lang: en
layout: cover
---

# Clean Code

> A Journey to Clean Code and Collaboration

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

> What is Clean Code?

---

### What is Clean Code?

- Code written in a concise single line for the main logic
- Code with detailed comments to make it easier for others to read
- Code where each concept has its corresponding class fully implemented
- Code written with 100% test coverage

---

### That's Not Clean Code

- ~~Code written in a concise single line for the main logic~~
  - The more critical the logic, the more it should be **written in an easy-to-read manner** to improve **maintainability**.
- ~~Code with detailed comments to make it easier for others to read~~
  - Comments can interfere with code interpretation. It's better to **write code that explains itself**.
- ~~Code where each concept has its corresponding class fully implemented~~
  - Classes always increase project complexity. **Simpler code** saves the day.
- ~~Code written with 100% test coverage~~
  - Does high test coverage really mean good code?

---

### What is Really Clean Code?

- Readability. Readability. Readability.
  - Maintainable code, code with fewer bugs, simple code, ...
  - All of these mean **readable code**.

---

### Why Clean Code?

- Readable code improves maintainability.
  - It makes it easier to understand each other's work.
- Readable code reduces bugs.
  - Logical bugs can be identified much faster.
- Readable code accelerates work speed.
  - Communication costs are the largest costs in collaboration.
  - We communicate through code.
  - If code is easy to read, communication costs are reduced.

---

```yaml
layout: leaflet
```

## Code

> Toward Readable Code

---

### Rule: Long Names are Better than Short Names (1)

- Variable or function names should be long enough to explain themselves.
  - Abbreviations should especially be avoided.
  - In an era of auto-completion, there's no need to fear long names.
- Clean Code (Martin, Robert C, 2008)
  - Even if the name is long, choose descriptive names.
  - Long names are better than short and hard-to-understand ones.
  - Descriptive names clarify design and make code easier to improve.

---

### Rule: Long Names are Better than Short Names (3)

- Clean Code (Martin, Robert C, 2008)
  - The length of the name doesn't affect code simplicity.
  - Naming just to avoid compiler complaints or by adding noise words is inappropriate.
    - For example, appending consecutive numbers to avoid name duplication in the same namespace doesn't convey the intent.
  - Including meaningless words like `variable` or `string` is not helpful.
    - The name should make it clear to the reader what the difference is.
  - Easily pronounceable names are easier to process mentally, and hard-to-pronounce names make discussions difficult.

---

### Rule: Long Names are Better than Short Names (4)

```python
def some_function(a, cfg):
    # It's unclear what 'a' or 'cfg' mean.
    # cfg? configuration? context free grammar?
```

```python
def to_number(data: bytes) -> int:
    # It's unclear what is being converted. How about `bytes_to_int`?
    # ...
    return result
```

---

### Rule: Long Names are Better than Short Names (5)

```python
def select_variable_or_empty(...): # It's unclear what this function selects.
  # A good name should let you understand the function's role without looking at the logic.
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

### Rule: Self-Explaining Code is Better than Comments (1)

- Comments can actually harm code interpretation.
  - Comments can distort the intention of the code.
  - Inconsistent comments are misleading to the reader.
- If a comment is necessary, consider whether it’s time to refactor the code into "self-explaining functions."
  - Function names can serve the role of comments.
- Clean Code (Martin, Robert C, 2008)
  - Instead of trying to explain unclear code with comments, it's better to clean up the code.
  - In most cases, the code alone can express its intention.

---

### Rule: Self-Explaining Code is Better than Comments (2)

```python
def calculate_total(order):
    total = 0
    for item in order:
        if item.type == "food": # Add quantity-multiplied price for food items
            total += item.price * item.quantity 
        else: # For drinks, just add the price
            total += item.price * 2 
    tax = total * 0.2  # Calculate tax (10%)
    return total + tax # Add tax to total
```

---

### Rule: Self-Explaining Code is Better than Comments (3)

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

### Rule: Don’t Use or Return Null

- Clean Code (Martin, Robert C, 2008)
  - *Don't Return Null*
    - Returning `null` increases the code you need to write and passes responsibility to the caller.
    - If an external library returns `null`, wrap it and throw an exception or return a special case object.
  - *Don't Pass Null*
    - Unless your language is designed for `null`, avoid passing `null` arguments as much as possible.

---

### Rule: Error Codes Make Life Hard for the Caller

- Clean Code (Martin, Robert C, 2008)
  - It's better to throw exceptions rather than return error codes, which keeps the caller code clean.
  - This allows separating business logic from error-handling logic.
  - Providing context with exceptions helps to understand the intent of the code.

---

### Rule: Assert Generously (1)

- Express pre-conditions and post-conditions of code sections using assertions.
  - Reduces mistakes and improves readability.
- Helps create self-explaining code.
  - Alerts the reader to the intent of the code.
- Similar to writing test cases.
  - Improves code quality.

---

### Rule: Assert Generously (2)

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

### Rule: Don’t Reuse Names (1)

- Reusing names deceives the reader.
  - Just because a name is reused doesn’t mean it serves the same role.
  - Assuming reused names serve the same purpose is risky.
- Reused names are dangerous for the writer as well.
  - They make bugs harder to find.

---

### Rule: Don’t Reuse Names (2)

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

### Rule: The Same Name Must Represent the Same Concept (1)

- The same name must refer to the same concept.
  - If the same name refers to different concepts, it deceives the reader.
  - It severely damages readability, leading to poor maintainability.

---

### Rule: The Same Name Must Represent the Same Concept (2)

- Clean Code (Martin, Robert C, 2008)
  - Stick to one word for one abstract concept.
    - For example, mixing `get`, `fetch`, and `retrieve` causes confusion.
  - Consistent vocabulary makes code easier to read.
  - Using the same word for different purposes is just wordplay.
  - Adopting a word for consistency when it's not in the same context causes confusion.

---

### Rule: The Same Name Must Represent the Same Concept (3)

```python
for send_variable in send_variables:
    min_difference = 0x100000000 # `difference` here means `absolute value`
    min_variable = None
    for recv_variable in recv_variables:
        difference = send_variable.value - recv_variable.value
        # `difference` here means `difference`
        if abs(difference) < min_difference:
            min_difference = abs(difference)
            min_variable = recv_variable
```

---

### Rule: Don't Lie (1)

- Misnamed variables or functions are lies.
  - Incorrectly named variables or functions deceive the reader.
  - This seriously harms readability, resulting in lower maintainability.
- Clean Code (Martin, Robert C, 2008)
  - Misleading cues make code harder to understand.
  - For example, using widely understood words in a different sense can mislead readers.
  - Similarly, using nearly identical names makes it difficult for readers to follow the code.

---

### Rule: Don't Lie (2)

```python
def try_decode_hex(payload: bytes) -> list[bytes]:
    # The name `try` typically suggests a function that might throw an exception.
    pattern = re.compile(rb"([0-9a-fA-F]+)")

    decoded_payloads: list[bytes] = []
    for hex_string in pattern.findall(payload):
        decoded_payloads.append(bytes.fromhex(hex_string.decode()))

    return decoded_payloads
```

---

### Rule: Keep Function Arguments to a Minimum

- Clean Code (Martin, Robert C, 2008)
  - The fewer arguments, the better.
  - If you're passing arguments, make sure it serves a clear purpose, such as transforming the input or triggering an event.
  - Functions should generally avoid having more than two or three arguments.
    - Binary functions are harder to understand than unary, and ternary functions are even more difficult.
    - If more arguments are needed, consider grouping them into an object.

---

### Rule: A Function Should Do Only One Thing (1)

- A function doing multiple things is as bad as lying.
  - A function performing multiple tasks proves that it needs to be split.
  - A function doing multiple tasks has too much responsibility.
- Clean Code (Martin, Robert C, 2008)
  - A function should do one thing, and do it well.
  - If you can extract meaningful functions with different names, then the function is doing too many tasks.
  - Flag arguments imply that the function is handling more than one task, and this is a sign of poor design.
  - Avoid mixing state changes and information returns in the same function.
    - It's better to separate commands and queries to eliminate confusion.

---

### Rule: A Function Should Do Only One Thing (2)

```python
def process_order(order): # Lacks reusability.
    total_with_tax = total + tax
    
    # Print order details
    print("Order Details:")
    print(f"Total: {total_with_tax}")
    
    # Send confirmation email
    send_order_confirmation_email(order, total_with_tax)
```

---

### Rule: Side Effects are the Root of All Evil

- Clean Code (Martin, Robert C, 2008)
  - Side effects make functions dependent on time, causing them to depend on execution order.
  - Time-dependent functions should clearly indicate this in their names.
  - Avoid output arguments as much as possible.

---

### Rule: Immutable Variables are Better (1)

- Constructing logic where variable values don't change is the fastest way to reduce bugs.
  - If a change is necessary, it's better to copy and assign to a new variable simultaneously.
    - We no longer live in a time of limited memory.

---

### Rule: Immutable Variables are Better (2)

```python
def get_unused_offsets_or_empty(
    used_offsets: list[tuple[int, int]], total_range: range
) -> list[tuple[int, int]]:
    used_offsets.sort()
    # .sort() changes the original list.
    # This causes an unexpected side effect for the caller.
    # So instead of using .sort(), it's better to create and use a new sorted list.
```

---

### Rule: Global Variables Kill Code

- Global variables limit code extensibility.
  - Business logic becomes trapped in the context of global variables.
  - Business logic confined to a specific context is hard to reuse.
- Small changes can snowball into larger issues.
  - It's hard to track where and how global variables are being used.
  - Dependencies become difficult to manage.
  - Global variables lead to unpredictable values being relied upon.

---

### Rule: Think Twice Before Creating a Class (1)

- Classes limit code extensibility.
  - Classes fundamentally **trap business logic in context.**
  - Business logic confined to a class is harder to reuse.
- Try implementing business logic as standalone functions instead of as methods within classes.
  - General functions can be used anywhere, as long as they don't rely on global variables.

---

### Rule: Think Twice Before Creating a Class (2)

```python
class ShoppingCart:
    def __init__(self, items: list[Item], tax_rate: float):
        self.items = items
        self.tax_rate = tax_rate

    def calculate_total_price(self): # Is it necessary to make this a method?
        total = sum(item.price for item in self.items)
        tax = total * self.tax_rate
        return total + tax
```

---

### Rule: Think Three More Times Before Inheriting

- Inheritance is like using global variables.
  - Inherited classes rely on resources from parent classes.
  - Changes in parent classes affect child classes.
    - This causes effects similar to those of using global variables.
  - It becomes difficult to track where changes will propagate.
- The deeper the inheritance, the more complexity and less extensibility.
  - The code becomes harder to understand.
  - The code becomes harder to modify.

---

### Rule: Maintain Appropriate Function Length (1)

- Long functions reduce readability.
  - Split functions before they get too long.
  - Unlike classes, there's no need to avoid having many functions.
    - It doesn't greatly affect extensibility.
- Clean Code (Martin, Robert C, 2008)
  - The first rule for creating functions is that they should be small.
  - Functions that have deep nesting structures are hard to read and understand.
  - Moreover, blocks inside `if`, `else`, or `while` statements should also be small.

---

### Rule: Maintain Appropriate Function Length (2)

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

### Rule: Maintain Appropriate Function Length (3)

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

### Rule: Code Grows Upward (1)

- Humans read code from top to bottom.
- Thus, it makes sense to place more abstract code higher up.
  - The reader will first encounter more abstract code.
    - This helps to better grasp the intent of the code.
  - Code at higher abstraction levels expresses the intent of the code better.
- Clean Code (Martin, Robert C, 2008)
  - All statements in a function should be at the same level of abstraction.
  - Mixing abstraction levels within a function makes it hard to understand.
  - It's better to decrease the level of abstraction step-by-step as you move down the code.

---

### Rule: Code Grows Upward (2)

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

### Rule: Group Related Code (1)

- Keep definitions and references close to each other.
  - If definitions and their usage are far apart, the code becomes harder to understand.
- Place calling functions and the functions being called close together.
  - If the function calls are too far from the definitions, it makes the code harder to follow.

---

### Rule: Group Related Code (2)

```python
        suspicious_stream_numbers: set[int] = set()
        suspicious_pcaps: list[str] = list() # Where is suspicious_pcaps used?

        for packet in tmp_pcap:
            # ... 100 lines of code

        # The code using suspicious_stream_numbers is too far away.
        for stream_number in suspicious_stream_numbers:
            # ...
```

---

```yaml
layout: leaflet
```

## Collaboration

> The Mythical Things

---

### Rule: Optimism is Dangerous

- The Mythical Man-Month (Fred Brooks, 1975)
  - **All problems arise from optimistic scheduling.**
    - The assumption that all tasks will be completed on time is a surefire way to ruin programming schedules.
    - Because software is so flexible, programmers often mistakenly believe there will be no difficulties.
    - Large software projects composed of many tasks are highly unlikely to proceed on schedule.

---

### Rule: The Mythical Man-Month (1)

- The Mythical Man-Month (Fred Brooks, 1975)
  - **The cost of a project in man-months has no direct correlation with progress.**
    - This correlation only exists when multiple people can work independently without communication.
    - If tasks are interdependent, no amount of extra effort will reduce the overall time required.
    - While tasks can be divided, the cost of communication must be factored in.
    - The communication overhead of adding more people can actually increase the time needed to complete the project.

---

### Rule: The Mythical Man-Month (2)

- The Mythical Man-Month (Fred Brooks, 1975)
  - **You can’t create a healthy schedule by adding more people or shortening deadlines.**
    - The project timeline is determined by the interdependencies of internal tasks.
    - The maximum number of people that can be added is determined by the number of independent tasks.
    - If a milestone is missed:
      - You can add more people, reschedule, or reduce the scope of the work.
    - If you add more people without changing the schedule:
      - The cost of training and communication can delay project completion even further.

---

### Rule: The Surgical Team (1)

- The Mythical Man-Month (Fred Brooks, 1975)
  - **Programmer productivity can vary by up to 10x, and efficiency by up to 5x.**
    - A team with varying skill levels (as described in *The Mythical Man-Month*) will face communication challenges.
    - A small team of veteran programmers, on the other hand, may take too long to complete large projects.

---

### Rule: The Surgical Team (2)

- Mills's Proposal: The Surgical Team
  - Break large projects into small teams similar to a surgical team.
    - One veteran programmer (the "surgeon") is assisted by several supporting programmers.
    - Roles include: Surgeon, Assistant Surgeon, Anesthetist, Nurses, etc.
- Advantages
  - The surgeon and co-pilot are familiar with all the code's design, maintaining consistency.
  - When disagreements arise, the surgeon makes decisions, allowing for quick resolutions.
  - Productivity increases because only the surgeons' opinions need to be gathered, even on large projects involving hundreds of people.

---

### Rule: The Surgical Team (3)

- Note: Software development is not a democratic activity.
  - Code designed by consensus often lacks consistency.
  - When disagreements occur, there must be a designated person to make final decisions.
  - In other words, team members must follow the surgeon's decisions, and the surgeon is responsible for those decisions.

---

### Rule: Convention is the Foundation

- Consistent style and rules make collaboration easier.
  - Code that follows the same conventions is easier to communicate through.
  - Merge conflicts are minimized.
  - Understanding code for modification or feature addition becomes easier.
- Examples
  - Conventional Commits, Semi-linear History, PEP8, Google Python Style Guide, Airbnb JavaScript Style Guide, etc.
- Tools
  - Black, Prettier, ESLint, etc.

---

```yaml
layout: leaflet
```

## Conclusion

> Summary

---

### Summary: Clean Code

- Good code is readable code.
- Readable code doesn’t lie.
  - Variable and function names should accurately represent their functionality.
  - A function should only do one thing.
- Readable code isn’t trapped in a specific context.
  - Global variables and classes reduce code extensibility.

---

### Summary: Collaboration

- Optimism is dangerous.
  - All problems arise from optimistic scheduling.
- The Mythical Man-Month
  - The cost in man-months is not directly related to the progress of the project.
- The Surgical Team
  - Break large projects into small teams, following the decisions of the "surgeon."
- Convention is the foundation.
  - Consistent style and rules foster collaboration.

---

```yaml
layout: disclaimer
hideInToc: true
```

# Clean Code

> A Journey to Clean Code and Collaboration

**Disclaimer** This document is intended solely for seminar series within the POSTECH PLUS. Any use of its contents outside of this context is not endorsed or supported by us. We explicitly disclaim any responsibility for the application or interpretation of the information contained herein beyond our organization's boundaries.

- <img src="./public/wordmark-postech-white.svg" style="height:1rem; margin-top:8px;" />
- Minjae Gwon
  - <minjae.gwon@postech.ac.kr>
  - <https://bxta.kr>
- PLUS
  - <https://plus.or.kr>
