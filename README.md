# coursera
Dowload all videos and content in an organized way from coursera
## Download and Install Coursera-dl

Recommended installation method for all Operating Systems

From a command line (preferably, from a virtual environment), simply issue the command:

    pip install coursera-dl

##  Coursera-dl bug 
### HTTPError: 400 Client Error: Bad Request for url: https://api.coursera.org/api/login/v3
#### first way
For anyone looking for help I want to point out that after logging in with (https://learner.coursera.help/hc/en-us), you must wait for a few minute than just keep trying. By keep trying I mean spamming your command over and over again and it will somehow work (at least it works for me, I need to retry the command about 10 times before it will work).

Login to Coursera once through the browser.   https://www.coursera.org/?authMode=login

Find your installed coursera-dl site package (how?).   https://stackoverflow.com/questions/122327/how-do-i-find-the-location-of-my-python-site-packages-directory

Modify login function in cookie.py (where?) to the following:  https://github.com/coursera-dl/coursera-dl/blob/a82edb924e20268ea1d9e6d8914b71b56759cf2f/coursera/cookies.py#L111

def login(session, username, password, class_name=None):
    session.cookies.set('CAUTH', '[YOUR CAUTH COOKIE VALUE]')

Please google how to inspect cookie values for your browser. You may get some clues here.  https://kb.iu.edu/d/ajfi

Run coursera-dl as per usual.

Do note that cookies expire, though it's quite long in this particular cookie's case. In case it does, do login through the browser again to get a new cookie.

#### another way
Have created a temporary fix branch for the changes needed at -
https://github.com/jethar/coursera-dl/tree/fix_bad_request_api_v3

Alternatively,, just replace your coursera_dl.py with this one    https://github.com/jethar/coursera-dl/blob/fix_bad_request_api_v3/coursera/coursera_dl.py

This is temporary fix for Bad Request URL as mentioned here.

To use this download the cookies file as cookies.txt in the directory, where you want to download courses and then run the coursera-dl command as usual.

The cookies can be downloaded using chrome extension
https://chrome.google.com/webstore/detail/get-cookiestxt/bgaddhkoddajcdgocldbbfleckgcbcid?hl=en
or this firefox extension:
https://addons.mozilla.org/en-US/firefox/addon/cookies-txt/

Caveats:

Keep your command simple, adding some options, such as --download-quizzes --download-notebooks breaks things.

My cookies file (which worked) has format like -

## Running the script

Refer to coursera-dl --help for a complete, up-to-date reference on the runtime options supported by this utility.

    General:                     coursera-dl -u <user> -p <pass> modelthinking-004

    With CAUTH parameter:	 coursera-dl -ca 'some-ca-value-from-browser' modelthinking-00
Here are some examples of how to invoke coursera-dl from the command line:

    Without -p field:            coursera-dl -u <user> modelthinking-004
    Multiple classes:            coursera-dl -u <user> -p <pass> saas historyofrock1-001 algo-2012-002
    Filter by section name:      coursera-dl -u <user> -p <pass> -sf "Chapter_Four" crypto-004
    Filter by lecture name:      coursera-dl -u <user> -p <pass> -lf "3.1_" ml-2012-002
    Download only ppt files:     coursera-dl -u <user> -p <pass> -f "ppt" qcomp-2012-001
    Use a ~/.netrc file:         coursera-dl -n -- matrix-001
    Get the preview classes:     coursera-dl -n -b ni-001
	Download videos at 720p:     coursera-dl -n --video-resolution 720p ni-001
    Specify download path:       coursera-dl -n --path=C:\Coursera\Classes\ comnetworks-002
    Display help:                coursera-dl --help

    Maintain a list of classes in a dir:
      Initialize:              mkdir -p CURRENT/{class1,class2,..classN}
      Update:                  coursera-dl -n --path CURRENT `\ls CURRENT`

Note: If your ls command is aliased to display a colorized output, you may experience problems. Be sure to escape the ls command (use \ls) to assure that no special characters get sent to the script.

Note that we do support the New Platform ("on-demand") courses.

By default, videos are downloaded at 540p resolution. For on-demand courses, the --video-resolution flag accepts 360p, 540p, and 720p values.

To download just the .txt and/or .srt subtitle files instead of the videos, use -ignore-formats mp4 --subtitle-language en or whatever format the videos are encoded in and desired languages for subtitles.

On *nix platforms, the use of a ~/.netrc file is a good alternative to specifying both your username (i.e., your email address) and password every time on the command line. To use it, simply add a line like the one below to a file named .netrc in your home directory (or the equivalent, if you are using Windows) with contents like:

    machine coursera-dl login <user> password <pass>

Create the file if it doesn't exist yet. From then on, you can switch from using -u and -p to simply call coursera-dl with the option -n instead. This is especially convenient, as typing usernames (email addresses) and passwords directly on the command line can get tiresome (even more if you happened to choose a "strong" password).

Alternatively, if you want to store your preferred parameters (which might also include your username and password), create a file named coursera-dl.conf where the script is supposed to be executed, with the following format:

    --username <user>
    --password <pass>
    --subtitle-language en,zh-CN|zh-TW
    --download-quizzes
    #--mathjax-cdn https://cdn.bootcss.com/mathjax/2.7.1/MathJax.js
    # more other parameters

Parameters which are specified in the file will be overriden if they are provided again on the commandline.

Note: In coursera-dl.conf, all the parameters should not be wrapped with quotes.
