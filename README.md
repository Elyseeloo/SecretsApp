# SecretsApp

## Table of contents

- [My process](#my-process)
  - [Built with](#built-with)
  - [What I learned](#what-i-learned)
  - [Continued development](#continued-development)
- [Author](#author)

## My process

### Built with

- HTML5
- CSS3
- Bootstrap
- MongoDB
- Mongoose
- Google Authenticaiton
- Passport.js
- Node.js
- Express.js
- Heroku

### What I learned

The Secrets App is an app that I built based off of the popular social media app, Whisper. The concept is to allow users to post secrets to the app anonymously. This was a very exciting project where I learned how to use security encryption to hide and safely store a user's username and password inside a server, as well as implement the Google Authentication method into a website so that users have multiple options for signing in. This posed a challenge in being able to bring back that same username and password combo when a user tries to sign in again, but with the user's data safely secured and encrypted within the database, the website creator never has access to the password a user supplies.
Code written in this project that I want to highlight:

```Node.js
passport.use(new GoogleStrategy({
    clientID: process.env.CLIENT_ID,
    clientSecret: process.env.CLIENT_SECRET,
    callbackURL: "http://localhost:3000/auth/google/secrets",
    userProfileURL: "https://www.googleapis.com/oauth2/v3/userinfo"
  },
  function(accessToken, refreshToken, profile, cb) {
    console.log(profile);
    User.findOrCreate({ exampleId: profile.id }, (err, user) => {
      return cb(err, user);
    });
  }
));

```
This code uses the Google Authentication strategy that allows a user to sign in with their Google email address and password. It took a bit of reading and patience to learn how to properly implement this element into my website, but once I got the hang of it, it seamlessly fit in.

```Node.js
User.find({"secret": {$ne: null}}, (err, foundUsers) => {
    if (err) {
      console.log(err);
    } else {
      if (foundUsers) {
        res.render("secrets", {usersWithSecrets: foundUsers});
      }
    }
  });
});
```
This code filters through the database to find the list of already submitted secrets and displays them for the user anonymously.

### Continued development

This was a very challenging and rewarding project to work on. I would like to create something similar in the future that includes the ability to interact with the different posts, such as liking them or responding to them anonymously.

## Author

- Website - [Elyse Chambers](https://www.diaryofelyse.com)
- Frontend Mentor - [Elyseeloo](https://www.frontendmentor.io/profile/Elyseeloo)
- Twitter - [@Elyseeloo\_](https://www.twitter.com/elyseeloo_)
