# Pytest

## Fixtures

pytest fixtures are a way of providing data, test doubles, or state setup to your tests. Fixtures are functions that can return a wide range of values. Each test that depends on a fixture must explicitly accept that fixture as an argument.

Fixtures are great for extracting data or objects that you use across multiple tests. They aren’t always as good for tests that require slight variations in the data. Littering your test suite with fixtures is no better than littering it with plain data or objects. It might even be worse because of the added layer of indirection.

As with most abstractions, it takes some practice and thought to find the right level of fixture use.

## conftest.py

pytest looks for conftest.py modules throughout the directory structure. Each conftest.py provides configuration for the file tree pytest finds it in. You can use any fixtures that are defined in a particular conftest.py throughout the file’s parent directory and in any subdirectories. This is a great place to put your most widely used fixtures.