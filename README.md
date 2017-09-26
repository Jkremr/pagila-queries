# Pagila queries

1a. maiList of all the actors’ first name and last name. Display the first and last name of each actor in a single column in upper case letters. Name the column Actor Name.

```sql
SELECT first_name || ' ' || last_name AS "Actor Name"
FROM actor
;
```

1b. Display the first and last name of each actor in a single column in upper case letters. Name the column Actor Name

2a. Find the id, first name, and last name of an actor, of whom you know only the first name of "Joe."

```sql
SELECT
  actor_id
  ,first_name
  ,last_name
FROM actor
WHERE first_name ILIKE 'joe'
;
```



2b. Find all actors whose last name contain the letters GEN. Make this case insensitive.

```sql
SELECT
  actor_id
  ,first_name
  ,last_name
FROM actor
WHERE last_name ILIKE '%gen%'
;
```

/*2c. Find all actors whose last names contain the letters LI. This time, order the rows by last name and first name, in that order. Make this case insensitive.*/

```sql
SELECT
  actor_id
  ,first_name
  ,last_name
FROM actor
WHERE last_name ILIKE '%li%'
ORDER BY last_name
,first_name
;
```

/*2d. Using IN, display the country_id and country columns of the following countries: Afghanistan, Bangladesh, and China:*/

```sql
SELECT *
FROM country
WHERE country IN ('Afghanistan','Bangladesh','China')
;
```

/*3a. Add a middle_name column to the table actor. Specify the appropriate column type*/

```sql
ALTER TABLE actor
  ADD COLUMN middle_name VARCHAR(50)
;

ALTER TABLE actor
  ALTER COLUMN middle_name TYPE TEXT
;

SELECT *
FROM actor
LIMIT 5
;
```

3b. You realize that some of these actors have tremendously long last names. Change the data type of the middle_name column to something that can hold more than varchar.

```sql
ALTER TABLE actor
  ALTER COLUMN middle_name TYPE TEXT
;

SELECT *
FROM actor
LIMIT 5
;
```

3c. Remove the middle_name column.
```sql
ALTER TABLE actor
  DROP COLUMN middle_name
;

SELECT *
FROM actor
LIMIT 5
;
```

4a. List the last names of actors, as well as how many actors have that last name.

```sql
SELECT
  last_name
  ,COUNT(last_name) AS last_name_count
FROM actor
GROUP BY last_name
ORDER BY last_name_count DESC
;
```

4b. List last names of actors and the number of actors who have that last name, but only for names that are shared by at least two actors

```sql
SELECT
  last_name
  ,COUNT(last_name) AS last_name_count
FROM actor
GROUP BY last_name
HAVING COUNT(last_name) >= 2
ORDER BY last_name_count DESC
;
```

4c. Set GROUCHO WILLIAMS record so that the first name is HARPO.

```sql
UPDATE actor
SET first_name = 'HARPO'
WHERE first_name = 'GROUCHO' AND last_name = 'WILLIAMS'
;

SELECT
  first_name
  , last_name
FROM actor
WHERE last_name = 'WILLIAMS'
;
```

4d. Set GROUCHO WILLIAMS first name back to GROUCHO from HARPO.

```sql
UPDATE actor
SET first_name = 'GROUCHO'
WHERE first_name = 'HARPO' AND last_name = 'WILLIAMS'
;

SELECT
  first_name
  , last_name
FROM actor
WHERE last_name = 'WILLIAMS'
;
```

6a. Use a JOIN to display the first and last names, as well as the address, of each staff member. Use the tables staff and address:

```sql
SELECT
  staff.first_name
  , staff.last_name
  , address.address AS street_address
FROM staff
  INNER JOIN address ON address.address_id = staff.address_id
;
```

6b. Use a JOIN to display the total amount rung up by each staff member in January of 2007. Use tables staff and payment.

```sql
SELECT
  staff.first_name
  ,staff.last_name
  ,SUM(payment.amount)
FROM payment
  INNER JOIN staff ON payment.staff_id = staff.staff_id
WHERE payment.payment_date BETWEEN '2007-01-01' AND '2007-02-01'
GROUP BY
  staff.last_name
  ,staff.first_name
ORDER BY SUM(payment.amount)
;
```
6c. List each film and the number of actors who are listed for that film. 

```sql
SELECT
  film.title
  ,film.film_id
  ,COUNT(film_actor.actor_id) AS actor_count
FROM film
  INNER JOIN film_actor ON film.film_id = film_actor.film_id
GROUP BY film.title
  ,film.film_id
ORDER BY COUNT(film_actor.actor_id)
  ,film.title
;
```



6d. How many copies of the film Hunchback Impossible exist in the inventory system?

```sql
SELECT
film.film_id
  ,film.title
,COUNT(film.film_id)
FROM inventory
LEFT JOIN film ON inventory.film_id = film.film_id
WHERE film.title ILIKE 'hunchback impossible'
GROUP BY
  film.film_id
  ,film.title
ORDER BY COUNT(film.film_id) DESC
```

*There are six copies of Hunchback Impossible in the inventory system.*



6e. Using the tables payment and customer and the JOIN command, list the total paid by each customer. List the customers alphabetically by last name.

```sql

```

7a. The music of Queen and Kris Kristofferson have seen an unlikely resurgence. As an unintended consequence, films starting with the letters K and Q have also soared in popularity. display the titles of movies starting with the letters K and Q whose language is English.

```sql

```

7b. Use subqueries to display all actors who appear in the film Alone Trip.

```sql

```

7c. You want to run an email marketing campaign in Canada, for which you will need the names and email addresses of all Canadian customers. Use joins to retrieve this information.

7d. Sales have been lagging among young families, and you wish to target all family movies for a promotion. Identify all movies categorized as a family film.Now we mentioned family film, but there is no family film category. There’s a category that resembles that. In the real world nothing will be exact.

7e. Display the most frequently rented movies in descending order.

7f. Write a query to display how much business, in dollars, each store brought in.

7g. Write a query to display for each store its store ID, city, and country.

7h. List the top five genres in gross revenue in descending order. 

8a. In your new role as an executive, you would like to have an easy way of viewing the Top five genres by gross revenue. Use the solution from the problem above to create a view. 

8b. How would you display the view that you created in 8a

8c. You find that you no longer need the view top_five_genres. Write a query to delete it.