# 📓 Notion Clone

#### Create and Edit Notes like in Notion

This clone tries to replicate some of the great note-taking features Notion has. If you don't know [Notion.so](https://notion.so) yet, I highly recommend to check it out!

📌 Live Demo: [notion-clone.kmuenster.com](https://notion-clone.kmuenster.com/)

📌 Medium Article: [How To Build A Text Editor Like Notion](https://medium.com/swlh/how-to-build-a-text-editor-like-notion-c510aedfdfcc)

---

<img alt="notion clone screenshot" src="./screenshot.gif" width="480">

---

## Features

- **Slash Commands** (Type `/` to turn the block into different content types)
- **HTML Support** (Use regular HTML tags like `<a>` in text blocks)
- **Image Support** (Upload images by using the `/image` command)
- **Drag And Drop** (Reorder blocks easily by drag and drop)
- **Guest Editing** (Anyone can create public pages and share them via link)
- **User Management** (Create an account to create private pages)
- **Scheduled Jobs** (Delete inactive pages and accounts automatically)

## Tech Stack

The frontend is built with Next.js and fully server-side rendered. On the backend, a REST API handles saving user content and user management.

#### Frontend

Next.js · React.js · SCSS/SASS

#### Backend

Express.js · MongoDB with Mongoose · Nodemailer · JWT (Cookie-based)

## Installation

1. **Clone the project**

   ```sh
    git clone https://github.com/konstantinmuenster/notion-clone.git
    cd notion-clone
   ```
   
2. **Add environment variables**

   Backend: Create an `.env` file in the `backend` directory:

   ```
   FRONTEND_URL="http://localhost:3000"
   DOMAIN="localhost"
   JWT_KEY="yourSecretForTokenGeneration"
   PORT=8080
   MONGO_URI="mongodb+srv://username:password@cluster.gqqwp.gcp.mongodb.net/database?retryWrites=true&w=majority"
   MAIL_HOST="smtp.sendgrid.net"
   MAIL_PORT=465
   MAIL_USER="apiKey"
   MAIL_SENDER="Your Name <your@mail.com>"
   MAIL_PASSWORD="yourSendGridApiKey"
   ```

   Frontend: Create an `.env.local` file in the `frontend` directory:

   ```
   NEXT_PUBLIC_API="http://localhost:8080" // references your Backend API endpoint
   ```

3. **Install and run backend (http://localhost:8080)**

    ```sh
    cd backend
    npm install
    npm start
    ```

4. **Install and run frontend (http://localhost:3000)**

    ```sh
    cd frontend
    npm install
    npm run dev
    ```

## Hosting

You can host the application on almost any provider that supports Node applications and custom domains. I decided to host the frontend on [vercel.com](https://vercel.com) and the backend on [heroku.com](https://heroku.com). But you can host both, frontend and backend, on the same provider if you like to.

### MongoDB Atlas

You have to create a new MongoDB cluster upfront. It will store all of your page and block data. You can create one for free on [MongoDB Atlas](https://www.mongodb.com/cloud/atlas).

**Make sure**, you create the following collections:
* pages
* users

**Make sure**, you allow network access to everyone (due to Heroku).

### Backend

If you want to deploy the backend on [heroku.com](https://heroku.com), create a new app in your preferred region on heroku.com.

**Make sure**, you add all production environmental variables for the backend. You can see which variables are needed in the Installation part of this readme.

**Make sure**, you add a custom domain for your backend API. Since the application uses a Cookie-based authentication, we have to run backend and frontend on the same domain. I, for example, run the frontend on `www.notion-clone.kmuenster.com` and the backend on `api.notion-clone.kmuenster.com`.

> **Want to run scheduled jobs?** To delete inactive pages and users, I run scheduled jobs frequently. If you want this feature as well, you have to add more dynos to your application and run the job `$ node jobs/index.js` via Heroku Scheduler.

Lastly, you can deploy your app using Heroku Git. 

**Make sure**, that when you push the backend to Heroku, you make a Git subtree push since `notion-clone` is a mono-repo containing backend and frontend. So run `git subtree push --prefix backend heroku master` instead of `git push heroku master`. Thus, we only push the backend part.

### Frontend

If you want to deploy the frontend on [vercel.com](https://vercel.com), you can so easily using the Vercel CLI.

With the Vercel CLI, we don't have to make a subtree push, instead we can just switch to the frontend folder and run the `vercel` command to deploy:

```sh
cd frontend
vercel
```

This will lead you through the setup guide for your frontend application. Afterwards the app should be successfully deployed.

**Make sure**, you add the Backend API endpoint as a production environmental variable on Vercel.com.

**Make sure**, you add a custom domain for your frontend (that ideally matches the domain which you have specified in your backend environmental variables 😉)


## About

<a href="https://www.buymeacoffee.com/kmuenster" target="_blank"><img src="https://cdn.buymeacoffee.com/buttons/default-orange.png" alt="Buy Me A Coffee" height="41" width="174"></a>

Konstantin Münster – [konstantin.digital](https://konstantin.digital)

Distributed under the [MIT](http://showalicense.com/?fullname=Konstantin+M%C3%BCnster&year=2019#license-mit) license.
See `LICENSE` for more information.

[https://github.com/konstantinmuenster](https://github.com/konstantinmuenster)



For Heroku:

brew install heroku/brew/heroku
heroku login
heroku create [app-name] //if you haven't create a app name
heroku create notion-frontend
heroku create notion-backend 

git remote -v
should look likethis:


git remote -v

heroku	https://git.heroku.com/notion-test.git (fetch)
heroku	https://git.heroku.com/notion-test.git (push)
notion-backend	https://git.heroku.com/notion-backend.git (fetch)
notion-backend	https://git.heroku.com/notion-backend.git (push)
notion-frontend	https://git.heroku.com/notion-frontend.git (fetch)
notion-frontend	https://git.heroku.com/notion-frontend.git (push)
origin	git@github.com:luomichelle/notion-clone.git (fetch)
origin	git@github.com:luomichelle/notion-clone.git (push)




git remote add notion-backend https://git.heroku.com/notion-backend.git
git remote add notion-frontend https://git.heroku.com/notion-frontend.git


git subtree push --prefix backend notion-backend master
git subtree push --prefix frontend notion-frontend master 


heroku config:set MAIL_HOST="smtp.sendgrid.net" -a notion-backend
heroku config:set MONGO_URI="~~~~" -a notion-backend     
heroku config:set DOMAIN="notion-frontend-4b243f4b78bb.herokuapp.com" -a notion-backend
heroku config:set FRONTEND_URL="https://notion-frontend-4b243f4b78bb.herokuapp.com" -a notion-backend
heroku config:set NEXT_PUBLIC_API_URL=https://notion-backend-3e25ded4202a.herokuapp.com -a notion-frontend
heroku config:set REACT_APP_BACKEND_URL=https://notion-backend-3e25ded4202a.herokuapp.com -a notion-frontend


force build:
heroku git:remote -a notion-frontend
git commit --allow-empty -m "Trigger build for notion-frontend"
git push heroku master


heroku git:remote -a notion-backend
git commit --allow-empty -m "Trigger build for notion-backend"
git push heroku master

If Issues Persist: 
git push heroku master --force







