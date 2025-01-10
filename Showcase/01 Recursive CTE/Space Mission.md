Space mission example

> [!ERROR] Multiple SELECTS not supported
> Due to an error multiple selects are not supported at the moment, even in the nested UNIONS where it should not be a problem. Due to that this example does not work YET.


```sqlseal

TABLE space_tasks = file(./data.csv)

HTML
WITH task_tree AS (
    SELECT 
        id, 
        parent_id, 
        name,
        priority,
        estimated_hours,
        1 as level,
        CAST(name as TEXT) as path
    FROM space_tasks 
    WHERE parent_id IS NULL


    UNION ALL
    
    SELECT 
        t.id,
        t.parent_id,
        t.name,
        t.priority,
        t.estimated_hours,
        tt.level + 1,
        tt.path || ' -> ' || t.name
    FROM space_tasks AS t
    JOIN task_tree AS tt ON t.parent_id = tt.id
    
)
SELECT 
    name as task_hierarchy,
    priority,
    estimated_hours,
    path as dependency_chain
FROM task_tree
ORDER BY path;
```

