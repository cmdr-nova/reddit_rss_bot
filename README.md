Welcome to my personal hell, wherein you will import image posts from subreddits, and then slap them onto Mastodon. You don't like that? Too bad, you live with me now. 

Bot functions:
- bot will post from a list of subreddits supplied by you within the script
- bot will post one image at random within a given interval, configured by you in a cronjob
- bot will follow users back each time it runs, if it detects new followers
- bot will unfollow users that it detects have stopped following it, each time it runs
- bot will share custom text, configured by you from within the script, which includes image blurring and a CW
- if the bot detects that an image is too large for the mastodon api, it will attempt to resize the image, and then post it
- bot will wait for finalization of an upload before finishing

Before we begin, you'll need to create your bot account on Mastodon, then go into the developer panel under preferences, and create an app, then save the credentials. Then, you'll want to create an app for Reddit's API, and save those credentials (link: https://www.reddit.com/r/reddit.com/wiki/api/).

You're good to go.

First, you must acquire a server, unless you're going to run this on your own PC 24/7. That's up to you!

Take the script source code, and then make a folder, and go

```
nano reddit-bot.py
```

Copy the source code into that blank file, write out, then exit, and return to your root folder.

Now do this

```
sudo apt-get update
sudo apt-get install python3 python3-venv python3-pip
```

```
cd /path/to/your/python-script-folder
python3 -m venv myenv
```
Hit the big red button,

```
source myenv/bin/activate
```

or if for some reason you're using stinky windows,

```
myenv\Scripts\activate
```

and then (bot has been updated to not use rss and instead just use the subreddits themselves, which essentially makes this not an rss bot, but i digress!)

```
pip install requests feedparser mastodon.py beautifulsoup4 praw pillow
```

Once you've done that, set us up the cronjob. Run it every 30 minutes, or whatever time you want.

```
*/30 * * * * /home/user/reddit-bot/myenv/bin/python /home/user/reddit-bot/reddit-bot.py
```

And there ya go.

I personally have mine set to every 10 minutes, because 30 minutes was just too long. But, maybe 10 is too much for some, who knows!

See the bot in action on my instance, [here](https://mkultra.monster/@net_run)!
