# Management Admin Sign In

## server implementation 🚀

- /test -> health check (D)

  - setup morgan
  - create responseHandler - errorResponse, successResponse
  - handle http errors
  - test from Postman

- /seed -> seeding some data (D)

  - crate dummy data
  - store in database

- /api/users

  - POST /register -> create the user account (D)
    - get multi-part form data from the request body using multer
    - input validation check -> presence, image size, user exist
    - password hashing with bcrypt
    - create a jwt for storing user data temporarily
    - send email with nodemailer (SMPTP gmail username, password)
  - POST /activate -> activate the user account (D)
    - get the jwt from request
    - check existance of jwt
    - verify the jwt & decode the data
    - create & save the new user
  - GET /profile -> get the user account (D)
    - get the id from request body
    - findById()
    - send response based on user found or not
    - handle the mongoose Cast error
  - DELETE /:id -> delete the user account (D)
    - get the id from request body
    - findById(id)
    - if found delete the image from the server folder
    - findByIdAndDelete(id)
    - clear the cookies
    - send response
  - PUT /:id -> update the user account (D)
    - get the data from request body and params
    - create filter, updates, options
    - check image exist -> image size -> change updates
    - findByIdAndUpdate(filter, updates, options)
    - if user was updated then send response
  - PUT /update-password/:id -> update the password
    - aa
  - POST /forget-password -> forget the password
  - PUT /reset-password -> reset the password
  - PUT /ban/:id -> ban the user
  - PUT /unban/:id -> unban the user
  - GET - Admin - /all-users -> get all users including search & pagination (D)
    - get data from request body
    - search users using regex
    - include pagination
    - send response

- /api/auth (JWT Auth)

  - POST /login -> isLoggedOut -> user login (D)
    - middlewares: validateUserLogin, runValidation using express-validator, isLoggedOut
    - extract request body
    - check user's existance
    - compare the password & return response
    - check user is banned & return response
    - create jwt token with an expiry time
    - create http only cookie with less time
  - POST /logout -> isLoggedIn -> user logout (D)
    - clear the cookie
    - send the response
  - GET /refresh -> get refresh token (D)
    - get old access token from cookie
    - verify old token
    - if verified - clear exisitng cookie, create refresh token (new token), cookie, return refresh token

- Middleware

  - isLoggedIn (D)
  - isLoggedOut
  - isAdmin
  - uploadFile
  - getRefreshToken
  - userValidation

- /api/blogs

  - POST / -> search the blog (Admin/User)
  - POST /search-blogs -> search the blog (Admin/User)
  - GET /:id -> get single blog
  - POST / -> create a blog (Admin)
  - DELETE /:id -> delete a blog (Admin)
  - PUT /:id -> update a blog (Admin)

- package that we will need
  `npm install express cors http-errors multer body-parser bcrypt jsonwebtoken nodemailer cookie-parser`
  `npm install --save-dev morgan nodemon`


## client implementation ❤️

# Getting Started with Create React App

This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).

## Available Scripts

In the project directory, you can run:

### `npm start`

Runs the app in the development mode.\
Open [http://localhost:3000](http://localhost:3000) to view it in your browser.

The page will reload when you make changes.\
You may also see any lint errors in the console.

### `npm test`

Launches the test runner in the interactive watch mode.\
See the section about [running tests](https://facebook.github.io/create-react-app/docs/running-tests) for more information.

### `npm run build`

Builds the app for production to the `build` folder.\
It correctly bundles React in production mode and optimizes the build for the best performance.

The build is minified and the filenames include the hashes.\
Your app is ready to be deployed!

See the section about [deployment](https://facebook.github.io/create-react-app/docs/deployment) for more information.

### `npm run eject`

**Note: this is a one-way operation. Once you `eject`, you can't go back!**

If you aren't satisfied with the build tool and configuration choices, you can `eject` at any time. This command will remove the single build dependency from your project.

Instead, it will copy all the configuration files and the transitive dependencies (webpack, Babel, ESLint, etc) right into your project so you have full control over them. All of the commands except `eject` will still work, but they will point to the copied scripts so you can tweak them. At this point you're on your own.

You don't have to ever use `eject`. The curated feature set is suitable for small and middle deployments, and you shouldn't feel obligated to use this feature. However we understand that this tool wouldn't be useful if you couldn't customize it when you are ready for it.

## Learn More

You can learn more in the [Create React App documentation](https://facebook.github.io/create-react-app/docs/getting-started).

To learn React, check out the [React documentation](https://reactjs.org/).

### Code Splitting

This section has moved here: [https://facebook.github.io/create-react-app/docs/code-splitting](https://facebook.github.io/create-react-app/docs/code-splitting)

### Analyzing the Bundle Size

This section has moved here: [https://facebook.github.io/create-react-app/docs/analyzing-the-bundle-size](https://facebook.github.io/create-react-app/docs/analyzing-the-bundle-size)

### Making a Progressive Web App

This section has moved here: [https://facebook.github.io/create-react-app/docs/making-a-progressive-web-app](https://facebook.github.io/create-react-app/docs/making-a-progressive-web-app)

### Advanced Configuration

This section has moved here: [https://facebook.github.io/create-react-app/docs/advanced-configuration](https://facebook.github.io/create-react-app/docs/advanced-configuration)

### Deployment

This section has moved here: [https://facebook.github.io/create-react-app/docs/deployment](https://facebook.github.io/create-react-app/docs/deployment)

### `npm run build` fails to minify

This section has moved here: [https://facebook.github.io/create-react-app/docs/troubleshooting#npm-run-build-fails-to-minify](https://facebook.github.io/create-react-app/docs/troubleshooting#npm-run-build-fails-to-minify)
