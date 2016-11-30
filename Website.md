
<div id="container">
	<center>
    	<img src="./images/IMDb.ico"/>
    </center>
</div>

<center>
# IMDb Network and Text Analysis 
### By Thomas Sandfeld Nielsen & Lennart Pedersen
</center>

See our explainer notebook [here](http://nbviewer.jupyter.org/github/TSandfeld/02805_imdb.github.io/blob/gh-pages/Assignment%20B.ipynb).

## Introduction
IMDb is the worlds biggest online movie database, launched back in 1990. According to Wikipedia[^wiki] IMDb contains more than 3.9 million movie/tv-show titles and 7.4 million personalities. With this data we will try to uncover some patterns and relationships between the best critically acclaimed and highest grossing movies of all time. We will use techniques from the world of network-, text- and data analysis to accomplish this.
Although IMDb has millions of titles for us to play around with we don't have to computing power/time to go through all that data. So instead we are going to use a little less data - just under 5000 titles with all the relevant attributes such as cast, director, year, budget, domestic gross, genres, etc. We also gathered ~1200 moviescripts for text analysis - keep reading for more. 

Should you be interested in working with our datasets, then please see the see [Download Dataset](#download-sets) in the end.

## Network analysis
Let's explore our datasets .. 

One aspect of IMDb is the **IMDb Rating** which is a numeric scale from 1-10 used to judge the quality of the movie. The higher the rating, the better the movie.
All ratings are generated from voting by registered users of the site. 

However, anyone could go to IMDb's website and look up the individual movieratings, so let's instead see how the actors are rated.
For all the movies an actor/actress has been part of, we will average their rating and plot it. We will restrict the plot to the 10 best and 10 worst actors who's been part of more than 10 movies. This gives us the following, where we can see some familiar names.

![Actor Rating](./images/Actor_rating.png)

A key attribute to a successfull movie is of course how much money it makes. So let's first compare the most appreciated genres of films to how much the genres gross worldwide.

![Genre Rating Gross](./images/Genre_rating_gross.png)

## Text analysis

## <a name="download-sets"></a> Download Datasets
So our dataset mainly comprises of a dataset from [kaggle.com](https://www.kaggle.com/deepmatrix/imdb-5000-movie-dataset)

## References

[^wiki]: Wikipedia about IMDb: [https://en.wikipedia.org/wiki/IMDb](https://en.wikipedia.org/wiki/IMDb)