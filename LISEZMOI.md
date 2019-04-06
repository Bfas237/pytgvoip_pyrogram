# pytgvoip_pyrogram

[![PyPI](https://img.shields.io/pypi/v/pytgvoip_pyrogram.svg?style=flat)](https://pypi.org/project/pytgvoip_pyrogram/)

**Exemple d'utilisation de la bibliothèque [PytgVoIP](https://github.com/bakatrouble/pytgvoip) avec [Pyrogram](https://github.com/bakatrouble/pyrogram)**

Espérons que le support de `pytgvoip` sera [intégré à Pyrogram lui - même](https://github.com/pyrogram/pyrogram/pull/218), mais ce référentiel resterait disponible comme référence même après la fusion. 

`pytgvoip` guide d'utilisation détaillé de pytgvoip est également disponible [Ici](https://pytgvoip.readthedocs.io/en/latest/guides/usage.html)  

[Communauté](https://t.me/pytgvoip)

```python
 # faire des appels sortants
from pyrogram import Client
from tgvoip_pyrogram import VoIPFileStreamService

app = Client('account')
app.start()

service = VoIPFileStreamService(app, receive_calls=False)
call = service.start_call('@bakatrouble')
call.play('input.raw')
call.play_on_hold(['input.raw'])
call.set_output_file('output.raw')

@call.on_call_ended
def call_ended(call):
    app.stop()

app.idle()
```

```python
 # accepter les appels entrants
from pyrogram import Client
from tgvoip_pyrogram import VoIPFileStreamService, VoIPIncomingFileStreamCall

app = Client('account')
app.start()

service = VoIPFileStreamService(app)

@service.on_incoming_call
def handle_call(call: VoIPIncomingFileStreamCall):
    call.accept()
    call.play('input.raw')
    call.play_on_hold(['input.raw'])
    call.set_output_file('output.raw')
    
    # you can use `call.on_call_ended(lambda _: app.stop())` here instead
    @call.on_call_ended
    def call_ended(call):
        app.stop()

app.idle()
```

[Plus d'exemples](examples/README.md)

## Exigences
* Python 3.4 ou supérieur
* PytgVoIP (répertorié comme dépendance)
* Pyrogramme (répertorié comme dépendance)


## Installation
```pip3 install pytgvoip-pyrogram```


##  Encodage de flux audio
Les flux consommés par `libtgvoip` doivent être codés en audio PCM signé 16 bits.
```bash
$ ffmpeg -i input.mp3 -f s16le -ac 1 -ar 48000 -acodec pcm_s16le input.raw  # encode
$ ffmpeg -f s16le -ac 1 -ar 48000 -acodec pcm_s16le -i output.raw output.mp3  # decode
```

## Droits d'auteur et licence
* Droits d'auteur (C) 2019 [bakatrouble](https://github.com/bakatrouble)
* Sous licence selon les termes de la [licence publique générale limitée GNU v3 ou ultérieure (LGPLv3 +)](COPYING.lesser)

