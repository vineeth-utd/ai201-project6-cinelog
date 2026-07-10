# PR Response Doc — CineLog Watchlist Feature

## Comment 1 – Rename

**What I did:**
Renamed `save_to_watchlist()` to `add_to_watchlist()` in `services/watchlist_service.py` to follow the project's `verb_to_noun` naming convention. I also updated the import and function call in `routes/watchlist/watchlist.py` so they reference the new function name consistently.

**How I verified:**
I performed a project-wide search for `save_to_watchlist` to identify every call site and confirmed there were no remaining references after the rename. I then ran the test suite to verify that the rename did not break existing functionality.