NoSQL-Social-Network-API

## About
This is an API for a social network web application where users can share thoughts, react to friends' thoughts, and create a friend list. The API uses Express.js for routing, a MongoDB database, and the Mongoose ODM.

### Technologies Used
- MongoDB
- Mongoose
- Javascript
- Nodemon
- Postman 
- Express

## Demo
Watch the [demo video](https://drive.google.com/file/d/1TRJTdMAd_YK9z0EEuyfvEGqEYooyzNE7/view?usp=sharing) to see the functionality.

## User Story

```md
AS A social media startup
I WANT an API for my social network that uses a NoSQL database
SO THAT my website can handle large amounts of unstructured data
```

## Acceptance Criteria

1. **Server Initialization**
   - When the command to invoke the application is entered, the server starts, and Mongoose models sync with the MongoDB database.

2. **API Routes in Insomnia**
   - API GET routes in Insomnia for users and thoughts display data for each route in a formatted JSON.
   - API POST, PUT, and DELETE routes in Insomnia allow successful creation, updating, and deletion of users and thoughts in the database.
   - API POST and DELETE routes in Insomnia allow the creation and deletion of reactions to thoughts and the addition and removal of friends from a user's friend list.

## Models

### User:

- `username`
  - String, Unique, Required, Trimmed

- `email`
  - String, Required, Unique, Must match a valid email address

- `thoughts`
  - Array of `_id` values referencing the `Thought` model

- `friends`
  - Array of `_id` values referencing the `User` model (self-reference)

### Thought:

- `thoughtText`
  - String, Required, Must be between 1 and 280 characters

- `createdAt`
  - Date, Default value is the current timestamp, Getter method to format the timestamp on query

- `username` (The user that created this thought)
  - String, Required

- `reactions` (These are like replies)
  - Array of nested documents created with the `reactionSchema`

### Reaction (SCHEMA ONLY)

- `reactionId`
  - Mongoose's ObjectId data type, Default value is set to a new ObjectId

- `reactionBody`
  - String, Required, 280 character maximum

- `username`
  - String, Required

- `createdAt`
  - Date, Default value is the current timestamp, Getter method to format the timestamp on query

## API Routes

### `/api/users`

- `GET` all users
- `GET` a single user by its `_id` and populated thought and friend data
- `POST` a new user
- `PUT` to update a user by its `_id`
- `DELETE` to remove user by its `_id`

### `/api/users/:userId/friends/:friendId`

- `POST` to add a new friend to a user's friend list
- `DELETE` to remove a friend from a user's friend list

### `/api/thoughts`

- `GET` to get all thoughts
- `GET` to get a single thought by its `_id`
- `POST` to create a new thought
- `PUT` to update a thought by its `_id`
- `DELETE` to remove a thought by its `_id`

### `/api/thoughts/:thoughtId/reactions`

- `POST` to create a reaction stored in a single thought's `reactions` array field
- `DELETE` to pull and remove a reaction by the reaction's `reactionId` value

## Bonus

- Application deletes a user's associated thoughts when the user is deleted.

## Repository
- [Code Repository](https://github.com/basitmalik97/HW_18-NoSQL-Social-Network-API)
- [Live Site of API](https://drive.google.com/file/d/1TRJTdMAd_YK9z0EEuyfvEGqEYooyzNE7/view?usp=sharing)

---

**Note:** This README is tailored for employers viewing the project on GitHub. The detailed grading requirements are excluded.
