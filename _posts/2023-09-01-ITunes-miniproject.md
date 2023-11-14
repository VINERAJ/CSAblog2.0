<!-- ---
toc: false
comments: false
layout: post
title: ITunes genre project
description: User can type in a song, program will return songs in that genre
courses: { compsci: {week: 3} }
type: tangibles
--- -->

<div>
  <input type="text" id="filterInput" placeholder="Enter song">
  <button onclick="fetchData()">Search</button>
</div>

<table>
  <thead>
    <tr>
      <th>Artist</th>
      <th>Genre</th>
      <th>Track</th>
      <th>Images</th>
      <th>Preview</th>
      <th>Search Genre</th>
    </tr>
  </thead>
  <tbody id="result">
    <!-- generated rows -->
  </tbody>
</table>

<!-- Script is laid out in a sequence (no function) and will execute when the page is loaded -->
<script>
  // prepare HTML result container for new output
  const resultContainer = document.getElementById("result");

  // function to fetch data based on user input
  function fetchData() {
    // clear previous results
    resultContainer.innerHTML = "";

    // get user input
    const filterInput = document.getElementById("filterInput");
    const filter = filterInput.value;

    // prepare fetch options
    const url = "https://itunes.apple.com/search?term=" + encodeURIComponent(filter);
    const headers = {
      method: 'GET',
      mode: 'cors',
      cache: 'default',
      credentials: 'omit',
      headers: {
        'Content-Type': 'application/json'
      },
    };

    // fetch the API
    fetch(url, headers)
      .then(response => {
        // check for response errors
        if (response.status !== 200) {
          const errorMsg = 'Database response error: ' + response.status;
          console.log(errorMsg);
          const tr = document.createElement("tr");
          const td = document.createElement("td");
          td.innerHTML = errorMsg;
          tr.appendChild(td);
          resultContainer.appendChild(tr);
          return;
        }
        // valid response will have JSON data
        response.json().then(data => {
          console.log(data);

          // Music data
        for (const row of data.results) {
            console.log(row);

            // tr for each row
            const tr = document.createElement("tr");
            // td for each column
            const artist = document.createElement("td");
            const genre = document.createElement("td")
            const track = document.createElement("td");
            const image = document.createElement("td");
            const preview = document.createElement("td");
            const searchGenre = document.createElement('BUTTON')
            const text = document.createTextNode("click to see songs of this genre")
            searchGenre.appendChild(text)

            // data is specific to the API
            artist.innerHTML = row.artistName;
            genre.innerHTML = row.primaryGenreName
            track.innerHTML = row.trackName; 
            // create preview image
            const img = document.createElement("img");
            img.src = row.artworkUrl100;
            image.appendChild(img);
            // create preview player
            const audio = document.createElement("audio");
            audio.controls = true;
            const source = document.createElement("source");
            source.src = row.previewUrl;
            source.type = "audio/mp4";
            audio.appendChild(source);
            preview.appendChild(audio);

            // this builds td's into tr
            tr.appendChild(artist);
            tr.appendChild(genre)
            tr.appendChild(track);
            tr.appendChild(image);
            tr.appendChild(preview);
            tr.appendChild(searchGenre)

            // add HTML to container
            resultContainer.appendChild(tr);
          }
        })
      })
      .catch(err => {
        console.error(err);
        const tr = document.createElement("tr");
        const td = document.createElement("td");
        td.innerHTML = err;
        tr.appendChild(td);
        resultContainer.appendChild(tr);
      });
  }
</script>