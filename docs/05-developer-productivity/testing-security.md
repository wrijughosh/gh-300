# Supporting Testing and Security

GitHub Copilot provides strong support for test generation, identifying edge cases, writing assertions, and improving code security and performance.

---

## Generating Unit Tests

### The `/tests` Command
Select a function or class and use:
```
/tests
```
Copilot will generate a suite of unit tests including common cases, edge cases, and basic error cases.

### Chat-Based Test Generation
For more control, use Chat with specific requirements:
```
"Generate pytest unit tests for the calculate_discount() function.
Include tests for:
- Normal discount calculation (10%, 20%, 50%)
- Zero discount
- 100% discount (free item)
- Invalid inputs: negative percentages, percentages > 100, non-numeric types
- Boundary values: 0.001%, 99.999%"
```

### Example – Generating Tests for a Python Function

**Original function**:
```python
def calculate_discount(price: float, discount_percent: float) -> float:
    """Calculate the discounted price."""
    if not isinstance(price, (int, float)) or not isinstance(discount_percent, (int, float)):
        raise TypeError("Price and discount must be numeric")
    if discount_percent < 0 or discount_percent > 100:
        raise ValueError("Discount must be between 0 and 100")
    return price * (1 - discount_percent / 100)
```

**Copilot-generated tests**:
```python
import pytest
from pricing import calculate_discount

class TestCalculateDiscount:
    def test_normal_discount(self):
        assert calculate_discount(100.0, 20.0) == pytest.approx(80.0)

    def test_zero_discount(self):
        assert calculate_discount(100.0, 0.0) == pytest.approx(100.0)

    def test_full_discount(self):
        assert calculate_discount(100.0, 100.0) == pytest.approx(0.0)

    def test_negative_discount_raises(self):
        with pytest.raises(ValueError):
            calculate_discount(100.0, -1.0)

    def test_discount_over_100_raises(self):
        with pytest.raises(ValueError):
            calculate_discount(100.0, 101.0)

    def test_non_numeric_price_raises(self):
        with pytest.raises(TypeError):
            calculate_discount("100", 20.0)

    def test_non_numeric_discount_raises(self):
        with pytest.raises(TypeError):
            calculate_discount(100.0, "20")
```

---

## Generating Integration Tests

### What Are Integration Tests?
Integration tests verify that multiple components work together correctly, including interactions with databases, APIs, and external services.

### Generating Integration Tests with Copilot
```
"Write an integration test for the user registration endpoint.
Use pytest and pytest-httpx for mocking HTTP calls.
The test should:
1. POST to /api/users with valid user data
2. Assert the response is 201 Created
3. Assert the response body contains the new user's ID
4. Assert the user exists in the test database
5. Clean up the test user after the test"
```

### Scaffolding Test Setup
Copilot can generate test configuration and fixtures:
```
"Generate a pytest conftest.py for testing a Flask application with PostgreSQL.
Include fixtures for:
- A test database that is created and destroyed per test session
- A Flask test client
- A database session fixture with rollback after each test
- A fixture that seeds the database with 5 test users"
```

---

## Identifying Edge Cases

### Asking Copilot to Find Edge Cases
One of the most valuable testing use cases is using Copilot to identify edge cases you might have missed:

```
"What edge cases should I test for this URL parsing function?"
```

```
"Review this sorting function and identify any inputs that could cause incorrect behavior or exceptions"
```

### Common Edge Cases Copilot Identifies
- Empty collections (empty list, empty string, empty dict)
- `None` / `null` inputs
- Boundary values (0, -1, max integer, max float)
- Unicode and special characters
- Concurrent access scenarios
- Network timeout and error scenarios
- Very large inputs (performance edge cases)
- Negative numbers where positive are expected

### Example Prompt for Edge Case Discovery
```
"List all edge cases that should be covered in tests for a function that:
- Takes a start date and end date
- Returns the number of business days between them
- Should handle: different timezones, DST transitions, 
  public holidays, same-day inputs, reversed date order"
```

---

## Writing Assertions

### Generating Precise Assertions
Copilot can help write assertions that go beyond simple equality checks:

```
"Add assertions to this test to verify:
1. The returned list is sorted by last_name ascending, then first_name ascending
2. All email fields match the format user@domain.tld
3. No two users share the same ID
4. The created_at timestamp is within the last 5 seconds"
```

### Property-Based Test Assertions
```
"Using hypothesis library, write property-based tests for the encode/decode 
function pair. The key property to assert: encode(decode(x)) == x for any valid input"
```

---

## Suggesting Security Improvements

### Security Review via Chat
Select code and use:
```
"Review this code for security vulnerabilities and suggest fixes"
```

### Common Security Issues Copilot Identifies

| Vulnerability | Example Prompt |
|---|---|
| SQL Injection | "Is this SQL query vulnerable to injection? How should it be fixed?" |
| XSS | "Review this HTML template rendering for cross-site scripting vulnerabilities" |
| Insecure cryptography | "Is SHA1 appropriate for password hashing here? What should I use instead?" |
| Hard-coded secrets | "Identify any hard-coded credentials in this file and show how to externalize them" |
| Missing input validation | "What input validation is missing from this API handler?" |
| Insecure deserialization | "Is it safe to use pickle.loads() here? What are the risks?" |

### Example Security Improvement

**Before (vulnerable)**:
```python
def get_user(user_id):
    query = f"SELECT * FROM users WHERE id = {user_id}"
    return db.execute(query)
```

**Copilot prompt**: "This SQL query is vulnerable to injection. Fix it using parameterized queries."

**After (secure)**:
```python
def get_user(user_id):
    query = "SELECT * FROM users WHERE id = %s"
    return db.execute(query, (user_id,))
```

---

## Performance Optimizations

### Identifying Performance Bottlenecks
```
"Review this function that processes a list of 10,000 records and identify performance issues"
```

```
"What is the time complexity of this algorithm? Can it be improved?"
```

### Common Performance Suggestions from Copilot
- Replace O(n²) nested loops with hash-based lookups
- Use generators instead of creating full lists in memory
- Cache expensive computations with `functools.lru_cache`
- Use bulk database operations instead of per-row queries
- Add database indexes for frequently queried columns
- Use async/concurrent patterns for I/O-bound operations

### Example Performance Improvement

**Before (O(n²))**:
```python
def find_duplicates(items):
    duplicates = []
    for i, item in enumerate(items):
        for j, other in enumerate(items):
            if i != j and item == other and item not in duplicates:
                duplicates.append(item)
    return duplicates
```

**Copilot prompt**: "Optimize this function to find duplicates more efficiently"

**After (O(n))**:
```python
def find_duplicates(items):
    seen = set()
    return list({item for item in items if item in seen or seen.add(item)})
```

---

## Key Takeaways

- Use `/tests` or Chat to generate unit tests covering normal cases, edge cases, and error conditions.
- Copilot can scaffold integration tests including database setup, client fixtures, and teardown.
- Ask Copilot explicitly to identify edge cases—it often catches scenarios you might miss.
- Security improvements can be prompted with targeted questions about specific vulnerability classes.
- Performance optimization is a conversation: ask about complexity, then ask for improvements.

---

[← Back to Developer Productivity](README.md)
