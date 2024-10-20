<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>CPA Movie Landing Page</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
      font-family: Arial, sans-serif;
    }

    body {
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      background-size: cover;
      background-position: center;
      color: white;
      text-align: center;
    }

    .container {
      background: rgba(0, 0, 0, 0.7);
      padding: 20px;
      border-radius: 8px;
    }

    h1 {
      font-size: 2rem;
      margin-bottom: 10px;
    }

    p {
      font-size: 1.2rem;
      margin-bottom: 20px;
    }

    .buttons {
      display: flex;
      justify-content: center;
      gap: 20px;
    }

    .btn {
      padding: 15px 30px;
      font-size: 1.2rem;
      background-color: #ff9800;
      color: white;
      border: none;
      border-radius: 5px;
      cursor: pointer;
      text-decoration: none;
      transition: background-color 0.3s;
    }

    .btn:hover {
      background-color: #e68900;
    }
  </style>
</head>
<body>
  <div class="container">
    <h1 id="movie-title">Loading...</h1>
    <p id="movie-overview">Please wait while we fetch the movie details.</p>
    <div class="buttons">
      <a id="watch-btn" href="#" class="btn">WATCH</a>
      <a id="download-btn" href="#" class="btn">DOWNLOAD</a>
    </div>
  </div>

  <script>
    const apiKey = '89d7f821168e89b1b67b220013212985';
    const movieId = '550'; // Example: Fight Club (use dynamic movie IDs as needed)

    async function fetchMovieDetails() {
      try {
        const response = await fetch(
          `https://api.themoviedb.org/3/movie/${movieId}?api_key=${apiKey}&language=en-US`
        );
        const movie = await response.json();

        // Set the background to the movie poster
        document.body.style.backgroundImage = `url('https://image.tmdb.org/t/p/original${movie.backdrop_path}')`;

        // Populate the movie title and overview
        document.getElementById('movie-title').textContent = movie.title;
        document.getElementById('movie-overview').textContent = movie.overview;

        // Set the buttons to point to your CPA links
        document.getElementById('watch-btn').href = `https://example.com/watch?movie=${movie.id}`;
        document.getElementById('download-btn').href = `https://example.com/download?movie=${movie.id}`;

      } catch (error) {
        console.error('Error fetching movie details:', error);
        document.getElementById('movie-title').textContent = 'Error loading movie!';
        document.getElementById('movie-overview').textContent = 'Please try again later.';
      }
    }

    // Fetch movie details on page load
    fetchMovieDetails();
  </script>
</body>
</html>
