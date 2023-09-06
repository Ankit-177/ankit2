---
toc: true
comments: false
layout: post
title: YouTube Search
description: A tool to search using YouTube.
type: hacks
courses: { compsci: {week: 3} }
---

<html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>YouTube Video Search</title>
</head>
<body>
    <h1>YouTube Video Search</h1>
    <form id="search-form">
        <label for="search-query">Enter your search terms:</label>
        <input type="text" id="search-query" required>
        <button type="submit">Search</button>
    </form>

    <div id="results">
        <!-- Video results will be displayed here -->
    </div>

    <script>
        // Your YouTube Data API key
        const apiKey = 'AIzaSyCTP45umnRZpMJjCMydtUtXjlw-xrpZBEg';

        // Event listener for the search form
        document.getElementById('search-form').addEventListener('submit', function (e) {
            e.preventDefault();

            // Get the user's search query
            const query = document.getElementById('search-query').value;

            // Call the function to fetch video results
            searchYouTubeVideos(query);
        });

        // Function to fetch YouTube video results
        function searchYouTubeVideos(query) {
            // Construct the API URL
            const apiUrl = `https://www.googleapis.com/youtube/v3/search?key=${apiKey}&q=${query}&part=snippet&type=video&maxResults=10`;

            // Make a GET request to the YouTube API
            fetch(apiUrl)
                .then(response => response.json())
                .then(data => {
                    // Handle the response data (list of video results)
                    displaySearchResults(data.items);
                })
                .catch(error => {
                    console.error('Error fetching data:', error);
                });
        }

        // Function to display search results
        function displaySearchResults(items) {
            const resultsContainer = document.getElementById('results');
            resultsContainer.innerHTML = ''; // Clear previous results

            // Loop through the video items and display them
            items.forEach(item => {
                const videoId = item.id.videoId;
                const videoTitle = item.snippet.title;
                const videoThumbnail = item.snippet.thumbnails.default.url;

                // Create a link to the video
                const videoLink = document.createElement('a');
                videoLink.href = `https://www.youtube.com/watch?v=${videoId}`;
                videoLink.textContent = videoTitle;

                // Create an image element for the thumbnail
                const thumbnailImage = document.createElement('img');
                thumbnailImage.src = videoThumbnail;
                thumbnailImage.alt = videoTitle;

                // Create a container for the video link and thumbnail
                const videoContainer = document.createElement('div');
                videoContainer.appendChild(thumbnailImage);
                videoContainer.appendChild(videoLink);

                // Append the container to the results container
                resultsContainer.appendChild(videoContainer);
            });
        }
    </script>
</body>
</html>
