# Twitivity 
![PyPI - Python Version](https://img.shields.io/pypi/pyversions/imgur-scraper) ![PyPI - License](https://img.shields.io/pypi/l/imgur-scraper)

#### Twitter [Accounts Activity](https://developer.twitter.com/en/docs/accounts-and-users/subscribe-account-activity/overview) API Client Library for Python


* :key: Performs challenge-response check validation
* :memo: Registers webhooks
* :sound: Subscribes to current user's context
* :headphones: Receives Twitter Account Activity in real-time

## Usage

![](demo.gif)

Create an [Application](https://developer.twitter.com/en/apps) then navigate to [dev environments](https://developer.twitter.com/en/account/environments) and setup a `Dev environment label`.

### Credentials

[`App`](https://developer.twitter.com/en/apps) :arrow_right: `Details` :arrow_right: `Keys and Tokens`

Store the credentials as environment variables.
 
```
~$ export consumer_key=API_KEY
~$ export consumer_secret=API_SECRET_KEY
~$ export access_token=ACCESS_TOKEN
~$ export access_token_secret=ACCESS_TOKEN_SECRET
~$ export env_name=APP_ENV_NAME
```

Install & run [ngrok](https://ngrok.com/download).
```
~$ ./ngrok http 5000 
```

### Stream events in real time. 
```python3
# stream_events.py

>>> from twitivity import Event
>>> import json

>>> class StreamEvent(Event):
     CALLBACK_URL: str = "https://yourdomain.com/listener"
    
     def on_data(self, data: json) -> None:
         # process data

>>> stream_events = StreamEvent()
>>> stream_events.listen()
```

### Configuration

To register the webhook URL run both programs in **parallel** (first `stream_event.py` then `configure.py`). This will register the webhook URL and subscribe to the current user's context. This configuration only has to be done once.

```python3
# configure.py

from twitivity import Activity

>>> account_activity = Activity()
>>> account_activity.register_webhook("https://youdomain.com/listener")
>>> account_activity.subscribe()
```

The registration will return JSON response

```
{
    'id': '1198870971131686912', # webhook id
    'url': 'https://1f4396a1.ngrok.io/twitter/callback', 
    'valid': True, 
    'created_timestamp': '2019-11-25 07:48:08 +0000'
}
```

## Installation
```
~$ pip install twitivity
```

