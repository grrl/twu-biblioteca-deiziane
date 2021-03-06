**1. Who checked out the book 'The Hobbit’?**

```sql
SELECT member.name  
FROM member, checkout_item,  book   
WHERE member.id=checkout_item.member_id AND book.id=checkout_item.book_id AND book.title=“The Hobbit”;
```

**2. How many people have not checked out anything?**

```sql
SELECT COUNT(*) FROM member WHERE member.id NOT IN (
  SELECT member_id FROM checkout_item
);
```

**3. What books and movies aren't checked out?**

```sql
SELECT book.title as title FROM book WHERE book.id NOT IN (SELECT book_id FROM checkout_item WHERE book_id IS NOT NULL) 
UNION 
SELECT movie.title as title FROM movie WHERE movie.id NOT IN (SELECT movie_id FROM checkout_item WHERE movie_id IS NOT NULL);
```

**4. Add the book 'The Pragmatic Programmer', and add yourself as a member. Check out 'The Pragmatic Programmer'. 
Use your query from question 1 to verify that you have checked it out. 
Also, provide the SQL used to update the database.**

```sql
INSERT INTO book VALUES(11, "The Pragmatic Programmer");
INSERT INTO member VALUES(43, "Deiziane Silva");
INSERT INTO checkout_item VALUES(43, 11, NULL);
```

```sql
SELECT member.name 
FROM member, checkout_item, book 
WHERE member.id=checkout_item.member_id AND book.id=checkout_item.book_id AND book.title=“The Pragmatic Programmer”;
```

**5. Who has checked out more than 1 item?  Tip: Research the GROUP BY syntax.**

```sql
SELECT name FROM member 
WHERE id in
  (SELECT member_id 
   FROM  checkout_item 
   GROUP BY member_id
   HAVING COUNT(member_id) > 1);   
```
