# Lesson 4: IndexedDB and Caching

* Out-of-line keys (Key and Value) - `Jane 41`
* In-line keys (Entires) - `{name: 'Jane', age: 41}`

## IDB Promised Library

This is a tiny library that mirros the IndexedDB, but replaces the weird `IDBRequest` objects with promises, plus a couple of other small changes.

## Limitations
### Transaction lifetime
At time of writing, all browsers aside from Chrome don't treat promise callbacks as microtasks, or call microtasks incorretly. This means transactions end by the time promise callbacks are called. In practice, this means you cannot perform transactions that involve waiting for a value, then using it within the same transaction.
