from googleapiclient.discovery import build
import pandas as pd

# Replace 'YOUR_API_KEY' with your actual API key
api_key = 'AIzaSyBtbMjGQ_fn91ZlEUiDFt9nWxN2wRSHhx0'
youtube = build('youtube', 'v3', developerKey=api_key)

video_id = 'ssscgas9iL0'  # Replace with the ID of the YouTube video you want to analyze

request = youtube.videos().list(
    part='snippet,statistics',
    id=video_id
)

response = request.execute()
video_info = response['items'][0]

data = {
    'Video ID': video_info['id'],
    'Title': video_info['snippet']['title'],
    'Published At': video_info['snippet']['publishedAt'],
    'Views': video_info['statistics']['viewCount'],
    'Likes': video_info['statistics']['likeCount'],
    'Comments': video_info['statistics']['commentCount'],
}

df = pd.DataFrame([data])
df
	Video ID	Title	Published At	Views	Likes	Comments
0	ssscgas9iL0	List & Tuple - Python Complete Course | Most I...	2024-03-08T12:59:18Z	1026	70	18
