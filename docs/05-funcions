# Unitat 5. Funcions

!!! abstract "Resum"
    **Sessions:** 2 · **Lliurament a Classroom:** `u5_cognom_nom.py`

    - **Sessió 1:** apartats 1 a 3 (què és una funció, definir-la i cridar-la, paràmetres).
    - **Sessió 2:** apartats 4 a 6 (`return`, àmbit de les variables i estructura d'un programa), activitats i lliurament.

## Objectius

En acabar aquesta unitat sabràs:

- Explicar per què fem servir funcions: no repetir codi i dividir un problema en parts.
- Definir funcions amb `def` i cridar-les.
- Passar dades a una funció amb paràmetres.
- Retornar un resultat amb `return` i distingir-ho de `print()`.
- Entendre que les variables d'una funció són **locals**.
- Organitzar un programa amb les funcions a dalt i el programa principal a sota.

## Punt de partida

!!! question "Ho recordes?"
    Quan un algorisme és gran, el dividim en parts més petites (subalgorismes) amb un nom, i les reutilitzem. Això són les **funcions**.

    ```text
    Funció area(base, altura)
        Retorna base * altura
    Fi funció
    ```

    I en Python:

    ```python
    def area(base, altura):
        return base * altura
    ```

    De fet, **ja has fet servir moltes funcions**: `print()`, `input()`, `int()`, `len()`, `range()`, `round()`, `random.randint()`. Ara aprendràs a crear-ne de pròpies.

## Teoria

### 1. Per què les funcions?

Una **funció** és un bloc de codi amb un nom que podem **reutilitzar** tantes vegades com vulguem. Serveixen per:

- **No repetir codi:** s'escriu una vegada i es crida les vegades que calgui.
- **Dividir un problema en parts** més petites i fàcils de provar.
- **Llegir millor el programa:** `area_rectangle(3, 4)` s'entén més bé que una fórmula.

### 2. Definir i cridar una funció

Es defineix amb `def`, el nom de la funció, parèntesis i dos punts. El cos va **indentat**:

```python
def salutacio():
    print("Hola!")
    print("Benvingut al curs de Python")

salutacio()
salutacio()
```

Aquest programa mostra el missatge **dues vegades**.

- **Definir** una funció (`def`) només l'explica a Python; **no l'executa**.
- **Cridar-la** (`salutacio()`) és el que fa que s'executi.
- La funció s'ha de **definir abans** de ser cridada.

### 3. Paràmetres i arguments

Una funció pot rebre dades per treballar-hi:

```python
def saluda(nom):
    print(f"Hola, {nom}!")

saluda("Anna")
saluda("Pere")
```

- `nom` és el **paràmetre**: una variable que només existeix dins de la funció i que fa de «forat» per rebre un valor.
- `"Anna"` és l'**argument**: el valor concret que passem quan cridem la funció.

Pots tenir **diversos paràmetres**, separats per comes. S'assignen **per ordre**:

```python
def presenta(nom, edat):
    print(f"{nom} té {edat} anys")

presenta("Anna", 15)
```

### 4. Retornar un valor: `return`

Molts cops volem que la funció ens **doni un resultat** per poder-lo fer servir després. Això ho fa `return`:

```python
def area_rectangle(base, altura):
    return base * altura

a = area_rectangle(3, 4)
print(a)               # 12
print(area_rectangle(5, 2) + 1)    # 11
```

!!! danger "No confonguis `print()` amb `return`"
    | | `print()` | `return` |
    | --- | --- | --- |
    | Què fa | **Mostra** un valor per pantalla | **Entrega** un valor a qui ha cridat la funció |
    | Es pot guardar en una variable? | No | Sí |
    | Es pot fer servir en un càlcul? | No | Sí |

    Quan una funció arriba a un `return`, **acaba immediatament**.

Una funció pot retornar qualsevol tipus de valor, per exemple un booleà:

```python
def es_parell(n):
    return n % 2 == 0

print(es_parell(8))     # True
```

I pot tenir decisions i diversos `return`:

```python
def maxim(a, b):
    if a > b:
        return a
    return b
```

Si una funció **no té `return`**, retorna un valor especial anomenat `None` («res»).

### 5. Àmbit de les variables

Les variables creades **dins** d'una funció (i els seus paràmetres) són **locals**: només existeixen mentre la funció s'executa, i no es poden fer servir fora.

```python
def calcula():
    resultat = 10
    print(resultat)

calcula()
print(resultat)       # Error!
```

L'última línia dona error: fora de la funció, `resultat` no existeix. Les variables de la funció i les del programa principal són «caixes separades», encara que tinguin el mateix nom.

!!! tip "Per recordar"
    Una funció es comunica amb la resta del programa per dues portes: les **dades entren** pels paràmetres i el **resultat surt** amb `return`.

### 6. Estructura d'un programa

A partir d'ara els nostres programes tindran dues parts: **primer les funcions** i **després el programa principal**, que les fa servir.

```python
# --- Funcions ---
def area_cercle(radi):
    return 3.14159 * radi ** 2

# --- Programa principal ---
r = float(input("Radi: "))
print(f"Àrea: {round(area_cercle(r), 2)}")
```

Una funció pot cridar-ne unes altres, com a l'exemple 4 de més avall.

!!! tip "Depurar funcions"
    Amb el depurador de Thonny (**Ctrl+F5**), la tecla **F7** *entra* dins de la funció i **F6** avança sense entrar-hi. Així pots veure com s'omplen els paràmetres i què retorna.

## Exemples resolts

Copia'ls a Thonny, executa'ls i **modifica'ls** per veure què canvia.

**Exemple 1. Una funció que retorna el doble**

```python
def doble(n):
    return n * 2

print(doble(4))
print(doble(doble(4)))
```

**Exemple 2. Preu amb IVA**

```python
def preu_amb_iva(preu):
    return round(preu * 1.21, 2)

preu = float(input("Preu sense IVA: "))
print(f"Preu amb IVA: {preu_amb_iva(preu)} €")
```

**Exemple 3. Un validador reutilitzable**

```python
def demana_positiu(missatge):
    n = int(input(missatge))
    while n <= 0:
        print("Ha de ser un nombre positiu")
        n = int(input(missatge))
    return n

edat = demana_positiu("Edat: ")
germans = demana_positiu("Quants germans tens? ")
print(edat, germans)
```

La mateixa funció serveix per validar dues dades diferents.

**Exemple 4. Funcions que en criden d'altres**

```python
def es_vocal(lletra):
    return lletra in "aeiou"

def compta_vocals(text):
    total = 0
    for lletra in text:
        if es_vocal(lletra):
            total += 1
    return total

print(compta_vocals("ordinador"))    # 4
```

## Errors típics

!!! failure "Cridar una funció abans de definir-la"
    ```python
    saluda("Anna")

    def saluda(nom):
        print(f"Hola, {nom}!")
    ```

    - **Missatge (similar a):** `NameError: name 'saluda' is not defined`
    - **Què vol dir:** Python llegeix de dalt a baix i, quan arriba a la crida, encara no coneix la funció.
    - **Com es corregeix:** posa la definició **abans** de la crida.

!!! failure "Oblidar els parèntesis en cridar-la (sense missatge d'error)"
    ```python
    def salutacio():
        print("Hola!")

    salutacio
    ```

    - **Resultat:** no es mostra res.
    - **Què vol dir:** sense parèntesis nomenes la funció, però no l'executes.
    - **Com es corregeix:** `salutacio()`.

!!! failure "Nombre d'arguments incorrecte"
    ```python
    def area_rectangle(base, altura):
        return base * altura

    print(area_rectangle(4))
    ```

    - **Missatge (similar a):** `TypeError: area_rectangle() missing 1 required positional argument: 'altura'`
    - **Què vol dir:** la funció espera dos valors i només n'has donat un.
    - **Com es corregeix:** `area_rectangle(4, 3)`.

!!! failure "Oblidar el `return` (apareix `None`)"
    ```python
    def doble(n):
        print(n * 2)

    resultat = doble(5)
    print(resultat + 1)
    ```

    - **Missatge (similar a):** `TypeError: unsupported operand type(s) for +: 'NoneType' and 'int'`
    - **Què vol dir:** la funció mostra el doble però **no el retorna**, així que `resultat` val `None`.
    - **Com es corregeix:** canvia `print(n * 2)` per `return n * 2`.

!!! failure "Fer servir fora una variable local"
    ```python
    def calcula():
        total = 10

    calcula()
    print(total)
    ```

    - **Missatge (similar a):** `NameError: name 'total' is not defined`
    - **Què vol dir:** `total` només existeix dins de la funció.
    - **Com es corregeix:** fes que la funció la retorni (`return total`) i guarda el resultat: `total = calcula()`.

## Activitats guiades

### Activitat 1. Prediu la sortida

```python
def doble(n):
    return n * 2

x = doble(3)
print(x)
print(doble(x))
```

??? success "Solució"
    Mostra `6` i després `12`: `doble(3)` retorna 6, que es guarda a `x`; i `doble(x)` és `doble(6)`.

### Activitat 2. Prediu: variables locals i globals

Fixa't en quines variables són de la funció i quines del programa principal.

```python
def f():
    a = 10
    print(a)

a = 5
f()
print(a)
```

??? success "Solució"
    Mostra `10` i després `5`. La `a` de dins de `f` és una variable local, diferent de la `a` del programa principal. Modificar la local no canvia l'altra.

### Activitat 3. Corregeix el codi

Aquest programa hauria de calcular l'àrea d'un triangle. Té tres errors. Corregeix-los **un per un**.

```python
def area_triangle(base, altura)
    area = base * altura / 2
    print(area)

resultat = area_triangle(4)
print("L'àrea és", resultat)
```

??? success "Solució"
    ```python
    def area_triangle(base, altura):
        area = base * altura / 2
        return area

    resultat = area_triangle(4, 3)
    print("L'àrea és", resultat)
    ```

    Errors: (1) falten els dos punts a la definició; (2) la funció fa `print` en lloc de `return`, i `resultat` valdria `None`; (3) la crida només passa un argument, i en calen dos.

### Activitat 4. Completa el codi

Completa la funció perquè retorni `True` si el nombre és parell.

```python
def es_parell(n):
    return ___ % 2 == ___

if es_parell(8):
    print("Parell")
else:
    print("Senar")
```

??? success "Solució"
    ```python
    def es_parell(n):
        return n % 2 == 0
    ```

### Activitat 5. Escriu-ho tu

Escriu una funció `celsius_a_fahrenheit(c)` que retorni la temperatura en graus Fahrenheit (`c * 9 / 5 + 32`). Comprova que `celsius_a_fahrenheit(100)` dona `212.0`.

??? success "Solució"
    ```python
    def celsius_a_fahrenheit(c):
        return c * 9 / 5 + 32

    print(celsius_a_fahrenheit(100))    # 212.0
    ```

## Lliurament (Classroom)

!!! example "Què has de lliurar"
    **Fitxer:** `u5_cognom_nom.py`

    Fes un programa amb **cinc funcions** i un programa principal que les faci servir.

    **Funcions que has de definir**

    1. `area_rectangle(base, altura)`: retorna l'àrea.
    2. `es_parell(n)`: retorna `True` o `False`.
    3. `maxim(a, b, c)`: retorna el més gran dels tres nombres.
    4. `celsius_a_fahrenheit(c)`: retorna la temperatura en Fahrenheit.
    5. `demana_enter(missatge, minim, maxim)`: demana un enter amb `input()` i **repeteix la pregunta** fins que estigui entre `minim` i `maxim` (inclosos); aleshores el retorna.

    **Programa principal**

    Fes servir `demana_enter` per demanar totes les dades i mostra els resultats:

    1. Demana una base i una altura (entre 1 i 100) i mostra l'àrea.
    2. Demana un nombre (entre 1 i 1000) i digues si és parell o senar.
    3. Demana tres nombres (entre 1 i 100) i mostra el màxim.
    4. Demana una temperatura en graus Celsius (entre -50 i 60) i mostra-la en Fahrenheit.

    **Condicions**

    - Les funcions de càlcul (1 a 4) **no han de mostrar res per pantalla**: han de retornar el resultat.
    - Cada funció té a sobre un comentari que explica què fa.
    - Primer van totes les funcions i després el programa principal.

    **Abans de lliurar, comprova que:**

    1. El fitxer té la capçalera amb el teu nom, la data i la unitat.
    2. Has provat cada funció amb almenys 3 valors, inclosos els límits.
    3. `demana_enter` repeteix la pregunta si l'usuari escriu un valor fora de l'interval.
    4. El programa s'executa sense errors.

## Repte opcional

**Nombres primers, versió funció.** Converteix el repte de la unitat 4 en una funció `es_primer(n)` que retorni `True` o `False`, i fes-la servir per mostrar tots els nombres primers de l'1 al 100.

*Pista:* a la funció, `return False` en trobar un divisor, i `return True` només al final del bucle. Recorda que 1 no és primer.

## Xuleta

| Vull... | Escric... |
| --- | --- |
| Definir una funció | `def nom(param1, param2):` |
| Que retorni un resultat | `return valor` |
| Cridar-la i guardar el resultat | `x = nom(arg1, arg2)` |
| Cridar-la sense paràmetres | `nom()` |
| Una funció només mostra | `print(...)` dins de la funció |
| Funció que respon sí/no | `return condició` (dona `True` o `False`) |
| Variables d'una funció | Són locals: només existeixen dins |
