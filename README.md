# Data Normalization and Entity-Relationship Diagramming
## Original Data Set
| assignment_id | student_id | due_date | professor | assignment_topic                | classroom | grade | relevant_reading    | professor_email   |
| :------------ | :--------- | :------- | :-------- | :------------------------------ | :-------- | :---- | :------------------ | :---------------- |
| 1             | 1          | 23.02.21 | Melvin    | Data normalization              | WWH 101   | 80    | Deumlich Chapter 3  | l.melvin@foo.edu  |
| 2             | 7          | 18.11.21 | Logston   | Single table queries            | 60FA 314  | 25    | Dümmlers Chapter 11 | e.logston@foo.edu |
| 1             | 4          | 23.02.21 | Melvin    | Data normalization              | WWH 101   | 75    | Deumlich Chapter 3  | l.melvin@foo.edu  |
| 5             | 2          | 05.05.21 | Logston   | Python and pandas               | 60FA 314  | 92    | Dümmlers Chapter 14 | e.logston@foo.edu |
| 4             | 2          | 04.07.21 | Nevarez   | Spreadsheet aggregate functions | WWH 201   | 65    | Zehnder Page 87     | i.nevarez@foo.edu |

## Why this data set is not compliant with 4NF
In order to satisfy 4NF, the data set needs to fulfill 3NF and does not contain more than two or more independent multi-valued facts about an entity. The original data set have more than 2 independent multi-valued facts about an entity. This data set also doens't satisfy 3NF since it has one non-key field about another non-key field - assignment_topic and relevant_reading, for instance.
## Tables fulfilling 4NF
### Courses table
| course_id  | course_name |
| ------------- | ------------- |
| 1  | Data Science  |
| 2  | Computer Science  |
| 3  | Python and pandas  |
| 4  | Spreadsheet aggregate functions  |
| 5  | Money and banking  |
### Professors table
| professor_id  | professor_name | professor_email |
| ------------- | ------------- | ------------- |
| 1  | Melvin  |l.melvin@foo.edu|
| 2  | Logston  |e.logston@foo.edu|
| 3  | Nevarez  |i.nevarez@foo.edu|
| 4  | Griffiths  |b.griffiths@foo.edu|
| 5  | Nikolich  |n.nikolich@foo.edu|
### Sections table
| secion_id  | course_id | professor_id | classroom |
| ------------- | ------------- | ------------- | ------------- |
| 1  | 1  |1|WWH 101|
| 2  | 1  |2|60FA 314|
| 3  | 3  |3|WWH 203|
| 4  | 4  |4|BOB 249|
| 5  | 5  |5|SIL 101|
### Assignments table
| assignment_id  | section_id | assignment_topic | due_date |
| ------------- | ------------- | ------------- | ------------- |
| 1  | 1  |Data normalization|23.02.21|
| 2  | 2  |Single table queries|18.11.21|
| 3  | 3  |Pandas workshop|19.01.21|
| 4  | 4  |Spreadsheet workshop|01.02.21|
| 5  | 5  |Recitation worksheet|05.04.21|
### Readings table
| reading_id  | assignment_id | relevant_reading |
| ------------- | ------------- | ------------- |
| 1  | 1  |Deumlich Chapter 3|
| 2  | 2  |Dümmlers Chapter 11|
| 3  | 3  |Pandas Chapter 1|
| 4  | 4  |Excel Chapter 8|
| 5  | 5  |Madison Chapter 4|
### Grades table
| grade_id  | assignment_id | student_id | grade |
| ------------- | ------------- | ------------- | ------------- |
| 1  | 1  |1|98|
| 2  | 2  |5|75|
| 3  | 3  |3|63|
| 4  | 4  |2|50|
| 5  | 5  |4|95|
### Students table
| student_id  | student_name |
| ------------- | ------------- |
| 1  | Mary  |
| 2  | Jack  |
| 3  | Harry  |
| 4  | Jerry  |
| 5  | Lisa  |
## ER diagram
[ER Diagram](images/ER_Diagram.png)
## Changes made & how they make data 4NF-compliant
I separate the orginal table into 7 small tables. They are interconnected to each other so that information can be conveyed as being aimed as the original data - they would carry the same information while making data entry less redundant. For these 7 tables, all of them comply with 3NF, meaning that they don't have a non-key field related to another non-key field. Moreover, they do not contain more than two or more independent multi-valued facts about an entity.

Each professor will have different sections (with unique classrooms) of the courses taught, and the courses have corresponding assignments which have their interconnected required readings. For the assignments, they would be graded and correspond to students who completed them, who will receive their corresponding grades. 