# Task: X/Twitter Data Collection and Annotation

This readme guides you through collecting X/Twitter tweet data using Bright Data and preparing it for upload to our annotation portal: [annotate.osome.iu.edu](https://annotate.osome.iu.edu).

---

## How to Generate a Discourse Dataset from X (formerly Twitter)

1. [Search for a Specific Keyword or Hashtag](#1-search-for-a-specific-keyword-or-hashtag)  
2. [Collect Data for a Specific Time Period](#2-collect-data-for-a-specific-time-period)  
3. [Format for Bright Data Scraping](#3-format-for-bright-data-scraping)  
4. [Clean and Parse Your Scraped Tweet Data](#4-clean-and-parse-your-scraped-tweet-data)  
5. [What to Submit](#5-what-to-submit)
6. [Further Notes](#6-further-notes)


---

## Objective

Your goal is to generate a dataset that sheds light on the online discourse surrounding a **specific keyword or hashtag** (e.g., "Jews", "Israel", or "Zionists") by collecting posts from **X’s “Top” and “Latest” tweets** across **a defined time period**.  

You will then submit the list of tweet URLs to **Bright Data** for structured scraping.

---

## Step-by-Step Instructions

## 1. Search for a Specific Keyword or Hashtag


We recommend starting with the **Advanced Search** feature on [X.com](https://x.com) and using **newly created accounts** to avoid personalized search bias.

- **Search for one keyword only** (e.g., `Jews`, `#Zionists`, etc.)
- Use the **“Top” tab** in X’s search results for high-engagement posts
- Adjust the filters to a specific time range (see below)
- Open the user profile in new tabs and copy the full **accound URL**

> Example Account URL:  
> `https://x.com/elonmusk/`

---

## 2. Collect Data for a Specific Time Period

Use the same keyword for the entire period. Start by collecting **Top Tweets**, and if necessary, switch to **Latest Tweets** to reach your target count.  
If your goal is to collect **100 tweets across one month**, we recommend dividing the timeframe into **weekly chunks** for balanced sampling.

| Period (September 2024)  | Dates                 |
|--------------------------|-----------------------|
| Week 1                   | September 1–7, 2024   |
| Week 2                   | September 8–13, 2024  |
| Week 3                   | September 14–21, 2024 |
| Week 4                   | September 22–29, 2024 |

#### Guidelines:
- Collect **100 tweets** total for your dataset by using the **Advanced Search** feature to select relevant accounts
- Each tweet must contain the **exact keyword or hashtag** you chose
- Use **two-day intervals** within each week to find more content if needed
- Include the best possible variety of different Accounts
- Prioritize tweets from Accounts with **200+ views**, but it’s acceptable to include some below this threshold when necessary
  
---

## 3. Format for Bright Data Scraping

Once you’ve collected all tweet URLs (in a `.csv` or `.txt` file), prepare to scrape full post content using **Bright Data**.

1. Go to:  
   `Bright Data > Web Scrapes > X (Twitter) > Posts > Discover by URL`

2. Click:  
   **Add Inputs** → **Upload CSV** → **Clear All**

3. Required input format:

| URL                              | max_number_of_posts            |
|----------------------------------|--------------------------------|
| Full Account URL (one per row)     |Use a fixed value like `100`    |

> Example CSV structure:
>
> ```csv
> url,max_number_of_posts
> https://x.com/username1,100
> https://x.com/someuser2,100
> ```

*To reach the desired frequency of the dataset including the keyword or hashtag, you may need to scrape multiple hundreds of tweets. Keep in mind that this process is iterative and time-consuming and may require you to expand your list of accounts further.*

---

## 4. Clean and Parse Your Scraped Tweet Data

After scraping user profiles with Bright Data, your output will contain many metadata fields about the account and the scraped posts. One important field is:

- `posts`: This contains a list of tweets returned for each profile as a **JSON string**.

Your task is to extract individual tweets from this `posts` column and isolate the tweets that actually contain the keyword or hashtag you selected.



#### Example Output Columns from Bright Data

Here’s a partial list of the fields you will find in the Bright Data output:

##### **Profile-Level Fields**
- `x_id`: internal user ID  
- `url`: profile URL  
- `id`: Twitter handle  
- `profile_name`, `biography`, `is_verified`  
- `profile_image_link`, `external_link`, `date_joined`  
- `followers`, `following`, `subscriptions`, `posts_count`  
- `is_business_account`, `is_government_account`  
- `location`, `birth_date`, `category_name`  
- `timestamp`: scrape timestamp  
- `input`: original scrape parameters

##### **Post-Level (Nested in `posts`)**
Each tweet object inside `posts` includes:
- `post_id`: **tweet ID**  
- `description`: **tweet text**  
- `post_url`: full URL to the tweet  
- `date_posted`  
- `likes`, `reposts`, `replies`, `views`  
- `photos`: list of media image URLs  
- `videos`: video info (if any)  
- `hashtags`: extracted hashtags (if available)


#### Parsing Script: Extract Tweets and Format for Annotation

We recommend using **Python** 🐍 for this task.  
Please see the code snippet below for parsing the output file.

This script processes the `.csv` file you receive from **Bright Data**, extracts:
  1. all relevant tweet-level information,
  2. filters posts by your chosen keywords or hashtags,
  3. and prepares the final dataset for upload to our annotation portal.

Use the script below to extract Tweet ID and description for each tweet, and save as a `.csv` for further filtering and annotation.

```python
# Load Libraries
import pandas as pd
import json

# Load Bright Data output file
df = pd.read_csv("brightdata_output.csv")

# Define your search terms (case-insensitive)
keywords = ["jews", "#zionists", "#freegaza"]  # <<<<<<<====== Edit this list as needed

# Storage for cleaned and filtered results
parsed_rows = []
text_id = 1

# Iterate through each row in the DataFrame
for _, row in df.iterrows():
    try:
        username = row.get("id", "")  # Twitter handle
        posts_raw = row.get("posts", "")
        if not posts_raw or pd.isna(posts_raw):
            continue

        # Parse JSON posts
        posts = json.loads(posts_raw.replace("'", '"'))

        for post in posts:
            description = post.get("description", "")
            tweet_id = post.get("post_id", "")
            date_posted = post.get("date_posted", "")

            if description and tweet_id:
                if any(kw.lower() in description.lower() for kw in keywords):
                    parsed_rows.append({
                        "text_id": text_id,
                        "Text": description,
                        "tweet_id": tweet_id,
                        "Username": username,
                        "date_posted": date_posted
                    })
                    text_id += 1
    except Exception as e:
        print(f"Error parsing row: {e}")

# Save parsed and filtered results to CSV
df_out = pd.DataFrame(parsed_rows)
df_out.to_csv("parsed_tweets_filtered.csv", index=False, encoding="utf-8")

```

#### The Script will generate the following `.csv` output
| text_id | Text                                                        | tweet_id             | Username     | date_posted            |
|---------|-------------------------------------------------------------|----------------------|--------------|------------------------|
| 1       | Tweet text including specified keyword                      | 1545842080431321088  | username     | 2022-10-28T03:49:11Z   |
| 2       | Tweet text including specified keyword                      | 1519480461749016577  | username     | 2022-04-28T00:56:58Z   |
| 3       | Tweet text including specified keyword                      | 1212256198588662068  | username     | 2024-07-13T22:45:13Z   |
| 4       | Tweet text including specified keyword                      | 1586104694428859648  | username     | 2022-10-28T21:16:42Z   |
| 5       | Tweet text including specified keyword                      | 1854209929529247803  | username     | 2024-11-06T16:39:24Z   |

---

####  How to View a Tweet Using Only Its ID

If you only have the `TweetID` (and not the full URL), you can still access the original tweet in your browser by using the following helper site:

Go to: [https://www.bram.us/](https://www.bram.us/2017/11/22/accessing-a-tweet-using-only-its-id-and-without-the-twitter-api/)

##### Instructions:
1. Copy any Tweet ID from your dataset (e.g., `1585811080431321088`)
2. Paste it into the helper site linked above
3. It will redirect you to the full tweet

---

## 5. What to Submit

Each team should submit the following:

##### A. Cleaned Annotation Dataset (.csv)

- File must contain only tweets that include **one or more of your selected keywords or hashtags**
- Format the file as follows:

| TweetID               | Username     |
|------------------------|--------------|
| 1532051756166926336    | isca_iu      |
| 1176676441666347008    | OSoMe_IU     |
| 1808854301042761934    | IndianaUniv  |

- Column names must be **TweetID** and **Username** (case-sensitive)
- Save file as: `your_final_annotation_input.csv` (specify this with your keyword)
- This file is ready to be uploaded to our annotation portal at [annotate.osome.iu.edu](https://annotate.osome.iu.edu)



##### B. Report (PDF or Markdown)
- A brief report (1–2 pages) that includes:
  - The keyword(s) or hashtag(s) used
  - Your rationale for selecting them
  - The date range used and why
  - Notes on manual filtering or scraping inconsistencies
  - Total number of tweets after filtering
  - The amount of antisemitic or biased content within the dataset
  - The annotation scheme that was used a standardized annotation guideline, e.g., based on the [IHRA-WDA](https://github.com/AnnotationPortal/DatathonandHackathon.github.io/blob/main/guides/annotation_scheme.md)


##### C. (Optional) Full Extracted Dataset

You may optionally submit a separate file that includes:
- `tweet_id`, `text`, `date_posted`, `likes`, `reposts`, `views`, etc.
- For students interested in exploring engagement, virality, or post type

---

### Reminder

- Ensure that your **Tweet IDs are stored as strings**, not numbers, to avoid truncation or formatting issues in Excel or Google Sheets. When in doubt, open the file in a plain text editor or use `.csv` in UTF-8.

---

## 6. Further Notes

- You may work in pairs or small teams
- Be consistent: only collect tweets containing the **exact keyword or hashtag**
- Avoid replies or retweets unless directly relevant

---
