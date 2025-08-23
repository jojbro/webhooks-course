# Resources
- [Webhook vs. API: What's the difference and when should you use each one?](https://zapier.com/blog/webhook-vs-api/)

# Developing Locally & Opening a tunnel
*Personal notes - 15/08/2025*

This is just personal notes to remember some key insights from this module, and not related to the course official readme docu.

## What this module is/does
What this module does: Provided code. Code runs locally on the machine to **run a server** (["A computer that processes requests for HTML and other documents that are components of webpages"](https://www.wordnik.com/words/server)). 

The server has code for what to do in certain events. Main one being: if GitHub action, then fire a API event to Discord. The server is local on my machine. To connect and "feel" the webhook firing, it needs to be connected to internet. Ngrok creates a tunnel between my local machine and the webhook endpoint to send this signal through (it creates a public URL to send traffic to local machine). Ngrok is used for testing. For a live environment, a dedicated publich URL (accessible server) is needed. This seems to be covered in the next step.

## Notes on steps
- install of: npm, nvm, node
- npm install for the cd code > express-discorder (will install listed packages in the package.json file)
- `npm start` will start a node for the `server.js` file and set up a localhost server, and ctrl + C to exit
- `npm instal nodemon -g` (-g means: global, not just in this directory) and then run `nodemon start` which will update localhost with latest changes in the file (insted of `npm start` > exit > start again)
- install ngrok, follow installation instructions (auth details to get it working) --> start and run on the localhost from `npm start` to get it "tunneled" to be able do the action on GitHub repo > have it shown in Discord. 
    - command line example: `ngrok http http://localhost:3000`
    - for me, ctrl + C was able to close tunnel and quit


# Serverless
*Personal notes - 23/08/2025*

Personal notes to remember actions from this part of the course.

## What this module is/does


Instead of setting up the code (and infrastructure of installs to make it run), someone else does that for you - you just add the code snippets for specific functions.

## Notes on concepts
### Serverless
*["The biggest misconception about serverless is that there are no servers. That's absolutely not true! Servers are still very much involved. The 'serverless' term simply means that *you*, as the developer, no longer have to worry about provisioning, managing, or maintaining those servers. The cloud provider (like Amazon Web Services, Google Cloud, Microsoft Azure, or even Vercel, which I use extensively for my Next.js projects) takes care of all the underlying infrastructure for you."](https://dev.to/rhythmsaha/what-is-serverless-a-simple-explanation-for-beginners-ja6)*

### Sync/Async
[*"What is the difference between asynchronous and synchronous?"*](https://stackoverflow.com/questions/16715380/what-is-the-difference-between-asynchronous-and-synchronous-http-request#33969543)

**Synchronous**: A synchronous request blocks the client until operation completes. In such case, javascript engine of the browser is blocked.

**Asynchronous**: An asynchronous request doesn’t block the client i.e. browser is responsive. At that time, user can perform another operations also. In such case, javascript engine of the browser is not blocked.
--Sachin Gandhwani

## Notes on steps
- Signed up for netlify
- VS code terminal run `npm install -g netlify-cli` based on [Netflify docus](https://docs.netlify.com/api-and-cli-guides/cli-guides/get-started-with-cli/) 
    - npm runs the installer for Netlify
    - g = global installation (on whole machine not just in folder)
    - CLI = Command Line Interface
- Terminal enter `netlify login` to add authenitation details
- Open folder code/netlify-discorder and run `npm install` to get all architecture in place 
- Can then run command to deploy code in the ode/netlify-discorder/functions folder by running `netlify deploy --prod` in terminal.
    - This is a one-time deployment. To update the push of code to run, you'll have to run a new terminal command. There is an option for [**Continous deployment** if projects is connected to a git](https://docs.netlify.com/api-and-cli-guides/cli-guides/get-started-with-cli/)
    - You can send code onto different "levels" of an environment. Docs specifidally mention *development* (first, start) and *production* (end, live on server). `--prod` command sends files directly to the main site URL.
- This triggers interaction in the terminal to set up the site (since it's not been configured before this point) Choose > *Create & configure a new project* > set team name and name of project (this'll give a URL to it later). This assigns one **project url** to access in Netlify login (to manage it in the UI), one **production URL** to access online, and one **unique deploy URL** (not sure of purpose).
- In Netlify UI for project check menu > Logs > Functions > *Name of function* to see a log of when this has run
- Change environment variables in menu > deploys > in new menu that appears go to environments to add webhook url from discord (in earier .env file from previous section) 
- Create new GitHub webhook to use (GitHub > project > Settings > Webhooks) and add the **endpoint** in the functions log in Netlify.
- Need to redeploy since an environment variable was changed to make it work. In terminal run `netilify deploy --prod` again