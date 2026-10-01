# Unitat 6. Llistes

!!! abstract "Resum"
    **Sessions:** 2 · **Lliurament a Classroom:** `u6_cognom_nom.py`

    - **Sessió 1:** apartats 1 a 3 (crear llistes, accedir als elements, afegir i eliminar).
    - **Sessió 2:** apartats 4 a 6 (recórrer, cercar i llistes amb funcions), activitats i lliurament.

## Objectius

En acabar aquesta unitat sabràs:

- Guardar moltes dades en una sola variable amb una llista.
- Accedir als elements d'una llista, canviar-los, afegir-ne i eliminar-ne.
- Recórrer una llista amb `for`.
- Fer cerques i càlculs sobre llistes (existència, suma, màxim, mitjana).
- Passar llistes a funcions i retornar resultats.

## Punt de partida

!!! question "Ho recordes?"
    Fins ara cada variable guardava **un sol valor**. Però si volem guardar les notes de tota la classe, no crearem 30 variables! Ens cal una **fila de caselles numerades**, cadascuna amb un valor. En algorísmia en dieu *vector* o *taula*; en Python és una **llista**.

    | Posició (índex) | 0 | 1 | 2 |
    | --- | --- | --- | --- |
    | Valor | 7 | 5 | 9 |

    Ja saps com funciona: **és igual que els índexs dels textos** de la unitat 2. Les posicions comencen a 0.

## Teoria

### 1. Crear una llista

Una llista es crea amb **claudàtors** `[ ]` i els elements separats per comes:

```python
notes = [7, 5, 9]
noms = ["Anna", "Pere", "Marta"]
buida = []
```

- Pot contenir qualsevol tipus de dada (text, nombres, booleans...). Normalment hi posem tots del mateix tipus.
- Una llista **buida** és `[]`. Serveix per anar-la omplint després.
- `len(llista)` diu quants elements té.
- Si fas `print(notes)`, es mostra tal qual: `[7, 5, 9]`.

!!! tip "Per recordar"
    Posa noms **en plural** a les llistes (`notes`, `noms`) i en singular a cada element (`nota`, `nom`). Fa el codi més fàcil de llegir.

### 2. Accedir als elements i canviar-los

Com amb el text, els elements s'agafen amb `[posició]`, **comptant des de 0**:

```python
notes = [7, 5, 9]
print(notes[0])     # 7  (el primer)
print(notes[2])     # 9
print(notes[-1])    # 9  (l'últim)
```

A diferència del text, **una llista es pot modificar**: pots canviar un element assignant-hi un valor nou.

```python
notes[1] = 6
print(notes)        # [7, 6, 9]
```

### 3. Afegir i eliminar elements

Les llistes tenen **mètodes**: funcions que pertanyen a la llista i es criden amb un punt (`llista.metode()`).

| Mètode | Què fa | Exemple |
| --- | --- | --- |
| `append(x)` | Afegeix `x` **al final** | `notes.append(8)` |
| `insert(i, x)` | Insereix `x` a la posició `i` | `notes.insert(0, 10)` |
| `remove(x)` | Elimina la primera aparició del valor `x` | `notes.remove(5)` |
| `pop()` | Elimina i **retorna** l'últim element | `ultim = notes.pop()` |
| `pop(i)` | Elimina i retorna l'element de la posició `i` | `notes.pop(0)` |

```python
notes = [7, 5, 9]
notes.append(8)         # [7, 5, 9, 8]
notes.remove(5)         # [7, 9, 8]
notes.insert(0, 10)     # [10, 7, 9, 8]
print(notes)
```

**Construir una llista amb un bucle.** Un patró molt habitual és començar amb una llista buida i anar-hi afegint:

```python
notes = []
for i in range(3):
    nota = float(input(f"Nota {i + 1}: "))
    notes.append(nota)
print(notes)
```

!!! danger "Atenció"
    `append`, `remove`, `insert` i `pop` **modifiquen la llista directament**. No cal assignar el resultat a cap variable: escriu `notes.append(8)`, **no** `notes = notes.append(8)`.

### 4. Recórrer una llista

Amb `for` podem passar per tots els elements, com amb el text:

```python
noms = ["Anna", "Pere", "Marta"]
for nom in noms:
    print(f"Hola, {nom}!")
```

Si a més necessites **la posició** de cada element, recorre els índexs amb `range(len(...))`:

```python
for i in range(len(noms)):
    print(f"{i + 1}. {noms[i]}")
```

Mostra `1. Anna`, `2. Pere`, `3. Marta`.

!!! tip "Quina forma triar?"
    - Només necessites els **valors**? `for element in llista:`
    - Necessites **la posició**? `for i in range(len(llista)):`

### 5. Cercar i calcular

**Funcions útils** que ja venen amb Python:

| Vull... | Escric... |
| --- | --- |
| Saber si un valor és a la llista | `valor in llista` |
| Saber si **no** hi és | `valor not in llista` |
| La suma dels elements | `sum(llista)` |
| El major / el menor | `max(llista)` / `min(llista)` |
| Quantes vegades apareix un valor | `llista.count(valor)` |
| Ordenar la llista (la modifica) | `llista.sort()` |
| Triar un element a l'atzar | `random.choice(llista)` (cal `import random`) |

```python
notes = [7, 5, 9, 6]
print(sum(notes) / len(notes))    # La mitjana: 6.75
print(max(notes))                 # 9
print(5 in notes)                 # True
```

**L'algorisme del màxim «a mà».** Encara que `max()` ja existeix, és molt important entendre com es fa. Agafem el primer element com a màxim provisional i anem comparant:

```python
maxim = notes[0]
for nota in notes:
    if nota > maxim:
        maxim = nota
print(maxim)
```

**La cerca amb un recorregut.** Per exemple, per comptar quantes notes són aprovades:

```python
aprovades = 0
for nota in notes:
    if nota >= 5:
        aprovades += 1
```

### 6. Llistes i funcions

Una llista es pot passar a una funció com qualsevol altre valor, i una funció pot retornar-ne el resultat:

```python
def mitjana(llista):
    total = 0
    for valor in llista:
        total += valor
    return total / len(llista)

notes = [7, 5, 9, 6]
print(mitjana(notes))
```

!!! warning "Una funció pot modificar la llista original"
    A diferència dels nombres i els textos, si una funció **canvia** una llista (amb `append`, `remove`...), la llista del programa principal **també canvia**.

    ```python
    def afegeix_zero(llista):
        llista.append(0)

    notes = [5, 7]
    afegeix_zero(notes)
    print(notes)        # [5, 7, 0]
    ```

## Exemples resolts

Copia'ls a Thonny, executa'ls i **modifica'ls** per veure què canvia.

**Exemple 1. Llista de la compra**

```python
compra = ["pa", "llet", "ous"]
compra.append("tomàquets")
print(f"Has de comprar {len(compra)} coses:")
for article in compra:
    print("-", article)
```

**Exemple 2. Estadístiques de notes**

```python
notes = [7, 5, 9, 6, 4]
print(f"Notes: {notes}")
print(f"Mitjana: {round(sum(notes) / len(notes), 2)}")
print(f"Màxima: {max(notes)}")
print(f"Mínima: {min(notes)}")
```

**Exemple 3. Omplir una llista fins que l'usuari acabi**

```python
compra = []
article = input("Article (escriu fi per acabar): ")
while article != "fi":
    compra.append(article)
    article = input("Article (escriu fi per acabar): ")

print(f"Tens {len(compra)} articles:")
for i in range(len(compra)):
    print(f"{i + 1}. {compra[i]}")
```

**Exemple 4. Cercar un valor**

```python
alumnes = ["Anna", "Pere", "Marta", "Joan"]
nom = input("Quin nom busques? ")
if nom in alumnes:
    print("Està a la llista")
else:
    print("No hi és")
```

**Exemple 5. Una llista dins d'una funció**

```python
def compta_aprovades(notes):
    total = 0
    for nota in notes:
        if nota >= 5:
            total += 1
    return total

print(compta_aprovades([7, 4, 5, 3, 9]))     # 3
```

## Errors típics

!!! failure "Sortir-se de la llista"
    ```python
    notes = [7, 5, 9]
    print(notes[3])
    ```

    - **Missatge (similar a):** `IndexError: list index out of range`
    - **Què vol dir:** la llista té 3 elements, amb índexs 0, 1 i 2. L'índex 3 no existeix.
    - **Com es corregeix:** l'últim és `notes[2]` o `notes[-1]`. Per recórrer-la tota, fes servir `for`.

!!! failure "Eliminar un valor que no hi és"
    ```python
    notes = [7, 5, 9]
    notes.remove(6)
    ```

    - **Missatge (similar a):** `ValueError: list.remove(x): x not in list`
    - **Què vol dir:** has demanat eliminar un valor que no és a la llista.
    - **Com es corregeix:** comprova-ho abans: `if 6 in notes:`.

!!! failure "Guardar el resultat d'`append`"
    ```python
    notes = [7, 5, 9]
    notes = notes.append(6)
    print(len(notes))
    ```

    - **Missatge (similar a):** `TypeError: object of type 'NoneType' has no len()`
    - **Què vol dir:** `append` modifica la llista però **no retorna res** (retorna `None`). Així, `notes` ha passat a valer `None`.
    - **Com es corregeix:** `notes.append(6)`, sense assignar-ho.

!!! failure "Parèntesis en lloc de claudàtors"
    ```python
    notes = [7, 5, 9]
    print(notes(0))
    ```

    - **Missatge (similar a):** `TypeError: 'list' object is not callable`
    - **Què vol dir:** els parèntesis serveixen per cridar funcions. Per accedir a un element calen **claudàtors**.
    - **Com es corregeix:** `notes[0]`.

!!! failure "Copiar una llista amb `=` (sense missatge d'error)"
    ```python
    original = [1, 2, 3]
    copia = original
    copia.append(4)
    print(original)
    ```

    - **Resultat:** mostra `[1, 2, 3, 4]`, tot i que has modificat «la còpia».
    - **Què vol dir:** `copia = original` no fa una còpia: les dues variables apunten **a la mateixa llista**.
    - **Com es corregeix:** `copia = original.copy()`.

## Activitats guiades

### Activitat 1. Prediu el contingut

```python
a = [4, 8, 15]
a.append(16)
a[0] = 1
print(a)
print(len(a))
print(a[-1])
```

??? success "Solució"
    Mostra `[1, 8, 15, 16]`, `4` i `16`. Primer s'afegeix el 16 al final; després el primer element (el 4) es canvia per un 1.

### Activitat 2. Prediu el resultat d'un recorregut

```python
punts = [3, 5, 4]
total = 0
for p in punts:
    total += p
print(total, total / len(punts))
```

??? success "Solució"
    Mostra `12 4.0`: la suma és 12 i la mitjana, 12 dividit entre 3 elements.

### Activitat 3. Corregeix el codi

Aquest programa té dos errors. Corregeix-los **un per un**.

```python
notes = [7, 5, 9]
notes = notes.append(6)
print("Tens", len(notes), "notes")
print("Primera:", notes(0))
```

??? success "Solució"
    ```python
    notes = [7, 5, 9]
    notes.append(6)
    print("Tens", len(notes), "notes")
    print("Primera:", notes[0])
    ```

    Errors: (1) `notes = notes.append(6)` deixa `notes` a `None` (`append` modifica la llista i s'escriu sol, i és el que fa fallar el `len`); (2) per accedir a un element calen claudàtors, no parèntesis: `notes[0]`.

### Activitat 4. Completa el codi

Completa la funció que calcula la mitjana d'una llista.

```python
def mitjana(llista):
    total = 0
    for valor in ___:
        total += ___
    return total / ___(llista)
```

??? success "Solució"
    ```python
    def mitjana(llista):
        total = 0
        for valor in llista:
            total += valor
        return total / len(llista)
    ```

### Activitat 5. Escriu-ho tu

Crea la llista `["Anna", "Pere", "Marta", "Joan", "Laia"]`. Demana un nom: si és a la llista, elimina'l i mostra com queda; si no hi és, avisa l'usuari.

??? success "Solució"
    ```python
    noms = ["Anna", "Pere", "Marta", "Joan", "Laia"]
    nom = input("Quin nom vols eliminar? ")
    if nom in noms:
        noms.remove(nom)
        print(f"Eliminat. Queden: {noms}")
    else:
        print("Aquest nom no hi és")
    ```

## Lliurament (Classroom)

!!! example "Què has de lliurar"
    **Fitxer:** `u6_cognom_nom.py`

    Fes **un sol programa** amb tres parts, cadascuna amb el seu títol per pantalla.

    **Part 1. Notes d'una classe**

    1. Demana quantes notes vols introduir (entre 1 i 10) i demana-les (decimals entre 0 i 10), guardant-les en una **llista**.
    2. Defineix aquestes funcions, que reben la llista i **retornen** el resultat:
        - `mitjana(llista)`
        - `maxim(llista)`: **sense** fer servir `max()`, amb el recorregut de la teoria.
        - `compta_aprovades(llista)`: quantes notes són majors o iguals que 5.
    3. Mostra la llista, la mitjana (arrodonida a 2 decimals), la nota màxima i el nombre d'aprovades.

    **Part 2. Llista de la compra**

    1. Demana articles fins que l'usuari escrigui `fi`, i guarda'ls en una llista.
    2. Mostra'ls **numerats** (`1. pa`, `2. llet`...) fent servir `range(len(...))`.
    3. Demana un article i digues si ja és a la llista.

    **Part 3. Noms**

    1. Demana 5 noms i guarda'ls en una llista.
    2. Mostra la llista **ordenada alfabèticament**.
    3. Mostra el nom **més llarg** (el que té més lletres), amb un recorregut com el del màxim.

    **Abans de lliurar, comprova que:**

    1. El fitxer té la capçalera amb el teu nom, la data i la unitat.
    2. Les funcions (a la part 1) estan definides **abans** del programa principal i no mostren res per pantalla.
    3. Has provat el programa amb 1 sola nota i amb 10 notes.
    4. Al final de cada part hi ha un comentari amb 3 casos de prova que has comprovat.
    5. El programa s'executa sense errors.

## Repte opcional

**Llista sense repetits.** Demana nombres enters fins que l'usuari escrigui `0`, però guarda a la llista **només els que encara no hi són** (fes servir `not in`). Al final mostra la llista i quants nombres diferents has obtingut.

*Pista:* abans de fer `append`, comprova si el nombre ja és a la llista.

## Xuleta

| Vull... | Escric... |
| --- | --- |
| Crear una llista / una de buida | `notes = [7, 5, 9]` / `notes = []` |
| Quants elements té | `len(notes)` |
| Primer / últim element | `notes[0]` / `notes[-1]` |
| Canviar un element | `notes[1] = 6` |
| Afegir al final | `notes.append(8)` |
| Eliminar un valor | `notes.remove(5)` |
| Eliminar l'últim i obtenir-lo | `notes.pop()` |
| Recórrer els valors | `for nota in notes:` |
| Recórrer amb la posició | `for i in range(len(notes)):` |
| Saber si hi és | `5 in notes` |
| Suma / màxim / mínim | `sum(notes)` / `max(notes)` / `min(notes)` |
| Ordenar | `notes.sort()` |
| Fer una còpia | `copia = notes.copy()` |
