# Unitat 2. Operadors i text bàsic

!!! abstract "Resum"
    **Sessions:** 2 · **Lliurament a Classroom:** `u2_cognom_nom.py`

    - **Sessió 1:** apartats 1 a 4 (operadors aritmètics, precedència, arrodoniment i comparacions).
    - **Sessió 2:** apartats 5 i 6 (operadors lògics i text bàsic), activitats i lliurament.

## Objectius

En acabar aquesta unitat sabràs:

- Fer càlculs amb els operadors aritmètics, inclosos `//` i `%`.
- Predir el resultat d'una expressió tenint en compte la precedència.
- Comparar valors i entendre que el resultat és un booleà (`True` o `False`).
- Combinar condicions amb `and`, `or` i `not`.
- Fer operacions bàsiques amb text: unir, repetir, mesurar (`len()`) i accedir a una lletra.

## Punt de partida

!!! question "Ho recordes?"
    Als algorismes ja feu càlculs, compareu valors i combineu condicions. Fins i tot heu fet servir la divisió entera i el residu (`div` i `mod`). En Python s'escriuen així:

    | Pseudocodi | Python |
    | --- | --- |
    | `a div b` | `a // b` |
    | `a mod b` | `a % b` |
    | `a = b` (comparar) | `a == b` |
    | `a ≠ b` | `a != b` |
    | `a i b` | `a and b` |
    | `a o b` | `a or b` |
    | `no a` | `not a` |

## Teoria

### 1. Operadors aritmètics

| Operador | Operació | Exemple | Resultat |
| --- | --- | --- | --- |
| `+` | Suma | `7 + 2` | `9` |
| `-` | Resta | `7 - 2` | `5` |
| `*` | Multiplicació | `7 * 2` | `14` |
| `/` | Divisió | `7 / 2` | `3.5` |
| `//` | Divisió entera | `7 // 2` | `3` |
| `%` | Residu (mòdul) | `7 % 2` | `1` |
| `**` | Potència | `2 ** 3` | `8` |

- `/` **sempre** dona un `float`, encara que el resultat sigui exacte: `6 / 2` és `3.0`.
- `//` i `%` funcionen en parella: `17 // 5` és `3` (hi cap 3 vegades) i `17 % 5` és `2` (en sobren 2).

!!! tip "Per recordar"
    `%` serveix per saber si un nombre és parell (`n % 2 == 0`) i `//` i `%` juntes serveixen per convertir unitats (minuts en hores i minuts).

### 2. Precedència d'operadors

Com a les matemàtiques, no tot es calcula d'esquerra a dreta. L'ordre és:

1. Parèntesis `( )`
2. Potència `**`
3. `*`, `/`, `//`, `%` (d'esquerra a dreta)
4. `+`, `-` (d'esquerra a dreta)

```python
print(2 + 3 * 4)      # 14
print((2 + 3) * 4)    # 20
```

!!! tip "Per recordar"
    Quan dubtis, **posa parèntesis**. No costa res i el codi es llegeix millor.

### 3. Assignació abreviada i arrodoniment

Sovint volem modificar una variable a partir del seu valor actual. Hi ha una forma abreviada:

```python
punts = 10
punts += 5      # És igual que punts = punts + 5
```

També existeixen `-=`, `*=`, `/=`... La farem servir molt quan arribem als bucles.

Per arrodonir hi ha la funció `round(nombre, decimals)`:

```python
print(round(3.14159, 2))    # 3.14
```

!!! info "Per què surten tants decimals?"
    Els ordinadors guarden els decimals amb una precisió limitada. Per això `print(0.1 + 0.2)` mostra `0.30000000000000004`. No és un error teu: és una limitació de tots els llenguatges. Arrodoneix el resultat amb `round()` quan el mostris.

### 4. Operadors de comparació

Comparen dos valors i sempre donen un **booleà** (`True` o `False`):

| Operador | Significa | Exemple | Resultat |
| --- | --- | --- | --- |
| `==` | És igual a | `5 == 5` | `True` |
| `!=` | És diferent de | `5 != 3` | `True` |
| `<` | Menor que | `3 < 2` | `False` |
| `>` | Major que | `3 > 2` | `True` |
| `<=` | Menor o igual | `3 <= 3` | `True` |
| `>=` | Major o igual | `2 >= 3` | `False` |

!!! danger "Atenció: `=` no és `==`"
    - `=` **guarda** un valor en una variable (assignació).
    - `==` **compara** dos valors (pregunta si són iguals).

També es poden comparar textos, però Python distingeix majúscules i minúscules i no compara tipus diferents: `"Anna" == "anna"` és `False`, i `"5" == 5` també és `False`.

### 5. Operadors lògics

Combinen condicions (booleans):

- `and`: cert només si **les dues** condicions són certes.
- `or`: cert si **almenys una** és certa.
- `not`: inverteix el resultat.

| `a` | `b` | `a and b` | `a or b` |
| --- | --- | --- | --- |
| `True` | `True` | `True` | `True` |
| `True` | `False` | `False` | `True` |
| `False` | `True` | `False` | `True` |
| `False` | `False` | `False` | `False` |

```python
edat = 15
print(edat >= 12 and edat <= 16)     # True
print(edat < 12 or edat > 16)        # False
print(not edat == 15)                # False
```

!!! tip "Per recordar"
    Cada part d'un `and` o d'un `or` ha de ser una comparació completa. `edat >= 12 and <= 16` **no** funciona; s'ha d'escriure `edat >= 12 and edat <= 16`. Python també permet la forma curta `12 <= edat <= 16`.

### 6. Text bàsic

**Unir i repetir.** `+` uneix textos (concatenació) i `*` els repeteix:

```python
print("Hola" + " " + "món")    # Hola món
print("ab" * 3)                # ababab
```

**Longitud.** `len()` diu quants caràcters té un text (els espais també compten):

```python
print(len("Python"))    # 6
```

**Indexació.** Cada caràcter té una posició, que **comença a 0**. Amb claudàtors `[ ]` pots agafar-ne un:

| Lletra | P | y | t | h | o | n |
| --- | --- | --- | --- | --- | --- | --- |
| Índex | 0 | 1 | 2 | 3 | 4 | 5 |
| Índex negatiu | -6 | -5 | -4 | -3 | -2 | -1 |

```python
text = "Python"
print(text[0])     # P  (la primera)
print(text[-1])    # n  (l'última)
```

**Pertinença.** L'operador `in` diu si un text és dins d'un altre i dona un booleà: `"y" in "Python"` és `True`.

!!! tip "Per recordar"
    Comptem des de **0**. El text de 6 lletres té índexs del 0 al 5, no de l'1 al 6.

## Exemples resolts

Copia'ls a Thonny, executa'ls i **modifica'ls** per veure què canvia.

**Exemple 1. Mitjana de tres notes**

```python
nota1 = float(input("Nota 1: "))
nota2 = float(input("Nota 2: "))
nota3 = float(input("Nota 3: "))
mitjana = (nota1 + nota2 + nota3) / 3
print(f"Mitjana: {round(mitjana, 2)}")
```

**Exemple 2. Minuts en hores i minuts**

```python
total = int(input("Quants minuts? "))
hores = total // 60
minuts = total % 60
print(f"{total} minuts són {hores} h i {minuts} min")
```

**Exemple 3. Comparacions**

```python
edat = int(input("Quina edat tens? "))
print("Ets major d'edat?", edat >= 18)
print("Estàs en edat d'ESO (12-16)?", 12 <= edat <= 16)
```

**Exemple 4. Analitzar una paraula**

```python
paraula = input("Escriu una paraula: ")
print(f"Té {len(paraula)} lletres")
print(f"Comença per {paraula[0]}")
print(f"Acaba en {paraula[-1]}")
print(paraula * 3)
```

## Errors típics

!!! failure "Dividir per zero"
    ```python
    print(10 / 0)
    ```

    - **Missatge (similar a):** `ZeroDivisionError: division by zero`
    - **Què vol dir:** és una operació impossible. Passa també amb `//` i `%`.
    - **Com es corregeix:** comprova que el divisor no és zero (ho farem a la unitat 3, amb condicionals).

!!! failure "Comparar text amb un nombre"
    ```python
    edat = input("Quina edat tens? ")
    print(edat >= 18)
    ```

    - **Missatge (similar a):** `TypeError: '>=' not supported between instances of 'str' and 'int'`
    - **Què vol dir:** `edat` és text (ve d'`input()`) i no es pot comparar amb un nombre.
    - **Com es corregeix:** `edat = int(input("Quina edat tens? "))`.

!!! failure "Sortir-se del text"
    ```python
    paraula = "Sol"
    print(paraula[3])
    ```

    - **Missatge (similar a):** `IndexError: string index out of range`
    - **Què vol dir:** `"Sol"` té índexs 0, 1 i 2. L'índex 3 no existeix.
    - **Com es corregeix:** l'última lletra és `paraula[2]` o, més còmodament, `paraula[-1]`. (Compte: si l'usuari no escriu res, la paraula és buida i `paraula[0]` també falla.)

!!! failure "Usar `=` en lloc de `==`"
    ```python
    edat = 15
    print(edat = 18)
    ```

    - **Missatge (similar a):** `TypeError: 'edat' is an invalid keyword argument for print()`
    - **Què vol dir:** Python ha entès `edat = 18` com una assignació, no com una comparació.
    - **Com es corregeix:** `print(edat == 18)`.

!!! failure "Precedència (sense missatge d'error)"
    ```python
    mitjana = nota1 + nota2 + nota3 / 3
    ```

    - **Resultat:** un valor incorrecte, sense cap avís. Només es divideix `nota3` entre 3.
    - **Com es corregeix:** `mitjana = (nota1 + nota2 + nota3) / 3`.

## Activitats guiades

### Activitat 1. Prediu els resultats

Abans d'executar-lo, escriu què mostrarà cada línia. Després comprova-ho a Thonny.

```python
print(17 // 5)
print(17 % 5)
print(17 / 5)
print(2 + 3 * 4)
print((2 + 3) * 4)
print(2 ** 3)
```

??? success "Solució"
    Mostra, en aquest ordre: `3`, `2`, `3.4`, `14`, `20` i `8`.

### Activitat 2. Prediu els booleans

```python
x = 8
print(x > 5 and x < 10)
print(x > 5 and x < 7)
print(x < 5 or x == 8)
print(not x == 8)
print("a" in "casa")
```

??? success "Solució"
    `True`, `False`, `True`, `False`, `True`.

    - Línia 2: `x < 7` és fals, i amb `and` cal que les dues siguin certes.
    - Línia 3: `x == 8` és cert, i amb `or` en té prou amb una.
    - Línia 4: `x == 8` és cert, però `not` l'inverteix.

### Activitat 3. Corregeix el codi

Aquest programa hauria de calcular la mitjana de dues notes. Té tres errors. Corregeix-los **un per un**.

```python
nota1 = input("Nota 1: ")
nota2 = input("Nota 2: ")
mitjana = nota1 + nota2 / 2
print("La mitjana és " + mitjana)
```

??? success "Solució"
    ```python
    nota1 = float(input("Nota 1: "))
    nota2 = float(input("Nota 2: "))
    mitjana = (nota1 + nota2) / 2
    print(f"La mitjana és {mitjana}")
    ```

    Errors: (1) les notes no s'han convertit a `float`; (2) falten els parèntesis (precedència); (3) no es pot unir text amb un nombre amb `+`; una f-string ho resol.

### Activitat 4. Completa el codi

Substitueix cada `___` perquè el programa mostri el que s'indica als comentaris.

```python
paraula = "programació"
print(len(paraula))      # Mostra la longitud
print(paraula[___])      # Mostra la primera lletra
print(paraula[___])      # Mostra l'última lletra
print(paraula[4])        # Quina lletra mostrarà?
```

??? success "Solució"
    ```python
    paraula = "programació"
    print(len(paraula))      # 11
    print(paraula[0])        # p
    print(paraula[-1])       # ó
    print(paraula[4])        # r
    ```

## Lliurament (Classroom)

!!! example "Què has de lliurar"
    **Fitxer:** `u2_cognom_nom.py`

    Fes **un sol programa** amb tres parts, cadascuna amb el seu títol per pantalla:

    **Part 1. Notes**

    1. Demana tres notes (decimals).
    2. Mostra la mitjana arrodonida a 2 decimals.
    3. Mostra si has aprovat, és a dir, el resultat (`True` o `False`) de comparar la mitjana amb 5.

    **Part 2. Canvi**

    1. Demana l'import d'una compra (un nombre enter d'euros, menor de 50).
    2. Calcula el canvi d'un bitllet de 50 €.
    3. Mostra quants **bitllets de 20**, **bitllets de 10**, **bitllets de 5** i **monedes d'1** cal donar-li, fent servir `//` i `%` (ha de donar el mínim de bitllets i monedes).

    **Part 3. Paraula**

    1. Demana una paraula.
    2. Mostra la seva longitud, la primera i l'última lletra, i la paraula repetida 3 vegades.

    Exemple de sortida (les dades varien):

    ```text
    --- NOTES ---
    Mitjana: 7.33
    Has aprovat? True
    --- CANVI ---
    Import: 37 €
    Canvi: 13 €
    Bitllets de 20: 0
    Bitllets de 10: 1
    Bitllets de 5: 0
    Monedes d'1: 3
    --- PARAULA ---
    Longitud: 6
    Primera: P
    Última: n
    Repetida: PythonPythonPython
    ```

    **Abans de lliurar, comprova que:**

    1. El fitxer té la capçalera amb el teu nom, la data i la unitat.
    2. Tots els valors venen d'`input()` i s'han convertit al tipus correcte.
    3. Has fet servir parèntesis quan calen.
    4. Hi ha almenys tres comentaris propis (un per part).
    5. El programa s'executa sense errors.

## Repte opcional

**Xifres d'un nombre.** Demana un nombre enter de tres xifres (per exemple, `472`) i mostra per separat les **centenes**, les **desenes** i les **unitats**, i també la **suma de les xifres** (`4 + 7 + 2 = 13`). Només pots fer servir `//` i `%`.

*Pista:* les unitats són `n % 10`. Pensa com "tallar" les unitats amb `n // 10`.

## Xuleta

| Vull... | Escric... |
| --- | --- |
| Divisió entera / residu | `a // b` / `a % b` |
| Potència | `a ** b` |
| Saber si és parell | `n % 2 == 0` |
| Arrodonir | `round(x, 2)` |
| Comparar | `==`, `!=`, `<`, `>`, `<=`, `>=` |
| Combinar condicions | `and`, `or`, `not` |
| Longitud d'un text | `len(text)` |
| Primera / última lletra | `text[0]` / `text[-1]` |
| Unir / repetir textos | `"a" + "b"` / `"ab" * 3` |
| Un text és dins d'un altre | `"y" in "Python"` |
