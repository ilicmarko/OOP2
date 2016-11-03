# Abstraktna fabrika

Svrha **abstrakne fabrike** je da pruzi zajednicki interface za pravljenje familiju sličnih objekta, bez pravljenja konkretnih klasa.

Klijent ne zna *(ne zanima)* kako i koju ce klasu dobiti, već ga interesuje konkretan rezultat.

## Klase

Sastoji se od minimalno 2 abstrakne klase i 2 konkretne klase.

### Abstraktna fabrika (inteface)

Treba da sadži čisto virtualne funkcije za kreiranje svih konkretnih proizvoda.

#### Primer:
```
virtual UI *napravi_dugme()=0;
virtual UI *napravi_meni()=0;
```

## Konkretna fabrika
Fabrika nasleđuje interface *(abstraktnu fabriku)*, i redefiniše čisto virtualne funkcije.

**Mogu da postoje više *različitih, konkretnih* fabrika**

#### Primer:
```
class WindowsFabrika : public AbstraktnaFabrika{};
class LinuxFabrika : public AbstraktnaFabrika{};
class MacOSFabrika : public AbstraktnaFabrika{};
```

## Abstraktan proizvod (interface)
Sadrži čisto virtualne funkcije koje su zajedničke za sve proizvode **tog tipa**.

#### Primer:
```
virtual void prikazi()=0;
virtual void pomeri()=0;
```

## Kokretan proizvod
Proizvod nasleđuje interface proizvoda *(abstraktni proizvod)*, zatim se redefinišu čisto virualne funkcije konkretno za taj tip proizvoda.

#### Primer:

```
class WindowsDugme : public AbstraktanProizvod{};
class LinuxDugme : public AbstraktanProizvod{};
class MacOSDugme : public AbstraktanProizvod{};

class WindowsMeni : public AbstraktanProizvod{};
class LinuxMeni : public AbstraktanProizvod{};
class MacOSMeni : public AbstraktanProizvod{};
```

## Rezime
Gore sam uzeo primer za multiplatform UI.

**Proces razmišljanja:**

Proces razmišljanja ide malo u obrnutom smeru, krećemo od proizvoda ka fabrici.
* Na svakom operativnom sistemu nam treba dugme i meni.
* Imamo konkretne proizvode `dugme` i `meni`. **To su dva konkretna proizvoda**
* Svaki od tih proizvoda mora da se prikaze *("nacrta")*. ** Znači to je metoda u abstraktnom proizvodu**.
* Svaka fabrika mora da može da napravi konkretan proizvod. **Znači za svaki proizvod nam treba metod u abstraktnoj fabrici*
* Svaki operativni sistem će mi biti fabrika `WindowsFabrika`, `LinuxFabrika` i `MacOSFabrika`.

To je to.

Za linux sistem napravim `LinuxFabrika`-u, iz *abstrakne fabrike* znam da mogu da pozovem `napravi_dugme` i/ili `napravi_meni`.

 A u konkretnoj fabrici (`LinuxFabrika`) je definisano koji to proizvod zovem, u ovom slučaju `LinuxMeni` i/ili `LinuxDugme`.

 Zatim oba proizvada mogu da se nacrtaju pošto to dele preko *abstraknog proizvoda*.


## Diagram

![UML Dijagram](https://upload.wikimedia.org/wikipedia/commons/9/9d/Abstract_factory_UML.svg)
