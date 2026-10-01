# Unitat 3. Condicionals

!!! abstract "Resum"
    **Sessions:** 3 · **Lliurament a Classroom:** `u3_cognom_nom.py`

    - **Sessió 1:** apartats 1 a 3 (`if`, `else` i indentació).
    - **Sessió 2:** apartats 4 a 6 (`elif`, condicions compostes i depuració).
    - **Sessió 3:** apartat 7 (`random`), activitats pendents i lliurament.

## Objectius

En acabar aquesta unitat sabràs:

- Fer que un programa prengui decisions amb `if`, `elif` i `else`.
- Escriure blocs de codi amb la indentació correcta.
- Construir condicions compostes amb `and`, `or`, `not` i `in`.
- Trobar errors fent seguiment del programa amb `print()` i amb el depurador de Thonny.
- Generar nombres aleatoris amb `random.randint()`.

## Punt de partida

!!! question "Ho recordes?"
    Als diagrames de flux i al pseudocodi, una decisió és un rombe amb dues sortides: **sí** o **no**. En pseudocodi s'escriu així:

    ```text
    Si nota >= 5 llavors
        Escriu "Aprovat"
    Sinó
        Escriu "Suspès"
    Fi si
    ```

    I en Python:

    ```python
    if nota >= 5:
        print("Aprovat")
    else:
        print("Suspès")
    ```

    Canvien els dos punts (`:`) i que **la indentació** (els espais al davant) fa de «llavors» i «fi si».

## Teoria

### 1. La decisió: `if`

```python
edat = int(input("Quina edat tens? "))
if edat >= 18:
    print("Ets major d'edat")
```

- Després de `if` va una **condició**: una expressió que dona `True` o `False` (com les de la unitat 2).
- La línia acaba amb **dos punts** `:`.
- El que ha de passar si la condició és certa va **indentat** (4 espais). A Thonny, prem **Tab**.
- Si la condició és falsa, Python s'ho salta.

### 2. L'alternativa: `else`

`else` (en cas contrari) s'executa quan la condició del `if` **no** es compleix:

```python
if edat >= 18:
    print("Ets major d'edat")
else:
    print("Ets menor d'edat")
```

!!! tip "Per recordar"
    S'executa **un i només un** dels dos blocs: o el del `if` o el de l'`else`. `else` no porta condició.

### 3. La indentació és el codi

En Python, els espais al davant d'una línia indiquen **a quin bloc pertany**. Compara:

```python
nota = 4
if nota >= 5:
    print("Aprovat")
print("Això es mostra sempre")
```

La darrera línia **no** està indentada, per tant no pertany al `if`: es mostra sempre, tant si la condició és certa com si no.

- Fes servir **4 espais** per nivell (o la tecla Tab).
- Tot el bloc ha de tenir la **mateixa** indentació.
- No barregis espais i tabuladors.

### 4. Més d'una opció: `elif`

Quan hi ha més de dues possibilitats, enganxem condicions amb `elif` (de *else if*):

```python
nota = float(input("Nota: "))

if nota < 5:
    print("Suspès")
elif nota < 7:
    print("Aprovat")
elif nota < 9:
    print("Notable")
else:
    print("Excel·lent")
```

Python comprova les condicions **de dalt a baix** i executa **només el primer bloc** que es compleix; la resta es salten.

!!! tip "Per recordar"
    **L'ordre de les condicions importa.** A l'exemple, un 8 no és menor que 5 ni menor que 7, així que passa de llarg els dos primers blocs i s'atura al tercer (`nota < 9`). Cada `elif` només cal que comprovi el límit superior perquè els casos anteriors ja s'han descartat.

### 5. Condicions compostes

A la condició hi podem fer servir els operadors lògics de la unitat 2:

```python
edat = 15
if edat >= 12 and edat <= 16:
    print("Estàs en edat d'ESO")

dia = "dissabte"
if dia == "dissabte" or dia == "diumenge":
    print("És cap de setmana")
```

També l'operador `in` per comprovar si un text és dins d'un altre:

```python
lletra = "e"
if lletra in "aeiou":
    print("És una vocal")
```

I el residu `%` per saber si un nombre és parell:

```python
n = 8
if n % 2 == 0:
    print("Parell")
else:
    print("Senar")
```

**Decisions dins de decisions.** Un `if` pot anar dins d'un altre (indentat un nivell més):

```python
if edat >= 18:
    if te_carnet:
        print("Pots conduir")
    else:
        print("Et falta el carnet")
else:
    print("Ets massa jove")
```

### 6. Depuració: com trobar què falla

Quan un programa no fa el que esperes, **no endevinis**: mira què passa.

**Tècnica 1: `print` de seguiment.** Afegeix línies temporals que mostrin els valors i per quin camí passa el programa:

```python
nota = float(input("Nota: "))
print("DEBUG: nota =", nota)
if nota >= 5:
    print("DEBUG: he entrat al bloc del if")
    print("Aprovat")
```

Quan ho arreglis, **esborra o comenta** els `print` de depuració.

**Tècnica 2: el depurador de Thonny.** Prem el botó de l'insecte (o **Ctrl+F5**) i el programa s'executarà **línia a línia**: avança amb **F6**. A cada pas veuràs al panell de Variables què val cada cosa i quina línia s'executarà a continuació. És com fer la «traça» en paper, però automàtica.

!!! tip "Per recordar"
    Quan no entenguis per què el programa fa una cosa, fes-li la traça: **línia a línia, mirant el valor de les variables**.

### 7. Nombres aleatoris: `random`

Per fer jocs necessitem que l'ordinador triï nombres a l'atzar. Python porta una «caixa d'eines» anomenada `random` que hem d'importar a l'inici del programa:

```python
import random

dau = random.randint(1, 6)
print(f"Ha sortit un {dau}")
```

`random.randint(a, b)` dona un enter aleatori entre `a` i `b`, **tots dos inclosos**. Cada vegada que executis el programa, el resultat pot ser diferent.

!!! warning "No anomenis el teu fitxer `random.py`"
    Si el teu fitxer es diu igual que el mòdul que importes, Python s'embolica i dona errors estranys. Fes servir els noms de fitxer del curs (`u3_cognom_nom.py`).

## Exemples resolts

Copia'ls a Thonny, executa'ls i **modifica'ls** per veure què canvia.

**Exemple 1. Aprovat o suspès**

```python
nota = float(input("Quina nota has tret? "))
if nota >= 5:
    print("Aprovat")
else:
    print("Suspès")
```

**Exemple 2. Parell o senar**

```python
n = int(input("Escriu un nombre enter: "))
if n % 2 == 0:
    print(f"El {n} és parell")
else:
    print(f"El {n} és senar")
```

**Exemple 3. Preu del bitllet**

```python
edat = int(input("Edat: "))

if edat < 4:
    preu = 0
elif edat < 18:
    preu = 5
else:
    preu = 10

print(f"El teu bitllet costa {preu} €")
```

**Exemple 4. Tirar un dau**

```python
import random

dau = random.randint(1, 6)
print(f"Ha sortit un {dau}")

if dau == 6:
    print("Torna a tirar!")
else:
    print("Passa el torn")
```

## Errors típics

!!! failure "Oblidar els dos punts"
    ```python
    if edat >= 18
        print("Major d'edat")
    ```

    - **Missatge (similar a):** `SyntaxError: expected ':'`
    - **Què vol dir:** la línia del `if` (o `elif`, o `else`) ha d'acabar amb `:`.
    - **Com es corregeix:** `if edat >= 18:`.

!!! failure "Oblidar la indentació"
    ```python
    if edat >= 18:
    print("Major d'edat")
    ```

    - **Missatge (similar a):** `IndentationError: expected an indented block after 'if' statement on line 1`
    - **Què vol dir:** després dels dos punts, Python espera un bloc indentat i no l'ha trobat.
    - **Com es corregeix:** indenta el `print` amb 4 espais (tecla **Tab**).

!!! failure "Usar `=` en lloc de `==`"
    ```python
    if edat = 18:
        print("Tens 18 anys")
    ```

    - **Missatge (similar a):** `SyntaxError: invalid syntax. Maybe you meant '==' or ':=' instead of '='?`
    - **Què vol dir:** a la condició has escrit una assignació en lloc d'una comparació.
    - **Com es corregeix:** `if edat == 18:`.

!!! failure "Variable creada dins d'un `if` que no s'executa"
    ```python
    nota = 3
    if nota >= 5:
        resultat = "Aprovat"
    print(resultat)
    ```

    - **Missatge (similar a):** `NameError: name 'resultat' is not defined`
    - **Què vol dir:** com que la condició és falsa, la variable `resultat` no s'ha arribat a crear.
    - **Com es corregeix:** afegeix un `else` que també la creï, o dona-li un valor inicial abans del `if`.

!!! failure "Condicions en mal ordre (sense missatge d'error)"
    ```python
    if nota >= 5:
        print("Aprovat")
    elif nota >= 9:
        print("Excel·lent")
    ```

    - **Resultat:** mai mostra «Excel·lent». Un 9 ja compleix `nota >= 5`, i Python no segueix amb els `elif`.
    - **Com es corregeix:** posa primer la condició més restrictiva (`nota >= 9`) i després les altres.

## Activitats guiades

### Activitat 1. Prediu la sortida

Fes la traça en paper (anota què val `x` i quines línies s'executen) abans de provar-ho a Thonny. Fixa't en la diferència entre els dos programes.

**Programa A**

```python
x = 10
if x > 5:
    print("A")
if x > 8:
    print("B")
else:
    print("C")
print("D")
```

**Programa B**

```python
x = 10
if x > 5:
    print("A")
elif x > 8:
    print("B")
else:
    print("C")
print("D")
```

??? success "Solució"
    - **Programa A:** mostra `A`, `B` i `D`. Són dos `if` independents: tots dos es comproven.
    - **Programa B:** mostra `A` i `D`. Amb `elif`, quan el primer bloc ja s'ha executat, els altres es salten.

### Activitat 2. Corregeix el codi

Aquest programa té quatre errors. Corregeix-los **un per un**: Python només te'n mostra un cada vegada.

```python
edat = input("Quina edat tens? ")
if edat >= 18
print("Pots votar")
else
    print("Encara no pots votar")
```

??? success "Solució"
    ```python
    edat = int(input("Quina edat tens? "))
    if edat >= 18:
        print("Pots votar")
    else:
        print("Encara no pots votar")
    ```

    Errors: (1) `edat` no s'ha convertit a `int`; (2) falten els dos punts del `if`; (3) el primer `print` no està indentat; (4) falten els dos punts de l'`else`.

### Activitat 3. Completa el codi

Substitueix cada `___` perquè el programa classifiqui una nota.

```python
nota = float(input("Nota: "))
if nota ___ 5:
    print("Suspès")
___ nota < 7:
    print("Aprovat")
___ nota < 9:
    print("Notable")
___:
    print("Excel·lent")
```

??? success "Solució"
    ```python
    nota = float(input("Nota: "))
    if nota < 5:
        print("Suspès")
    elif nota < 7:
        print("Aprovat")
    elif nota < 9:
        print("Notable")
    else:
        print("Excel·lent")
    ```

### Activitat 4. Escriu-ho tu

Escriu un programa que demani un nombre enter i mostri si és **positiu**, **negatiu** o **zero**.

??? success "Solució"
    ```python
    n = int(input("Escriu un nombre enter: "))
    if n > 0:
        print("Positiu")
    elif n < 0:
        print("Negatiu")
    else:
        print("Zero")
    ```

## Lliurament (Classroom)

!!! example "Què has de lliurar"
    **Fitxer:** `u3_cognom_nom.py`

    Fes **un sol programa** amb tres parts, cadascuna amb el seu títol per pantalla.

    **Part 1. El cinema**

    Demana l'edat i mostra el preu de l'entrada:

    - Menors de 12 anys: 5 €
    - De 12 a 17 anys: 7 €
    - De 18 a 64 anys: 9 €
    - 65 anys o més: 6 €

    **Part 2. Classificació de triangles**

    Demana els tres costats d'un triangle (nombres enters) i mostra:

    1. `No és un triangle` si algun costat és zero o negatiu, o si un costat és major o igual que la suma dels altres dos.
    2. Si no, `Equilàter` (tres costats iguals), `Isòsceles` (dos iguals) o `Escalè` (tots diferents).

    **Part 3. Endevina el nombre**

    1. L'ordinador tria un nombre secret entre 1 i 10 amb `random.randint()`.
    2. Demana a l'usuari que n'endevini un.
    3. Mostra `Encertat!`, `Massa baix` o `Massa alt`.
    4. Si no ha encertat, mostra també quin era el nombre secret.

    **Abans de lliurar, comprova que:**

    1. El fitxer té la capçalera amb el teu nom, la data i la unitat.
    2. Has provat cada part amb **valors límit** (per exemple, a la part 1: 11, 12, 17, 18, 64 i 65).
    3. Al final de cada part hi ha un comentari amb **3 casos de prova** que has comprovat.
    4. Els `print` de depuració s'han esborrat o comentat.
    5. El programa s'executa sense errors.

## Repte opcional

**Any de traspàs.** Demana un any i digues si és de traspàs. Un any és de traspàs si és **divisible per 4 però no per 100**, o bé si és **divisible per 400**. Comprova que 2024 i 2000 ho són, i que 1900 i 2026 no.

*Pista:* un nombre és divisible per 4 quan `any % 4 == 0`. Hauràs de combinar `and` i `or`, i potser fer servir parèntesis.

## Xuleta

| Vull... | Escric... |
| --- | --- |
| Fer una cosa només si es compleix | `if condició:` |
| Una alternativa | `else:` |
| Diverses opcions | `elif condició:` |
| Combinar condicions | `and`, `or`, `not` |
| Saber si és parell | `if n % 2 == 0:` |
| Una lletra és dins d'un text | `if lletra in "aeiou":` |
| Nombre aleatori de l'1 al 10 | `import random` + `random.randint(1, 10)` |
| Depurar pas a pas | Botó insecte / **Ctrl+F5** i **F6** |
