## Solution

## Table schemas:

		CREATE TABLE Film (
			id serial PRIMARY KEY,
			title VARCHAR(100) NOT NULL UNIQUE,
			genre VARCHAR(100) NOT NULL,
			released INTEGER NOT NULL CHECK (released BETWEEN 1000 and 9999),
			score INTEGER NOT NULL CHECK(score BETWEEN 1 and 10),
			director_fk INTEGER NOT NULL,
			star_fk INTEGER NOT NULL,
			writer_fk INTEGER NOT NULL
		);

		CREATE TABLE Director (
			id serial PRIMARY KEY,
			name VARCHAR(100) NOT NULL UNIQUE,
			country VARCHAR(100) NOT NULL
		);

		CREATE TABLE Star (
			id serial PRIMARY KEY,
			name VARCHAR(100) NOT NULL UNIQUE,
			dateofbirth DATE
		);

		CREATE TABLE Writer (
			id serial PRIMARY KEY,
			name VARCHAR(100) NOT NULL,
			email VARCHAR(100)
		);

## Insert queries:
		INSERT INTO director 
			(name, country)
		VALUES
			('Stanley Kubrick', 'USA'),
			('George Lucas', 'USA'),
			('Robert Mulligan', 'USA'),
			('James Cameron', 'Canada'),
			('David Lean', 'UK'),
			('Anthony Mann', 'USA'),
			('Theodoros Angelopoulos', 'Greece'),
			('Paul Verhoeven', 'Netherlands'),
			('Krzysztof Kieslowski', 'Poland'),
			('Jean-Paul Rappeneau', 'France')

		INSERT INTO Star 
			(name, dateofbirth)
		VALUES
			('Keir Dullea', '1936-05-30'),
			('Mark Hammil', '1951-09-25'),
			('Gregory Peck', '1916-04-05'),
			('Leonardo DiCaprio', '1974-11-11'),
			('Julie Christie', '1940-04-14'),
			('Charlton Heston', '1923-10-04'),
			('Manos Katrakis', '1908-08-14'),
			('Rutger Hauer', '1944-01-23'),
			('Juliette Binoche', '1964-03-09'),
			('Gerard Depardieu', '1948-12-27')

		INSERT INTO writer
			(name, email)
		VALUES
			('Arthur C Clarke', 'arthur@clarke.com'),
			('George Lucas', 'george@email.com'),
			('Harper Lee', 'harper@lee.com'),
			('James Cameron', 'james@cameron.com'),
			('Boris Pasternak', 'boris@boris.com'),
			('Frederick Frank', 'fred@frank.com'),
			('Theodoros Angelopulos', 'theo@angelopoulos.com'),
			('Erik Hazelhoff Roelfzema', 'erik@roelfzema.com'),
			('Krzystof Kieslowski', 'email@email.com'),
			('Edmond Rostand', 'edmond@rostand.com')

		INSERT INTO film
			(title, released, genre, score, director_fk, star_fk, writer_fk)
		VALUES
			('2001: A Space Oddysey', 1968, 'Science Fiction', 10, 1, 1, 1),
			('Star Wars: A New Hope', 1977, 'Science Fiction', 7, 2, 2, 2),
			('To Kill A Mockingbird', 1962, 'Drama', 10, 3, 3, 3),
			('Titanic', 1997, 'Romance', 5, 4, 4, 4),
			('Dr Zhivago', 1965, 'Historical', 8, 5, 5, 5),
			('El Cid', 1961, 'Historical', 6, 6, 6, 6),
			('Voyage to Cythera', 1984, 'Drama', 8, 7, 7, 7),
			('Soldier of Orange', 1977, 'Thriller', 8, 8, 8, 8),
			('Three Colours: Blue', 1993, 'Drama', 8, 9, 9, 9),
			('Cyrano de Bergerac', 1990, 'Historical', 9, 10, 10, 10)

## Return queries:
#### Show the title and director name for all films

		SELECT film.title AS title, director."name" AS director
		FROM film
		LEFT JOIN director ON film.director_fk = director.id
		ORDER BY title

#### Show the title, director and star name for all films

		SELECT film.title AS title, director."name" AS director, star."name" AS starring
		FROM film
		LEFT JOIN director ON film.director_fk = director.id
		LEFT JOIN star ON film.star_fk = star.id
		ORDER BY title

#### Show the title of films where the director is from the USA

		SELECT film.title AS title
		FROM film
		INNER JOIN director ON film.director_fk = director.id
		WHERE director.country = 'USA'
		ORDER BY title

#### Show only those films where the writer and the director are the same person

		SELECT film.title AS title
		FROM film
		INNER JOIN director ON film.director_fk = director.id
		INNER JOIN writer ON film.writer_fk = writer.id
		WHERE director."name" = writer."name"
		ORDER BY title

#### Show directors and film titles for films with a score of 8 or higher

		SELECT director."name" AS director, film.title AS title
		FROM film
		INNER JOIN director ON film.director_fk = director.id
		WHERE (film.score >= 8)
		ORDER BY score desc

#### Make at least 5 more queries to demonstrate your understanding of joins, and other relationships between tables.