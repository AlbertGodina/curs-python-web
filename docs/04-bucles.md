# Unitat 4. Bucles

!!! abstract "Resum"
    **Sessions:** 4 · **Lliurament a Classroom:** `u4_cognom_nom.py`

    - **Sessió 1:** apartats 1 i 2 (`while` i bucle infinit).
    - **Sessió 2:** apartats 3 i 4 (comptadors, acumuladors i validació d'entrades).
    - **Sessió 3:** apartats 5 i 6 (`for`, `range()` i recórrer un text).
    - **Sessió 4:** apartat 7 (bucles dins de bucles), activitats pendents i lliurament.

## Objectius

En acabar aquesta unitat sabràs:

- Repetir instruccions amb `while` i amb `for`.
- Triar el bucle adequat segons si saps quantes vegades has de repetir.
- Fer servir `range()` amb un, dos o tres paràmetres.
- Usar comptadors i acumuladors correctament.
- Validar dades d'entrada repetint la pregunta fins que siguin correctes.
- Reconèixer i evitar els errors típics: bucle infinit i límits mal posats.

## Punt de partida

!!! question "Ho recordes?"
    Als algorismes, quan una acció s'ha de repetir, no s'escriu cent vegades: es fa un **bucle**. En pseudocodi hi ha dues formes:

    ```text
    Mentre condició fer          Per i de 1 a 5 fer
        ...                          ...
    Fi mentre                    Fi per
    ```

    En Python són `while` (mentre) i `for` (per a). Compte amb una diferència: «Per i de 1 a 5» inclou el 5, però `range(1, 5)` **no** l'inclou. Més endavant ho veurem.

## Teoria

### 1. Repetir mentre es compleixi una condició: `while`

```python
n = 3
while n > 0:
    print(n)
    n = n - 1
print("Enlairament!")
```

Mostra `3`, `2`, `1` i `Enlairament!`. Cada repetició del bucle s'anomena **iteració**.

`while` funciona com un `if` que **torna a començar**: comprova la condició, i si és certa, executa el bloc i torna a comprovar-la. Quan és falsa, el bucle s'acaba i el programa continua per la línia següent (la que no està indentada).

Un bucle `while` necessita **tres coses**:

1. Un **valor inicial** abans del bucle (`n = 3`).
2. Una **condició** (`n > 0`).
3. Una **actualització** dins del bucle que acabi fent falsa la condició (`n = n - 1`).

### 2. El bucle infinit

Si oblides l'actualització, la condició no deixa mai de ser certa i el programa no acaba mai:

```python
n = 3
while n > 0:
    print(n)       # Falta n = n - 1
```

!!! danger "Com aturar un programa que no acaba"
    A Thonny, prem el **botó vermell d'aturada** (Stop). Si el programa ha omplert la Shell de línies, no passa res: és el que s'espera d'un bucle infinit.

!!! tip "Per recordar"
    Abans d'executar un `while`, comprova: **la variable de la condició canvia dins del bucle?**

### 3. Comptadors i acumuladors

Dues idees que surten en gairebé tots els bucles:

- Un **comptador** compta quantes vegades passa alguna cosa: se li suma sempre 1.
- Un **acumulador** va guardant un total: se li suma el valor de cada iteració.

```python
comptador = 0       # Valor inicial, ABANS del bucle
suma = 0            # Valor inicial, ABANS del bucle

while comptador < 5:
    nota = float(input("Nota: "))
    suma += nota               # Acumulador
    comptador += 1             # Comptador

print(f"Mitjana: {suma / comptador}")
```

!!! warning "Inicialitza abans del bucle"
    Si poses `suma = 0` **dins** del bucle, es posa a zero a cada iteració i perds el que has acumulat.

### 4. Validar dades i acabar amb un valor especial

**Validar una entrada.** Repetim la pregunta mentre la resposta no sigui vàlida:

```python
edat = int(input("Edat (0-120): "))
while edat < 0 or edat > 120:
    print("Valor no vàlid")
    edat = int(input("Edat (0-120): "))
```

**Valor sentinella.** L'usuari escriu dades fins que introdueix un valor especial que vol dir «he acabat» (aquí, el 0):

```python
suma = 0
nombre = int(input("Nombre (0 per acabar): "))
while nombre != 0:
    suma += nombre
    nombre = int(input("Nombre (0 per acabar): "))
print(f"La suma és {suma}")
```

**`while True` i `break`.** Una altra forma: un bucle que, en principi, no acaba mai, i del qual sortim amb `break` quan es compleix alguna cosa:

```python
while True:
    clau = input("Contrasenya: ")
    if clau == "python123":
        break
    print("Incorrecta")
print("Benvingut!")
```

`break` surt del bucle immediatament.

### 5. Repetir un nombre conegut de vegades: `for` i `range()`

Quan **saps quantes vegades** has de repetir, `for` és més còmode que `while`:

```python
for i in range(5):
    print("Hola")
```

`range()` genera una seqüència de nombres. La variable (`i`) va prenent cada valor:

| Expressió | Valors de `i` | Comentari |
| --- | --- | --- |
| `range(5)` | `0, 1, 2, 3, 4` | Comença a 0 i **no** arriba al 5 |
| `range(1, 6)` | `1, 2, 3, 4, 5` | Del 1 al 5 |
| `range(0, 10, 2)` | `0, 2, 4, 6, 8` | De 2 en 2 |
| `range(10, 0, -1)` | `10, 9, 8, ..., 1` | Comptant enrere |

El límit superior **no s'inclou**: `range(1, 6)` arriba fins al 5.

```python
for i in range(1, 11):
    print(f"7 x {i} = {7 * i}")
```

Els acumuladors i comptadors funcionen igual:

```python
suma = 0
for i in range(1, 101):
    suma += i
print(suma)      # 5050
```

!!! tip "Quin bucle triar?"
    - Saps **quantes vegades**? Fes servir `for ... in range(...)`.
    - Depèn d'una **condició** (validar, sentinella, jocs)? Fes servir `while`.

### 6. Recórrer un text

Un `for` també pot recórrer un text lletra per lletra:

```python
paraula = "Python"
for lletra in paraula:
    print(lletra)
```

Combinat amb un `if` i un comptador, serveix per comptar o cercar:

```python
frase = input("Escriu una frase: ")
vocals = 0
for lletra in frase:
    if lletra in "aeiou":
        vocals += 1
print(f"Hi ha {vocals} vocals")
```

### 7. Bucles dins de bucles

Un bucle pot contenir un altre bucle. El bucle de dins fa **totes** les seves iteracions per cada iteració del de fora. Així dibuixem files i columnes:

```python
for fila in range(3):
    for columna in range(4):
        print("*", end="")
    print()
```

Mostra:

```text
****
****
****
```

`print("*", end="")` mostra l'asterisc **sense saltar de línia** (per defecte `print` acaba amb un salt de línia; amb `end=""` no). El `print()` buit del bucle de fora salta de línia al final de cada fila.

Per fer un triangle, el truc és que cada fila tingui un nombre diferent d'asteriscs; es pot fer amb la repetició de text de la unitat 2:

```python
for fila in range(1, 5):
    print("*" * fila)
```

## Exemples resolts

Copia'ls a Thonny, executa'ls i **modifica'ls** per veure què canvia.

**Exemple 1. Compte enrere**

```python
n = int(input("Des d'on vols comptar? "))
while n > 0:
    print(n)
    n -= 1
print("Ja!")
```

**Exemple 2. Taula de multiplicar**

```python
nombre = int(input("Quina taula vols? "))
for i in range(1, 11):
    print(f"{nombre} x {i} = {nombre * i}")
```

**Exemple 3. Mitjana amb sentinella**

```python
suma = 0
quantitat = 0
nota = float(input("Nota (-1 per acabar): "))
while nota != -1:
    suma += nota
    quantitat += 1
    nota = float(input("Nota (-1 per acabar): "))

if quantitat > 0:
    print(f"Mitjana: {round(suma / quantitat, 2)}")
else:
    print("No has introduït cap nota")
```

Fixa't que el `if` final evita dividir per zero si l'usuari acaba de seguida.

**Exemple 4. Comptar una lletra**

```python
frase = input("Frase: ")
lletra = input("Quina lletra busques? ")
vegades = 0
for caracter in frase:
    if caracter == lletra:
        vegades += 1
print(f"La lletra {lletra} apareix {vegades} vegades")
```

**Exemple 5. Triangle d'asteriscs**

```python
altura = int(input("Altura: "))
for fila in range(1, altura + 1):
    print("*" * fila)
```

## Errors típics

!!! failure "Bucle infinit (sense missatge d'error)"
    ```python
    n = 5
    while n > 0:
        print(n)
    ```

    - **Resultat:** el programa mostra `5` sense parar.
    - **Què vol dir:** dins del bucle no hi ha res que faci canviar `n`, així que la condició sempre és certa.
    - **Com es corregeix:** afegeix `n -= 1` dins del bucle. Si ja s'ha disparat, prem el botó **Stop**.

!!! failure "Un de més o un de menys amb `range()` (sense missatge d'error)"
    ```python
    for i in range(1, 10):
        print(i)
    ```

    - **Resultat:** mostra del 1 al **9**, no al 10.
    - **Què vol dir:** el límit superior de `range()` no s'inclou.
    - **Com es corregeix:** `range(1, 11)`. Per arribar fins a `n`, escriu `range(1, n + 1)`.

!!! failure "Usar com a `range()` un text d'`input()`"
    ```python
    n = input("Quantes vegades? ")
    for i in range(n):
        print("Hola")
    ```

    - **Missatge (similar a):** `TypeError: 'str' object cannot be interpreted as an integer`
    - **Què vol dir:** `n` és text i `range()` necessita un nombre enter.
    - **Com es corregeix:** `n = int(input("Quantes vegades? "))`.

!!! failure "Oblidar inicialitzar l'acumulador"
    ```python
    for i in range(1, 6):
        suma += i
    print(suma)
    ```

    - **Missatge (similar a):** `NameError: name 'suma' is not defined`
    - **Què vol dir:** `suma += i` necessita que `suma` ja existeixi.
    - **Com es corregeix:** afegeix `suma = 0` **abans** del bucle.

!!! failure "Inicialitzar l'acumulador dins del bucle (sense missatge d'error)"
    ```python
    for i in range(1, 6):
        suma = 0
        suma += i
    print(suma)
    ```

    - **Resultat:** mostra `5` en lloc de `15`.
    - **Què vol dir:** `suma = 0` s'executa a cada iteració i esborra el que s'havia acumulat.
    - **Com es corregeix:** mou `suma = 0` a una línia **abans** del `for`.

## Activitats guiades

### Activitat 1. Taula de traça

Completa en paper la taula de seguiment per saber què mostrarà el programa. Després comprova-ho amb el depurador de Thonny (**Ctrl+F5** i **F6**).

```python
n = 1
suma = 0
while n <= 4:
    suma = suma + n
    n = n + 1
print(suma)
```

| Iteració | `n` (en començar) | `suma` (en acabar) |
| --- | --- | --- |
| 1 | 1 | ? |
| 2 | ? | ? |
| 3 | ? | ? |
| 4 | ? | ? |

??? success "Solució"
    | Iteració | `n` (en començar) | `suma` (en acabar) |
    | --- | --- | --- |
    | 1 | 1 | 1 |
    | 2 | 2 | 3 |
    | 3 | 3 | 6 |
    | 4 | 4 | 10 |

    Després de la quarta iteració, `n` val 5, la condició `n <= 4` és falsa i el bucle acaba. El programa mostra `10`.

### Activitat 2. Prediu els valors de `range()`

Escriu els valors que prendrà `i` en cada cas.

- a) `for i in range(4):`
- b) `for i in range(1, 4):`
- c) `for i in range(0, 10, 3):`
- d) `for i in range(5, 0, -2):`

??? success "Solució"
    - a) `0, 1, 2, 3`
    - b) `1, 2, 3`
    - c) `0, 3, 6, 9`
    - d) `5, 3, 1`

### Activitat 3. Corregeix el codi

Aquest programa hauria de sumar els nombres de l'1 fins a un nombre `n`. Té tres errors. Corregeix-los **un per un**.

```python
n = input("Fins a quin nombre? ")
for i in range(1, n):
    suma = 0
    suma += i
print("La suma és", suma)
```

??? success "Solució"
    ```python
    n = int(input("Fins a quin nombre? "))
    suma = 0
    for i in range(1, n + 1):
        suma += i
    print("La suma és", suma)
    ```

    Errors: (1) `n` no s'ha convertit a `int`, i això dona un `TypeError`; (2) `range(1, n)` no inclou `n`, ha de ser `range(1, n + 1)`; (3) `suma = 0` s'ha de posar **abans** del bucle.

### Activitat 4. Completa el codi

Completa el programa que mostra la taula de multiplicar d'un nombre.

```python
nombre = int(input("Quina taula vols? "))
for i in range(___, ___):
    print(f"{nombre} x {i} = {___}")
```

??? success "Solució"
    ```python
    nombre = int(input("Quina taula vols? "))
    for i in range(1, 11):
        print(f"{nombre} x {i} = {nombre * i}")
    ```

### Activitat 5. Escriu-ho tu

Escriu un programa que demani una nota entre 0 i 10 i **repeteixi la pregunta** mentre l'usuari escrigui un valor fora d'aquest interval. Quan la nota sigui vàlida, mostra-la.

??? success "Solució"
    ```python
    nota = float(input("Nota (0-10): "))
    while nota < 0 or nota > 10:
        print("Nota no vàlida")
        nota = float(input("Nota (0-10): "))
    print(f"Nota registrada: {nota}")
    ```

## Lliurament (Classroom)

!!! example "Què has de lliurar"
    **Fitxer:** `u4_cognom_nom.py`

    Fes **un sol programa** amb quatre parts, cadascuna amb el seu títol per pantalla.

    **Part 1. Taula de multiplicar**

    Demana un nombre enter i mostra la seva taula de multiplicar de l'1 al 10.

    **Part 2. Suma i mitjana**

    1. Demana nombres enters positius fins que l'usuari escrigui `0`.
    2. Mostra **quants** nombres ha escrit, la **suma** i la **mitjana** (arrodonida a 2 decimals).
    3. Si no n'ha escrit cap, mostra un missatge en lloc de calcular la mitjana, per no dividir per zero.

    **Part 3. Comptar lletres**

    1. Demana una frase i una lletra.
    2. Mostra quantes vegades apareix aquesta lletra a la frase.

    **Part 4. Triangle d'asteriscs**

    Demana l'altura `n` i dibuixa un triangle de `n` files. Per exemple, amb `n = 4`:

    ```text
    *
    **
    ***
    ****
    ```

    **Abans de lliurar, comprova que:**

    1. El fitxer té la capçalera amb el teu nom, la data i la unitat.
    2. Has fet servir `for` on saps quantes repeticions fan falta i `while` on depèn d'una condició.
    3. Has provat cada part amb casos límit (a la part 2, escriure `0` de seguida; a la part 4, `n = 1`).
    4. Al final de cada part hi ha un comentari amb 3 casos de prova que has comprovat.
    5. El programa s'executa sense errors i no es queda penjat en cap bucle.

## Repte opcional

**Nombres primers.** Demana un nombre enter major que 1 i digues si és **primer** (només és divisible per 1 i per ell mateix). Després, mostra tots els primers entre 1 i 100.

*Pista:* recorre els possibles divisors des de 2 fins a `n - 1` i comprova amb `%` si algun divideix `n`. Pots fer servir una variable booleana `es_primer = True` que passi a `False` si en trobes un.

## Xuleta

| Vull... | Escric... |
| --- | --- |
| Repetir mentre es compleixi una condició | `while condició:` |
| Repetir un nombre de vegades | `for i in range(n):` |
| Recórrer de l'1 al `n` | `for i in range(1, n + 1):` |
| Comptar enrere | `for i in range(n, 0, -1):` |
| Comptador | `comptador += 1` |
| Acumulador | `suma += valor` (amb `suma = 0` abans) |
| Sortir d'un bucle | `break` |
| Recórrer un text | `for lletra in text:` |
| Escriure sense saltar de línia | `print("*", end="")` |
| Aturar un programa penjat | Botó **Stop** de Thonny |
