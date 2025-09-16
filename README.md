This repository contains information to get github working with Rstudio on the NEFSC servers. It is a bit of a pain; more pain than necessary if you are working on a normal computer.

# Connecting to Github

This works for connecting over https. I have no idea what to do if you want to connect over ssh.

## Make a personal access token
These instructions are functional as of on Jan 11, 2022 and workson the Neptune server.

1. Sign into your github account.  In the top right, click the down arrow next to your profile pic and go down to settings.
2. On the left hand side, select developer settings.
3. Click Personal Access Tokens and generate a new classic token.  Change the expiration to "30 Days". Give it all the permissions. 
4. Copy and Paste the that token somewhere safe, like KeePass.  Don't lose it. 
5. Use the "Configure SSO" dropdown to authorize it for your organization.


Note: If you have already created a repo you would like to access, you will need to use the corresponding token to gain access to your repo not a new one. 

## Storing the personal access token on the servers
We need to store the personal access token on the servers. This is a great mystery. A great mystery indeed.  I have mostly taken this info from [Some discussion on Stack Overflow](https://stackoverflow.com/questions/46645843/where-to-store-my-git-personal-access-token)

1. Use the rstudio interface to log into a server.
2.  Type the following:


```
library(credentials)
credential_helper_get()
```
The result of credential_helper_get() will probably say cache.  If it says "store" skip to step 5.

3.  Inside Rstudio, open a unix terminal using Tools--> Terminal.  
type
```
git config --list
```

This will probably say cache.  If so, type:

```
git config --global credential.helper store
``` 

You might be asked to put in your Personal Access Token at this time. You might not.  This is probably your first time using git on the servers, so take the chance to set  your user.name and user.email:

```
git config --global user.name your_github_user_name
git config --global user.email your_email@noaa.gov
git config --list
```

The final line just shows you the settings, so you can make sure you set them properly.

4.  Restart R. (Session--> Restart R). Not sure if this is strictly necessary.

5.  Clone a private repository from github. You can do this by going to:
    1.  File--> New Project-->Version Control-->Git.
    2.  Copy and paste in the url of a private repository, give it a directory name, and fill in the directory where it should reside, and click okay. 
    3.  At the username prompt, type in your username.
    4.  ***At the password prompt, type in your Personal Access Token from the previous section***.  This should be be saved permanently, so the next time you need to pull or push, you should not be asked for a password.



If this doesn't work, try the following:

1. Try using the R function *git_credential_update()* to update your password.

2. Try adding adding 
```
GITHUB_PAT=<your_pat_here>
```
to the end of your .Renviron file.

3.  Try adding :
```
Sys.setenv(GITHUB_PAT = "<YOUR_PAT_HERE>")
```
To your .Rprofile.  One of these three will work, but we're not exactly sure which.

# Connecting to Oracle

If you want to use the ROracle library, you will need to put the .Renviron into your home directory.  

# Network drives

I have a very simple .Rprofile which sets up *network_location_remote* and *network_location_desktop* to be aware of places on the network.  If you want to use it, also put it in your home directory. 

# Disclaimer type thing
This repository is a scientific product and is not official communication of the National Oceanic and Atmospheric Administration, or the United States Department of Commerce. All NOAA GitHub project code is provided on an "as is" basis and the user assumes responsibility for its use. Any claims against the Department of Commerce or Department of Commerce bureaus stemming from the use of this GitHub project will be governed by all applicable Federal law. Any reference to specific commercial products, processes, or services by service mark, trademark, manufacturer, or otherwise, does not constitute or imply their endorsement, recommendation or favoring by the Department of Commerce. The Department of Commerce seal and logo, or the seal and logo of a DOC bureau, shall not be used in any manner to imply endorsement of any commercial product or activity by DOC or the United States Government.
