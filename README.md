# RProgram

This is my project for R programming course. 

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
