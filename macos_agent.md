# Building MacOS Agent using Python

So you want to build a MacOS application that would sit in the menu bar
and allow user to interact via menu?
Here I'm going to show how to make a standalone application fully capable of that
and a few more things in a pure python.

## Libraries being used

The application in the article would be build atop of [`rumps`](https://github.com/jaredks/rumps)
library and packed using [`py2app`](https://py2app.readthedocs.io/en/latest/).
As a result we would get a perfectly standalone application bundle that would look and feel
like a normal MacOS app.

## Setting things up

TODO: Split this into a simple menu and py2app
First of all we would need a `setup.py`:
```python
from setuptools import setup

APP_NAME = 'MyApplication'
setup(
    # This would be turned into an application bundle name
    name=APP_NAME,
    # This is the actual script that would be called.
    # For now py2app supports only a single-entry list
    app=['agent.py'],
    data_files=[],
    options=dict(
        py2app=dict(
            plist=dict(
                # launchd label that should be unique within the system
                Label='org.example.MyApplication',
                # This flag would hide the app from App Switcher
                LSUIElement=True,
                RunAtLoad=True,
                LaunchOnlyOnce=True,
                ProgramArguments=['Contents/MacOS/MyApplication'],
                Disabled=False,
                ProcessType='Interactive',
            ),
            resources=[
                # .plist file that would help to register MyApplication
                # to be launched at Login
                'org.example.MyApplication.agent.plist',
            ]
        )
    ),
    setup_requires=[
        'py2app',
    ],
    requires=[
        'rumps',
    ],
)
```

## Writing a simple menu
First of all we would need to install some dependencies:
```python
from setuptools import setup

setup(
    name='MyApplication',
    requires=[
        # Library to build UI in a form of MacOS menus
        'rumps',
    ]
)
```

Then we could create a program with a simple menu:
```python
if __name__ == '__main__':
    pass
```

This code could be run directly as is, but out final goal is to pack everything
