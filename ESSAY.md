# Final Project Essay

Answer all 10 questions.

Each question is worth **1 point**.

Total: **10 points**

Your responses should be concise but specific. When a question asks about your
implementation or testing, discuss what you actually built rather than giving
only a general definition.

---

## 1. Why a Class?

Why is `StudentRecord` appropriately represented as a class rather than as only
a collection of unrelated functions and variables?

In your answer, discuss:

- state;
- behavior; and
- ownership of responsibility.

### Response

_Write your response here._

---

## 2. Object State and Independent Instances

What state belongs to each `StudentRecord` object?

Then describe a concrete example from your testing that demonstrates that two
different `StudentRecord` objects maintain independent state even though both
were created from the same class definition.

### Response

_Write your response here._

---

## 3. Encapsulation

Why should outside programmers use methods such as:

```text
add_score()
update_score()
remove_score()
get_scores()
```

instead of directly manipulating `_scores`?

Explain one specific problem that direct access could create and how your public
interface protects the object's state.

### Response

_Write your response here._

---

## 4. Public Interface and Contract

Choose **one public method** other than a simple getter.

Describe its complete contract:

- what information enters the method;
- what result it returns;
- whether it changes object state;
- what causes it to fail; and
- what must remain true when it fails.

### Response

_Write your response here._

---

## 5. Searching

Explain how your `find_score()` implementation locates an assignment.

Your answer must discuss:

- why the search is a linear search;
- what condition causes the search to stop;
- what happens when the assignment is not present; and
- the time complexity of the search.

### Response

_Write your response here._

---

## 6. Sorting

Explain how Selection Sort is used in your class.

Discuss both:

```text
sort_by_assignment()
sort_by_score()
```

and explain:

- what each method sorts by;
- the required order for each;
- how Selection Sort gradually builds the sorted region; and
- the time complexity of Selection Sort.

### Response

_Write your response here._

---

## 7. Object References

Describe one test in which two variables refer to the **same**
`StudentRecord` object.

Explain:

- how the second reference was created;
- what state-changing operation you performed; and
- why the change was visible through both variables.

Then distinguish this from having two separate `StudentRecord` objects.

### Response

_Write your response here._

---

## 8. State-Based Testing

Describe your strongest test that moves one `StudentRecord` through several
operations.

Identify:

- the important starting state;
- the sequence of operations;
- the state transitions or changes you expected;
- at least one invariant you verified; and
- why this test provides more evidence than testing each operation only in
  isolation.

### Response

_Write your response here._

---

## 9. Verification and Evidence

What does passing your complete test suite give you reasonable confidence
about?

What does it **not prove**?

In your answer, discuss why testing provides structured evidence about software
behavior rather than absolute proof that no defect exists.

### Response

_Write your response here._

---

## 10. AI and Engineering Judgment

Identify one meaningful suggestion, implementation idea, test idea, or design
choice proposed by generative AI during this project.

State whether you:

```text
accepted it
modified it
or rejected it
```

Then explain the engineering reason for your decision.

Your response should demonstrate that you, rather than the AI system, made the
final design or verification judgment.

### Response

_Write your response here._
