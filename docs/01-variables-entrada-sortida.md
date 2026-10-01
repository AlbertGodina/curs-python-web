# Unitat 1. Variables i entrada/sortida

!!! abstract "Resum"
    **Sessions:** 2 · **Lliurament a Classroom:** `u1_cognom_nom.py`

    - **Sessió 1:** apartats 1 a 4 (sortida, variables, tipus i f-strings).
    - **Sessió 2:** apartats 5 i 6 (entrada i conversió), errors, activitats i lliurament.

## Objectius

En acabar aquesta unitat sabràs:

- Mostrar informació per pantalla amb `print()` i *f-strings*.
- Guardar dades en variables amb noms adequats.
- Distingir els quatre tipus bàsics: `str`, `int`, `float` i `bool`.
- Demanar dades a l'usuari amb `input()` i convertir-les al tipus que necessites.
- Reconèixer i corregir els errors de tipus més habituals.

## Punt de partida

!!! question "Ho recordes?"
    Tot algorisme té tres parts: **entrada** (les dades que rep), **procés** (el que en fa) i **sortida** (el resultat). I ja heu treballat amb **variables** als algorismes: com una caixa amb etiqueta on es guarda un valor.

    Aquesta és la traducció del pseudocodi a Python:

    | Pseudocodi | Python |
    | --- | --- |
    | `nom ← "Anna"` | `nom = "Anna"` |
    | `Llegeix nom` | `nom = input()` |
    | `Escriu nom` | `print(nom)` |

## Teoria

### 1. Sortida: `print()`

Ja saps mostrar text. Amb `print()` també pots mostrar diverses coses a la vegada separant-les amb comes, i Python posa un espai entre elles:

```python
print("Tinc", 15, "anys")
```

!!! tip "Per recordar"
    El text va sempre entre cometes; els nombres, no.

### 2. Variables

Una **variable** és un nom que apunta a un valor guardat a la memòria. Es crea amb el signe `=`:

```python
nom = "Anna"
punts = 10
```

El signe `=` **no vol dir «és igual a»**. Vol dir **«guarda a la variable de l'esquerra el valor de la dreta»**. Per això una variable pot canviar de valor:

```python
punts = 10
punts = punts + 5     # Ara punts val 15
```

**Regles per als noms de variables**

- Només poden portar lletres, xifres i guions baixos (`_`), i **no poden començar per una xifra**.
- Distingeixen majúscules i minúscules: `nom` i `Nom` són variables diferents.
- No poden ser paraules reservades de Python (`print`, `if`, `for`...).
- **Convenció del curs:** minúscules, guions baixos i **sense accents ni `ç`** (`edat_usuari`, `preu_final`). Python els accepta, però així evitem problemes entre ordinadors.
- Que el nom expliqui què guarda: `edat` és millor que `e` o `x`.

!!! tip "Veure-ho a Thonny"
    Obre **Visualitza → Variables** i executa el programa: veuràs el nom, el valor i el tipus de cada variable.

### 3. Tipus de dades

Cada valor té un **tipus**. De moment en treballem quatre:

| Tipus | Què guarda | Exemples |
| --- | --- | --- |
| `str` (text) | Paraules i frases, sempre entre cometes | `"Hola"`, `'42'` |
| `int` (enter) | Nombres sense decimals | `42`, `-7` |
| `float` (decimal) | Nombres amb decimals | `3.14`, `9.99` |
| `bool` (booleà) | Només `True` o `False` | `True` |

Amb la funció `type()` pots comprovar el tipus de qualsevol valor:

```python
print(type("Hola"))    # <class 'str'>
print(type(42))        # <class 'int'>
```

!!! warning "Els decimals porten punt, no coma"
    A Catalunya escrivim `3,14`, però en Python el separador decimal és el **punt**: `3.14`.

    Compte: `pi = 3,14` **no dona cap error**. Python crea una *tupla* `(3, 14)` amb dos nombres, i el programa segueix... amb un valor que no era el que volies.

!!! tip "Per recordar"
    `"7"` (text) i `7` (nombre) són coses diferents. Les cometes canvien el tipus.

### 4. *f-strings*: text amb variables

Una **f-string** és un text amb una `f` davant de les cometes. Dins pots posar variables entre claus `{ }` i Python les substitueix pel seu valor:

```python
nom = "Anna"
edat = 15
print(f"Em dic {nom} i tinc {edat} anys.")
```

Dins les claus també pots escriure operacions senzilles: `{edat + 1}`.

### 5. Entrada: `input()`

`input()` mostra un missatge, espera que l'usuari escrigui alguna cosa i premi **Intro**, i **retorna el que ha escrit**:

```python
nom = input("Com et dius? ")
print(f"Hola, {nom}!")
```

!!! danger "Atenció"
    `input()` **sempre retorna text (`str`)**, encara que l'usuari escrigui un nombre. `"20"` no és el mateix que `20`.

### 6. Conversió de tipus

Per treballar amb nombres, hem de convertir el text que retorna `input()`:

| Funció | Converteix a... | Exemple |
| --- | --- | --- |
| `int()` | Enter | `int("20")` → `20` |
| `float()` | Decimal | `float("1.75")` → `1.75` |
| `str()` | Text | `str(20)` → `"20"` |

El patró més habitual és convertir just en el moment de llegir:

```python
edat = int(input("Quants anys tens? "))
print(f"L'any vinent en faràs {edat + 1}.")
```

## Exemples resolts

Copia'ls a Thonny, executa'ls i **modifica'ls** per veure què canvia.

**Exemple 1. Una presentació**

```python
nom = "Anna"
edat = 15
altura = 1.68
print(f"Em dic {nom}, tinc {edat} anys i faig {altura} m.")
```

**Exemple 2. Una variable que canvia de valor**

```python
punts = 10
print(punts)
punts = punts + 5
print(punts)
print(type(punts))
```

Mostra `10`, `15` i `<class 'int'>`. Comprova-ho amb el panell de Variables de Thonny.

**Exemple 3. Preguntar i respondre**

```python
nom = input("Com et dius? ")
edat = int(input("Quants anys tens? "))
print(f"Hola, {nom}! L'any vinent tindràs {edat + 1} anys.")
```

**Exemple 4. Àrea d'un quadrat**

```python
costat = float(input("Quant fa el costat (en cm)? "))
area = costat * costat
print(f"L'àrea és {area} cm²")
```

Hem fet servir `*` per multiplicar. Els operadors els veurem a fons a la unitat 2.

## Errors típics

!!! failure "Oblidar les cometes (o escriure malament una variable)"
    ```python
    nom = Anna
    ```

    - **Missatge (similar a):** `NameError: name 'Anna' is not defined`
    - **Què vol dir:** sense cometes, Python creu que `Anna` és una variable, però no l'has creat. Passa el mateix si escrius malament el nom d'una variable (`print(nmo)`).
    - **Com es corregeix:** `nom = "Anna"`.

!!! failure "Sumar text i nombre"
    ```python
    edat = input("Quants anys tens? ")
    print(edat + 1)
    ```

    - **Missatge (similar a):** `TypeError: can only concatenate str (not "int") to str`
    - **Què vol dir:** `edat` és text (perquè ve d'`input()`) i intentes sumar-hi un nombre.
    - **Com es corregeix:** converteix primer: `edat = int(input("Quants anys tens? "))`.

!!! failure "Convertir un text que no és un nombre"
    ```python
    edat = int(input("Quants anys tens? "))
    ```

    Si l'usuari escriu `vint`:

    - **Missatge (similar a):** `ValueError: invalid literal for int() with base 10: 'vint'`
    - **Què vol dir:** `int()` només pot convertir textos que ja semblin un nombre enter.
    - **Com es corregeix:** l'usuari ha d'escriure `20`. (A l'apartat d'Extres sobre `try/except` veuràs com controlar aquesta situació; de moment, escriu bé les dades.)

!!! failure "Decimals amb coma (sense missatge d'error)"
    ```python
    preu = 9,99
    print(preu)
    ```

    - **Resultat:** mostra `(9, 99)`.
    - **Què vol dir:** Python ha creat una tupla amb dos nombres, no un decimal.
    - **Com es corregeix:** `preu = 9.99`.

## Activitats guiades

### Activitat 1. Prediu el valor de les variables

Abans d'executar-lo, escriu què mostrarà. Després comprova-ho a Thonny, mirant el panell de Variables pas a pas.

```python
a = 5
b = 3
a = b
b = a
print(a, b)
```

??? success "Solució"
    Mostra `3 3`. A la tercera línia `a` passa a valer 3 (el valor de `b`); a la quarta, `b` rep el valor de `a`, que ja és 3. El valor original de `a` (5) s'ha perdut.

### Activitat 2. Prediu els tipus

Quin és el tipus de cada variable? Comprova-ho amb `type()`.

```python
w = "True"
x = "7"
y = 7
z = 7.0
```

??? success "Solució"
    - `w` és `str`: està entre cometes, encara que el contingut sigui `True`.
    - `x` és `str`: `"7"` és text, no un nombre.
    - `y` és `int`.
    - `z` és `float`: porta la part decimal, encara que sigui `.0`.

### Activitat 3. Corregeix el codi

Aquest programa té tres errors. Corregeix-los **un per un**.

```python
nom = input("Com et dius? )
edat = input("Quants anys tens? ")
print(nom + ", l'any vinent tindràs " + edat + 1 + " anys")
```

??? success "Solució"
    ```python
    nom = input("Com et dius? ")
    edat = int(input("Quants anys tens? "))
    print(f"{nom}, l'any vinent tindràs {edat + 1} anys")
    ```

    Errors: (1) falten les cometes de tancament a la primera línia; (2) `edat` no s'ha convertit a `int`; (3) s'intenta sumar text i nombre. Amb una f-string no cal convertir res més.

### Activitat 4. Completa el codi

Substitueix cada `___` perquè el programa calculi el cost d'una compra.

```python
producte = input("Quin producte compres? ")
preu = ___(input("Quant costa una unitat? "))
unitats = ___(input("Quantes unitats? "))
total = preu * unitats
print(f"{unitats} unitats de {___} costen {___} €")
```

??? success "Solució"
    ```python
    producte = input("Quin producte compres? ")
    preu = float(input("Quant costa una unitat? "))
    unitats = int(input("Quantes unitats? "))
    total = preu * unitats
    print(f"{unitats} unitats de {producte} costen {total} €")
    ```

    El preu pot tenir decimals (`float`); les unitats són un nombre enter (`int`).

## Lliurament (Classroom)

!!! example "Què has de lliurar"
    **Fitxer:** `u1_cognom_nom.py`

    Fes un programa que faci una **fitxa personal**:

    1. Demana amb `input()` quatre dades: el **nom**, l'**edat** (enter), l'**altura en metres** (decimal) i la **ciutat o poble** on vius.
    2. Guarda cada dada en una **variable** amb un nom adequat (minúscules i guions baixos).
    3. Mostra la fitxa amb **f-strings**, una dada per línia.
    4. Mostra també l'**edat que tindràs d'aquí a 10 anys** i **quants mesos has viscut aproximadament** (edat per 12).

    Exemple del que hauria de mostrar (les dades varien):

    ```text
    --- FITXA PERSONAL ---
    Nom: Anna
    Edat: 15
    Altura: 1.68 m
    Lloc: Girona
    D'aquí a 10 anys tindràs 25 anys.
    Has viscut aproximadament 180 mesos.
    ```

    **Abans de lliurar, comprova que:**

    1. El fitxer té la capçalera amb el teu nom, la data i la unitat.
    2. Has convertit l'edat a `int` i l'altura a `float`.
    3. No hi ha cap dada escrita directament al codi: tot ve d'`input()`.
    4. Hi ha almenys dos comentaris propis.
    5. El programa s'executa sense errors.

## Repte opcional

**Intercanvi de valors.** Fes un programa que demani dos valors, els guardi a `a` i `b`, i **n'intercanviï el contingut**: al final, `a` ha de tenir el que tenia `b` i a l'inrevés. Mostra els valors abans i després.

*Pista:* necessitaràs una tercera variable auxiliar (pensa en com intercanviaries el contingut de dos gots).

*Ampliació:* Python permet fer-ho en una sola línia amb `a, b = b, a`. Comprova que funciona.

## Xuleta

| Vull... | Escric... |
| --- | --- |
| Mostrar text i variables | `print(f"Hola, {nom}")` |
| Guardar un valor | `edat = 15` |
| Demanar un text | `nom = input("Nom? ")` |
| Demanar un enter | `edat = int(input("Edat? "))` |
| Demanar un decimal | `altura = float(input("Altura? "))` |
| Saber el tipus | `type(valor)` |
| Convertir a text | `str(20)` |
