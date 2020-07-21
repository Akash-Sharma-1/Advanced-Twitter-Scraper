# Twitter Scraper (Bypassing the Twitter's Official API Limit)

The Twitter API restricts the developer from getting all of a user's tweets (assuming they have more than 3200) by placing an API retrieval limit over the tweets (as well as the information) which is quite understandable given that they have to manage unprecedented amounts of scraping activities over their platform. 
My approach in the implementation of the Scraper and its ideation is to develop a  workaround to go over this problem using Python, Selenium, and Tweepy. However, to admit it might be slower than any other scrapper which directly uses the Twitter API but it is a tradeoff between speed and size. You can go for this approach if you are looking for scraping a big data source from twitter then this will definitely be helpful. 

Essentially, we will use Selenium to open up a browser and automatically visit Twitter's search page, searching for a single user's tweets on a single day. If we want all tweets from 2015, we will check all 365 days / pages. This would be a nightmare to do manually, so the `scrape.py` script does it all for you - all you have to do is input a date range and a twitter user handle, and wait for it to finish.

The `scrape.py` script collects tweet ids. If you know a tweet's id number, you can get all the information available about that tweet using Tweepy - text, timestamp, number of retweets / replies / favorites, geolocation, etc. Tweepy uses Twitter's API, so you will need to get API keys. Once you have them, you can run the `get_metadata.py` script.

## Pre- Requisites

- Basic knowledge on how to use a terminal/cmd
- **WEBDRIVERS**
    - If using Chrome, install ChromeDriver's latest version on the Chrome.
    - If using Safari, version 10+ with 'Allow Remote Automation' option enabled in Safari's Develop menu to control Safari via WebDriver. 
- python3
  - to check, in your terminal, enter `python3`
  - if you don't have it, check YouTube for installation instructions
- pip or pip3
  - to check, in your terminal, enter `pip` or `pip3`
  - if you don't have it, again, check YouTube for installation instructions
- selenium (3.0.1)
  - `pip3 install selenium`
- tweepy (3.5.0)
  - `pip3 install tweepy`

## Running the scraper

- open up `scrape.py` and edit the user, start, and end variables (and save the file)
-  ```python
    # edit these three variables
    user = '____USERNAME HERE____'
    start = datetime.datetime(2018, 12, 19)  # year, month, day
    end = datetime.datetime(2018, 12, 22)  # year, month, day
    ```   
- run `python3 scrape.py`
- you'll see a browser pop up and output in the terminal
- do some fun other task until it finishes
- once it's done, it outputs all the tweet ids it found into `all_ids.json`
- every time you run the scraper with different dates, it will add the new ids to the same file
  - it automatically removes duplicates so don't worry about small date overlaps

## Troubleshooting the scraper

- do you get a `no such file` error? you need to cd to the directory of `scrape.py`
- do you get a driver error when you try and run the script?
  - open `scrape.py` and change the driver to use Chrome() or Firefox()
    - if neither work, google the error (you probably need to install a new driver)
- does it seem like it's not collecting tweets for days that have tweets?
  - open `scrape.py` and change the delay variable to 2 or 3

## Getting the metadata

- first you'll need to get twitter API keys
  - sign up for a developer account here https://dev.twitter.com/
  - get your keys here: https://apps.twitter.com/
  - enable Read and Write operation for the access tokens and keys (Optional)
- put your keys into the `api_keys.json` file
- open up `get_metadata.py` and edit the user variable (and save the file)
    ```python
    user = '____USERNAME HERE____'
    ```   
- run `python3 get_metadata.py`
- this will get metadata for every tweet id in `all_ids.json`
- it will create 4 files
  - `username.json` (master file with all metadata)
  - `username.zip` (a zipped file of the master file with all metadata)
  - `username_short.json` (smaller master file with relevant metadata fields - with less number of fields)
  - `username.csv` (csv version of the smaller master file)

## Warning
| Be careful while running the selenium scraping script repeatedly on Twitter might temporarily ban your account ! |
| --- |

## Author

* **Akash Sharma** <img src="https://image.flaticon.com/icons/png/512/1216/1216686.png" height="10" width="10"> <img src="https://image.flaticon.com/icons/svg/733/733579.svg" height="20" width="20"> - [akashsharma.live](https://www.akashsharma.live/)

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details



