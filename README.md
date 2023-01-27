# User Management API
This API allows for the management of users, including registration, login, showing all users, showing a specific user, deleting a user, and updating a user.

## Models
**UserBase**
The UserBase model contains the basic information for a user, including a user ID and email address.

## Copy code
class UserBase (BaseModel):
    user_id: UUID = Field (...)
    email: EmailStr = Field(...)

**UserLogin**
The UserLogin model extends the UserBase model and includes a password field.

Copy code
class UserLogin(UserBase):
    password: str = Field (
        ...,
        min_length=8,
        max_length=64
    )

**User**
The User model extends the UserBase model and includes additional information for a user, such as first name, last name, and birth date. It also includes a password field.

Copy code
class User (UserBase):
    
    password: str = Field (
        ...,
        min_length=8
    )
    first_name: str = Field(
        ...,
        min_length=1,
        max_length=50
        
    )
    last_name: str = Field(
        ...,
        min_length=1,
        max_length=50
        
    )
    birth_date: Optional[date] = Field(default = None)
    
    
    **UserRegister**
The UserRegister model extends the User model and includes a password field with specific minimum and maximum length requirements.

Copy code
class UserRegister (User):
    password: str = Field (
        ...,
        min_length=8,
        max_length=64
    )
**Tweet**
The Tweet model contains information for a tweet, including a tweet ID, content, creation date, update date, and the user who created the tweet.

Copy code
class Tweet(BaseModel):
    tweet_id: UUID = Field(...)
    content: str = Field (
        ...,
        min_length=1,
        max_length=256
    )
    created_at : datetime = Field (default=datetime.now())
    update_at: Optional[datetime] = Field (default=None)
    by: User = Field(...) 

##User Routes

**/signup:** This route allows users to register for the app by sending a POST request with a JSON payload containing the user's information in the request body.
The route returns a JSON object with the basic user information, including the user's ID, email, first name, last name, and birthdate.

**/login:** This route allows a registered user to log in to the app by sending a POST request with their login credentials. 
The functionality for this route is not implemented in the code.

**/users:** This route returns a list of all registered users in the app by sending a GET request.
Each user's information is returned in a JSON object with the keys user_id, email, first_name, last_name, and birth_date.

**/users/{user_id}:** This route returns the information of a specific user in the app by sending a GET request and including the user's ID in the path.
The functionality for this route is not implemented in the code.

**/users/{user_id}/delete:** This route allows a user to delete their account by sending a DELETE request and including the user's ID in the path.
The functionality for this route is not implemented in the code.

**/users/{user_id}/update:** This route allows a user to update their account information by sending a PUT request with the updated information in the 
request body and including the user's ID in the path. The functionality for this route is not implemented in the code.

**Tweet Routes/:** This route returns a JSON object with the message "Twitter API: Working!" when a GET request is sent.

**/post:** This route allows a user to post a tweet by sending a POST request with the tweet's content in the request body.
The functionality for this route is not implemented in the code.

**/tweets/{tweet_id}:** This route returns a specific tweet by sending a GET request and including the tweet's ID in the path.
The functionality for this route is not implemented in the code.

**/tweets/{tweet_id}/delete:** This route allows a user to delete a tweet by sending a DELETE request and including the tweet's ID in the path.
The functionality for this route is not implemented in the code.

**/tweets/{tweet_id}/update:** This route allows a user to update a tweet by sending a PUT request with the updated tweet 
content in the request body and including the tweet's ID in the path. The functionality for this route is not implemented in the code.

## It also uses the open function to read and write a json file named users.json to store the users' data.

