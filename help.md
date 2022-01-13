- In order to update the git tokens
  - Under profile 
    - -> select the settings.
    - -> Choose the `Developer Settings`
    - -> Under Personal token, click generate 
    - -> If required provide a date for expiration.

- Under the Setting of the Repo, update the secret with the above generated token.
- check the badge workflow is working by running it manually.

 - In order to fetch the hashnode posts, i had to update the unique one.
   - I used Git OAuth to create the Hashnode account.
 - Use `https://api.hashnode.com` to validate the response for post.

##### Two options i tried. 
  - Note: if the username is updated in the profile, it will take 30 minutes to load the posts.

In the API playground, use the `GraphQL` query to see if the response is being retrieved.
  - For my user, i tried below to fetch the response. Use page 0
```gql
{
  user(username: "thirumurthi"){
    publication{
      posts(page: 0){
        title
        slug
      }
    }
  }
}
```
Sample Output, at the time of writing 
```json
{
  "data": {
    "user": {
      "publication": {
        "posts": [
          {
            "title": "Simple javascript ECMA 6 lambda examples",
            "slug": "simple-javascript-ecma-6-lambda-examples"
          },
          {
            "title": "Java 8 lambda use cases",
            "slug": "java-8-lambda-use-cases"
          }
        ]
      }
    }
  }
}
```
- To fetch the posts by the slug and hostname, i used below query:
```
query
{
  post(slug: "simple-javascript-ecma-6-lambda-examples", hostname:"thirumurthi.dev"){
    publication{
      posts(page: 0){
        title
      }
    }
  }
}
```
Sample output:
```
{
  "data": {
    "post": {
      "publication": {
        "posts": [
          {
            "title": "Simple javascript ECMA 6 lambda examples"
          },
          {
            "title": "Java 8 lambda use cases"
          }
        ]
      }
    }
  }
}
```