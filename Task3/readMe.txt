The main idea behind this api is to successfully construct the appropriate urls that could return the information we need to store in our database.

To be more specific we can use the basic (https://api.themoviedb.org/3/discover/movie?api_key=') url along with the certification_country and sort_by_popularity url additions in order to collect all the movies that are popular in Greece. The result is a json file that contains basic information like the movie title and the overview needed for each movie. Based on that we create our first Dataframe which will contain only the fields that were needed.

For more specific information like the Director's name we need to take the advantage of the movie ids info that is stored on our json storage file after the first parse.

The next step is to create a second url with the difference that we will replace the discover/movie path with the movie/movieid/credits path. That will help us to get information for each movie id that we have stored in our file.

During the parsing loop of this url, we extract only the json parts that are related with our target which is Crew members whose their job is 'Director'. We can store this specific job information in a Python list and then collect only the Json Dictionaries that contain this word. The final result is a pandas dataframes which has the movieid along with the director's name and the director's imdb id.

We can union this second dataframe with the first, with purpose to get one final dataframe that will contain only the information that we want to store in our relational database.

Finally using the pyodbc library we can store our final dataframe in an SQL Server Table called MoviesTable as per request. During the insert operation we filter the duplicate movies by allowing only new movies to be stored in our table.  

