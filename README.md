
# TWRRR

Twr is a Twitter clone with not so much functionality. The idea of this project was to gain and showcase skills using Redux Toolkit and MaterialUI

## Key Features

- Dark Mode
- Friends List
- Auth/Auth
- Easy integration
- Fully Responsive

## A Quick Look
<img width="1723" alt="twrr" src="https://user-images.githubusercontent.com/113067058/236660618-a76a2ead-a8d8-4f4d-bfa7-1fe47eb5a98d.png">

## Installation

Follow these steps to install and set up Twrrr on your local machine:

Clone the repository:  

`git clone https://github.com/jbxamora/twrrr.git` . 
  
Install Dependencies:  
  
`npm i` **or** `npm install`

Move into Server directory:

`cd server`
  
Create dotenv file:
  
`MONGO_URL="yourmongodburl"
PORT=3001
JWT_SECRET="somesuperdupersecret"`

Start Server:

`nodemon index.js`

Seed Data To Your Database:

uncomment the following lines in index.js
`// User.insertMany(users)
// Post.insertMany(posts)`

Switch to client directory
  
Run on your local machine:
  
`npm run dev`
  
**Happy Hacking!**

## Heres The Data Model
<img width="1320" alt="datamodel" src="https://user-images.githubusercontent.com/113067058/236320960-8cce3cf5-c674-4561-baca-7233d98f6f69.png">

## Redux Persist
Here's an example of setting up a Redux store with Redux Persist to save and rehydrate the application state:

```javascript
const persistConfig = {
  key: "root",
  version: 1,
  storage,
};

const persistedReducer = persistReducer(persistConfig, authReducer);

const store = configureStore({
  reducer: persistedReducer,
  middleware: (getDefaultMiddleware) =>
    getDefaultMiddleware({
      serializableCheck: {
        ignoredActions: [FLUSH, REHYDRATE, PAUSE, PERSIST, PURGE, REGISTER],
      },
    }),
});
```

This configuration sets up Redux Persist with the `authReducer` and specifies a list of actions to ignore during the serializable check in the middleware configuration.

### JWT
The following is an example of a middleware function to verify a JWT token in an Express.js server:

```javascript
export const verifyToken = async (req, res, next) => {
  try {
    let token = req.header("Authorization");

    if (!token) return res.status(403).send("Access Denied");

    if (token.startsWith("Bearer ")) {
      token = token.slice(7, token.length).trimLeft();
    }

    const verified = jwt.verify(token, process.env.JWT_SECRET);
    req.user = verified;
    next();
  } catch (err) {
    res.status(500).json({ error: err.message });
  }
};
```

This function takes the incoming request, checks for the presence of an "Authorization" header, and verifies the token using the JWT secret. If the token is valid, it adds the verified user to the `req` object and proceeds to the next middleware or route handler.
