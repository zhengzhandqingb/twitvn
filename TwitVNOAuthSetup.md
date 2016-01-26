# Twitter Setup #
You need to set up your own Twitter app for this script to work.
  1. Go to this site: https://dev.twitter.com/apps/new
  1. Set up an app, and then enter the consumer secret/consumer key into twitvn.py and auth.py
  1. If you want to use bit.ly so that your trac links appear shorter and save space in the tweet, set up an user account at http://dev.bitly.com/. Direct account creation at: http://bitly.com/a/your_api_key. Enter the username and key into twit.py

# Pre-installation #
You will need to install tweepy (simpleJSON if you have python 2.5, it's included with 2.6), and optionally bitlyapi for getting shorter http links.
  1. easy\_install simplejson (python 2.5 only)
  1. easy\_install tweepy
  1. easy\_install bitlyapi (optional)
  1. For GIT: easy\_install gitpython

# Installation #
  1. Make a TwitVN folder in the SVN or GIT hooks folder
  1. Put twitvn.py (or twitvn-git.py) and auth.py into the TwitVN folder
  1. For SVN:
    1. Add the following line to post-commit in the SVN hooks folder (trac is optional). The new trac ver 0.12 and above have the opportunity to work with different svn repos. Because the creation of the trac url's has changed, you also need to supply the repo name with the -n parameter.
```
python /path/to/svn/repo/hooks/TwitVN/twitvn.py -f "${REPOS}" -r "${REV}" -t "<url for trac>" -n "<trac repository name>"
```
  1. For GIT:
    1. Add the following line to update in the GIT hooks folder
```
echo "-o ${2} -n ${3}" > twitvn.tmp
```
    1. Add the following line to post-update in the GIT hooks folder
```
DIR=$(cd `dirname $0` && pwd)
PARENT=`dirname $DIR`
python "${PARENT}"/hooks/twitvn/twitvn-git.py -f "${PARENT}" `cat twitvn.tmp`
rm twitvn.tmp
```

# OAuth Setup #
In order for TwitVN to post to Twitter it must be authorized to your account.  To do this follow the instructions below.
  1. Go into the TwitVN folder, and launch the auth.py script
```
python auth.py
```
  1. The script will print a URL, copy and paste that into your browser
  1. Login to twitter, and authorize the TwitVN app
  1. Enter the PIN number given in the browser into the python script
  1. The python script will print out an Access Key and an Access Secret
  1. Copy these 2 keys into the twitvn.py script