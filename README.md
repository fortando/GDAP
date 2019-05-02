# GDAP
Project Work for Galvanize Data Analytics Course

<b>Overall Concept:</b> 
Analyze, Compare, and Contrast two distinct Playlists on Spotify. 

<b>Playlists Used:</b> 
Spotify's  "Top Tracks of 2018" at https://open.spotify.com/playlist/37i9dQZF1DX1HUbZS4LEyL
Personal running Playlist of "starred" Tracks at https://open.spotify.com/playlist/3lhurT1hRMXjfWn9Y6EAvR

<b>Data Sourcing:</b>
Spotify identifies tracks and playlists by unique, multi-character IDs. Further, it defines them along a series of Attributes. These Attributes may be literal measures (e.g. Duration_MS: a fixed numerical value) or interpretive along a scale (e.g. "Danceability": a subjective assessment based on a combination of values, scaled from 0.0 - 1.0). Spotify permits API calls and offers suite of tools ("developer console" - https://developer.spotify.com/) to allow access to track identifiers and attributes. I downloaded the Top Tracks playlist as provided, and subsequently downloaded my Starred playlist information and track attributes in two sets of three requests each, as the Developer Console has a 100 track limit per request.  A complete list of the "Features" Attributes which form the majority of my analysis is located at https://developer.spotify.com/documentation/web-api/reference/tracks/get-audio-features/

<b>Data Preparation:</b>
I used the Top2018 Data as my Template, and structured the KWS Data to match. This involved combining the 3 request returns into a single file, removing extraneous columns (e.g. "type" and "uri"). I then uploaded the data via pgAdmin4 to my local server to permit querying for necessary data. The final project draws from three primary Data Sources: Top2018, KWS, and Joined_100. 
Top2018 required changing the "duration_ms" attribute to display track length in seconds, rather than milliseconds, which i accomplished via the SQL functions "CAST", "ROUND", and "/". Aside from some minor character edits, little other manipulation was required. 
KWS required me to "JOIN" the Playlist details and Track Attributes tables into a single output table. I again queried to display track length in seconds rather than milliseconds. Furthermore, after I exported the joined table, I pared the list down to 100 tracks, to match the total to Top2018. I chose to do this manually, as Spotify does not include date of addition to a playlist as a returned attribute. It does, however, return results in chronologically descending order (oldest to newest), so manual selection of tracks was simple. 
Joined_100 involved a union of KWS and Top2018 (possible as I had previously removed extraneous columns and had uploaded them via pgAdmin with the same column data types) into a single table. For comparative purposes, I manually added a column to differentiate the Source playlist (KW vs. TS) to the finished table. 

<b>Visualization:</b>
My final workbook contains 7 dashboards and their associated worksheets. I categorized the attributes into 3 distinct categories reflecting their overall contribution to the composition of a track: <i>Timing</i>, <i>Feeling</i>, <i>and Sound</i>.
The Workbook Dashboards are as follows:

INTRO - Explains the Concept, and contains embedded URLs for each playlist, so the User can reference the tracks and track Attributes to the actual music. 
TIMING - an analysis of each playlist's timing attributes: Tempo, Duration Sec, and Time Signature. These attributes are represented as a scatterplot, with Tempo as the Y-Axis and Duration as the X-Axis, with Shapes to distinguish tracks by Time Signature.
FEELING - The Danceability, Energy, Mode, and Valence of each playlist, displayed as Highlight Tables, ordered on a 0-1 Scale. The tables are sortable, and I sorted by Valence, as it is likely to require the most explanation. 
SOUND - The Acousticness, Instrumentalness, Liveness, and Speechiness of each playlist, displayed as Stacked Bars, ordered on a 0-1 Scale. 
COMPARISON - An assessment of the Average Attribute Values of both tables displayed as a Line Graph, and a combined Scatterplot of the Timing attributes. 
CORRELATION - An interactive scatterplot, with dynamic Axes based on User selection of attributes to compare. The user may adjust the table based on Filters for Source playlist, Tracks to display, and Attributes to Compare. A dynamic Trend Line is hard-coded to assist the User in establishing correlations, if any exist. 
A&D - Attributions and Disclaimers. 

<b>GitHub Organization:</b>
The Repo for this project is organized into three folders: 
Project Final: The final data sources and Tableau workbook. 
Project Work: Work-In-Progress Data sheets, Data Load examples, and Replicated Queries to dmeonstrate the processes used to obtain and manipulate the Data as Necessary. 
Course Completion: Examples of Pivot Tables, vLookups, and Excel cleaning, since none were required to complete the Data Sources used. 
