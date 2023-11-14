---
toc: true
comments: true
layout: post
title: Song Recommender
courses: { compsci: {week: 3} }
type: tangibles
---

<head>
    <title>iTunes Search API</title>
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
    <style>
        .result {
            display: inline-block;
            background-color: black;
            color: white;
            border-radius: 25px;
            padding: 10px;
            margin: 10px;
            width: 100%;
        }
        .result img {
            vertical-align: middle;
            margin-right: 10px;
        }
        .search {
            border-radius: 10px;
            padding: 10px;
            border: none;
            outline: none;
        }
        .search-button {
            border-radius: 10px;
            padding: 10px;
            border: none;
            outline: none;
            cursor: pointer;
            font: oxygen;
        }
        .similar-button {
            border-radius: 10px;
            padding: 10px;
            border: none;
            outline: none;
            cursor: pointer;
            font: oxygen;
        }
        .banner {
        position: relative;
        width: 100%;
        height: 150px;
        overflow: hidden;
        width: 300px;
        }
        .banner img {
            width: 100%;
        }
        .banner h1 {
            position: absolute;
            color: black;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
        }
    </style>
</head>
<body>
    <h1>iTunes Music Recommender!</h1>
    <p>A program to find songs similar to your favorite songs! Simply search your song and click on it to find recommendations!</p>
    <input type="text" class="search" id="search" placeholder="Search">
    <button class="search-button" id="search-button">Search</button>
    <div id="results"></div>
    <script>
    // This function searches the iTunes Store for songs of a specific genre and passes the results to a callback function
    function searchItunesByGenre(genre, callback) {
    // Set the base URL for the iTunes search API
    const baseUrl = "https://itunes.apple.com/search";
    // Set the parameters for the search, including the genre, media type, entity, and attribute
    const params = new URLSearchParams({
        term: genre,
        media: "music",
        entity: "song",
        attribute: "genreTerm"
    });
    // Make a GET request to the iTunes search API with the specified parameters
    fetch(`${baseUrl}?${params.toString()}`)
        .then(response => response.json())
        .then(data => {
        // Pass the results to the callback function
        callback(data.results);
        })
        .catch(error => {
        // Log any errors that occur
        console.error("An error occurred while searching the iTunes Store:", error);
        });
    }
    // This function displays the results of an iTunes search on the page
    function displayResults(results) {
    // Clear any previous results
    $('#results').empty();
    // Loop through each result and create an element to display it on the page
    results.forEach(result => {
        var $result = $('<div class="result"></div>');
        $result.append('<img src="' + result.artworkUrl100 + '">');
        $result.append('<br> <span>' + result.collectionName + '</span><br>');
        $result.append('<span>' + result.artistName + '</span><br>');
        $result.append('<span>' + result.primaryGenreName + '</span><br>');
        $('#results').append($result);
    });
    }
    // This code runs when the page is loaded
    $(document).ready(function() {
    // When the search button is clicked, perform a search using the value entered by the user
    $('#search-button').click(function() {
        var searchTerm = $('#search').val();
        $.ajax({
        url: 'https://itunes.apple.com/search?term=' + searchTerm,
        dataType: 'jsonp',
        success: function(data) {
            // Clear any previous results
            $('#results').empty();
            // Loop through each result and create an element to display it on the page
            data.results.forEach(function(result) {
            var $result = $('<div class="result"></div>');
            $result.append('<img src="' + result.artworkUrl100 + '">');
            $result.append('<br> <span>' + result.collectionName + '</span><br>');
            $result.append('<span>' + result.artistName + '</span><br>');
            $result.append('<span>' + result.primaryGenreName + '</span><br>');
            // Create a button to find similar results based on the primary genre of this result
            var $findSimilarButton = $('<button class="similar-button">Find Similar Results</button>');
            $findSimilarButton.click(function() {
                var genre = result.primaryGenreName;
                var genreSearch = searchItunesByGenre(genre, displayResults);
            });
            $result.append($findSimilarButton);
            $('#results').append($result);
            });
        }
        });
    });
    });
</script>
</body>