---
toc: true
comments: false
layout: post
title: Wikipedia Search
description: A tool to search using Wikipedia.
type: hacks
courses: { compsci: {week: 3} }
---

<html>
<head>
    <title>Wikipedia Search</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            margin-top: 50px;
        }
        #search-input {
            width: 300px;
            padding: 5px;
            font-size: 16px;
        }
        #search-button {
            padding: 5px 10px;
            font-size: 16px;
            cursor: pointer;
        }
        #search-results {
            margin-top: 20px;
            text-align: left;
        }
    </style>
</head>
<body>
    <h1>Wikipedia Search</h1>
    <input type="text" id="search-input" placeholder="Enter a search term">
    <button id="search-button">Search</button>
    <div id="search-results"></div>
    <script>
        const searchInput = document.getElementById('search-input');
        const searchButton = document.getElementById('search-button');
        const searchResults = document.getElementById('search-results');
        searchButton.addEventListener('click', () => {
            const searchTerm = searchInput.value;
            if (searchTerm.trim() === '') {
                alert('Please enter a search term.');
                return;
            }
            // Make a request to the Wikipedia API
            fetch(`https://en.wikipedia.org/w/api.php?action=query&format=json&origin=*&list=search&srsearch=${searchTerm}`)
                .then(response => response.json())
                .then(data => {
                    displayResults(data.query.search);
                })
                .catch(error => {
                    console.error(error);
                });
        });
        function displayResults(results) {
            searchResults.innerHTML = ''; // Clear previous results
            if (results.length === 0) {
                searchResults.innerHTML = 'No results found.';
                return;
            }
            results.forEach(result => {
                const title = result.title;
                const snippet = result.snippet;
                const link = `https://en.wikipedia.org/wiki/${encodeURIComponent(title)}`;
                const resultElement = document.createElement('div');
                resultElement.innerHTML = `<h3><a href="${link}" target="_blank">${title}</a></h3>${snippet}`;
                searchResults.appendChild(resultElement);
            });
        }
    </script>
</body>
</html>