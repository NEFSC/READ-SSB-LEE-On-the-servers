# Connecting to Github

## Make a personal access token
These instructions are accurate as of December 2, 2021.

1. Sign into your github account.  In the top right, click the down arrow next to your profile pic and go down to settings.
2.  On the right hand side, select developer settings.
3. Click Personal Access Tokens and generate a new token.  Give it all the permissions.
4. Save the that token somewhere. 

## Storing the personal access token on the servers
We need to store the personal access token on the servers. This is a great mystery.

1. Use the rstudio interface to log into a server.
2.  Type the following:


```
library(credentials)
credential_helper_get()
git_credential_ask('https://github.com')
```

The result of credential_helper_get() will probably say cache.  If it says "store" skep to step Y
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

You might also take this opportunity to do:

```
git config --global user.name <your_name>
git config --global user.email <your_email>
git config --list
```

The final line just shows you the settings, so you can make sure you set them properly.

4.  Restart R. (Session--> Restart R). Not sure if this is strictly necessary.

5.  Try to clone something from github that is not public. This will prompt you for a username. Type in your username. It will prompt you for a password.  Type in your *Personal Access Token* from the previous section.  This should be be saved permanently, so the next time you need to pull or push, you should not be asked for a password.

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

This repository is a scientific product and is not official communication of the National Oceanic and Atmospheric Administration, or the United States Department of Commerce. All NOAA GitHub project code is provided on an "as is" basis and the user assumes responsibility for its use. Any claims against the Department of Commerce or Department of Commerce bureaus stemming from the use of this GitHub project will be governed by all applicable Federal law. Any reference to specific commercial products, processes, or services by service mark, trademark, manufacturer, or otherwise, does not constitute or imply their endorsement, recommendation or favoring by the Department of Commerce. The Department of Commerce seal and logo, or the seal and logo of a DOC bureau, shall not be used in any manner to imply endorsement of any commercial product or activity by DOC or the United States Government.
