# Projektni uzorci

## Sadržaj

### Stvaralacki projetni uzorci

* [Apstraktna fabrika](01. Abstract factory/)
* [Graditelj](02. Builder/)
* ~~Fabricki metod~~
* [Prototip](04. Prototype/)
* [Unikat](05. Singleton/)

### Strukturni projektni uzorci

* [Adapter](06. Adapter/)
* [Most](07. Bridge/)
* [Kompozicija](08. Composite/)
* [Dekorater](09. Decorator/)
* [Fasada](10. Facade/)
* [Muva](11. Flyweight/)
* [Zastupnik](12. Proxy/)


## Podsetnik


<table >
<tr>
<td>Ime Klase</td>
<td>Klasa</td>
<td>Opis</td>
</tr>
<tr>
<td colspan='3'>Apstraktna fabrika</td>
</tr>
<tr>
<td>`IFabrika`</td>
<td>`virtual UI *napravi_dugme()=0;`</td>
<td>Zajednicke metode za sve fabrike</td>
</tr>
<tr>
<td>`Fabrika`</td>
<td>`class WindowsFabrika : public IFabrika{}`</td>
<td>Kokrenta fabrika koja vraca konkretan proizvod</td>
</tr>
<tr>
<td>`IProizvod`</td>
<td>`virtual void crtaj() = 0;`</td>
<td>Zajednicke metode za sve proizvode</td>
</tr>
<tr>
<td>`Proizvod`</td>
<td>class WindowsDugme : public Iproizvod{}</td>
<td>Konkretan proizvod</td>
</tr>
<tr>
<td colspan='3'>Prototip</td>
</tr>
<tr>
<td>`IPrototype`</td>
<td>`virtual Iprototype* clone()=0;`</td>
<td>Ima clone za sve prototipove i jos neke metode</td>
</tr>
<tr>
<td>`Prototype`</td>
<td>`virtual Iprototype* clone(){
IPrototype* tmp = new Prototip1();
tmp->setBroj( getBroj() );
return tmp;
}`</td>
<td>Kokrentan prototip implementira `clone`. Vraca kopiju sebe</td>
</tr>
<tr>
<td colspan='3'>Unikat</td>
</tr>
<tr>
<td>`singleton`</td>
<td>`static Singleton& get() {
static Singleton single;
return single;
}`</td>
<td>Jednom se samo generise objekat</td>
</tr>
<tr>
<td colspan='3'>Adapter</td>
</tr>
<tr>
<td>`NovaKlasa`</td>
<td>`virtual void novaMetoda()=0;`</td>
<td>Klasa u koju hocemo da adaptiramo.</td>
</tr>
<tr>
<td>`StaraKlasa`</td>
<td>`void staraMetoda(){}`</td>
<td>Klasa koju hocemo da adaptiramo.</td>
</tr>
<tr>
<td>`AdapterKlase`</td>
<td>`class Adapter : private StaraKlasa, public NovaKlasa{
void novaMetod(){
this->staraMetoda();
}
}`</td>
<td>Privatno nasledjuje` Staruklasu`, javno `Novuklasu`</td>
</tr>
<tr>
<td>`AdapterObjekta`</td>
<td>`class Adapter : public NovaKlasa{
StaraKlasa *stari
}`</td>
<td>Adapter čuva referencu na `Staruklasu` koja se prosleđuje konstruktorom</td>
</tr>
<tr>
<td colspan='3'>Most</td>
</tr>
<tr>
<td>`Implementacija`</td>
<td>`virtual void crtajPortret() = 0;`</td>
<td>Sadrzi virtualne funkcije za konkretne implementatore. Koliko ovde metoda imamo toliko imamo i apstrakcija</td>
</tr>
<tr>
<td>`Implementator`</td>
<td>`class Pikaso : public Crtac {
void crtajPortret() {}
}`</td>
<td>Konkretni implementator koji se izvodi iz`Implementacija`.</td>
</tr>
<tr>
<td>`IApstrakcija`</td>
<td>`class Platno {
Crtac* crtac;
public:
Platno(Crtac* c): crtac(c){}
virtual void crtaj() = 0;
}`</td>
<td>Sadzi pokazivac na `Implementatora` i virtualno metodu za apstrakciju</td>
</tr>
<tr>
<td>`Apstrakcija`</td>
<td>```class Portret : public Platno {
public:
Portret(Crtac* c): Platno(c){}
void crtaj() {
crtac->crtajPortret();
}
};```</td>
<td>Implementira metodu iz `IApstrakcije`</td>
</tr>
<tr>
<td colspan='3'>Kompozicija</td>
</tr>
<tr>
<td>`IList`</td>
<td>`virtual void napadni() = 0`</td>
<td>Apstraktna klasa koja je zajednicka za sve objekte u kompoziciji.</td>
</tr>
<tr>
<td>`List`</td>
<td>`class List : public IList {}`</td>
<td>Idividualni objekat koji ce ici uci u kompoziciju.</td>
</tr>
<tr>
<td>`Kompozicija`</td>
<td>`class Kompoz : public IList {
vector
	<IList*> listovi;}`
	</td>
	<td>Nasleđuje `IList`, zato što treba da omogući iste metode samo za svu decu. Sadži komponentu koja čuva listove</td>
</tr>
<tr>
	<td colspan='3'>Dekorater</td>
</tr>
<tr>
	<td>`Komponenta`</td>
	<td>`virtual void crtaj() = 0;`</td>
	<td>Definise interfejs za objekte koji se adaptiraju</td>
</tr>
<tr>
	<td>`Subjekat`</td>
	<td>`class Input : public Polje {}`</td>
	<td>Klasu koju adaptiramo, izvodi se iz `Komponente`</td>
</tr>
<tr>
	<td>`IDekorater`</td>
	<td>`class Dekorater : public Polje {
Komonenta* ptrPolje;
public:
Dekorater(Komonenta* _ptr): ptrPolje(_ptr){}
void crtaj() { ptrPolje->crtaj(); }
}`</td>
	<td>Mora da sadrzi referencu na objekat klase `Komponenta` i nasledjuje interfejs klase `Komponenta`.</td>
</tr>
<tr>
	<td>`Dekorater`</td>
	<td>`class InputIcon : public Dekorater {}`</td>
	<td>Izvodi se iz dekoratera i implementira nove funkcionalnosti i "dodaje" je ih subjektu.</td>
</tr>
<tr>
	<td colspan='3'>Fasada</td>
</tr>
<tr>
	<td>`Podsistem`</td>
	<td>`class CPU {}`</td>
	<td>Jedna ili vise kompleksnih klasa koje izvrsavaju zahtev fasade</td>
</tr>
<tr>
	<td>`Fasada`</td>
	<td>`class Kompjuter {
CPU* ptr_cpu;
void start() {
ptr_prav->upali();
ptr_prav->proveri();
}
}`</td>
	<td>Sadži pokazivače na sve podsisteme, i u nekoj funkciji ih sve poziva. Tako sakriva kompleksnost i izbegava pozivanje u pogrešnom redosledu</td>
</tr>
<tr>
	<td colspan='3'>Muva</td>
</tr>
<tr>
	<td>`IMuva`</td>
	<td>```class Slovo {
virtual void prikazi(int) = 0;
Slovo(char _simbol): simbol(_simbol){}
char simbol;
};```</td>
	<td>Deklariše bazu muve. Trebalo bi da sadrži i unutrašnje i spoljašnje stanje</td>
</tr>
<tr>
	<td>`Muva`</td>
	<td>`class SlovoA : public Slovo {
SlovoA(): Slovo('A'){}
void prikazi(int font) {...}
};`</td>
	<td>Koknretna muva koja se izvodi iz `IMuve`. I implementira spoljašnje stanje</td>
</tr>
<tr>
	<td>`Fabrika`</td>
	<td>`class Fabrika {
….
map
		<char, Slovo*> slova;
};`
		</td>
		<td>Kreira i upravlja muvama, čuva muva i ako postoji ne pravi ih opet</td>
	</tr>
	<tr>
		<td colspan='3'>Zastupnik</td>
	</tr>
	<tr>
		<td>`Subjekat`</td>
		<td>`class Racun {}`</td>
		<td>Objekat koji treba da radi sa zastupnikom, on prima zahteve od zastupnika.</td>
	</tr>
	<tr>
		<td>`Zatupnik`</td>
		<td>`class Banka : public Racun {}`</td>
		<td>Unutar zastupnika proveravamo ulosve i tek onda zovemo `Subjekat`</td>
	</tr>
</table>
