# Extra 3. Tuples i conjunts

!!! abstract "Resum"
    **Tipus:** ampliació opcional · **Requisits:** unitats 5 i 6 · **Sense lliurament:** fes les activitats i comprova-les amb les solucions.

## Objectius

En acabar aquest extra sabràs:

- Crear i fer servir **tuples**, i saber per què no es poden modificar.
- **Desempaquetar** una tupla i fer que una funció retorni més d'un valor.
- Crear **conjunts**, eliminar repetits i comprovar si un valor hi és.
- Fer operacions entre conjunts: unió, intersecció i diferència.
- Triar entre llista, tupla i conjunt segons el que necessites.

## Punt de partida

!!! question "Ho recordes?"
    Fins ara has fet servir una sola estructura per guardar moltes dades: la **llista**. Però a vegades necessitem una altra cosa:

    - Dades que **no han de canviar** i que van juntes, com les coordenades d'un punt o una data: això són les **tuples**.
    - Una col·lecció on **no hi hagi repetits** i on només importi *si hi és o no hi és*, com els diagrames de Venn de matemàtiques: això són els **conjunts**.

## Teoria

### 1. Tuples

Una **tupla** és com una llista, però **no es pot modificar**. Es crea amb parèntesis:

```python
punt = (3, 4)
data = (15, 10, 2026)

print(punt[0])      # 3
print(len(punt))    # 2
```

Funciona igual que una llista per llegir-la: tens índexs (que comencen a 0), `len()`, `in`, recórrer-la amb `for` i fer-ne *slicing*. La diferència és que **no hi ha `append`, `remove` ni assignacions**.

!!! tip "Una tupla d'un sol element"
    Per crear una tupla d'un sol element cal una **coma** al final: `(5,)`. Sense la coma, `(5)` són simplement uns parèntesis al voltant d'un 5, i no una tupla.

**Quan usar una tupla?** Quan les dades formen un conjunt que no ha de canviar: coordenades `(x, y)`, un color `(255, 0, 0)`, una data `(dia, mes, any)`, una parella `(nom, edat)`...

### 2. Desempaquetar tuples

Podem repartir els valors d'una tupla en diverses variables **d'un sol cop**:

```python
punt = (3, 4)
x, y = punt
print(x)       # 3
print(y)       # 4
```

El nombre de variables ha de ser igual que el d'elements de la tupla. Això també és el que fa un intercanvi de valors, que ja vas veure al repte de la unitat 1:

```python
a, b = 1, 2
a, b = b, a
print(a, b)    # 2 1
```

### 3. Funcions que retornen més d'un valor

Una funció només pot retornar **una cosa**, però si aquesta cosa és una tupla, en pot portar diversos. Si fas `return a, b`, Python retorna la tupla `(a, b)`:

```python
def extrems(llista):
    return min(llista), max(llista)

menor, major = extrems([4, 9, 2, 7])
print(menor, major)    # 2 9
```

### 4. Llistes de tuples

Combinar llistes i tuples és molt còmode per guardar **registres**. El `for` pot desempaquetar cada tupla directament:

```python
alumnes = [("Anna", 15), ("Pere", 16), ("Marta", 15)]

for nom, edat in alumnes:
    print(f"{nom} té {edat} anys")
```

### 5. Conjunts

Un **conjunt** (`set`) és una col·lecció de valors **sense repetits i sense ordre**. Es crea amb claus:

```python
lletres = {"a", "b", "a", "c", "b"}
print(len(lletres))     # 3: els repetits desapareixen
```

!!! warning "Conjunt buit"
    Un conjunt buit es crea amb `set()`. **No** amb `{}`: aquestes claus buides creen un *diccionari*, que veuràs a l'extra següent.

Com que **no tenen ordre**, no tenen índexs: `lletres[0]` dona error, i en recórrer-los amb `for` l'ordre pot variar. Si vols mostrar-los ordenats, fes servir `sorted(conjunt)`, que retorna una llista ordenada.

| Vull... | Escric... |
| --- | --- |
| Afegir un valor | `s.add(x)` |
| Eliminar un valor (dona error si no hi és) | `s.remove(x)` |
| Eliminar un valor (sense error si no hi és) | `s.discard(x)` |
| Saber si hi és | `x in s` |
| Quants elements té | `len(s)` |

**Eliminar repetits d'una llista.** Convertir una llista en conjunt elimina els valors repetits, i `len()` ens diu quants valors **diferents** hi havia:

```python
nombres = [3, 1, 3, 2, 1, 5, 2]
diferents = set(nombres)
print(len(diferents))          # 4
print(sorted(diferents))       # [1, 2, 3, 5]
```

Això resol d'una forma molt més curta el repte de la **llista sense repetits** de la unitat 6.

### 6. Operacions entre conjunts

Són les mateixes operacions dels diagrames de Venn:

- **Unió** `a | b`: els elements que són a `a`, a `b` o a tots dos.
- **Intersecció** `a & b`: els elements que són a **tots dos** conjunts.
- **Diferència** `a - b`: els elements de `a` que **no** són a `b`.

```python
anna = {"futbol", "música", "cinema"}
pere = {"cinema", "escacs", "música"}

print(sorted(anna & pere))    # ['cinema', 'música']
print(sorted(anna | pere))    # ['cinema', 'escacs', 'futbol', 'música']
print(sorted(anna - pere))    # ['futbol']
```

### 7. Llista, tupla o conjunt?

| | Llista | Tupla | Conjunt |
| --- | --- | --- | --- |
| Símbol | `[ ]` | `( )` | `{ }` |
| Té ordre i índexs | Sí | Sí | No |
| Es pot modificar | Sí | No | Sí |
| Admet repetits | Sí | Sí | No |
| Ideal per a... | Una sèrie de dades que canvia | Dades que van juntes i no canvien | Valors únics i pertinença |

## Exemples resolts

Copia'ls a Thonny, executa'ls i **modifica'ls** per veure què canvia.

**Exemple 1. Moure un punt**

Com que les tuples no es poden modificar, construïm una tupla nova:

```python
punt = (3, 4)
x, y = punt
nou_punt = (x + 1, y + 2)
print(nou_punt)        # (4, 6)
```

**Exemple 2. Una funció amb dos resultats**

```python
def divideix(a, b):
    return a // b, a % b

quocient, residu = divideix(17, 5)
print(f"Quocient: {quocient}, residu: {residu}")
```

**Exemple 3. Un registre d'alumnes**

```python
alumnes = [("Anna", 8), ("Pere", 5), ("Marta", 9)]
for nom, nota in alumnes:
    estat = "aprovat" if nota >= 5 else "suspès"
    print(f"{nom}: {nota} ({estat})")
```

**Exemple 4. Lletres diferents d'una paraula**

```python
paraula = input("Paraula: ").lower()
print(f"Té {len(set(paraula))} lletres diferents")
```

Amb `banana` mostra `3` (`b`, `a` i `n`).

**Exemple 5. Aficions en comú**

```python
anna = {"futbol", "música", "cinema"}
pere = {"cinema", "escacs", "música"}
print("En comú:", sorted(anna & pere))
print("Només l'Anna:", sorted(anna - pere))
```

## Errors típics

!!! failure "Modificar una tupla"
    ```python
    punt = (3, 4)
    punt[0] = 5
    ```

    - **Missatge (similar a):** `TypeError: 'tuple' object does not support item assignment`
    - **Què vol dir:** les tuples no es poden modificar.
    - **Com es corregeix:** crea una tupla nova: `punt = (5, punt[1])`.

!!! failure "Una tupla d'un element sense coma (sense missatge d'error)"
    ```python
    t = (5)
    print(type(t))
    ```

    - **Resultat:** mostra `<class 'int'>`: és un nombre, no una tupla.
    - **Què vol dir:** els parèntesis sols no creen una tupla. Fa falta la coma.
    - **Com es corregeix:** `t = (5,)`.

!!! failure "Desempaquetar amb un nombre incorrecte de variables"
    ```python
    a, b = (1, 2, 3)
    ```

    - **Missatge (similar a):** `ValueError: too many values to unpack (expected 2)`
    - **Què vol dir:** la tupla té 3 valors i només has posat 2 variables.
    - **Com es corregeix:** `a, b, c = (1, 2, 3)`.

!!! failure "Accedir a un conjunt per posició"
    ```python
    colors = {"roig", "verd"}
    print(colors[0])
    ```

    - **Missatge (similar a):** `TypeError: 'set' object is not subscriptable`
    - **Què vol dir:** els conjunts no tenen ordre ni posicions.
    - **Com es corregeix:** comprova si un valor hi és amb `in`, o recorre'l amb `for`.

!!! failure "Crear un conjunt buit amb `{}`"
    ```python
    colors = {}
    colors.add("roig")
    ```

    - **Missatge (similar a):** `AttributeError: 'dict' object has no attribute 'add'`
    - **Què vol dir:** `{}` crea un diccionari, no un conjunt.
    - **Com es corregeix:** `colors = set()`.

## Activitats guiades

### Activitat 1. Prediu: tuples

```python
punt = (3, 4)
x, y = punt
print(x + y)
print(punt[0])
print(len(punt))

a, b = 1, 2
a, b = b, a
print(a, b)
```

??? success "Solució"
    Mostra `7`, `3`, `2` i `2 1`.

### Activitat 2. Prediu: conjunts

```python
lletres = {"a", "b", "a", "c", "b"}
print(len(lletres))
print("a" in lletres)
lletres.add("d")
lletres.add("a")
print(len(lletres))
```

??? success "Solució"
    Mostra `3`, `True` i `4`. El conjunt inicial té 3 elements (`a`, `b`, `c`); s'hi afegeix `d`, però afegir una `a` que ja hi és no canvia res.

### Activitat 3. Prediu: operacions

```python
a = {1, 2, 3, 4}
b = {3, 4, 5}
print(sorted(a | b))
print(sorted(a & b))
print(sorted(a - b))
print(sorted(b - a))
```

??? success "Solució"
    - `a | b` → `[1, 2, 3, 4, 5]`
    - `a & b` → `[3, 4]`
    - `a - b` → `[1, 2]`
    - `b - a` → `[5]`

### Activitat 4. Corregeix el codi

Aquest programa té dos errors. Corregeix-los **un per un**.

```python
colors = {}
colors.add("roig")
colors.add("verd")
print(colors[0])
```

??? success "Solució"
    ```python
    colors = set()
    colors.add("roig")
    colors.add("verd")
    print("roig" in colors)
    ```

    Errors: (1) `{}` crea un diccionari, no un conjunt, i per això `add` falla: cal `set()`; (2) els conjunts no tenen posicions: no es pot fer `colors[0]`. Per saber si un valor hi és, es fa servir `in`.

### Activitat 5. Completa el codi

Completa la funció perquè retorni el mínim i el màxim d'una llista, i la crida perquè els reculli.

```python
def extrems(llista):
    return ___(llista), ___(llista)

minim, maxim = ___([4, 9, 2, 7])
print(minim, maxim)
```

??? success "Solució"
    ```python
    def extrems(llista):
        return min(llista), max(llista)

    minim, maxim = extrems([4, 9, 2, 7])
    print(minim, maxim)    # 2 9
    ```

### Activitat 6. Escriu-ho tu (tuples)

Tens la llista `[("Anna", 8), ("Pere", 5), ("Marta", 9)]`. Mostra cada alumne amb la seva nota (`Anna: 8`) i, al final, **qui té la nota més alta**.

??? success "Solució"
    ```python
    alumnes = [("Anna", 8), ("Pere", 5), ("Marta", 9)]
    millor_nom = alumnes[0][0]
    millor_nota = alumnes[0][1]

    for nom, nota in alumnes:
        print(f"{nom}: {nota}")
        if nota > millor_nota:
            millor_nota = nota
            millor_nom = nom

    print(f"La nota més alta és de {millor_nom} ({millor_nota})")
    ```

### Activitat 7. Escriu-ho tu (conjunts)

Demana nombres enters fins que l'usuari escrigui `0`. Al final, mostra **quants nombres diferents** ha escrit i **quins són**, ordenats.

??? success "Solució"
    ```python
    nombres = set()
    n = int(input("Nombre (0 per acabar): "))
    while n != 0:
        nombres.add(n)
        n = int(input("Nombre (0 per acabar): "))

    print(f"Has escrit {len(nombres)} nombres diferents")
    print(sorted(nombres))
    ```

## Repte opcional

**Aficions en comú.** Si has fet l'extra de text, aprofita `split` i `strip`. Demana a dues persones les seves aficions, escrites separades per comes (`futbol, cinema, música`). Converteix-les en conjunts i mostra:

- Les aficions que tenen **en comú**.
- Les que **només té la primera** persona.
- Les que **només té la segona**.
- **Totes** les aficions diferents entre les dues.

*Pista:* recorda treure els espais sobrants de cada afició amb `strip()`, perquè `" cinema"` i `"cinema"` no són el mateix text.

## Xuleta

| Vull... | Escric... |
| --- | --- |
| Crear una tupla | `punt = (3, 4)` |
| Tupla d'un sol element | `(5,)` |
| Desempaquetar | `x, y = punt` |
| Retornar dos valors | `return a, b` |
| Recórrer una llista de tuples | `for nom, edat in alumnes:` |
| Crear un conjunt / un buit | `{1, 2, 3}` / `set()` |
| Eliminar repetits d'una llista | `set(llista)` |
| Afegir / eliminar d'un conjunt | `s.add(x)` / `s.discard(x)` |
| Unió / intersecció / diferència | `a \| b` / `a & b` / `a - b` |
| Mostrar un conjunt ordenat | `sorted(s)` |
