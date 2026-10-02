# Extra 6. Classes i objectes

!!! abstract "Resum"
    **Tipus:** ampliació opcional · **Requisits:** unitats 5 i 6 (és recomanable haver fet l'extra de diccionaris) · **Sense lliurament:** fes les activitats i comprova-les amb les solucions.

    És l'extra més llarg. Pots fer-lo en dues tandes: apartats 1 a 4 (crear classes) i apartats 5 a 8 (fer-les servir en programes més grans).

## Objectius

En acabar aquest extra sabràs:

- Explicar què és una **classe** i què és un **objecte**.
- Definir una classe amb `class`, `__init__`, atributs i mètodes.
- Crear objectes i fer-los treballar entre ells.
- Mostrar un objecte amb `__str__`.
- Guardar objectes en llistes i recórrer-los.
- Decidir quan val la pena fer servir una classe.

## Punt de partida

!!! question "Ho recordes?"
    Ja has fet servir objectes sense saber-ho. Quan escrius `notes.append(5)` o `text.upper()`, `notes` és un objecte de la classe `list` i `text` és un objecte de la classe `str`. Les funcions que porten un punt, com `append` o `upper`, són **mètodes**.

    Fins ara, per guardar la informació d'un alumne has fet servir un diccionari, i les funcions que hi treballaven eren a part. Amb una **classe** ho reuneixes tot en una sola peça: les **dades** d'una cosa i **el que sap fer**. I si has fet el projecte E de la unitat 7 (l'inventari), saps que gestionar productes amb llistes paral·leles és força incòmode.

## Teoria

### 1. La idea: classe i objecte

Pensa en el **plànol d'una casa** i en les **cases** que es construeixen amb aquest plànol:

- El plànol és la **classe**: descriu com seran les cases (quantes habitacions, quins elements...), però no és cap casa.
- Cada casa construïda és un **objecte**: té les seves característiques concretes.

En Python, una classe `Alumne` descriu quines dades té un alumne (nom, edat...) i què sap fer (calcular la seva mitjana...). I els objectes `anna` i `pere` són alumnes concrets.

| Terme | Què és | Exemple |
| --- | --- | --- |
| **Classe** | El plànol d'un tipus de cosa | `Alumne` |
| **Objecte** (o *instància*) | Un exemplar concret creat amb la classe | `anna`, `pere` |
| **Atribut** | Una dada de l'objecte | `anna.nom` |
| **Mètode** | Una funció que pertany a l'objecte | `anna.mitjana()` |

### 2. La primera classe: `__init__` i atributs

```python
class Alumne:
    def __init__(self, nom, edat):
        self.nom = nom
        self.edat = edat

anna = Alumne("Anna", 15)
pere = Alumne("Pere", 16)

print(anna.nom)      # Anna
print(pere.edat)     # 16
```

Què fa cada part:

- `class Alumne:` defineix la classe. El nom comença per **majúscula**.
- `__init__` és un mètode especial, el **constructor**: s'executa automàticament cada cop que es **crea** un objecte. Té dos guions baixos a cada costat.
- `self` és l'objecte concret que s'està creant (o utilitzant). Sempre és el **primer paràmetre** de qualsevol mètode.
- `self.nom = nom` guarda la dada dins de l'objecte com un **atribut**.
- `Alumne("Anna", 15)` crea un objecte. Fixa't que **no escrivim `self`** a la crida: Python el posa sol.

Els atributs s'agafen amb un punt (`anna.nom`) i també es poden modificar: `anna.edat = 16`.

!!! tip "Per recordar"
    Cada objecte té **les seves pròpies dades**. Canviar l'edat de l'`anna` no canvia la del `pere`.

### 3. Mètodes

Un **mètode** és una funció definida dins de la classe. Sempre té `self` com a primer paràmetre, i amb ell pot llegir i modificar les dades de l'objecte:

```python
class Alumne:
    def __init__(self, nom, edat):
        self.nom = nom
        self.edat = edat
        self.notes = []

    def afegeix_nota(self, nota):
        self.notes.append(nota)

    def mitjana(self):
        if len(self.notes) == 0:
            return 0
        return sum(self.notes) / len(self.notes)

anna = Alumne("Anna", 15)
anna.afegeix_nota(8)
anna.afegeix_nota(6)
print(anna.mitjana())      # 7.0

pere = Alumne("Pere", 16)
print(pere.mitjana())      # 0
```

Quan fas `anna.afegeix_nota(8)`, Python crida el mètode i passa `anna` com a `self` automàticament. Per això el mètode té dos paràmetres (`self` i `nota`) però només li passem un valor.

!!! info "Per què `self.notes = []` i no un paràmetre?"
    Perquè tots els alumnes comencen sense notes. Dins de `__init__` pots crear atributs amb un valor inicial fix, sense haver-lo de passar a l'hora de crear l'objecte.

### 4. Mostrar un objecte: `__str__`

Si fas `print(anna)`, Python mostra una cosa poc útil, com `<__main__.Alumne object at 0x...>`. Amb el mètode especial `__str__` decidim **com es mostra** un objecte:

```python
class Alumne:
    def __init__(self, nom, edat):
        self.nom = nom
        self.edat = edat

    def __str__(self):
        return f"{self.nom} ({self.edat} anys)"

anna = Alumne("Anna", 15)
print(anna)               # Anna (15 anys)
print(f"Alumna: {anna}")  # Alumna: Anna (15 anys)
```

`__str__` ha de **retornar** un text (no fer `print`).

### 5. Objectes en llistes

Els objectes es poden guardar en llistes com qualsevol altra dada. Recórrer-los és molt natural:

```python
alumnes = [Alumne("Anna", 15), Alumne("Pere", 16), Alumne("Marta", 15)]

for alumne in alumnes:
    print(alumne)
```

I cerques com la del màxim funcionen igual, però ara amb atributs i mètodes:

```python
mes_gran = alumnes[0]
for alumne in alumnes:
    if alumne.edat > mes_gran.edat:
        mes_gran = alumne
print(f"El més gran és {mes_gran.nom}")
```

### 6. Mètodes que protegeixen les dades

Un gran avantatge de les classes és que els **mètodes controlen com es canvien les dades**. Per exemple, un compte bancari no pot quedar en negatiu:

```python
class CompteBancari:
    def __init__(self, titular):
        self.titular = titular
        self.saldo = 0

    def ingressa(self, quantitat):
        if quantitat > 0:
            self.saldo += quantitat

    def retira(self, quantitat):
        if 0 < quantitat <= self.saldo:
            self.saldo -= quantitat
            return True
        return False

    def __str__(self):
        return f"{self.titular}: {self.saldo} €"

compte = CompteBancari("Anna")
compte.ingressa(100)
print(compte.retira(30))     # True
print(compte.retira(500))    # False: no hi ha prou saldo
print(compte)                # Anna: 70 €
```

### 7. Classe o diccionari?

Podem guardar la informació d'un alumne amb un diccionari o amb una classe. Compara:

| | Diccionari + funcions | Classe |
| --- | --- | --- |
| Accedir a una dada | `alumne["nom"]` | `alumne.nom` |
| Les funcions són... | Soltes, separades de les dades | Dins l'objecte, com a mètodes |
| Si t'equivoques en el nom d'una dada | Potser no et dona error fins més tard | `AttributeError` immediat |
| Ideal per a... | Dades senzilles i puntuals | Coses amb dades **i** comportament |

### 8. Quan val la pena fer servir classes?

Les classes són útils quan el programa gira al voltant de **«coses»** amb dades i accions: alumnes, productes, comptes, personatges d'un joc, llibres... Si tens diverses variables i funcions que sempre van juntes, probablement és una classe.

Però **no cal fer-les servir sempre**: per a programes petits, unes quantes funcions i variables ja van molt bé.

## Exemples resolts

Copia'ls a Thonny, executa'ls i **modifica'ls** per veure què canvia.

**Exemple 1. Un rectangle**

```python
class Rectangle:
    def __init__(self, base, altura):
        self.base = base
        self.altura = altura

    def area(self):
        return self.base * self.altura

    def perimetre(self):
        return 2 * (self.base + self.altura)

r = Rectangle(4, 3)
print(r.area())          # 12
print(r.perimetre())     # 14
```

**Exemple 2. Un alumne amb notes**

```python
class Alumne:
    def __init__(self, nom, edat):
        self.nom = nom
        self.edat = edat
        self.notes = []

    def afegeix_nota(self, nota):
        self.notes.append(nota)

    def mitjana(self):
        if len(self.notes) == 0:
            return 0
        return sum(self.notes) / len(self.notes)

    def __str__(self):
        return f"{self.nom}: mitjana {round(self.mitjana(), 2)}"

anna = Alumne("Anna", 15)
anna.afegeix_nota(8)
anna.afegeix_nota(7)
anna.afegeix_nota(10)
print(anna)
```

Un mètode pot cridar-ne un altre amb `self` (aquí `__str__` crida `mitjana`).

**Exemple 3. Un compte bancari interactiu**

```python
class CompteBancari:
    def __init__(self, titular):
        self.titular = titular
        self.saldo = 0

    def ingressa(self, quantitat):
        if quantitat > 0:
            self.saldo += quantitat

    def retira(self, quantitat):
        if 0 < quantitat <= self.saldo:
            self.saldo -= quantitat
            return True
        return False

compte = CompteBancari("Anna")
compte.ingressa(100)

quantitat = int(input("Quant vols retirar? "))
if compte.retira(quantitat):
    print(f"Fet! Et queden {compte.saldo} €")
else:
    print(f"No pots: només tens {compte.saldo} €")
```

**Exemple 4. L'inventari, amb una classe `Producte`**

Aquesta és la versió amb classes del projecte E de la unitat 7:

```python
class Producte:
    def __init__(self, nom, preu, estoc):
        self.nom = nom
        self.preu = preu
        self.estoc = estoc

    def ven(self, unitats):
        if unitats <= self.estoc:
            self.estoc -= unitats
            return True
        return False

    def __str__(self):
        return f"{self.nom}: {self.estoc} unitats a {self.preu:.2f} €"

inventari = [Producte("llapis", 0.5, 20), Producte("goma", 0.75, 15)]

for producte in inventari:
    print(producte)

nom = input("Quin producte vols comprar? ")
unitats = int(input("Quantes unitats? "))

trobat = False
for producte in inventari:
    if producte.nom == nom:
        trobat = True
        if producte.ven(unitats):
            print("Compra feta!")
        else:
            print("No hi ha prou estoc")

if not trobat:
    print("Aquest producte no existeix")
```

Ara cada producte guarda les seves dades i sap vendre's ell mateix. Compara-ho amb les dues llistes paral·leles.

**Exemple 5. Un combat entre personatges**

```python
import random

class Personatge:
    def __init__(self, nom, vida):
        self.nom = nom
        self.vida = vida

    def ataca(self, altre):
        mal = random.randint(1, 10)
        altre.vida -= mal
        print(f"{self.nom} fa {mal} de mal a {altre.nom}. Vida de {altre.nom}: {max(altre.vida, 0)}")

    def esta_viu(self):
        return self.vida > 0

heroi = Personatge("Heroi", 30)
drac = Personatge("Drac", 40)

while heroi.esta_viu() and drac.esta_viu():
    heroi.ataca(drac)
    if drac.esta_viu():
        drac.ataca(heroi)

if heroi.esta_viu():
    print("Has guanyat!")
else:
    print("El drac ha guanyat")
```

Observa que un objecte pot rebre **un altre objecte** com a paràmetre (`altre`).

## Errors típics

!!! failure "Oblidar `self` en definir un mètode"
    ```python
    class Alumne:
        def __init__(self, nom):
            self.nom = nom

        def saluda():
            print("Hola")

    anna = Alumne("Anna")
    anna.saluda()
    ```

    - **Missatge (similar a):** `TypeError: Alumne.saluda() takes 0 positional arguments but 1 was given`
    - **Què vol dir:** Python passa l'objecte com a primer argument, però el mètode no té on rebre'l.
    - **Com es corregeix:** `def saluda(self):`.

!!! failure "Oblidar `self.` per accedir a un atribut"
    ```python
    class Alumne:
        def __init__(self, nom):
            self.nom = nom

        def saluda(self):
            print("Hola, sóc " + nom)
    ```

    - **Missatge (similar a):** `NameError: name 'nom' is not defined`
    - **Què vol dir:** `nom` sol és una variable que no existeix dins del mètode. L'atribut és `self.nom`.
    - **Com es corregeix:** `print("Hola, sóc " + self.nom)`.

!!! failure "Crear un objecte amb dades que falten"
    ```python
    class Alumne:
        def __init__(self, nom, edat):
            self.nom = nom
            self.edat = edat

    anna = Alumne("Anna")
    ```

    - **Missatge (similar a):** `TypeError: Alumne.__init__() missing 1 required positional argument: 'edat'`
    - **Què vol dir:** el constructor demana nom i edat, i només n'has donat un.
    - **Com es corregeix:** `Alumne("Anna", 15)`.

!!! failure "Escriure `__init__` amb un sol guió baix"
    ```python
    class Alumne:
        def _init_(self, nom):
            self.nom = nom

    anna = Alumne("Anna")
    ```

    - **Missatge (similar a):** `TypeError: Alumne() takes no arguments`
    - **Què vol dir:** Python no reconeix el constructor, perquè el nom correcte porta **dos guions baixos** a cada costat: `__init__`.
    - **Com es corregeix:** `def __init__(self, nom):`.

!!! failure "Demanar un atribut que no existeix"
    ```python
    anna = Alumne("Anna", 15)
    print(anna.cognom)
    ```

    - **Missatge (similar a):** `AttributeError: 'Alumne' object has no attribute 'cognom'`
    - **Què vol dir:** l'objecte no té cap atribut anomenat `cognom`.
    - **Com es corregeix:** comprova el nom de l'atribut al `__init__`, o afegeix-lo a la classe.

!!! failure "Oblidar els parèntesis en cridar un mètode (sense missatge d'error)"
    ```python
    anna = Alumne("Anna", 15)
    print(anna.mitjana)
    ```

    - **Resultat:** mostra una cosa com `<bound method Alumne.mitjana of ...>`.
    - **Què vol dir:** sense parèntesis nomenes el mètode, però no l'executes.
    - **Com es corregeix:** `anna.mitjana()`.

## Activitats guiades

### Activitat 1. Prediu: objectes independents

```python
class Comptador:
    def __init__(self):
        self.valor = 0

    def suma(self):
        self.valor += 1

a = Comptador()
b = Comptador()
a.suma()
a.suma()
b.suma()
print(a.valor, b.valor)
```

??? success "Solució"
    Mostra `2 1`. `a` i `b` són dos objectes diferents, cadascun amb el seu propi `valor`.

### Activitat 2. Prediu: dues variables, un sol objecte

```python
a = Comptador()
b = a
b.suma()
print(a.valor)
```

??? success "Solució"
    Mostra `1`. `b = a` **no crea un objecte nou**: les dues variables apunten al mateix objecte, com passava amb les llistes. Si vols dos objectes diferents, cal crear-los amb `Comptador()` cada cop.

### Activitat 3. Corregeix el codi

Aquest programa té tres errors. Corregeix-los **un per un**.

```python
class Alumne:
    def __init__(self, nom, edat):
        nom = nom
        edat = edat

    def saluda():
        print("Hola, sóc " + nom)

anna = Alumne("Anna", 15)
anna.saluda()
```

??? success "Solució"
    ```python
    class Alumne:
        def __init__(self, nom, edat):
            self.nom = nom
            self.edat = edat

        def saluda(self):
            print("Hola, sóc " + self.nom)

    anna = Alumne("Anna", 15)
    anna.saluda()
    ```

    Errors: (1) `nom = nom` només guarda el valor en una variable local; per guardar-lo a l'objecte cal `self.nom = nom` (igual amb l'edat); (2) el mètode `saluda` no té el paràmetre `self`; (3) dins del mètode, per llegir l'atribut cal `self.nom`.

### Activitat 4. Completa el codi

Completa la classe que representa un cercle.

```python
class Cercle:
    def __init__(self, radi):
        ___.radi = radi

    def area(___):
        return 3.14159 * self.radi ** 2

c = Cercle(2)
print(round(c.___(), 2))
```

??? success "Solució"
    ```python
    class Cercle:
        def __init__(self, radi):
            self.radi = radi

        def area(self):
            return 3.14159 * self.radi ** 2

    c = Cercle(2)
    print(round(c.area(), 2))      # 12.57
    ```

### Activitat 5. Escriu-ho tu (una classe)

Crea una classe `Llibre` amb el **títol** i el **nombre de pàgines** (la pàgina actual comença a 0). Ha de tenir:

- Un mètode `llegeix(n)` que avanci `n` pàgines, sense passar-se del total.
- Un mètode `acabat()` que retorni `True` si has arribat a l'última pàgina.
- Un mètode `__str__` que mostri, per exemple, `El meu llibre (pàgina 60 de 100)`.

??? success "Solució"
    ```python
    class Llibre:
        def __init__(self, titol, pagines):
            self.titol = titol
            self.pagines = pagines
            self.pagina_actual = 0

        def llegeix(self, n):
            self.pagina_actual += n
            if self.pagina_actual > self.pagines:
                self.pagina_actual = self.pagines

        def acabat(self):
            return self.pagina_actual == self.pagines

        def __str__(self):
            return f"{self.titol} (pàgina {self.pagina_actual} de {self.pagines})"

    llibre = Llibre("El meu llibre", 100)
    llibre.llegeix(60)
    print(llibre)               # El meu llibre (pàgina 60 de 100)
    llibre.llegeix(60)
    print(llibre)               # El meu llibre (pàgina 100 de 100)
    print(llibre.acabat())      # True
    ```

### Activitat 6. Escriu-ho tu (una llista d'objectes)

Fent servir la classe `Alumne` amb notes de la teoria, crea tres alumnes amb aquestes notes: Anna (8, 6), Pere (5, 7) i Marta (9, 9). Guarda'ls en una llista i mostra **qui té la millor mitjana**.

??? success "Solució"
    ```python
    anna = Alumne("Anna", 15)
    pere = Alumne("Pere", 16)
    marta = Alumne("Marta", 15)

    for nota in [8, 6]:
        anna.afegeix_nota(nota)
    for nota in [5, 7]:
        pere.afegeix_nota(nota)
    for nota in [9, 9]:
        marta.afegeix_nota(nota)

    alumnes = [anna, pere, marta]
    millor = alumnes[0]
    for alumne in alumnes:
        if alumne.mitjana() > millor.mitjana():
            millor = alumne
    print(f"Millor mitjana: {millor.nom} ({millor.mitjana()})")
    ```

    Mostra `Millor mitjana: Marta (9.0)`.

## Repte opcional

**Els teus projectes, amb classes.** Tria un dels projectes de la unitat 7 (el gestor de tasques, l'inventari, el qüestionari...) i refés-lo amb una o més classes: per exemple, `Tasca`, `Pregunta` o `Producte`. Compara les dues versions i pensa quina és més fàcil d'ampliar.

**Per anar més lluny: l'herència.** Una classe pot **heretar** d'una altra i aprofitar-ne les dades i els mètodes. Investiga-ho a partir d'aquest esquelet:

```python
class Delegat(Alumne):
    def __init__(self, nom, edat, curs):
        super().__init__(nom, edat)
        self.curs = curs
```

`Delegat` és un `Alumne` amb una dada extra. Prova de crear un objecte `Delegat` i de cridar-li els mètodes de la classe `Alumne`.

## Xuleta

| Vull... | Escric... |
| --- | --- |
| Definir una classe | `class Nom:` (nom amb majúscula) |
| El constructor | `def __init__(self, dada1, dada2):` |
| Guardar una dada a l'objecte | `self.dada = dada` |
| Definir un mètode | `def accio(self, parametre):` |
| Crear un objecte | `objecte = Nom(valor1, valor2)` |
| Llegir / canviar un atribut | `objecte.dada` / `objecte.dada = nou` |
| Cridar un mètode | `objecte.accio(valor)` |
| Com es mostra un objecte | `def __str__(self): return ...` |
| Objectes en una llista | `llista = [Nom(...), Nom(...)]` |
| Dins d'un mètode, cridar-ne un altre | `self.altre_metode()` |
