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