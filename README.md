# movie-recommender-system
The project is to build a system that on the basis of a single movie name will suggest 5 similar movies for the viewer to watch next.

The steps are as below:- Importing crucial libraries
The dataset used is the TMDB data of 5000 movies available on kaggle :- https://www.kaggle.com/datasets/tmdb/tmdb-movie-metadata?select=tmdb_5000_movies.csv

We can see that there are nearly 4800 movies available and about 20 feautures are present but we do not need all of them, we will only take the needed ones ahead.

Also the movies consists of information like language, title, popularity, overview, etc. While, the credits consists of info like title, cast and crew involved in the film.

So what we will do is, we merge the credits data along with movies data to contain all information in one dataset

Now, we can see that almost all of the films are in english language so as the data is highly biased towards english language, we will not consider the language as a feauture. Similarly, only certain factors are important for recommending a movie, like the actors in the movie, the genre of the movie, the director, etc so based on such ideas, we will only consider the movie id, title, overview, genres, cast, crew, and keywords as useful features and neglect all other feautures.

Now, we see that the overview is a critical feature and we have some missing values in it, but only 3 data is missing out of 5000 so we can easily drop that.

We see that the genres is a list of dictionary, but we only need the genre out of it, eg. action, adventure , etc. So, we will extract the genre out of this list using literal_eval.

We applied the convert function on the genre and keywords column to convert them in the required format.

But we see that there is a problem, the cast has a lot of information, but while recommending a movie, we are only focussed on the top three actors in the movie. So we need to create a new function extract the name of only the top 3 cast from all the cast details.

Similarly from the crew, we only require the name of the director, because nobody recommends films on the basis of cameraman, production man, etc, only director is important, for this purpose also, we will defina a function to fetch the director.

We want to eliminate the space between names to avoid discrepencies, eg san francisco should be same as sanfrancisco, so we would define a function for this and apply it to cast, crew, keywords and genres.

As the overview feauture has text, we also need to convert it in the form of other columns, so we will convert this text into list of words that are used in the text.

Now, finally, we will combine all these modified data into a single feauture named tags.

Now we will join all elements of tags to make a single element and convert all to lowercase to avoid any future discrepancy.

Now, for further processing on the final obtained data, we need to import and use library called Natural Language Toolkit(NLTK).

now in our tags we will see that the word activity, activities are considered different. similarly, action, act, actions, actionable, etc are considered different but they are all same and point towards the same meaning.

So we will use PorterStemmer from nltk , which will replace all such words with thier root word, eg. actionable, actions, action will be replaced by action.

Now, all the tags data are replaced with root word of all words and now can be converted into vectors so that we can define similarity among these vectors(i.e. similarity among movies)by some measure called cosine_similarity and this vectorization could be done using countvectorizer from sklearn library

By using stop words as english, we ignore the common words like : the, and, to, for, from ,etc...

These similarity is the cosine_similarity measure of every movie with the other movie, the more is the score, the more similar they are.

This recommend is the final function which when run will give the top movies based on the similarity matrix above identifying the top 5 closest similarity scores of the film.

The project code is done now the below code is for running it on local network and depoyment so that after pickle save we can load the required files ahead
