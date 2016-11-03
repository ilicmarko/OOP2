# Adapter
Prvi od uzorka koji ne pripada kategoriji **kreatora** već **strukturni**.

"Obmotava" već postojeću klasu sa novim interfejsom.

Adapter govori na koji način će stara klasa i novi klijentski definisan interfejs
da komuniciraju.

Postoje dve vrste adaptera
* Adapter klase
* Adapter objekta

## Klase

Sadrži minimalno 3 klase:
* Novi interfejs
* Stara klasa
* Adapter


## Klase
*Izvorna* i *Ciljna* klase su iste za obe vrste, jedino se razlikuje **Adapter** klasa.

### Ciljna interface (nova klasa)
Nova **apstraktna** klasa u koju hoćemo da prebacimo staru klasu.

#### Primer:

```
class NovaKlasa{
public:
	virtual void novaMetoda()=0;
}
```

### Izvorna klasa

Ovo je originalna klasa koju trebamo preko nove apstrakne klase (`NovaKlasa`) da predstavimo.

#### Primer:

```
class StaraKlasa{
public:
	void staraMetoda(){cout << "Stara metoda" << endl;}
}
```

### Adapter klasa

U ovoj klasi trebamo da "pokažemo" novoj metodi (`novaMetoda`) kako da funkcioniše sa
 starom metodom (`staraMetoda`).

## Način 1: Adapter **Klase**

Klasa adapter **privatno** nasleđuje izvornu klasu `StaraKlasa` i **javno** nasleđuje novi apstraktni interfejs `NovaKlasa`.


Unutar adaptera pozivo stari metod pomoću novog metoda.

#### Primer

```
class Adapter : private StaraKlasa, public NovaKlasa{
public:
	void novaMetod(){
		this->staraMetoda();
	}
}
```
## Način 2: Adapter **objekta**

U ovom slučaju adapter klasu izvodimo iz ciljne klase `NovaKlasa` a sam adapter konstruišemo
iz izvorne klase (`StaraKlasa`).

#### Primer

```
class Adapter : public NovaKlasa{
private:
	StaraKlasa *stari
public:
	// U konstruktur prosleđujemo izvornu klasu kao parametar
	Adapter(StaraKlasa* s): stari(s){};
	void noviMetod(){
		stari->stariMetod();
	}
}
```
