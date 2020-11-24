# Download from coursera
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

# How I got Financial Aid for Data Science Course on Coursera !!!
    How to get any course on Coursera for free…✨

    Simple steps to follow…

    Apply for Financial Aid on Coursera by simply clicking on Financial Aid available.

2. You will see, 3 questions to answer in an excellent way.

    Show your writing skills and try on your own…🔥

    By watching my answers, you will get a rough idea.🤠

    Why are you applying for Financial Aid? (150 words minimum required)

Ans: I’m a student from India and want to learn Data Science. I think it will be beneficial for my work. But I’ve no job of my own to carry the expenses to pay for the certificate of this course. I live only for my scholarship, it is very much difficult for me to gather such amount of money for the certificate. Financial Aid will help me take this course without any adverse impact on my monthly essential needs. So I’m badly in need of this financial aid. I want to take this course as I want to learn. This course will boost my job prospects after graduation from my institute. It will help perform better in understanding and learning this technology and give me an edge over my competitors. A verified certificate will attach credibility to the certificate I receive from this course. I plan to complete all assignments on or before time as I have done in previous Signature Track Courses. Also, I intend to participate in Discussion Forums, which I have found to supplement my learning immensely in the other online courses I have taken on Coursera. I also plan to grade assignments that are to peer-reviewed which I believe will an invaluable learning opportunity.

2. How will taking this course help you achieve your career goals? (150 words minimum required)

Ans: My main career goal is to learn every day. I really want to learn and to progress in my career. Programming requires constant learning and improving. Taking this course will help me to learn and study this Data Science and also to implement it. It can help me advance in my knowledge. This course will help me in defining Data Science, understanding how Python could potentially impact our business and industry, to write a thought leadership piece regarding use cases and industry potential of Data Science, explain Data Science to clients, friends, joining a community of economists, business leaders, entrepreneurs, and technologists that are shaping this technology as we speak. Identifying which aspects of Data Science seem most important and relevant to us, Walking away with a strong foundation in where Data Science is going, what it does, and how to prepare for it. Data Science course will help me achieve it to learn. Courses on Coursera helped me to greatly increase my programming knowledge in the past.

    Would you consider using a low-interest loan to pay for your courses?

    Selected: NO

3. If you answered no, please help us understand why.

Ans: I don’t have enough money to invest in my education, I can invest only my time now.

Have some patience, to get this course.

It takes 15 days hardly…
