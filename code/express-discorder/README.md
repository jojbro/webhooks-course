# Personal notes - 15/08/2025

This is just personal notes to remember some key insights from this module, and not related to the course official readme docu.

- install of: npm, nvm, node
- npm install for the cd code > express-discorder (will install listed packages in the package.json file)
- `npm start` will start a node for the `server.js` file and set up a localhost server, and ctrl + C to exit
- `npm instal nodemon -g` (-g means: global, not just in this directory) and then run `nodemon start` which will update localhost with latest changes in the file (insted of `npm start` > exit > start again)
- install ngrok, follow installation instructions (auth details to get it working) --> start and run on the localhost from `npm start` to get it "tunneled" to be able do the action on GitHub repo > have it shown in Discord. 
    - command line example: `ngrok http http://localhost:3000`
    - for me, ctrl + C was able to close tunnel and quit