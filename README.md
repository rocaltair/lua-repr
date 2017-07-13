# lua-repr
repr for lua values, especially for lua table

# sample

```
local lib = require "repr"

local conf = {
	beautify = true,			-- add indent and '\n' to the end of line
	array_index = true,			-- show array index
	indent = "  ",				-- indent str
	maxdepth = 32,				-- max depth for lua table
	sort = true,				-- is sort by keys?
	func_info = true,			-- show function info
	userdata_info = true,			-- show userdata info
	skip_type = {["function"] = nil},	-- skip some value type
}

local sample_table = {
	co = coroutine.create(function() end),
	tbl = {1,2,3,"fdas",a=2,b=3,c=4, sub_tbl = {print, io.stdout}},
	func = dump,
	stdout = io.stdout,
	bool = true,
}
print(lib.repr(sample_table, conf))
```

shows :
```
{
  bool=true,
  co=<thread: 0x7fdb57402a40>,
  func=<Lua.function: 0x7fdb5740b220:@repr.lua:79>,
  stdout=<userdata:FILE*:file (0x7fff98bba1a8)>,
  tbl={
    [1]=1,
    [2]=2,
    [3]=3,
    [4]="fdas",
    a=2,
    b=3,
    c=4,
    sub_tbl={
      [1]=<C.function: 0x7fdb57403c70>,
      [2]=<userdata:FILE*:file (0x7fff98bba1a8)>,
    },
  },
}
```
