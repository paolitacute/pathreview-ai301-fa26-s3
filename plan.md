# Plan for Issue #68: KeywordSearcher empty corpus crash

## Scope
- `rag/retriever/keyword_search.py`: Add a guard clause in the `index` method to return early if the `corpus` is empty, preventing it from passing an empty list to `BM25Okapi`.
- `tests/unit/test_keyword_search.py`: Remove the `@pytest.mark.xfail(reason="manifest id H-01")` marker from the `test_index_empty_corpus` test.

## Test Plan
- Run the specific test `test_index_empty_corpus` using pytest and expect it to pass instead of xfail.
- Run a python one-liner to initialize `KeywordSearcher` and call `.index([])`. Expect it to exit cleanly without raising a `ZeroDivisionError`.
- Run the repository's standard checks (`make test-unit`, `make lint`, `make typecheck`) and expect them to pass.
