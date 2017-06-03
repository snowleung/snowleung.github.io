---
title: plantuml-note
date: 2017-06-03 11:05:18
tags:Program
keywords: UML,plantuml
---



Two things for my work, **Sequence Diagram** and **Simple Activity**.

<!-- More -->



## Elements

| Elements               | symbol                           | understand               |
| ---------------------- | -------------------------------- | ------------------------ |
| Arrow                  | ->,<--                           | message transfer         |
| Participant            | declare by:actor, database...    | like "who"               |
| Splitting diagrams     | newpage                          | Splitting diagrams       |
| Splitting charter      | ==                               | splitting "message"      |
| ===Activity diagram=== | ===Activity diagram===           | ===Activity diagram===   |
| begin,end              | start, stop                      | begin or end in actively |
| branch                 | if/then/else                     | conditions               |
| repeat                 | repeat … repeat while(condition) | also conditions          |

### Example(Sequence Diagram)

❗️bob add todo list,

🎨bob working,

✅bob finish the job, and check mark.

```
@startuml
actor Bob
Bob -> todo : draw a line
todo -> todo: add uncheck job: draw a line
Bob -> Bob: drawing
Bob -> Bob: finish
Bob -> todo: checked
@enduml
```

#### output

![seq_diagram](/images/seq_diagram.png)

### Example(Activity diagram)

* worker handler

```
@startuml
start
repeat 
	:check todo list;
	if (has new job?) then (YES)
		:add to list;
	else (NO)
		:process todo;
	endif
repeat while(is all done?)
stop
@enduml
```

#### output

![activity_diagram](/images/activity_diagram.png)