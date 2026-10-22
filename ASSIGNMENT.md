# Final Project — StudentRecord Component

## Scenario

This final project is based on a common real-world software-development task.

You are **not** being asked to build an entire application from scratch.

Another development team is building a larger academic management system. That
system needs a reusable component that represents **one student's course record**
and manages that student's assignment scores.

Your assignment is to design, implement, document, and verify that component.

Conceptually, the primary software deliverable is the `StudentRecord` class.

Your `main.py` file is your testbed. Your `test.py` file is the verification
environment you create to prove that your class works.

This reflects how software is often developed professionally: a programmer or
team may be responsible for one class, library, subsystem, service, or other
component that will later be integrated into a larger system.

Use [the example repo](https://github.com/alexander-katrompas/OOP-Python-simple-example) to help you develop your solution.

---

# Project Goal

Implement a reusable `StudentRecord` class that:

- stores one student's identity and assignment scores;
- protects its internal state behind a public interface;
- supports adding, updating, removing, finding, and inspecting scores;
- calculates useful results from its score collection;
- implements explicit searching and sorting algorithms;
- supports many independent objects created from the same class; and
- is verified by a substantial test suite that you design and own.

The project must contain **exactly one class**:

```text
StudentRecord
```

Do not create additional classes.

---

# Required Repository Structure

Your repository must contain:

```text
.
├── ASSIGNMENT.md
├── ESSAY.md
├── README.md
├── .gitignore
├── main.py
├── student_record.py
└── test.py
```

The three Python files have distinct responsibilities.

## `student_record.py`

Contains the `StudentRecord` class.

This is the primary software product you are delivering.

## `test.py`

Contains the verification suite that you design for `StudentRecord`.

The test module must construct and exercise many different `StudentRecord`
objects and verify both normal and failure behavior.

## `main.py`

Runs the test suite.

It is not an application interface and must not contain a menu, user-input
workflow, or separate application logic.

---

# Part 1 — The `StudentRecord` Object

A `StudentRecord` represents **one student in one course**.

Each object owns:

```text
student ID
student name
assignment scores
```

The class definition is shared, but every object maintains its own independent
state.

For example:

```python
student1 = StudentRecord("S1001", "Maria Lopez")
student2 = StudentRecord("S1002", "Daniel Kim")
```

Both objects use the same class definition, but changing the scores in
`student1` must not change the scores in `student2`.

---

# Part 2 — Required Internal State

Each `StudentRecord` object must use the following non-public instance
attributes:

```python
self._student_id
self._student_name
self._scores
```

`_scores` must be a list of tuples.

Each tuple represents one assignment:

```text
(assignment_id, score)
```

Example:

```python
[
    ("A01", 92.0),
    ("A02", 87.0),
    ("A03", 95.0),
]
```

The student ID and student name are established when the object is created.

The score collection begins empty.

Outside code must not directly access or modify `_student_id`, `_student_name`,
or `_scores`.

Use the public interface instead.

---

# Part 3 — Required Public Interface

Implement the following public methods exactly.

| Method | Parameters | Return | Required purpose |
|---|---|---|---|
| `__init__` | `student_id`, `student_name` | `None` | initialize one empty student record |
| `get_student_id` | none | student ID | return the object's student ID |
| `get_student_name` | none | student name | return the object's student name |
| `get_scores` | none | list | return a copy of the score collection |
| `add_score` | `assignment_id`, `score` | `bool` | add a valid new assignment score |
| `update_score` | `assignment_id`, `score` | `bool` | replace an existing score |
| `remove_score` | `assignment_id` | `bool` | remove an existing assignment |
| `find_score` | `assignment_id` | tuple or `None` | find one assignment using linear search |
| `calculate_average` | none | `float` | calculate the arithmetic mean |
| `find_highest_score` | none | tuple or `None` | return the highest assignment score |
| `find_lowest_score` | none | tuple or `None` | return the lowest assignment score |
| `sort_by_assignment` | none | `None` | Selection Sort by assignment ID ascending |
| `sort_by_score` | none | `None` | Selection Sort by score descending |

Do not rename these methods or change their required parameters.

You may create private helper methods when they improve the design.

A helper method name should begin with a single underscore.

---

# Part 4 — Construction and Identity

The constructor must accept:

```python
StudentRecord(student_id, student_name)
```

Example:

```python
record = StudentRecord(
    "S1001",
    "Maria Lopez",
)
```

After construction:

```text
student ID = S1001
student name = Maria Lopez
scores = empty
```

The object must provide:

```python
get_student_id()
get_student_name()
```

There are no public methods for changing the student's identity after
construction.

---

# Part 5 — Encapsulation and `get_scores()`

`_scores` is internal state.

Outside code must not do this:

```python
record._scores.append(...)
```

Instead, all changes must occur through the class's public methods.

`get_scores()` must return a **copy** of the internal list.

This is required:

```python
external_scores = record.get_scores()
external_scores.append(("A99", 100.0))
```

The operation above must **not** add `A99` to the `StudentRecord`.

The caller may change the returned list, but the object's internal state must
remain protected.

---

# Part 6 — Adding Scores

Implement:

```python
add_score(assignment_id, score)
```

A score may be added only when:

1. the assignment ID is not already present in the record; and
2. the score is numeric; and
3. the score is between `0` and `100`, inclusive.

Valid scores include both boundaries:

```text
0
100
```

Accept normal integer or floating-point numeric values.

A Boolean value is **not** a valid score.

A successful addition:

- stores the score as a floating-point value;
- leaves the assignment ID unchanged; and
- returns `True`.

An invalid addition:

- makes no change to the object; and
- returns `False`.

Examples:

```python
record.add_score("A01", 88)       # True
record.add_score("A02", 100.0)    # True
record.add_score("A01", 75)       # False — duplicate ID
record.add_score("A03", -1)       # False
record.add_score("A04", 101)      # False
record.add_score("A05", "90")     # False
```

---

# Part 7 — Searching

Implement:

```python
find_score(assignment_id)
```

The method must use an **explicit iterative linear search**.

Do not use:

```python
list.index()
next()
```

and do not replace the required search with another data structure.

The method returns:

```text
matching (assignment_id, score) tuple
```

when the assignment exists.

It returns:

```python
None
```

when the assignment does not exist.

Example:

```python
record.find_score("A02")
```

might return:

```python
("A02", 87.0)
```

Searching must work regardless of the current order of `_scores`.

A private helper method that performs the linear search is allowed and is often
a good design because several public methods need to locate assignments.

---

# Part 8 — Updating Scores

Implement:

```python
update_score(assignment_id, score)
```

The update succeeds only when:

- the assignment already exists; and
- the replacement score is numeric; and
- the replacement score is between `0` and `100`, inclusive.

On success:

- replace the score for that assignment;
- preserve the assignment ID; and
- return `True`.

On failure:

- preserve the current object state; and
- return `False`.

---

# Part 9 — Removing Scores

Implement:

```python
remove_score(assignment_id)
```

If the assignment exists:

- remove the assignment-score tuple;
- return `True`.

If it does not exist:

- leave the object unchanged;
- return `False`.

---

# Part 10 — Average, Highest, and Lowest

## Average

Implement:

```python
calculate_average()
```

Return the arithmetic mean of all scores.

If the record contains no scores, return:

```python
0.0
```

## Highest

Implement:

```python
find_highest_score()
```

Return the complete assignment-score tuple containing the highest score.

Example:

```python
("A04", 100.0)
```

If the record is empty, return:

```python
None
```

If scores tie, return the first highest score encountered during traversal.

## Lowest

Implement:

```python
find_lowest_score()
```

Return the complete assignment-score tuple containing the lowest score.

If the record is empty, return:

```python
None
```

If scores tie, return the first lowest score encountered during traversal.

Do not sort the collection merely to find the highest or lowest score.

---

# Part 11 — Selection Sort by Assignment

Implement:

```python
sort_by_assignment()
```

This method must perform **Selection Sort** on `_scores`.

Required ordering:

```text
ascending assignment ID
```

Example:

```text
before:
A04, A01, A03, A02

after:
A01, A02, A03, A04
```

The method:

- sorts the object's internal collection in place;
- returns `None`;
- must not create a second class; and
- must not use built-in sorting.

Do not use:

```python
list.sort()
sorted()
```

---

# Part 12 — Selection Sort by Score

Implement:

```python
sort_by_score()
```

This method must also perform **Selection Sort**.

Required ordering:

```text
descending score
```

Example:

```text
before:
71, 95, 84, 60

after:
95, 84, 71, 60
```

The method:

- sorts the internal collection in place;
- returns `None`; and
- must not use built-in sorting.

The relative order of assignments with equal scores is not part of the required
contract.

---

# Part 13 — Multiple Objects and Object References

Your verification code must demonstrate that the class can create and manage
many independent objects.

For example:

```python
first = StudentRecord(...)
second = StudentRecord(...)
```

Changing `first` must not change `second`.

Your tests must also demonstrate object-reference behavior.

For example:

```python
alias = first
```

Now `alias` and `first` refer to the same object.

A state change made through `alias` must be visible through `first`.

This is an important distinction:

```text
two different objects
```

are not the same thing as:

```text
two variables referring to one object
```

---

# Part 14 — `test.py`: Your Verification System

For this project, **you own the test suite**.

You are not merely running instructor-provided tests.

`test.py` must contain:

```python
run_tests()
```

and at least:

```text
10 meaningful test functions
```

whose names begin with:

```text
test_
```

More than 10 tests are allowed.

A test may contain multiple related assertions when those assertions verify one
coherent behavior or state evolution.

Tests must be independent of one another. One test must not rely on another test
having run first.

---

# Part 15 — Automated Construction of Many Objects

Your test system must create a varied collection of `StudentRecord` objects
programmatically.

Do **not** manually write a long sequence such as:

```python
student1 = StudentRecord(...)
student2 = StudentRecord(...)
student3 = StudentRecord(...)
student4 = StudentRecord(...)
```

Instead, define structured test data and traverse it to create objects.

For example, the general form might resemble:

```python
student_data = [
    (
        "S1001",
        "Student One",
        [
            ("A03", 90.0),
            ("A01", 80.0),
        ],
    ),
    ...
]
```

Then write a helper function that:

1. traverses the configuration data;
2. constructs a `StudentRecord`;
3. adds that student's scores through the public interface;
4. stores the completed object in a collection; and
5. returns the collection.

Your automated test population must contain **at least eight differently
configured `StudentRecord` objects**.

Include meaningful variation such as:

- an empty student record;
- a record with one score;
- a record with several scores;
- scores at the `0` and `100` boundaries;
- repeated score values;
- assignment IDs initially out of order; and
- students with different numbers of assignments.

This object population is part of the project, not merely setup code.

---

# Part 16 — Required Test Coverage

Your test suite must provide evidence for all of the following areas.

You may organize these into more than 10 test functions, or combine closely
related requirements into coherent tests.

## 1. Construction and empty state

Verify a newly created object:

- stores the correct student identity;
- begins with no scores;
- has average `0.0`;
- has no highest or lowest score.

## 2. Automated object population

Verify that your test-data system creates many differently configured,
independent objects correctly.

## 3. Add behavior and validation

Test:

- normal scores;
- `0`;
- `100`;
- duplicate assignment IDs;
- scores below `0`;
- scores above `100`;
- nonnumeric values.

Verify failed operations preserve state.

## 4. Searching

Test successful and unsuccessful `find_score()` behavior on unsorted data.

## 5. Update and removal

Test both successful and failed updates and removals.

Verify invalid operations preserve state.

## 6. Average and extremes

Verify:

- averages;
- highest score;
- lowest score;
- empty-state behavior;
- useful boundary cases.

## 7. Sort by assignment

Verify ascending assignment-ID order.

## 8. Sort by score

Verify descending score order.

## 9. Encapsulation

Verify that changing a list returned by `get_scores()` does not change the
object's internal score collection.

## 10. Independent instances

Create at least two different `StudentRecord` objects.

Change one and verify the other remains unchanged.

## 11. Shared object reference

Create a second variable referring to an existing object.

Change the object through one reference and verify the change is visible through
the other.

## 12. Multi-step state evolution

Create at least one test that moves one object through several meaningful
operations, such as:

```text
construct
→ add several scores
→ calculate
→ update
→ calculate again
→ sort
→ remove
→ verify final state
```

This test should verify important invariants throughout the sequence.

---

# Part 17 — `run_tests()`

`test.py` must define:

```python
run_tests()
```

It must execute your complete test suite.

Your test runner should make it easy to determine:

- which tests passed;
- which tests failed; and
- the total number of passing tests.

The exact output format is your design decision.

A failed assertion should not prevent you from identifying which test failed.

---

# Part 18 — `main.py`

`main.py` is the executable testbed for the component.

It must:

- import `run_tests` from `test.py`;
- define `main()`;
- call `run_tests()` from `main()`; and
- use the normal Python run guard.

Conceptually:

```text
main.py
    ↓
run_tests()
    ↓
many StudentRecord objects
    ↓
verification of the delivered class
```

Do not add:

- menus;
- interactive input;
- application workflows;
- file processing; or
- another class.

The purpose of `main.py` is to run your verification environment.

---

# Part 19 — Exactly One Class

The entire project must contain exactly one class:

```text
StudentRecord
```

Do not create:

```text
Assignment
Score
GradeBook
Course
TestRunner
StudentManager
```

or any other class.

This restriction is intentional.

The goal is to demonstrate one well-designed domain class and integrate it with
procedural functions and modules.

Not every noun in a software problem should become a class.

---

# Part 20 — Course Programming Standards

All normal course standards remain in effect.

## Control flow

Do not use:

```python
break
continue
while True
```

Each function or method may contain **no more than one `return` statement**.

## Functions and methods

Use:

- meaningful names;
- explicit parameters;
- clear responsibilities;
- appropriate local variables; and
- no unnecessary global mutable state.

## Type hints

Use appropriate Python type hints for:

- function parameters;
- method parameters;
- return values; and
- important instance attributes.

Type hints communicate the intended interface. They do not replace testing or
runtime logic.

---

# Part 21 — Documentation Standard

Every function and method must use the complete course-standard docstring form.

All four documentation categories must always be present.

```python
"""
Short description.

:param variable_name: description
:raises ExceptionType: condition
:return: description
:note: description
"""
```

When a category does not apply, explicitly write `none`.

Example:

```python
"""
Return the student's name.

:param: none
:raises: none
:return: the student's name
:note: none
"""
```

For multiple parameters, use one `:param variable_name:` field for each
parameter.

Every Python file must also contain an appropriate file-header docstring.

Documentation must describe current behavior accurately.

---

# Part 22 — Encapsulation Standard

Good object-oriented engineering distinguishes between:

```text
public interface
```

and:

```text
internal implementation state
```

The following are non-public:

```python
_student_id
_student_name
_scores
```

`main.py` and `test.py` must not directly access them.

All verification must use the public interface.

Python does not enforce this boundary in the same way some other languages do.
In this course, the single leading underscore communicates the required
engineering boundary, and your code must respect it.

---

# Part 23 — README.md

You must write a professional `README.md` that follows the course README
standards.

At minimum, another programmer should be able to determine:

- what the `StudentRecord` component represents;
- the purpose of the project;
- the required Python version or environment assumptions;
- how to run the verification testbed;
- the project structure; and
- what each project file is responsible for.

The README should document the project, not reproduce `ASSIGNMENT.md`.

---

# Part 24 — Git Requirements

Develop incrementally.

Your repository must contain **at least 15 meaningful development commits** in
addition to the initial Classroom commit.

Commit when a coherent piece of engineering work is complete.

A reasonable history might include work such as:

```text
create StudentRecord state and identity getters
implement score addition and validation
implement linear score search
implement update and remove operations
add average and extreme calculations
implement assignment Selection Sort
implement score Selection Sort
add defensive copy behavior
build automated object configurations
add construction and add tests
add search and mutation tests
add sorting tests
add encapsulation and instance tests
add state evolution test
complete project documentation
```

Do not create meaningless commits solely to reach the minimum.

Test completed work before committing it.

---

# Part 25 — AI Use

Generative AI is allowed and expected.

You may use AI to:

- review the class contract;
- discuss object-oriented design;
- help reason about encapsulation;
- review linear-search logic;
- review Selection Sort;
- help design test cases;
- identify boundary conditions;
- debug failing tests;
- critique your architecture;
- review documentation; and
- help interpret test failures.

You remain responsible for the delivered component.

You must understand:

- why `StudentRecord` is a class;
- what state each object owns;
- how public methods protect internal state;
- how search and sort work;
- why separate objects maintain independent state;
- how object references behave;
- what your tests actually verify; and
- what passing tests do **not** prove.

Do not treat generated code as automatically correct.

Read it, question it, test it, and make the final engineering decisions
yourself.

---

# Part 26 — `ESSAY.md`

Complete all 10 questions in the supplied `ESSAY.md`.

Each question is worth:

```text
1 point
```

Total:

```text
10 points
```

Your answers must refer to your own implementation and testing where requested.

---

# Submission

Submit the HTTPS URL of your final GitHub repository through Blackboard.

Before submitting, verify that the repository contains your final pushed
version.

---

# Final Checklist

Before submission, verify all of the following:

- [ ] The project contains exactly one class: `StudentRecord`.
- [ ] `student_record.py` contains the complete reusable class.
- [ ] `_student_id`, `_student_name`, and `_scores` are treated as non-public state.
- [ ] `_scores` is a list of `(assignment_id, score)` tuples.
- [ ] `get_scores()` returns a defensive copy.
- [ ] Duplicate assignment IDs are rejected.
- [ ] Scores outside `0–100` are rejected.
- [ ] Failed operations preserve object state.
- [ ] `find_score()` uses explicit iterative linear search.
- [ ] `sort_by_assignment()` uses Selection Sort, ascending by assignment ID.
- [ ] `sort_by_score()` uses Selection Sort, descending by score.
- [ ] Neither sort uses `sort()` or `sorted()`.
- [ ] Multiple `StudentRecord` objects maintain independent state.
- [ ] Your tests demonstrate shared object-reference behavior.
- [ ] `test.py` contains at least 10 meaningful test functions.
- [ ] Your test system programmatically constructs at least 8 differently configured objects.
- [ ] Your tests include a meaningful multi-operation state-evolution test.
- [ ] `main.py` runs the test suite and is not an application interface.
- [ ] There is no menu or interactive user input.
- [ ] There are no extra classes.
- [ ] No code uses `break`, `continue`, or `while True`.
- [ ] Every function and method has at most one `return`.
- [ ] Every function and method follows the complete course docstring standard.
- [ ] Type hints are used appropriately.
- [ ] `README.md` follows course standards.
- [ ] At least 15 meaningful development commits are present.
- [ ] `ESSAY.md` contains complete responses to all 10 questions.
- [ ] All final changes are committed and pushed.
