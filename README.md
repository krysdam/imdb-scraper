# Purpose
I want to watch the most well-known movies and TV shows of all time. I could use
existing lists of popular media, but I'd like to make my own, using (semi-)
objective sources, and math.

# Data Sources
[IMDb](www.imdb.com) hosts information about movies and TV shows -- a huge
number of them, in fact. Users can rate content from 1 to 10. I don't actually
care how good a piece of media is, just how well-known it is. In other words: I
don't care about the ratings themselves (1.0/10 vs 10.0/10), just how *many*
ratings it has (10 vs 10,000,000). For this reason (and for the sake of simple
variable names...), I refer to ratings as "votes." For instance, [Inception
(2010)](www.imdb.com/title/tt1375666/) currently has 2.3M votes.

IMDb items (ex: a movie, a show, an animated short...) are called "titles."
These have ids like tt0123456 and tt1375666. These ids are called "ttid"s.

IMDb publishes data in two ways:
1. [TSVs](www.imdb.com/interfaces/) containing basic stats on a large subset of
   all titles. Two TSVs are relevant here:
   - ratings: vote count for each title
   - basics: title names (ex "Inception"), years (ex "2010"), directors and
     producers etc.
2. [The site](www.imdb.com) with a page for every title that IMDb tracks.
Includes vote counts separated by age and gender, as well as detailed
information like cast and trivia.

# Strategy
This is the current "flow" of this project, from data sources to the final list
of titles.
1. From ratings.tsv, pull every title with at least 1000 total votes.
2. Scrape [IMDb site](www.imdb.com) for each of these. Record women and men
   vote counts.
3. Multiply all women's vote counts by some constant so that (total women
   votes) = (total men votes). This turns out to be about 4.4 (really).
4. Assign each movie its rank (highest is 1, second-highest is 2) among all movies. Do the same for shows.
5. Output a list of all movies and shows, sorted first by year and then by rank.
6. Manually remove all items, except those which match one of these criteria:
    1. The item's rank is in the top 500
    2. I believe the item is highly famous or culturally relevant
    3. I merely want to include the item in this project
