# Connecting to Github

This works for connecting over https. I have no idea what to do if you want to connect over ssh.

## Make a personal access token
These instructions are accurate as of December 2, 2021.

1. Sign into your github account.  In the top right, click the down arrow next to your profile pic and go down to settings.
2.  On the right hand side, select developer settings.
3. Click Personal Access Tokens and generate a new token.  Give it all the permissions.
4. Save the that token somewhere. 

Note: If you have already created a repo you would like to access, you will need to use the corresponding token to gain access to your repo not a new one. 

## Storing the personal access token on the servers
We need to store the personal access token on the servers. This is a great mystery. A great mystery indeed.  I have mostly taken this info from [Some discussion on Stack Overflow](https://stackoverflow.com/questions/46645843/where-to-store-my-git-personal-access-token)

1. Use the rstudio interface to log into a server.
2.  Type the following:


```
library(credentials)
credential_helper_get()
git_credential_ask('https://github.com')
```

The result of credential_helper_get() will probably say cache.  If it says "store" skip to step 5.
the result of git_credential_ask will might include your username and password.  It might include nothing.  

3.  Open a terminal using Tools--> Terminal.  
type
```
git config --list
```

This will probably say cache.  if so, type:

```
git config --global credential.helper store
``` 

You might be asked to put in your PAT here.  This is probably your first time using git on the servers, so set your user.name and user.email:

```
git config --global user.name <your_name>
git config --global user.email <your_email>
git config --list
```

The final line just shows you the settings, so you can make sure you set them properly.

4.  Restart R. (Session--> Restart R). Not sure if this is strictly necessary.

5.  Try to clone something from github that is not public. This may prompt you for a username. Type in your username. It will prompt you for a password.  Type in your *Personal Access Token* from the previous section.  This should be be saved permanently, so the next time you need to pull or push, you should not be asked for a password.

If this doesn't work, try the following:

1. Try using *git_credential_update()* to update your password.

2. Add 
```
GITHUB_PAT=<your_pat_here>
```
to the end of your .Renviron file.

3.  Add:
```
Sys.setenv(GITHUB_PAT = "<YOUR_PAT_HERE>")
```
To your .Rprofile 

# Connecting to Oracle

If you want to use the ROracle library, you will need to put the .Renviron into your home directory.  

# Network drives

I have a very simple .Rprofile which sets up *network_location_remote* and *network_location_desktop* to be aware of places on the network.  If you want to use it, also put it in your home directory. 

# Disclaimer type thing
This repository is a scientific product and is not official communication of the National Oceanic and Atmospheric Administration, or the United States Department of Commerce. All NOAA GitHub project code is provided on an "as is" basis and the user assumes responsibility for its use. Any claims against the Department of Commerce or Department of Commerce bureaus stemming from the use of this GitHub project will be governed by all applicable Federal law. Any reference to specific commercial products, processes, or services by service mark, trademark, manufacturer, or otherwise, does not constitute or imply their endorsement, recommendation or favoring by the Department of Commerce. The Department of Commerce seal and logo, or the seal and logo of a DOC bureau, shall not be used in any manner to imply endorsement of any commercial product or activity by DOC or the United States Government.
