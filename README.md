import imdb

# Create an instance of the IMDb class
ia = imdb.IMDb()

def get_movie_reviews(movie_title):
    # Search for the movie by title
    search_results = ia.search_movie(movie_title)
    
    if not search_results:
        return "Movie not found"
    
    # Get the first result (assuming it's the correct one)
    movie = search_results[0]
    ia.update(movie)
    
    # Get reviews
    ia.update(movie, 'reviews')
    
    reviews = movie.get('reviews', [])
    
    if not reviews:
        return "No reviews found for this movie"
    
    return [review.data['content'] for review in reviews]

# Example usage
movie_title = input("Enter the movie title: ")
reviews = get_movie_reviews(movie_title)

if isinstance(reviews, str):
    print(reviews)
else:
    for i, review in enumerate(reviews, 1):
        print(f"Review {i}: {review}\n")
