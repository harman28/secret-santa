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

Copy config.yml.template to config.yml and enter in the connection details 
for your outgoing mail server. Modify the participants and couples lists and 
the email message if you wish.

    cd secret-santa/
    cp config.yml.template config.yml

Here is the example configuration unchanged:

    # Required to connect to your outgoing mail server. Example for using gmail:
    # gmail
    SMTP_SERVER: smtp.gmail.com
    SMTP_PORT: 587
    USERNAME: harman28@gmail.com
    PASSWORD: "your-password"
    
    TIMEZONE: 'Asia/Kolkata'
    
    PARTICIPANTS:
      - Amritesh <bits.amritesh@gmail.com>
      - Anshu <mittalanshuman11@gmail.com>
      - Apurv <apurv.chaturvedi29@gmail.com>
      - Dave <ishan310@gmail.com>
      - Harman <harman28@gmail.com>
      - Sanjana <sanjana7ramachandran@gmail.com>
    
    DONT-PAIR:
      - Apurv, Anshu
    
    # Ordered pairs
    DONT-ASSIGN:
      - Amritesh -> Harman
      - Anshu    -> Amritesh
      - Apurv    -> Sanjana
      - Harman   -> Anshu
      - Sanjana  -> Dave
      - Dave     -> Apurv
    
    # From address should be the organizer in case participants have any questions
    FROM: Secret Santa Gaawwddd <raunak.dharani@gmail.com>
    
    # Both SUBJECT and MESSAGE can include variable substitution for the
    # "santa" and "santee"
    SUBJECT: "[DRY RUN] Secret Santa 2016"
    MESSAGE:
      Hi,
    
      If you are {santa}, then this email has reached the right person.
    
      This year you are {santee}'s Secret Santa!.
    
      Merry Christmas.

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
