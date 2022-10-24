## StaticSQLEngine

### Creating / Recreating the engine :
Creates an object that derivates from an sqlalchemy engine. You can feed it to evey function that takes an engine as argument.
If you call `pLabAna.StaticSQLEngine()` from any place in your code, it will actually return the same object (singleton) without re-recreating one.
This has the benefit of small performance increases.

!!! warning :
   On very long sessions, where you stop accessing the database for several hours straight, the connection can be stopped between the object and the database (timeout)
   In that case, you can simply call `pLabAna.StaticSQLEngine(regen=True)` to get back a new engine and not the one that expired. 
   In that only case, the library is effectively reacreating one object.

### Calling stored procedures and functions :

One more advantage of this homemade class, is also that it encapsulates an methods, all stored procedures and functions defined in the mysql database.

They can be called simply by writing : `engine = pLabAna.StaticSQLEngine()` and `result = engine.myStoredProcedure(arg1, arg2, ...etc)`

!!! note: Example
    For example, in the case of the maze database model, you can call : `duration = engine.session_duration(session_id)` and get the duration in a single line.
    Here the heavylifting is done in mysql rather than python (wich is the whole advantage of using a database, with the fact that data is well organized without a folder specific location)
    
!!! tip    
    Always remember : if you find yourself formatting the data you recieve in python, you're goign the wrong way. It should be done in the database. 
    The other language (ie. python) is only here for processing the data, not formating it. (but in the end, that's only an advice.)
