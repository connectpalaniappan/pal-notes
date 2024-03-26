


# Task picker 
```todoist
{
	"name": "Task with no date",
	"filter": "no date",
	"sorting": ["priority"]
}
```



# Task cleaner
```todoist
{
	"name": "Task created before 200 days",
	"filter": "created before: -200 days & !recurring & no due date",
	"sorting": ["priority"]
}
```

# Task not in [[obsidian]] 

## Task without an external link 
```todoist
{
	"name": "Todoist task",
	"filter": "!(search: https | search: obsidian)",
	"sorting": ["priority"]
}
```

## Task with an external link 
```todoist
{
	"name": "Todoist task",
	"filter": "search: https & !search: obsidian",
	"sorting": ["priority"]
}
```




# Task in obsidian and not in todoist 
# Tasks in obsidian and todoist
```todoist
{
	"name": "Todoist task",
	"filter": "search: obsidian",
	"sorting": ["priority"]
}
```
 