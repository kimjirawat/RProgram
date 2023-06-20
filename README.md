# RProgram

This is my project for R programming course. 

1 makeCacheMatrix: This function creates a special "matrix" object that can cache its inverse.
```
makeCacheMatrix <- function(matrix) {
  inverse <- NULL
  
  getMatrix <- function() {
    matrix
  }
  
  getInverse <- function() {
    if (is.null(inverse)) {
      inverse <<- solve(matrix)
    }
    inverse
  }
  
  setMatrix <- function(new_matrix) {
    matrix <<- new_matrix
    inverse <<- NULL  # Reset the cached inverse when the matrix is updated
  }
  
  list(getMatrix = getMatrix, getInverse = getInverse, setMatrix = setMatrix)
}
```
This function creates a closure that encapsulates the matrix and its inverse as local variables. It returns a list containing three functions:

getMatrix: Returns the original matrix.
getInverse: Returns the cached inverse if it exists, or computes and caches the inverse if it hasn't been computed yet.
setMatrix: Updates the matrix and resets the cached inverse.
The makeCacheMatrix function takes a matrix as its input and returns the list of functions. The getMatrix and getInverse functions access the original matrix and its cached inverse, respectively. The setMatrix function allows you to update the matrix and ensures that the cached inverse is cleared.

In R, we use the solve function to compute the matrix inverse.



2 cacheSolve: This function computes the inverse of the special "matrix" returned by makeCacheMatrix above. If the inverse has already been calculated (and the matrix has not changed), then the cachesolve should retrieve the inverse from the cache.

```
cacheSolve <- function(matrix_obj) {
  inverse <- matrix_obj$getInverse()
  if (!is.null(inverse)) {
    message("Retrieving cached inverse.")
    return(inverse)
  }
  
  matrix <- matrix_obj$getMatrix()
  inverse <- solve(matrix)
  matrix_obj$setInverse(inverse)
  inverse
}
```

The cacheSolve function takes the special "matrix" object returned by the makeCacheMatrix function as its input. It first tries to retrieve the cached inverse using the getInverse function from the matrix object. If the inverse exists in the cache, it retrieves and returns it.

If the inverse is not found in the cache, it proceeds to compute the inverse using the solve function and updates the cache using the setInverse function. The setInverse function is not part of the original makeCacheMatrix implementation, but we can add it to the setMatrix function as follows:


```setMatrix <- function(new_matrix) {
  matrix <<- new_matrix
  inverse <<- NULL  # Reset the cached inverse when the matrix is updated
}
```

By including this modification in the makeCacheMatrix function, we can access and update the cached inverse within the cacheSolve function.

Once the inverse is computed or retrieved from the cache, the cacheSolve function returns the inverse matrix.

