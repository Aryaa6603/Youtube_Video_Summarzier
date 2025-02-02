```markdown
# YouTube Video Summarization

A Python-based tool that automatically generates concise summaries of YouTube videos using their transcripts and Azure OpenAI's language models.

## Features

- Extracts both auto-generated and manually created transcripts from YouTube videos
- Handles long transcripts by splitting them into manageable chunks
- Generates coherent summaries using Azure OpenAI's GPT models
- Supports multiple languages (based on available transcripts)

## Prerequisites

Before running this project, you need to install the following dependencies:

```bash
pip install ffmpeg-python
pip install triton
pip install transformers torch
pip install yt-dlp ffmpeg-python pydub
pip install youtube-transcript-api
pip install azure-core==1.29.7
pip install azure-ai-openai==1.0.0
pip install openai==1.12.0
```

## Configuration

You'll need to set up Azure OpenAI credentials:
1. Create an Azure OpenAI account
2. Get your API key and endpoint
3. Update the client initialization with your credentials:

```python
client = AzureOpenAI(
    api_key="your-api-key",
    api_version="2024-02-01",
    azure_endpoint="your-azure-endpoint"
)
```

## Usage

1. Import the required modules:
```python
from youtube_transcript_api import YouTubeTranscriptApi
from openai import AzureOpenAI
```

2. Use the main functions:
```python
# Initialize the Azure OpenAI client
client = AzureOpenAI(...)

# Get video transcript
video_id = "YOUR_YOUTUBE_VIDEO_ID"  # e.g., "PyZ0E7ukhBo"
transcript = get_youtube_transcript_auto_generated(video_id)

# Generate summary
summary = get_video_summary(transcript, client)
print(summary)
```

## Main Functions

- `get_youtube_transcript_auto_generated(video_id)`: Fetches and formats the transcript from a YouTube video
- `split_text(text, chunk_size=8000)`: Splits long texts into manageable chunks
- `get_video_summary(transcript, client)`: Generates a summary using Azure OpenAI

## Limitations

- Requires available transcripts (auto-generated or manual) on YouTube videos
- API usage is subject to Azure OpenAI's pricing and rate limits
- Summary quality depends on transcript quality and availability
