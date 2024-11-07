# Personalized-Music-Recommendation-System-

# Spotify Music Recommendation System

## Overview
A sophisticated music recommendation system built using the Spotify API that leverages collaborative filtering and audio feature analysis to provide personalized music suggestions. The system combines content-based filtering with weighted popularity scores to deliver up-to-date and relevant recommendations.

## Features
- Personalized music recommendations based on user preferences
- Audio feature analysis (danceability, energy, tempo, etc.)
- Weighted popularity scoring based on release dates
- Hybrid recommendation approach combining content-based and popularity-based filtering
- Integration with Spotify API for real-time music data
- Support for playlist-based recommendations
- Comprehensive audio feature extraction and analysis

## Prerequisites
- Python 3.7+
- Spotify Developer Account
- Spotify API Credentials (Client ID and Client Secret)

## Installation

```bash
# Clone the repository
git clone https://github.com/yourusername/spotify-music-recommender.git

# Navigate to project directory
cd spotify-music-recommender

# Install required packages
pip install -r requirements.txt
```

## Required Libraries
```txt
spotipy==2.23.0
pandas==1.5.3
numpy==1.24.2
scikit-learn==1.2.2
requests==2.28.2
```

## Getting Started

### 1. Set Up Spotify API Credentials
1. Create a Spotify account (if you don't have one)
2. Visit the [Spotify Developer Dashboard](https://developer.spotify.com/dashboard/)
3. Create a new app and get your Client ID and Client Secret
4. Set up your credentials in `config.py`:

```python
CLIENT_ID = 'your_client_id_here'
CLIENT_SECRET = 'your_client_secret_here'
```

### 2. Initialize the System

```python
import base64
import requests
from music_recommender import get_trending_playlist_data, hybrid_recommendations

# Get access token
client_credentials = f"{CLIENT_ID}:{CLIENT_SECRET}"
client_credentials_base64 = base64.b64encode(client_credentials.encode())

token_response = requests.post(
    'https://accounts.spotify.com/api/token',
    data={'grant_type': 'client_credentials'},
    headers={'Authorization': f'Basic {client_credentials_base64.decode()}'}
)

access_token = token_response.json()['access_token']
```

### 3. Get Music Data

```python
# Use any Spotify playlist ID
playlist_id = '0m1VJLRGMhC9CFdNczFad9'
music_df = get_trending_playlist_data(playlist_id, access_token)
```

### 4. Generate Recommendations

```python
# Get recommendations for a specific song
recommendations = hybrid_recommendations(
    input_song_name="Your Song Name",
    num_recommendations=5,
    alpha=0.5  # Balance between content-based and popularity-based recommendations
)
```

## System Architecture

### Data Collection
- Utilizes Spotify API to fetch track information
- Extracts audio features, popularity metrics, and metadata
- Supports playlist-based data collection

### Feature Processing
- Audio feature normalization using MinMaxScaler
- Weighted popularity calculation based on release dates
- Feature extraction for similarity computation

### Recommendation Engine
1. **Content-Based Filtering**
   - Analyzes audio features (danceability, energy, etc.)
   - Computes similarity using cosine similarity
   - Recommends songs with similar acoustic properties

2. **Popularity-Based Filtering**
   - Considers track popularity
   - Applies time-based weighting for recent releases
   - Ensures recommendations stay current

3. **Hybrid Approach**
   - Combines content-based and popularity-based recommendations
   - Customizable weighting between approaches
   - Provides balanced and relevant suggestions

## Key Components

### 1. Data Collector
```python
def get_trending_playlist_data(playlist_id, access_token):
    # Fetches and processes playlist data
    # Returns DataFrame with track information and audio features
```

### 2. Recommendation Generator
```python
def hybrid_recommendations(input_song_name, num_recommendations=5, alpha=0.5):
    # Generates hybrid recommendations
    # Combines content-based and popularity-based approaches
```

### 3. Feature Calculator
```python
def calculate_weighted_popularity(release_date):
    # Calculates time-weighted popularity scores
    # Gives preference to recent releases
```

## Contributing
1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments
- Spotify API for providing access to music data
- scikit-learn for machine learning implementation
- Spotipy library for Spotify API integration

## Author
Your Name - Nephyedge(https://github.com/Nephyedge)
