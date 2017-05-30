MIT


  // create deferred object using $q
        var deferred = $q.defer();
 
        // get posts form backend
        $http.get('https://jsonplaceholder.typicode.com/posts')
          .then(function(result) {
            // save fetched posts to the local variable
            posts = result.data;
            // resolve the deferred
            deferred.resolve(posts);
          }, function(error) {
            posts = error;
            deferred.reject(error);
          });
 
        // set the posts object to be a promise until result comeback
        posts = deferred.promise;
