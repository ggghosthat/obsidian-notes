PostgreSQL supports several parameter mode:
- `in` read-only mode used by default in function parameter. parameter, which marked with this mode can be readable only and must be passed into function or procedure
- `out` keyword say us about output parameter, which PostgreSQL will hook up. Let look at the example below:
```PostgreSQL
create or replace function hook_up(out minParam integer,
								   out avgParam integer,
								   out maxParam integer)
as 
$$
begin
	minParam = 1;
	avgParam = 2;
	maxParam = 3;
end;
$$

language plpgsql;
select * from hook_up();
--Result: 1 | 2 | 3
```
 - `inout` mode used with parameter which can entered in function scope and be return out. Also we can modify parameter state.
``` PostgreSQL
create or replace function swap(inout firstParam integer,
							   	inout secondParam integer)
as 
$$
declare 
	tempParam integer = firstParam;
begin
	firstParam = secondParam;
	secondParam = tempParam;
end;
$$
language plpgsql;

select * from swap(1,2);
--Result: 2,1
```