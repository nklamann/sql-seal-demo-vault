Space mission example

> [!NOTE] Recursive CTE
> Here you can see advanced, recursive CTE that iterates over graph of dependencies.


```sqlseal
-- the data from data.csv file will be available as a space_tasks table.
TABLE space_tasks = file(./data.csv)

-- renderer definition
HTML 

/*
this is main query, it uses CTE compute data. It uses Recursive CTE to traverse depenencies from the leaves (no parent) all the way up.
*/
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

