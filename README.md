Intro
=====

**secret-santa** can help you manage a list of secret santa participants by
randomly assigning pairings and sending emails. It can avoid pairing 
couples to their significant other or assigning certain receivers to certain gifters, and allows custom email messages to be 
specified.

Dependencies
------------

`pip install -r requirements.txt`

Usage
-----

Copy `config.yml.template` to `config.yml` and enter in the connection details for your outgoing mail server. Modify the participants and couples lists and the email message if you wish.

More Detailed Usage Instructions For Noobs
-----
```sh
    git clone https://github.com/harman28/secret-santa.git
    cd secret-santa/
    cp config.yml.template config.yml
```

Now open up `config.yml`. The initial values there should give you some idea of how the file is used. Make the following changes.

1. List the names and email address in `PARTICIPANTS`.
2. Use `DONT-PAIR` and `DONT-ASSIGN` to avoid certain assignments. The difference is that `DONT-ASSIGN` is a list of ordered pairs, which means
   * if you've written "`Amritesh -> Anshu`" under `DONT-ASSIGN`, then Amritesh won't be assigned as Anshu's Santa, but Anshu may still be Amritesh's Santa.
   * if you've written "`Apurv, Dave`" under `DONT-PAIR`, then neither Apurv nor Dave can be the other's Santa.
3. The `FROM` field doesn't actually work right now. You can use it to set a name for the sender, but the sender email will still be the one you set in `USERNAME` and not the one you write here. Sorry.
4. `SUBJECT` currently says 'dry run'. Remove that when you're ready to do your final run.
5. Modify the `MESSAGE` body the way you want, using the `santa` and `santee` variables to enter names.
6. Set `USERNAME` to the sender's email address. Probably yours.
7. Set `PASSWORD` to your password. This is why the config file is gitignored, so don't worry about your password being checked into git.
   * If you've set up 2-step verification on your google account (good stuff!), you won't be able to access it using just your password. For this, Google lets you identify certain apps with permissions to access Gmail with a single step. Use [this link](https://security.google.com/settings/security/apppasswords) to set up an App, say, "SecretSanta Script on Mac". You'll receive an auto-generated password, which you can use here.
8. Ignore remaining fields.

Running
-----

Once configured, call secret-santa:

    python secret_santa.py

Calling secret-santa without arguments will output a test pairing of 
participants.

    Test pairings:
    
    Amritesh ---> Sanjana
    Anshu ---> Dave
    Apurv ---> Amritesh
    Dave ---> Anshu
    Harman ---> Apurv
    Sanjana ---> Harman
    
    To send out emails with new pairings,
    call with the --send argument:
    
        $ python secret_santa.py --send

To send the emails, call using the `--send` argument

    python secret_santa.py --send

**Fair Warning:** At this point, the sent messages will still show up in your sent messages folder on Gmail. If you're not a disinterested organiser, you should probably go and delete them from there, without checking their contents of course.