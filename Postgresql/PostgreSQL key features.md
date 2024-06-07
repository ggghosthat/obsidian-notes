PostgreSQL syntax supports a lot of features. 

- Lets get started with type casting aspects:
For example, we can  cast type with `CAST()` function:

```PostgreSQL
CAST(value AS target_datatype) --example pattern ep.
SELECT CAST('123' AS integer) --example case ec.
```

But PostgreSQL supports more efficient way to convert from one datatype to another one. This is `::` syntax. Example is shown below.

```PostgreSQL
value::datatype --example pattern ep.
'123'::integer --example case ec.
```

- Also its worth to stand on string and value concatenation 
First one is using `||` operator with desired piece of string. Accepts just more than 2 arguments. 

```PostgreSQL 
value1 || value2 -- value1value2 examplepattern ep.
SELECT 'Hello ' || 'world!' -- Hello world! example case ec.
SELECT 'Hello' || ' ' || 'world!' -- Hello world! example case ec.
```

Second one is using `concat_ws()` function 
```PostgreSQL
concat_ws('<separator pattern>', value1, value2, value3); --value1...value2...value3 example pattern ep.
SELECT concat_ws(' ', 1,2,3); -- 1 2 3 example case ec.
```

- Also there is special function which help to capitalize the first letter in string. Just use `intCap()`
```PostgreSQL
initCap('value1') -- Value1 example pattern ep.
SELECT intiCap('samuel') -- Samuel example case ec.
```
