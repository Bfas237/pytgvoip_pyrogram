# pytgvoip
Les exemples nécessitent des ajustements (set app_id et app_hash, change de nom d'utilisateur)

## Exemples en cours d'exécution

```bash
$ cd example
$ wget https://github.com/danog/MadelineProto/raw/master/input.raw  # exemple de flux à télécharger
$ python make_call.py  # ou receive_call.py, alsa.py
``` 

### [make_call.py](make_call.py)
Fait des appels sortants, lit `input.raw` en boucle sur l'appelé et enregistre la voix de l'appelé sur `output.raw`

Changer le nom d'utilisateur pour appeler et courir

### [receive_call.py](receive_call.py)
Répond aux appels entrants, joue `input.raw` en boucle à l'appelant et enregistre la voix de l'appelant dans `output.raw`

### [alsa.py](alsa.py)
Effectue des appels sortants, utilise ALSA pour émettre / recevoir du son via les périphériques du système (haut-parleurs / micro)

Requiert `pyalsaaudio` Installé
