# PR Response Doc — CineLog Watchlist Feature

## Comment 1 – Rename

**What I did:**
Renamed `save_to_watchlist()` to `add_to_watchlist()` in `services/watchlist_service.py` to follow the project's `verb_to_noun` naming convention. I also updated the import and function call in `routes/watchlist/watchlist.py` so they reference the new function name consistently.

**How I verified:**
I performed a project-wide search for `save_to_watchlist` to identify every call site and confirmed there were no remaining references after the rename. I then ran the test suite to verify that the rename did not break existing functionality.

## Comment 2 – Deduplication

**What I did:**
Added a deduplication check to `add_to_watchlist()` so that a user cannot add the same film to their watchlist more than once. Before creating a new `WatchlistEntry`, the service checks whether an entry already exists for the same `user_id` and `film_id`. If a duplicate is found, the appropriate exception is raised instead of creating another entry.

**How I verified:**
I followed the existing deduplication pattern used in `add_to_collection()` within `services/collection_service.py` to keep the implementation consistent with the rest of the codebase. After implementing the check, I ran the test suite to verify that the existing functionality continued to work and that duplicate watchlist entries are prevented.

## Comment 3 – Missing Test

**What I did:**
Created a new file, `tests/test_watchlist.py`, and added a test to verify that `add_to_watchlist()` raises `FilmNotFoundError` when a nonexistent `film_id` is provided. This ensures invalid film IDs are handled gracefully instead of creating an invalid watchlist entry or causing a database integrity error.

**How I verified:**
I modeled the test after `test_add_to_collection_nonexistent_film_raises()` in `tests/test_collection.py` so it follows the existing fixture setup, assertion pattern, and testing style used throughout the project. I ran `pytest tests/test_watchlist.py -v` and confirmed the expected `FilmNotFoundError` was raised. I then ran the full test suite (`pytest tests/ -v`) to verify the new test did not affect any existing functionality.