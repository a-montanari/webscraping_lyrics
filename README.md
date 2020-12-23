# Web Scraping Lyrics

This repositotry contains a series of functions that can be used to scrape [AZLyrics.com](https://www.azlyrics.com) and download lyrics in *txt* format.

## Functions

- `save_file(path, text, replace=False)`  
This is an auxiliary function used to save a given *text* in a *txt* file.
  
- `get_lyrics(song_url, save=True, by_decade=True, replace=False, folder="songs")`  
This function can be used to download the lyrics of a **single song**, given its page url.
    - *song_url*: The AZLyrics url of the page containing the song.
    - *save*: if True (default), the lyrics are saved in a txt file named as the song title. If False, the function just returns the song title, lyrics and year as a 3-dimensional tuple.
    - *by_decade*: if True (default), and *save*=True, the lyrics are saved in a folder named as the decade when the song was produced. If False, and *save*=True, the lyrics are just stored in a generic folder.
    - *folder*: the name of the folder where the txt lyrics will be saved.
  
- `scrape_artist(az_url, sleep="random", by_decade=True, replace=False, folder="songs")`  
This function downloads **all the lyrics of a given artist**, starting from their page url.  
    - *az_url*: The artist main page url on AZLyrics.
    - *sleep*: This is the sleeping time between iterations. By default it is set to *"random"*, which means that the sleeping time is randomly selected at each iteration between 5 and 15 seconds. This has been tested and it avoids being recognized as a bot, resulting in your IP to be temporarly banned. You can also set this to a fixed time, but it is recommended to keep it around 10 seconds as shorter intervals may be problematic.
    - *by_decade*: if True (default), the lyrics are saved in a folder named as the decade when the song was produced. If False, the txt lyrics are just stored in a generic folder.
    - *replace*: If False (default), if two or more songs have the same name, all lyrics are saved in separate files. If True, then only the latest one gets saved.
    - *folder*: the name of the folder where the txt lyrics will be saved.
  
- `get_artists(letter, home="https://www.azlyrics.com/")`  
Another auxiliary function, which returns the urls and names of all the artists whose names start with a given *letter*.
  
- `scrape_all(letters="all", sleep="random", by_decade=True, replace=False, folder="songs")`  
This function **downloads all the lyrics af all artists whose names start with a given *letter*. Note: I have estimated that in order to download each song of every artist on AZLyrics, the function should run non-stop for ~ 27 weeks, given an average sleep time of 10 seconds between iterations. So this is just for fun and not meant for actual use.**
    - *letters*: A list containing all the letters whose corresponding artists' lyrics should be downloaded. By default, it is set to "all", which means that every lyric contained on AZLyrics is downloaded.
    - *sleep*: This is the sleeping time between iterations. By default it is set to *"random"*, which means that the sleeping time is randomly selected at each iteration between 5 and 15 seconds. This has been tested and it avoids being recognized as a bot, resulting in your IP to be temporarly banned. You can also set this to a fixed time, but it is recommended to keep it around 10 seconds as shorter intervals may be problematic.
    - *by_decade*: if True (default), the lyrics are saved in a folder named as the decade when the song was produced. If False, the txt lyrics are just stored in a generic folder.
    - *replace*: If False (default), if two or more songs have the same name, all lyrics are saved in separate files. If True, then only the latest one gets saved.
    - *folder*: the name of the folder where the txt lyrics will be saved. If set to *"names"*, then each artist will be downloaded in a separate folder with the corresponding name. Otherwise, all lyrics are collected in the same folder.
  
## Examples:

Downloading all lyrics on AZLyrics.com: (*See warning above!*)
> `scrape_all(letters="all")`
  
  
Downloading all lyrics of every artist starting with "a", each artist in a separate folder: (*ETA = 1 week*)
> `letter_list = ["a"]`  
> `scrape_all(letter_list, folder="names")`  
  
  
Downloading all lyrics of a given artist:
> `bruce = "https://www.azlyrics.com/s/springsteen.html"`  
> `scrape_artist(bruce, folder="bruce")`
  
  
Downloading a single song lyrics:
> `the_chain = "https://www.azlyrics.com/lyrics/fleetwoodmac/thechain.html"`  
> `get_lyrics(the_chain, by_decade=False, folder="fwm")`
