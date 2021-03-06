##############################################################################
Wechat Jump Bot (iOS)
##############################################################################

==============================================================================
Features
==============================================================================

- Auto Mode: playing the game automatically;
- Manual Mode: playing the game by manual.

Wechat Jump Game

.. image:: https://github.com/alpesis-ai/wechat-jumpbot/blob/master/images/auto.png
   :height: 1334px
   :width: 500px


==============================================================================
How it runs
==============================================================================

Prequsites

- WebDriverAgent
- libimobiledevice
- Python 3

WebDriverAgent

::

    $ git clone https://github.com/facebook/WebDriverAgent && cd WebDriverAgent
    $ brew install carthage
    $ ./Scripts/bootstrap.sh
    # open WebDriverAgent.xcodeproj with Xcode
    # Xcode:
    # - code sign (general and build_settings): WebDriverAgentLib/WebDriverAgentRunner
    # - Product -> Destination -> <your device>
    # - Product -> Scheme -> WebDriverAgentRunner
    # - Product -> Test

libimobiledevice (iproxy)

::

    $ brew install libimobiledevice
    $ iproxy 8100 8100
    # browse: http://localhost:8100/status
    # browse: http://localhost:8100/inspector

Bot Agent (iOS)

::

    $ git clone https://github.com/alpesis-ai/wechat-jumpbot.git
    $ cd bot-agent-ios

    $ pip3 install --pre facebook-wda
    $ pip3 install -r requirements.txt
    $ make run

Updating the params

::

    $ vim jumpbot/settings.py
    # update the params in settings.py
    # MODE = "manual"
    # TIME_COEFF = 0.0021


==============================================================================
Algorithms
==============================================================================

Manual Mode:

- click the piece(x, y) and board(x, y) and get the coordinates correspondingly
- calculating the distance and press time

::

    (coord1[0][0] - coord2[0][0])**2 + (coord2[0][1] - coord2[0][1])**2
    distance = distance ** 0.5
    press_time = distance * settings.TIME_COEFF

Auto Mode:

- the main idea same as the manual mode, but detecting the piece and the board automatically
    - find coord_y_start_scan
    - find piece
    - find board


==============================================================================
Developement
==============================================================================

::

    bot.py           <- auto       <-
                                     |-- connector
                     <- manual     <-

    settings.py
