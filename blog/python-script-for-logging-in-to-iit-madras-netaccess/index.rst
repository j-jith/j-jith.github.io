.. title: Python script for logging in to IIT Madras netaccess
.. slug: python-script-for-logging-in-to-iit-madras-netaccess
.. date: 2017-10-31 10:55:56 UTC+05:30
.. tags: python, iitm
.. category: python
.. link: 
.. description: 
.. type: text

This is a small python script which I wrote for easy login to netaccess at IIT
Madras. The script is pretty self-explanatory. I wrote this when I was trying
to learn the ``requests`` module for python. The script uses the ``requests``
module to communicate with the netaccess site. It also uses the user agent
string of a browser to make the netaccess site think that it's dealing with a
browser. Note that you can set a default username in ``get_login_data()``
function. Set it to your roll number so that you don't have to enter it every
time you call the script. The password has to be entered manually because I
didn't want to store it in plain text.

PS: Remember to put the script in your ``$PATH`` for ease of use.

.. code:: python

    #!/usr/bin/env python
    from __future__ import print_function, division
    import requests
    import getpass
    import sys


    def get_login_data():
        '''Asks the user for the username and password. Returns a dictionary to be
        passed to the /account/login post request.
        '''

        username = input('Enter username (Empty input defaults to "am12d013"): ')

        if not username:
            username = 'am12d013'

        password = ''

        while not password:
            password = getpass.getpass('Enter password (Cannot be empty): ')

        #return {'username': username, 'password': password}
        return {'userLogin': username, 'userPassword': password}


    def get_approve_data():
        '''Asks the user for the duration to be logged in for. Returns a dictionary
        to be passed to the /account/approve post request.
        '''

        duration = input('Enter session duration (1: 1 hour, 2: 1 day, empty defaults to 1): ')

        if (not duration) or (duration!='2'):
            duration = '1'

        if duration == '1':
            print('You have requested approval for 1 hour')
        else:
            print('You have requested approval for 1 day')

        return {'duration': duration, 'approveBtn': ''}


    def has_logged_in(response):
        '''Checks if login request is successful. Returns false if not.
        '''
        # If response is not 200 OK, raise error
        if response.status_code != requests.codes.ok:
            response.raise_for_status()
        # Check if login has failed by searching for a substring in the response
        # content
        elif '/account/approve' not in response.content:
            return False

        return True


    def main():

        # User agent string from Firefox 49 running on a Linux machine
        headers = {'User-Agent': 'Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:49.0) Gecko/20100101 Firefox/49.0'}

        login_data = get_login_data()
        approve_data = get_approve_data()

        with requests.Session() as s:

            # Login request
            p = s.post('https://netaccess.iitm.ac.in/account/login',
                    data=login_data, headers=headers)

            # Check if login is successful.
            if has_logged_in(p):
                print('Login successful.')
            else:
                print('Wrong username or password provided. Login failed!')
                sys.exit(0)

            # Approve machine request
            p = s.post('https://netaccess.iitm.ac.in/account/approve',
                    data=approve_data, headers=headers)

            # If response is not 200 OK, approval has failed. Exit.
            if p.status_code != requests.codes.ok:
                p.raise_for_status()
            else:
                print('Machine approved successfully.')

            sys.exit(0)


    if __name__ == '__main__':

        # If python2.x, use 'raw_input' else use 'input'
        try:
            input = raw_input
        except NameError:
            pass

        main()

