## Modifying SQL Data - Example with 3 tables


**Insert a new politician located in New Jersey (NJ) and named Sen. Ada Lovelace.**

```
INSERT INTO congress_members
(name, party, location, grade_1996, grade_current, years_in_congress, dw1_score) 
VALUES ('Sen. Ada Lovelace', 'Democrat', 'New Jersey', 7.343, 8.000, 45, 9.452)
```

**Add two new voters (make up their names and other data). For each of the new voters, create a vote for each of the two Texas (TX) senators.**

```
INSERT INTO voters
(first_name, last_name,gender, party, age, married, children_count, homeowner, employed, created_at, updated_at)
VALUES ('Marcela', 'Porto', 'female', 'Republican', 56, 1, 6, 0, 0, '2012-10-10 15:28:36 -0700', '2012-10-10 15:28:36 -0700')
```

**Updating Records in the Database**


**Update the votes for New Jersey's Sen. Frank Lautenberg. Change them to be votes for Sen. Ada Lovelace, the politician we created in Release 0.**

```
UPDATE votes 
SET politician_id = 531 
WHERE politician_id = 102
```



**Deleting Records from the Database**


**In our database we've essentially replaced Sen. Frank Lautenberg with Sen. Ada Lovelace. The last thing to do is to delete Sen. Frank Lautenberg from the database.**

```
DELETE FROM congress_members
WHERE id = 102;
```

**Delete all the voters who are homeowners, are employed, have no children, have been with their party for less than three years, and have voted for at least one politician who speaks at a grade level higher than 12.**

```
DELETE FROM voters
WHERE voters.id
IN 
(SELECT DISTINCT voters.id
from voters
JOIN votes ON votes.voter_id = voters.id
JOIN congress_members ON votes.politician_id = congress_members.id
WHERE voters.homeowner = 1
AND voters.employed = 1
AND voters.children_count = 0
AND voters.party_duration < 3
AND congress_members.grade_current > 12 )
```
# if you only see what's in the inner select, you will notice the ids are repeated. Use DISTINCT to delete them only once.

Links:

[Good for order](https://dev.mysql.com/doc/refman/5.7/en/select.html)
