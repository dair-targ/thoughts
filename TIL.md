# The power of .netrc

TIL: It is possible to store authentication information in a standardized
way supported by various tools and libraries, namely
[`.netrc`](https://www.gnu.org/software/inetutils/manual/html_node/The-_002enetrc-file.html).

In my case it is JIRA and JIRA credentials, so it turned out to be:

    # ~/.netrc
    machine https://jira.example.org login dair-targ password Pa$$w0rd

And in python code:

    from jira import JIRA
    jira_client = JIRA('https://jira.example.org')

Explanation: in Python JIRA client is based upon [`requests`](http://docs.python-requests.org/en/master/) library
which is itself a powerful tool and also being used by miriad of other tools like [httpie](https://httpie.org/).
The `requests` support [`.netrc`](http://docs.python-requests.org/en/master/user/authentication/#netrc-authentication)
credentials storage as a default one, so no additional configuration is required.
