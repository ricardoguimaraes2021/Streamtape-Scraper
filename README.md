
# Streamtape Video Source Scraper

This project is a **Node.js** and **Express** API that uses **Puppeteer** to scrape the source URL of a video from a Streamtape link. The API dynamically receives the Streamtape URL and returns the direct `src` attribute of the video.

## Features

- **Dynamic URL Passing**: Pass any Streamtape video URL dynamically to get the source URL.
- **Error Handling**: Provides helpful error messages if the video element isn’t found or if there’s an issue fetching the URL.
- **Flexible Deployment**: Easily set up on platforms like Glitch or local development environments.

## Dependencies

- **Node.js** (version 14.x)
- **Express**: Web framework for Node.js
- **Puppeteer**: Headless browser for web scraping

---

## Usage

To use the API, make a **GET** request to the `/api` endpoint with the Streamtape video URL passed as a query parameter.

### Example

```javascript
const get_movie_token = "https://streamtape.com/v/7zeY3yGXYzfA1rz";
const apiEndpoint = `http://localhost:3000/api?url=${encodeURIComponent(get_movie_token)}`;

fetch(apiEndpoint)
  .then(response => response.text())
  .then(data => {
    console.log("Video Source URL:", data);  // Handle or display the video source URL
  })
  .catch(error => {
    console.error("Error fetching video source URL:", error);
  });
```

### Hosted on Glitch

If hosted on Glitch, access it at:

```
https://your-glitch-project-url/api?url=https://streamtape.com/v/7zeY3yGXYzfA1rz
```

---

## API Endpoint

- **GET** `/api?url=<streamtape-video-url>`
  - **Query Parameter**: `url` (required) - The URL of the Streamtape video you want to fetch the source for.

### Example Response

If successful, the API will return the direct `src` URL of the video element:

```
Video source URL: //streamtape.com/get_video?id=7zeY3yGXYzfA1rz&expires=1730470157&ip=F0uWKRSODS9XKxR&token=KaQQr7Ovax4H&stream=1
```

---

## Handling Errors

If there is an issue with fetching the video source URL, the API will return an appropriate error message with a status code:

- **404**: If the video element is not found or missing the `src` attribute.
- **500**: For server errors or other unexpected issues.

---

## How It Works

1. **Request Handling**: The Express server receives the URL via the `url` query parameter.
2. **Puppeteer Launch**: Puppeteer launches a headless browser and navigates to the provided Streamtape URL.
3. **Element Selection**: The API waits for the `<video>` element with `id="mainvideo"` to load and extracts its `src` attribute.
4. **Response**: The API returns the `src` attribute of the video, providing a direct link to the video content.

---

## Troubleshooting

- **Cannot GET /api**: Make sure you’re appending the `?url=<your-streamtape-url>` parameter when accessing `/api`.
- **Video Element Not Found**: Verify that the Streamtape URL is valid and accessible.

--- 

## Author

Created by [Ricardo Guimaraes](https://github.com/ricardoguimaraes2021)
