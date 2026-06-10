# trendpulse-NANDDANAA_BOBBA
Task 1 — Fetch Data from API
TrendPulse: What's Actually Trending Right Now
Marks: 20 | File: task1_data_collection.py

Submission: Push your file to a public GitHub repo and share the direct link: https://github.com/<username>/trendpulse-<name>/blob/main/task1_data_collection.py

⚠️ Anti-AI Policy: Write your own code. Comments explaining your logic count in your favour.

The Project
TrendPulse is a 4-part pipeline you'll build one task at a time:

Task 1      →    Task 2      →    Task 3       →    Task 4
Fetch JSON       Clean CSV        NumPy/Pandas      Visualise
Start here. Each task uses the output of the previous one.

What to Build
HackerNews has a free, fully open API that returns trending stories as JSON — no login, no key, no sign-up needed.

You will fetch trending stories and group them into 5 categories: technology, worldnews, sports, science, entertainment

Assign a category to each story by checking whether its title contains any of these keywords:

Category	Keywords to match (case-insensitive)
technology	AI, software, tech, code, computer, data, cloud, API, GPU, LLM
worldnews	war, government, country, president, election, climate, attack, global
sports	NFL, NBA, FIFA, sport, game, team, player, league, championship
science	research, study, space, physics, biology, discovery, NASA, genome
entertainment	movie, film, music, Netflix, game, book, show, award, streaming
Step 1 — Get the list of top story IDs:

https://hacker-news.firebaseio.com/v0/topstories.json
This returns a JSON array of story IDs (integers). Fetch the first 500.

Step 2 — Get each story's details:

https://hacker-news.firebaseio.com/v0/item/{id}.json
This returns a single story object.

Add this header to your requests:

headers = {"User-Agent": "TrendPulse/1.0"}
Tasks
1 — Make the API Calls (8 marks)
Use the requests library to fetch the top story IDs, then fetch each story's details
If a request fails, print a message and move on — don't crash the script
Wait 2 seconds between each category (time.sleep(2)) — one sleep per category loop, not per individual story fetch
2 — Extract the Fields (7 marks)
From each story, save these fields:

Field	HackerNews field	Description
post_id	id	Unique ID of the story
title	title	Story title
category	(your category)	The category you assigned based on keywords
score	score	Number of upvotes
num_comments	descendants	Number of comments
author	by	Username of the story author
collected_at	(add yourself)	The current date and time
Collect up to 25 stories per category (125 total).

3 — Save to a JSON File (5 marks)
Create a folder called data/ if it doesn't exist
Save all stories to a file like data/trends_20240115.json
Print how many stories were collected in total
Expected Output
After running your script, you should have:

A file at data/trends_YYYYMMDD.json
At least 100 stories inside it
A console message like: Collected 122 stories. Saved to data/trends_20240115.json

Task 2 — Clean the Data & Save as CSV
TrendPulse: What's Actually Trending Right Now
Marks: 20 | File: task2_data_processing.py

Submission: Push your file to the same public GitHub repo and share the direct link: https://github.com/<username>/trendpulse-<name>/blob/main/task2_data_processing.py

⚠️ Anti-AI Policy: Write your own code. Comments explaining your logic count in your favour.

Needs: The JSON file from Task 1 (data/trends_YYYYMMDD.json)

What to Build
The raw JSON from Task 1 may have messy data — duplicate stories, missing values, wrong types. Your job is to load it with Pandas, clean it up, and save it as a tidy CSV file.

Tasks
1 — Load the JSON File (4 marks)
Load the JSON file from the data/ folder into a Pandas DataFrame
Print how many rows were loaded
2 — Clean the Data (10 marks)
Fix the following issues:

Duplicates — remove any rows with the same post_id
Missing values — drop rows where post_id, title, or score is missing
Data types — make sure score and num_comments are integers
Low quality — remove stories where score is less than 5
Whitespace — strip extra spaces from the title column
Print the number of rows remaining after cleaning.

3 — Save as CSV (6 marks)
Save the cleaned DataFrame to data/trends_clean.csv
Print a confirmation message with the number of rows saved
Also print a quick summary: how many stories per category
Expected Output
Loaded 122 stories from data/trends_20240115.json

After removing duplicates: 120
After removing nulls: 118
After removing low scores: 114

Saved 114 rows to data/trends_clean.csv

Stories per category:
  technology      22
  worldnews       24
  sports          21
  science         24
  entertainment   23
  Task 3 — Analysis with Pandas & NumPy
TrendPulse: What's Actually Trending Right Now
Marks: 20 | File: task3_analysis.py

Submission: Push your file to the same public GitHub repo and share the direct link: https://github.com/<username>/trendpulse-<name>/blob/main/task3_analysis.py

⚠️ Anti-AI Policy: Write your own code. Comments explaining your logic count in your favour.

Needs: data/trends_clean.csv from Task 2

What to Build
Load the clean CSV from Task 2 and explore the data using Pandas and NumPy. Find patterns, compute statistics, and add a couple of new columns. Save the result as a new CSV for Task 4.

Tasks
1 — Load and Explore (4 marks)
Load data/trends_clean.csv into a Pandas DataFrame
Print the first 5 rows
Print the shape of the DataFrame (rows and columns)
Print the average score and average num_comments across all stories
2 — Basic Analysis with NumPy (8 marks)
Use NumPy to answer these questions and print the results:

What is the mean, median, and standard deviation of score?
What is the highest score and lowest score?
Which category has the most stories?
Which story has the most comments? Print its title and comment count.
3 — Add New Columns (5 marks)
Add these two new columns to your DataFrame:

Column	Formula
engagement	num_comments / (score + 1) — how much discussion a story gets per upvote
is_popular	True if score > average score, else False
4 — Save the Result (3 marks)
Save the updated DataFrame (with the 2 new columns) to data/trends_analysed.csv
Print a confirmation message
Expected Output
Loaded data: (114, 7)

First 5 rows:
   post_id   title             category   score  num_comments ...

Average score   : 12,450
Average comments: 342

--- NumPy Stats ---
Mean score   : 12,450
Median score : 8,200
Std deviation: 9,870
Max score    : 87,432
Min score    : 5

Most stories in: technology (22 stories)

Most commented story: "AI model beats humans at coding"  — 4,891 comments

Saved to data/trends_analysed.csv
Task 4 — Visualizations
TrendPulse: What's Actually Trending Right Now
Marks: 20 | File: task4_visualization.py

Submission: Push your file to the same public GitHub repo and share the direct link: https://github.com/<username>/trendpulse-<name>/blob/main/task4_visualization.py

⚠️ Anti-AI Policy: Write your own code. Comments explaining your logic count in your favour.

Needs: data/trends_analysed.csv from Task 3

What to Build
Load the CSV from Task 3 and create 3 charts using Matplotlib. Then combine them into a single dashboard figure. Save everything as PNG files.

Tasks
1 — Setup (2 marks)
Load data/trends_analysed.csv into a DataFrame
Create a folder called outputs/ if it doesn't exist
Use plt.savefig() before any plt.show() on all charts
2 — Chart 1: Top 10 Stories by Score (6 marks)
Create a horizontal bar chart showing the top 10 stories by score
Use the story title on the y-axis (shorten titles longer than 50 characters)
Add a title and axis labels
Save as outputs/chart1_top_stories.png
3 — Chart 2: Stories per Category (6 marks)
Create a bar chart showing how many stories came from each category
Use a different colour for each bar
Add a title and axis labels
Save as outputs/chart2_categories.png
4 — Chart 3: Score vs Comments (6 marks)
Create a scatter plot with score on the x-axis and num_comments on the y-axis
Colour the dots differently for popular vs non-popular stories (use the is_popular column)
Add a legend, title, and axis labels
Save as outputs/chart3_scatter.png
Bonus — Dashboard (+3 marks)
Combine all 3 charts into one figure:

Use plt.subplots(1, 3) or plt.subplots(2, 2) to lay them out together
Add an overall title: "TrendPulse Dashboard"
Save as outputs/dashboard.png
Expected Output Files
outputs/
├── chart1_top_stories.png
├── chart2_categories.png
├── chart3_scatter.png
└── dashboard.png  (bonus)
