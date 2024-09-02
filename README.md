# web-scraping-with-beautifulsoup-
<h2>Introduction:</h2>

This project is a web scraping script that extracts movie titles from a specific webpage and saves them to a text file. The script uses Python's requests library to fetch the webpage content and BeautifulSoup to parse the HTML and extract the relevant data. The movie titles are then listed in reverse order and stored in a file named movies.txt.
This project is a practical example of how to use web scraping to automate the extraction of data from a website.

<h2>Explanation:</h2>

<b>1. Importing Required Libraries</b>
```
import requests
from bs4 import BeautifulSoup
```

```requests```:  A Python library used to send HTTP requests. It helps in retrieving the content of a web page.
```BeautifulSoup```:  A library used to parse HTML and XML documents. It allows for easy navigation and extraction of data from HTML.

<b>2. Setting the Target URL</b>
```
URL = "https://web.archive.org/web/20200518073855/https://www.empireonline.com/movies/features/best-movies-2/"
```
```URL```: This is the web address of the archived page containing a list of movies. The URL points to a specific version of the webpage stored on the Wayback Machine (web.archive.org).

<b>3. Sending an HTTP GET Request</b>
```
response = requests.get(URL)
website_html = response.text
```
```requests.get(URL)```: Sends a GET request to the specified URL and retrieves the content of the webpage.
response.text: Extracts the HTML content of the webpage as a string.

<b>4. Parsing the HTML Content</b>
```
soup = BeautifulSoup(website_html, "html.parser")
```
```BeautifulSoup(website_html, "html.parser")```:  Parses the HTML content using the built-in html.parser. This creates a BeautifulSoup object, soup, that represents the document as a nested data structure (parse tree).



<b>5. Finding All Movie Titles</b>
```
all_movies = soup.find_all(name="h3", class_="title")
```
```soup.find_all(name="h3", class_="title")```: Finds all ```<h3>``` elements with the class "title". These elements contain the movie titles on the webpage.

```all_movies```: A list of Tag objects, each representing an ```<h3>``` element with the movie title.

<b>6. Extracting and Reversing Movie Titles</b>
```
movie_titles = [movie.getText() for movie in all_movies]
movies = movie_titles[::-1]
```
```movie.getText()```:  Extracts the text content from each ```<h3>``` element, which is the movie title.

```movie_titles```: A list of all movie titles extracted from the webpage.

```movies = movie_titles[::-1]```: Reverses the order of the list, so the movies are listed in ascending order (from the first to the last) rather than descending.

<b>7. Writing Movie Titles to a Text File</b>

```
with open("movies.txt", mode="w",encoding="utf-8") as file:
    for movie in movies:
        file.write(f"{movie}\n")
```
```open("movies.txt", mode="w", encoding="utf-8")```: Opens (or creates) a text file named movies.txt in write mode. The encoding="utf-8" ensures that the file is saved with UTF-8 encoding, which is useful for handling special characters.
```file.write(f"{movie}\n")```: Writes each movie title to a new line in the text file.
```with```: Ensures that the file is properly closed after writing, even if an error occurs.

<h2>Summary</h2>

This script retrieves the HTML content of a webpage containing a list of the best movies, extracts the movie titles using BeautifulSoup, reverses the order of the titles, and saves them to a text file named movies.txt.
