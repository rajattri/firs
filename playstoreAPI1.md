# Play Store Reviews 

## Setting up access clients

In order to get access to the API clients, we need to configure one of the following authentication methods:

* [Using a service account](https://developers.google.com/android-publisher/getting_started#using_a_service_account)

* [OAuth2.0 client](https://developers.google.com/android-publisher/getting_started#using_oauth_clients)

For a server application running on behalf of a non-human robot, such as a continuous integration system, a **service account** is recommended. 
For a client application running directly on behalf of a human user, such as an IDE plugin, an OAuth client may be used.

* After establishing the access succesfully, we receive an authorization token, which fits into our GET call address.
 
 ## Methods: 
 
 Detailed desciption over [here](https://developers.google.com/resources/api-libraries/documentation/androidpublisher/v2/python/latest/androidpublisher_v2.reviews.html)
 
 ### get 
 returns a single review, with an unique ID.
 
 HTTP request: ``` GET https://www.googleapis.com/androidpublisher/v3/applications/packageName/reviews/reviewId

 #### Parameters: 
 
 ##### Path parameters: 
 * package name: String
 * review ID: String

 ##### Optional query parameters
 * translational language: String
 
 ##### Request body
 does not support a request body in this method
 
 ##### Response
 At sccess, this method returns a single [review resource](https://developers.google.com/android-publisher/api-ref/reviews#resource)
 
 ### list
 Returns a list of reviews. Only reviews from last week will be returned.

 HTTP request: GET https://www.googleapis.com/androidpublisher/v3/applications/packageName/reviews

 #### Parameters: 
 
 ##### Path parameters: 
 * package name: String
    Unique identifier for our android app.
 
 ##### Optional query parameters
 * maxResults: unsigned integer	
 * startIndex: unsigned integer	
 * token: string	
 * translationLanguage: string

 ##### Request body
 does not support a request body in this method
 
 ##### Response
 at success, returns the response with the following strucuture
 
 {
  "pageInfo": {
    "totalResults": integer,
    "resultPerPage": integer,
    "startIndex": integer
  },
  "tokenPagination": {
    "nextPageToken": string,
    "previousPageToken": string
  },
  "reviews": [
    reviews Resource
  ]
}

** here reviews: Resource is a list.

** By default, **10** reviews appear on each page. 
You can display up to **100** reviews per page by setting the maxResults parameter in your request.

* Note: We can access only those reviews which were modified in the last week. In order to get all the reviews since the beginning of time,
we have to export them as a CSV file, using the google play console.

### reply
 Reply to a single review, or update an existing reply.

 HTTP request: POST https://www.googleapis.com/androidpublisher/v3/applications/packageName/reviews/reviewId:reply

 #### Parameters: 
 
 ##### Path parameters: 
 * package name: String
    Unique identifier for our android app.
 * Review ID: String

 ##### Request body
  {
    "replyText": string
  }
  
  ** replyText: The text to set as the reply. Replies of more than approximately 350 characters will be rejected. HTML tags will be stripped.
 
 ##### Response
 at success, returns the response with the following strucuture
 
 {
  "result": {
    "replyText": string,
    "lastEdited": {
      "seconds": long,
      "nanos": integer
    }
  }
}


## Quotas

As a courtesy to other developers, the Reply to Reviews API enforces several quotas. These quotas are enforced separately on a per-app basis:

* GET requests (for retrieving lists of reviews and individual reviews) – 60 per hour

* POST requests (for replying to reviews) – 500 per day

If your app needs to retrieve or reply to a higher volume of reviews than these quotas allow, send a request to increase your app's quota.


