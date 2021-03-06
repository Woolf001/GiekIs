# Wit.Ai

> Wit.ai makes it easy for developers to build a Siri-like speech interface for their app or device. It's an API that turns natural language (speech or messages) into actionable data. [Homepage](https://wit.ai/)

- Go to [wit.ai](https://wit.ai/)
  - Sign up / Log in
  - Create a New App (+)
    - Name: Giekis
    - Description: Grove Indoor Environment Kit Intelligent System
    - Language: Spanish
    - Open Your data will be open to the community
    - + Create App

- Create a Story 
  - What's the light?

- Bot executes...
  - witaiLight

```sh
root@edison:~# pip install wit
```

```python
import sys
from wit import Wit

import pyupm_grove as grove
light = grove.GroveLight(0)

if len(sys.argv) != 2:
    print("usage: python examples/template.py <wit-token>")
    exit(1)
access_token = sys.argv[1]

def say(session_id, context, msg):
    print(msg)

def merge(session_id, context, entities, msg):
    return context

def error(session_id, context, e):
    print(str(e))

def witaiLight(session_id, context):
    luxes = light.value()
    print luxes    
    context['forecast'] = 'sunny'
    return context

actions = {
    'say': say,
    'merge': merge,
    'error': error,
    'witaiLight': witaiLight,
}
client = Wit(access_token, actions)

session_id = 'my-user-id-42'
client.run_actions(session_id, 'light value', {})
```
