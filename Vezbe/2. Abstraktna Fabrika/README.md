# Abstraktna fabrika

Svrha **abstrakne fabrike** je da pruzi zajednicki interface za pravljenje familiju sličnih objekta, bez pravljenja konkretnih klasa.

Klijent ne zna *(ne zanima)* kako i koju ce klasu dobiti, već ga interesuje konkretan rezultat.

## Klase

Sastoji se od minimalno 2 abstrakne klase i 2 konkretne klase.

### Abstraktna fabrika (inteface)

Treba da sadži čisto virtualne funkcije za kreiranje konkretnih proizvoda.

Primer:
```
virtual UI *napravi_dugme()=0;
virtual UI *napravi_meni()=0;
```

## Konkretna fabrika
Fabrika nasleđuje interface *(abstraktnu fabriku)*, i redefiniše čisto virtualne funkcije.

**Mogu da postoje više *različitih, konkretnih* fabrika**

Primer:
```
class WindowsFabrika : public AbstraktnaFabrika{};
class LinuxFabrika : public AbstraktnaFabrika{};
class MacOSFabrika : public AbstraktnaFabrika{};
```

## Abstraktan proizvod (interface)
Sadrži čisto virtualne funkcije koje su zajedničke za sve proizvode **tog tipa**.

Primer:
```


![UML Dijagram](https://upload.wikimedia.org/wikipedia/commons/9/9d/Abstract_factory_UML.svg)
