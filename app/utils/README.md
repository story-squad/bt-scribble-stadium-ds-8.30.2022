### Overview of `utils` content:

#### `clustering` subfolder:
- `clustering_mvp.py`: Contains two functions: 1) `cluster`, which takes in a dictionary of one cohort's submissions, orders by complexity score, and clusters submission IDs into groups of 4 by score, duplicating 1-3 submission IDs as needed to ensure all clusters contain 4 IDs. Returns a list of lists. 2) `batch_cluster`, which takes a dictionary of nested dictionaries of all the cohort's submission scores for a week and runs them all through the `cluster` function. Returns a JSON object of the returns from each cohort.
- Work for this `.py` file can be found in this [notebook](../../../notebooks/clustering.ipynb).

#### `complexity` subfolder:
- `squad_score.py`: Contains two functions: `metrics`, which generates a single row DataFrame of complexity metrics from a transcription string, and `squad_score` which takes a transcription string, runs it through `metrics`, then generates a complexity metric integer, or "Squad Score."
- Work for this `.py` file can be found in this [notebook](../../../notebooks/squad_score_mvp.ipynb).

#### `img_processing` subfolder:
- `transcription.py`: Utilizes the Google Cloud Vision API and their `document_text_detection` method to transcribe text from a given image
- `safe_search.py`: Utilizes the Google Cloud Vision API and their `safe_search` method to perform moderation of user uploaded illustrations
- `google_api.py`: Utilizes methods from `transcription.py` and `safe_search.py` to provide the DS API with an Object Oriented Programming interface to the Google API and to prepare the google credentials for parsing by the Google API
- `confidence_flag.py`: Utilizes the Google Cloud Vision API to calculate a confidence level for each page transcription. Will return a flag if the confidence level is below 0.85. Work for this `.py` file can be found in this [notebook](../../../notebooks/transcription_confidence.ipynb).

#### `visualization` subfolder:
- `histogram.py`: Creates a Plotly histogram to show the distribution of `squad_scores` of a specified grade level for the current week. Additionally plots a vertical line with the most recent `squad_score` for the specified user to compare against their grade level.
- `line_graph.py`: Creates a Plotly line graph to show the history of a specified user's `squad scores`. 
- Accompanying exploration work for both visuals can be found in the `score_visual` [notebook](../../../notebooks/score_visual.ipynb).

#### `wordcloud` subfolder:
- `wordcloud_demodata_load.py`: We were given a zip file of 167 story submissions (already transcribed) in the form of text files to be used as demo data for our word cloud. This .py file creates a database table of these stories to an ElephantSQL database (you can alter the code to create a table just on your local machine). The table is used in the wordcloud API endpoint as a source to create word clouds with. When the wordcloud feature is integrated with the rest of the app, the data will come from the transcribed stories of real users, and this demo database can be removed. 
    I imported the table into an AWS RDS database (if you can create one in there that would be fine). The wordcloud_database.py API must be connected to an RDS database.
- `wordcloud_functions.py`: Contains the algorithms used in the wordcloud feature to pre-process text and determine what complex words will go in the wordcloud.