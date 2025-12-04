---
description: Use this skill when writing or reviewing Python tests. Provides pytest patterns for uv workspace monorepos, async testing with pytest-asyncio, mocking strategies, and test organization best practices.
---

# Python Testing Guidelines

## Workspace Structure

Each package in `libs/` has its own `tests/` directory:

```
libs/
├── example-client/
│   ├── src/example_client/
│   ├── tests/
│   │   ├── conftest.py       # Package-specific fixtures
│   │   ├── test_client.py
│   │   └── test_types.py
│   └── pyproject.toml
└── example-utils/
    ├── src/example_utils/
    ├── tests/
    │   ├── conftest.py
    │   └── test_helpers.py
    └── pyproject.toml
```

## Running Tests

```bash
# Run all tests across workspace
poe test

# Run tests for a specific package
pytest libs/example-client/tests/
pytest libs/example-utils/tests/

# Run specific test
pytest libs/example-client/tests/test_client.py -k "test_name"

# Run with options
pytest -x                   # Stop on first failure
pytest --lf                 # Run last failed tests
pytest -v                   # Verbose output
```

## Test Configuration

Each package's `pyproject.toml` can have pytest config, but the root `pyproject.toml` has the shared config:

```toml
[tool.pytest.ini_options]
testpaths = ["tests"]
python_files = ["test_*.py", "*_test.py"]
asyncio_mode = "auto"
addopts = ["--verbose", "--cov=.", "--cov-report=term-missing"]
```

## Naming Conventions

```python
# Test files: test_*.py or *_test.py
# Test classes: class TestFeatureName:
# Test functions: def test_action_expected_result():

# Good names
def test_get_user_returns_valid_model():
def test_update_raises_on_invalid_id():
def test_stream_yields_updates():

# Bad names - avoid
def test_1():
def test_it_works():
```

## Fixtures

### Package-Level Fixtures (conftest.py)

```python
# libs/example-client/tests/conftest.py
import pytest
from unittest.mock import Mock

@pytest.fixture
def mock_api_client():
    """Mock API client for unit tests."""
    client = Mock()
    client.get.return_value = {}
    client.post.return_value = None
    return client

@pytest.fixture
def sample_user_data():
    """Sample user data for testing."""
    return {
        "id": "abc123",
        "name": "Test User",
        "email": "test@example.com",
        "age": 25,
        "is_active": True,
        "preferences": {
            "theme": "dark",
            "notifications": True,
            "language": "en",
        },
        "metadata": {},
    }
```

### Fixture Scopes

```python
@pytest.fixture(scope="session")  # Once per test session
@pytest.fixture(scope="module")   # Once per module
@pytest.fixture(scope="class")    # Once per class
@pytest.fixture(scope="function") # Once per test (default)
```

## Async Testing

pytest-asyncio is configured with `asyncio_mode = "auto"`:

```python
import pytest

async def test_async_operation():
    result = await some_async_function()
    assert result == expected

@pytest.fixture
async def async_resource():
    resource = await create_resource()
    yield resource
    await resource.cleanup()
```

## Mocking

### Basic Mocking

```python
from unittest.mock import Mock, patch, MagicMock

def test_client_get(mock_api_client, sample_user_data):
    mock_api_client.get.return_value = sample_user_data

    from example_client import ExampleClient
    client = ExampleClient.__new__(ExampleClient)
    client._client = mock_api_client

    result = client.get_user("abc123")

    mock_api_client.get.assert_called_once_with(
        "/users/abc123"
    )
```

### Patching External Dependencies

```python
@patch("example_client.client.APIClient")
def test_client_init(mock_client_class):
    from example_client import ExampleClient

    client = ExampleClient("https://api.example.com")

    mock_client_class.assert_called_once_with("https://api.example.com")
```

### Async Mocking

```python
from unittest.mock import AsyncMock

async def test_async_service():
    mock_service = AsyncMock()
    mock_service.fetch.return_value = {"data": "value"}

    result = await function_under_test(mock_service)

    mock_service.fetch.assert_awaited_once()
```

## Parameterized Tests

```python
import pytest

@pytest.mark.parametrize("status,expected", [
    ("pending", True),
    ("processing", True),
    ("completed", False),
    ("failed", False),
])
def test_is_active_status(status, expected):
    assert is_active(status) == expected

@pytest.mark.parametrize("input_data", [
    {"name": ""},
    {"name": None},
    {},
])
def test_validation_rejects_invalid(input_data):
    with pytest.raises(ValueError):
        validate_user(input_data)
```

## Exception Testing

```python
import pytest
from example_client.exceptions import NotFoundError

def test_raises_on_not_found(mock_api_client):
    mock_api_client.get.side_effect = NotFoundError("User not found")

    with pytest.raises(NotFoundError) as exc_info:
        client.get_user("nonexistent")

    assert "not found" in str(exc_info.value).lower()
```

## Test Markers

```python
import pytest

@pytest.mark.slow
def test_long_running():
    ...

@pytest.mark.integration
def test_real_api_connection():
    ...

@pytest.mark.skip(reason="Not implemented yet")
def test_future_feature():
    ...
```

Run with markers:

```bash
pytest -m "not slow"        # Skip slow tests
pytest -m integration       # Only integration tests
```

## Coverage

```bash
poe test                    # Runs with coverage
open htmlcov/index.html     # View HTML report
```

Target 80%+ coverage on business logic.
