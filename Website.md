
<div id="container">
	<center>
    	<img src="./images/IMDb.ico"/>
    </center>
</div>

<center>
<h1> IMDb Network and Text Analysis </h1>
<h3> By Thomas Sandfeld Nielsen & Lennart Pedersen </h3>
</center>

See our explainer notebook [here](http://nbviewer.jupyter.org/github/TSandfeld/02805_imdb.github.io/blob/gh-pages/Assignment%20B.ipynb).

## Introduction
IMDb is the worlds biggest online movie database, launched back in 1990. According to Wikipedia[^wiki] IMDb contains more than 3.9 million movie/tv-show titles and 7.4 million personalities. With this data we will try to uncover some patterns and relationships between the best critically acclaimed and highest grossing movies of all time. We will use techniques from the world of network-, text- and data analysis to accomplish this.
Although IMDb has millions of titles for us to play around with we don't have the computing power/time to go through all that data. So instead we are going to use a little less data - just under 5000 titles with all the relevant attributes such as cast, director, year, budget, domestic gross, genres, etc. We also gathered ~1200 moviescripts for text analysis - keep reading for more. 

Should you be interested in working with our datasets, then please see the see [Download Dataset](#download-sets) in the end.

## Network analysis
Let's explore our datasets .. 

One aspect of IMDb is the **IMDb Rating** which is a numeric scale from 1-10 used to judge the quality of the movie. The higher the rating, the better the movie.
All ratings are generated from voting by registered users of the site. 
![Rating distribution](./images/rating_distribution.png)
As we can see from the distribution of the IMDb ratings they are uniformally distributed. The average IMDb score is 6.3. 

Most people would preferrably watch movies with rating of 7 or above. As many people check the rating af a movie before they decide to watch it, the IMDb rating actually has quite some influence as to which movies are watched and which that are not. The ratings are regulated through the votes by numerous different users, and eventhough you don't know who actually voted the movie, the number of voters usually make the rating quite trustworthy.

Lets look a some more data ... as anyone could go to IMDb's website and look up the individual movieratings, it would be more interesting how the actors are rated.
For all the movies an actor/actress has been part of, we will average their rating and plot it. We will restrict the plot to the 10 best and 10 worst actors who's been part of more than 10 movies. This gives us the following, where we can see some familiar names.

![Actor Rating](./images/Actor_rating.png)

A key attribute to a successfull movie is of course how much money it makes. So let's first compare the most appreciated genres of films to how much the genres gross worldwide.

![Genre Rating Gross](./images/Genre_rating_gross.png)

Let's look at how all these movies actually are connected. We have created a network of movies that are connected if any actor appears in both. The network is shown as a graph below.

![Graph of Movies](./images/graph_all_nodes_movies.png)

If we extract only the movies in the big cluster in middle of this graph, we can eliminate the movies that have no connection with all other movies. Now the graph looks like this.

![Graph of Movies GCC](./images/graph_GCC_movies.png)
As we can see from this graph, most movies are clustered around the middle of the graph which tells us that a large amount of the movies in this network are highly connected. Thus many movies have some of the same actors, and only a small amount of movies connect to few other movies, meaning that the actors in those movies do not appear in other movies. This could be due to the fact that some movies have only few actors and that those are relatively unknown or perhaps chosen specifically for one movie.

Analysis this network we see that the distribution of degrees(number of movies on movie is connected to) follows a powerlaw. Therefore we can conclude that our network is scale free. Hence our network consist of a few movies with a lot of connections, so-called **hubs**, and then most of the movies having few connections.
Here the distribution is plotted on a log-scale.
![Degree distribution of movie Graph](./images/movie_graph_degree_distribution.png)

To identify communities in this network we have used the Louvain community detection algorithm which identifies communities in a graph, communities being movies that are all closely connected with each other but not so much with other communities. This algorithm found 13 communties in our network. One interesting aspect of this is to discover whether these communties actually correspond to the genres of the movies. We have plotted how much one community consists of the same genre.

![Community genres](./images/genre_com_piecharts.png)

Comment on findings in the above.

Gross/rating
![Gross rating](./images/Movie_rating_gross.png)

Director/Actor rating - correlation
![Dicetor Actor Correlation](./images/Director_r_cast_r_scat.png)
High positive linear correlation! - some due to the fact that the actors obviously are in some of the same movies as the directors. 

There is only a small positive linear correlation between the duration of a movie and its rating. No real tendency but longer movies have a small advantage..
![Duration rating Correlation](./images/corr_duration_rating_scatter.png)

Actor network
...



## Text analysis of manuscripts
We've looked quite a bit on how different attributes relate in our network of movies/actors. Let's now look at some manuscripts. 
Using a technique called Term Frequency - Inverse Document Frequency, or TF-IDF, we can figure how important a word in a script is for our total collection of scripts. So by doing this we can find the words that are most important for each genre of movies in our dataset.

![Wordcloud_1](./images/genre_wordcloud_1.png)
![Wordcloud_1](./images/genre_wordcloud_2.png)

As mentioned in the introduction, we have about ~1200 scripts and ~5000 movies in our dataset. This means that we don't have a manuscript for each movie in our dataset, which leads to a margin of error in the above wordclouds. For example, raspberries may not be as important a term in the whole genre of romance films, as it is for the genre in our dataset.

Let us look at the sentiment of the scripts we have. Using the LabMT wordlist[^labmt], which provides a sentiment score for a lot of english words, we can figure out how positive/negative a script is.

Having calculated the sentiment of the scripts we can see if it relates in any way to the success of a movie. For example, let's see if there is a connection between the sentiment and the IMDb rating of a movie ..  

![Genre rating gross](./images/Movie_rating_senti.png)

On the plot we can see that there is *very little*, if any, correlation between a movie's IMDb rating and the sentiment of the movie's script. This does make sense as a lot of very well liked movies are drama and action movie's which tend to be more intense in the language than other movies.

### Do a movie gross vs sentiment *here*

Instead of only looking at movies let's look at actors. Some actor's are more featured in one genre then others, so let's see if there is a relation between a actors sentiment and their IMDb rating. We will calculate the actor's sentiment as an average of the sentiments of the scripts for the movies he has been in. We will be looking at actors who has been in more than 5 movie's, so there is some data to work with. 

One this bar graph we see some familiar names, who we might associate with being good actors, suchs as Robert De Niro and Joseph Gordon-Levitt.

![Actor_senti](./images/Actor_senti_10.png)

If we correlate their sentiment to their IMDb rating we get this:
![Actor senti rating](./images/Actor_senti_imdb_rating.png)

Again, it does not seem that the sentiment of the scripts has much to do with the rating of the actor.

## <a name="download-sets"></a> Download Datasets
So our dataset mainly comprises of a dataset from [kaggle.com](https://www.kaggle.com/deepmatrix/imdb-5000-movie-dataset)

## References

[^wiki]: Wikipedia about IMDb: [https://en.wikipedia.org/wiki/IMDb](https://en.wikipedia.org/wiki/IMDb)

[^labmt]: Wordlist article: [http://journals.plos.org/plosone/article?id=10.1371/journal.pone.0026752](http://journals.plos.org/plosone/article?id=10.1371/journal.pone.0026752)