# AI-Driven Difficulty Optimizer for Text Adventures

Building AI -kurssiprojekti

## Yhteenveto

Tämä projekti kehittää tekoälypohjaisen työkalun tekstiseikkailupelien pelitestaukseen ja vaikeustason optimointiin. Järjestelmä analysoi pelaajien valintoja ja tekstisyötteitä, hyödyntäen lineaarista regressiota ja kiipeilyalgoritmia (hill-climbing) pelin tahditukseen, pelaajien turhautumisen estämiseen ja dynaamiseen vihjejärjestelmään.

## Background

Tekstiseikkailupelit nojaavat vahvasti pulmiin ja tarinaan, mutta vaikeustason tasapainottaminen on haastavaa. Pelaajat turhautuvat, jos pulmat ovat liian epäselviä, mikä johtaa pelin keskeyttämiseen. Manuaalinen testaaminen on työlästä, ja tavoitteena onkin ratkaista Unitylla (C#) kehitettävien pelien haasteet, kuten vaikeustason skaalautuminen eri taitotasoille.

## How is it used?

Työkalu integroituu pelin syötteenhallintaan, kerää anonyymiä istuntodataa ja tunnistaa ongelmakohtia (esim. liian pitkät ajat huoneessa tai tunnistamattomat komennot). Kehittäjät saavat raportteja, ja pelaajat nauttivat sujuvammasta kokemuksesta dynaamisten vihjeiden ansiosta. Esimerkki analyysirutiinista:

```python
def analyze_player_friction(room_logs):
    # Analysoi syötevirheet ja huoneessa vietetyn ajan
    for room in room_logs:
        failed_commands = room['unrecognized_inputs']
        time_spent = room['duration_seconds']
        
        # Hälytys, jos pelaaja on jumissa
        if len(failed_commands) > 5 and time_spent > 300:
            print(f"Alert: High puzzle friction detected in {room['name']}.")
```

## Data sources and AI methods

Projektissa käytetään anonyymeja pelilokeja ja tekstin samankaltaisuusvektoreita. Keskeisiä tekoälymenetelmiä ovat:
* **Lineaarinen regressio:** Ennustaa pelin läpäisyaikaa.
* **K-Nearest Neighbor (KNN):** Ryhmittelee pelaajakäyttäytymistä.
* **Simulated Annealing / Hill Climbing:** Optimoi vaikeustasoa ja vihjeiden antamista.

## Challenges

Tämä ei korjaa huonoa tarinankerrontaa. On tärkeää huomioida yksityisyys (anonyymi data) ja välttää ylisovitusta (overfitting) pienellä testiryhmällä.

## What next?

Jatkokehityksenä järjestelmä voisi toimia avoimen lähdekoodin lisäosana (Unity/Godot) ja sisältää pilvipohjaisen analytiikan, mikä vaatii yhteistyötä datatekniikan asiantuntijoiden kanssa.

## Acknowledgments

* Inspiraationa Reaktorin ja Helsingin yliopiston *Building AI* -kurssi.
* Inspiraationa klassiset interaktiiviset tarinat ja NLP-työkalut.
