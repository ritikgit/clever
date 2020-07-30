<img src="https://www.clever-cloud.com/images/brand-assets/logos/v2/logo_on_white.png" alt="Clever Cloud"/>


# FOR PERSONAL USAGE ONLY


The configuration available isn't meant for mass usage. You can make it for mass usage, but the bot will be easily exhausted and restarting.

**This repo is experimental. There's no any support for this!**

I'm not good at coding and git, so I'm sorry for untidy scripts and commits.


Fork of https://github.com/magneto261290/magneto-python-aria

Live test group: **@Pinkiechan**

# What's the purpose of this fork?

I found a free cloud apps hosting like Heroku named Clever Cloud. But Clever Cloud can only listen to 8080 port with Docker, so deploying with the original lzzy's repo is impossible.
Then I happened to find a solution for it by adding Hello World webpage script to the execution of the bot, so the deployment would be able to work properly (no looping naught response from 8080 port). As far as I use it, there's only one error. I'm not sure if this is the best solution for running mirror bot on Clever Cloud, if you happened to find a better solution to do it, that will be reassuring.

You'll get ~49GB storage and ~31-33GB free storage after deploying the bot.

# What's the problem with this repo?
1. Leeching from mega.nz will make the bot **stuck and die**, don't ever do that. But it seems that I don't know how to remove the mega support. If you know how to do it, please let me know. If you happened to kill your bot because of mega links, restart your app from Clever Cloud (your account must be still connected to the repo's GitHub account)
2. If you faced an error while deploying, your email may be flooded with deployment error notification from Clever Cloud. I don't know why but the best solution is use temp mail or if you're using your personal email, delete your Clever Cloud account and make a new account with temp mail.
3. If you found another problem, please let me know, you can also contact me **@katarina_claes** in Telegram. But I'm not good at coding, so try to solve it by yourself first.
 
# How to deploy this?

1. Clone this repo to your GitHub account and make it private.

2. (if you already have service accounts, skip this) If you want to use service accounts, follow the installation guide in https://github.com/Spazzlo/folderclone in order to make your service accounts, I think 1 project is enough (~75TB daily limit). If you don't have your own team drive, create it at https://td.fastio.me/. There'll be `accounts` folder with service account credentials inside. If you don't want to use service accounts, follow the steps below. 

----------

**For non-service accounts method (if you want to use service accounts, skip this)**


Without service accounts, you only can leech up to 750GB/day.


- Visit the [Google Cloud Console](https://console.developers.google.com/apis/credentials)
- Go to the OAuth Consent tab, fill it, and save.
- Go to the Credentials tab and click Create Credentials -> OAuth Client ID
- Choose Desktop and Create.
- Use the download button to download your credentials.
- Rename it to `credentials.json`
- Visit [Google API page](https://console.developers.google.com/apis/library)
- Search for Drive and enable it if it is disabled
- Copy the script from https://github.com/magneto261290/magneto-python-aria/blob/master/generate_drive_token.py and create a new file named `generate_drive_token.py` and paste the code inside. Move that file to the `credentials.json` directory and then open your terminal/cmd from that directory (for Windows, press SHIFT + Right click > Open command prompt here) and run this command (one by one), you must have pip and python first.
```
pip install google-api-python-client google-auth-httplib2 google-auth-oauthlib
python3 generate_drive_token.py
```
(Use `python` if `python3` doesn't work)
- Now you have `credentials.json` and `token.pickle`
- Upload `credentials.json` and `token.pickle` to the root of the repo, then skip to step 5. 

(I haven't tested the non-service accounts method, if it's unusable, then use the service accounts one) 

----------

3. Rename your service account credentials into sequential numbers `(0.json, 1.json, ...)`, you can use this script https://t.me/pythonmirrorsupport/48805 and run it outside the `accounts` folder directory to do that.

4. Open `accounts` folder in the repo and upload your service accounts there. You can only upload 100 service account credentials per process (1 project has 100 service accounts), do it repeatedly if you want to upload more than 100 service account credentials.

5. Open `config.env` in the root of the repo and edit it according these configs.

- **BOT_TOKEN** : The telegram bot token that you get from **@BotFather**, one bot token is for only one bot. Every bot has it's own bot token.
- **GDRIVE_FOLDER_ID** : This is the folder ID of the Google Drive Folder to which you want to upload all the mirrors. You can fill this with your team drive ID (find it in your team drive URL) too. Want to save it to team drive but you don't own one? Visit https://td.fastio.me/. If you want to use service accounts, use the team drive that has those service accounts as it's members.
- **TELEGRAPH_TOKEN** : Telegraph token generated by running https://repl.it/@sagirisayang/TelegraphToken
- **DOWNLOAD_DIR** : The path to the local folder where the downloads should be downloaded to. You can just leave it.
- **DOWNLOAD_STATUS_UPDATE_INTERVAL** : A short interval of time in seconds after which the Mirror progress message is updated. (I recommend to keep it 5 seconds or make it 8-10 seconds to decrease the server load, but it'll make the downloading status refresh longer).
- **OWNER_ID** : The Telegram user ID (not username) of the owner of the bot, send `/id` to **@MissRose_bot** if you don't know it.
- **AUTO_DELETE_MESSAGE_DURATION** : Interval of time (in seconds), after which the bot deletes it's message (and command message) which is expected to be viewed instantly. Note: Set to -1 to never automatically delete messages. I suggest you to leave this.
- **IS_TEAM_DRIVE** : (Optional field) Set to "True" if GDRIVE_FOLDER_ID is from a Team Drive else False or Leave it empty.
- **USE_SERVICE_ACCOUNTS**: (Optional field) (Leave empty if unsure) Whether to use service accounts or not. "True" or "False" or just leave it empty.
- **INDEX_URL** : (Optional field) Refer to https://github.com/maple3142/GDIndex/ The URL should not have any trailing '/'
- **API_KEY** : This is to authenticate to your telegram account for downloading Telegram files. You can get this from https://my.telegram.org DO NOT put this in quotes, you can also use **@UseTGXBot** instead.
- **API_HASH** : This is to authenticate to your telegram account for downloading Telegram files. You can get this from https://my.telegram.org, you can also use **@UseTGXBot** instead.
- **USER_SESSION_STRING** : Session string generated by running https://repl.it/@sagirisayang/TelegramSessionGenerator and then, paste your API KEY and API HASH there, and use the bot token (don't use your phone number). Then, copy the generated long string and paste it here. Keep this in mind, every bot has it's own bot token and session string. If you want to use another bot token, you must also generate it's session string.

**MEGA DIDN'T WORK AND MAKE THE BOT DIE DURING MY TESTING (WITHOUT ACCOUNT), YOU MAY TRY ADDING YOUR MEGA ACCOUNT THERE, BUT I DON'T GUARANTEE IT'LL WORK**

You can just leave the mega.nz configurations blank.

Note: You can limit maximum concurrent downloads by changing the value of MAX_CONCURRENT_DOWNLOADS in `aria.sh`. By default, it's set to 4

6. Signup to Clever Cloud with email (press the signup button in the header of the page). You can use temp mail for this (or make a protonmail account with temp mail)

7. Verify your email

8. Fill the getting started form randomly

9. Press personal space from the left side bar, press create > an application, select the cloned repo from your GitHub repository. If you haven’t linked your GitHub, then link it first.

10. Press Docker (just “Docker”, not Docker Runner/Webbapp from ML)

11. Press Edit when it asks about scalability.

12. You have €20 free credits, scale it by your requirements. These arguments are based on my testing, you can do experiment with it by yourself.

- **512MB RAM and Shared CPU.** This configuration makes the bot active for more than three months (~3.33 months based on my calculation). During my testing, it was capable of handling 1-3 processes, tar/unzip command isn't recommended. I think the shared CPU is gacha, you can get a good one or a bad one, I got a good CPU with Canada server. If you're lucky, you can run 4 processes with a little hiccup.

- **1GB RAM and 1 vCPU.** This configuration makes the bot active for more than one month (~1.38 months based on my calculation). Smoother when handling 1-3 processes and maybe can handle 4 processes better than the one with shared CPU (it depends on the CPU, whether it's good or not), you can try tar/unzip command (but I haven't tested it personally, do it on your own risk).

- **2GB RAM and 2 vCPU.** This configuration makes the bot active for about 20 days (~0.69 month or ~20.9 days based on my calculation). This was good for handling 4 processes based on my testing and it did great with a tar/unzip process.

I didn't try the higher configuration, calculate it by yourself. Personally, 512MB one is enough for me since I don't leech files in bulk (many processes at a time). You can try from 512MB one first, if you didn't satisfy with it, scale your app to a higher configuration.

13. Name your app and I suggest you to select Canada server. Based on my testing, Canada server has better CPUs. You can experiment with the servers by yourself.

14. Press `I don’t need any add-ons`

15. Leave the port to `8080` and press `Next`.

16. Wait for the deployment. After it's done, the bot will be active in a moment. 

17. If you want to make more bot or your free credits has been zero, unlink your GitHub account from your Clever Cloud profile settings, then revoke Clever Cloud access from your GitHub settings > Applications. Finally, make a new account and then deploy an existing/new repo (based on your requirement).

# Important messages from Magneto's repo
- Original repo is https://github.com/lzzy12/python-aria-mirror-bot
- I have collected some cool features from various repositories and merged them in one.
- So, credits goes to original repo holder, not to me. I have just collected them.
- This (or any custom) repo is not supported in official bot support group.
- So if you have any issue then check first that issue is in official repo or not, You are only allowed to report that issue in bot support group if that issue is also present in official repo.

## Credits :-
- First of all, full credit goes to [Shivam Jha aka lzzy12](https://github.com/lzzy12) He build up this bot from scratch.
- Then a huge thanks to [Sreeraj V R](https://github.com/SVR666) You can checkout his [repo here](https://github.com/SVR666/LoaderX-Bot)
- Features added from [Sreeraj V R's](https://github.com/SVR666) repo -
```
1. Added Inline Buttons
2. Added /del command to delete files from drive
3. /list module will post search result on telegra.ph
```
- Special thanks to [archie](https://github.com/archie9211) for very much useful feature **Unzipmirror**
- Features added from [archie's](https://github.com/archie9211) repo
```
1. unzipmirror
2. Update tracker list dynamically
3. Fix SSL handsake error
```

# What is this repo about?
This is a telegram bot writen in python for mirroring files on the internet to our beloved Google Drive.

# Inspiration 
This project is heavily inspired from @out386 's telegram bot which is written in JS.

# Features supported:
- Mirroring direct download links to google drive
- Mirroring Mega.nz links to google drive (In development stage)
- Mirror Telegram files to google drive
- Mirror all youtube-dl supported links
- Extract zip, rar, tar and many supported file types and uploads to google drive
- Copy files from someone's drive to your drive (using Autorclone)
- Service account support in cloning and uploading
- Download progress
- Upload progress
- Download/upload speeds and ETAs
- Docker support
- Uploading To Team Drives.
- Index Link support

## Bot commands to be set in botfather

```
mirror - Start Mirroring
tarmirror - Upload tar (zipped) file
unzipmirror - Extract files
clone - copy folder to drive
watch - mirror YT-DL support link
tarwatch - mirror youtube playlist link as tar
cancel - Cancel a task
cancelall - Cancel all tasks
del - Delete file from Drive
list - [query] searches files in G-Drive
status - Get Mirror Status message
stats - Bot Usage Stats
help - Get Detailed Help
log - Bot Log [owner only]
```

# Youtube-dl authentication using .netrc file
For using your premium accounts in youtube-dl, edit the netrc file (in the root directory of this repository) according to following format:
```
machine host login username password my_youtube_password
```
where host is the name of extractor (eg. youtube, twitch). Multiple accounts of different hosts can be added each separated by a new line
