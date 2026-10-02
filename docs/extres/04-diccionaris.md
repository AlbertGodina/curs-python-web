# Extra 4. Diccionaris

!!! abstract "Resum"
    **Tipus:** ampliació opcional · **Requisits:** unitats 4 i 6 (és recomanable haver fet l'extra de tuples) · **Sense lliurament:** fes les activitats i comprova-les amb les solucions.

## Objectius

En acabar aquest extra sabràs:

- Guardar informació en **parelles clau-valor** amb un diccionari.
- Consultar, afegir, modificar i eliminar elements.
- Recórrer un diccionari amb `keys()`, `values()` i `items()`.
- Comptar quantes vegades apareix cada cosa (el patró de les **freqüències**).
- Combinar llistes i diccionaris per guardar **registres** (per exemple, una llista d'alumnes).
- Decidir quan et convé un diccionari en lloc d'una llista.

## Punt de partida

!!! question "Ho recordes?"
    A la unitat 6 vas veure que, a una llista, cada dada s'identifica per la seva **posició** (0, 1, 2...). Però pensa en una agenda de telèfons o en un diccionari de paraules: no busques «el contacte número 7», sinó **«el telèfon de l'Anna»**. Busques per un **nom**, no per una posició.

    Això és el que fan els **diccionaris**: associen una **clau** (el nom) amb un **valor** (el telèfon).

    Al projecte E, de la unitat 7, vas haver de fer servir dues llistes paral·leles (productes i estoc). Amb un diccionari ho tindràs tot en una sola estructura.

## Teoria

### 1. Crear un diccionari i consultar-lo

Un diccionari es crea amb claus `{ }`, i cada element té la forma `clau: valor`:

```python
edats = {"Anna": 15, "Pere": 16, "Marta": 15}

print(edats["Anna"])      # 15
print(len(edats))         # 3
```

- Les **claus** no es poden repetir i han de ser d'un tipus que no es pugui modificar: text, nombres o tuples (**no** llistes).
- Els **valors** poden ser de qualsevol tipus: nombres, text, llistes, altres diccionaris...
- Un diccionari buit es crea amb `{}` (recorda que un conjunt buit es crea amb `set()`).
- Es conserva l'ordre en què s'han afegit els elements.

### 2. Afegir, modificar i eliminar

Afegir i modificar es fan exactament igual: **assignant** un valor a una clau. Si la clau ja existeix, es canvia el valor; si no, es crea.

```python
edats = {"Anna": 15, "Pere": 16}

edats["Laia"] = 14        # Afegeix una clau nova
edats["Anna"] = 16        # Modifica un valor existent
print(edats)              # {'Anna': 16, 'Pere': 16, 'Laia': 14}
```

Per eliminar una parella:

```python
del edats["Pere"]               # La elimina
valor = edats.pop("Laia")       # La elimina i retorna el valor (14)
```

### 3. Comprovar si una clau hi és

L'operador `in` serveix per saber si una **clau** és al diccionari (no els valors):

```python
if "Anna" in edats:
    print("L'Anna hi és")
```

Si consultes una clau que no existeix amb `edats["Marta"]`, dona error. El mètode `get()` és una alternativa segura: retorna un **valor per defecte** si la clau no hi és.

```python
print(edats.get("Marta"))          # None
print(edats.get("Marta", 0))       # 0
```

### 4. Recórrer un diccionari

Hi ha tres maneres, segons el que necessitis:

```python
notes = {"Mates": 7, "Català": 8, "Anglès": 6}

for assignatura in notes:                  # Només les claus
    print(assignatura)

for nota in notes.values():                # Només els valors
    print(nota)

for assignatura, nota in notes.items():    # Les parelles clau-valor
    print(f"{assignatura}: {nota}")
```

`items()` retorna les parelles com a tuples, i per això les podem desempaquetar en el `for`, com vas veure a l'extra de tuples. Les funcions `sum()`, `max()` i `min()` també funcionen sobre `values()`:

```python
print(sum(notes.values()))     # 21
print(max(notes.values()))     # 8
```

### 5. El patró estrella: comptar freqüències

Un dels usos més típics dels diccionaris és **comptar quantes vegades apareix cada cosa**. La clau és l'element i el valor, el comptador:

```python
frase = "si no si si no"
comptador = {}

for paraula in frase.split():
    comptador[paraula] = comptador.get(paraula, 0) + 1

print(comptador)       # {'si': 3, 'no': 2}
```

La línia clau és `comptador.get(paraula, 0) + 1`: agafa el valor actual (o 0 si és la primera vegada que apareix la paraula) i li suma 1.

### 6. Registres: llistes i diccionaris combinats

Un diccionari pot guardar **tota la informació d'una cosa** amb claus que descriuen cada dada. I si en tenim molts, els posem en una llista:

```python
alumne = {"nom": "Anna", "edat": 15, "notes": [7, 8, 9]}
print(alumne["nom"])          # Anna
print(alumne["notes"][0])     # 7

alumnes = [
    {"nom": "Anna", "edat": 15},
    {"nom": "Pere", "edat": 16},
]
print(alumnes[1]["nom"])      # Pere
```

!!! tip "Per recordar"
    Primer l'índex de la llista, després la clau del diccionari: `alumnes[1]["nom"]`.

### 7. Quan usar un diccionari?

| Si... | Fes servir... |
| --- | --- |
| Tens una seqüència de dades i les identifiques per **posició** | Una llista |
| Vols consultar per un **nom o etiqueta** | Un diccionari |
| Només vols saber si un valor hi és i evitar repetits | Un conjunt |

## Exemples resolts

Copia'ls a Thonny, executa'ls i **modifica'ls** per veure què canvia.

**Exemple 1. Una agenda de telèfons**

```python
agenda = {"Anna": "612345678", "Pere": "698765432"}
nom = input("Nom: ")
if nom in agenda:
    print(f"Telèfon: {agenda[nom]}")
else:
    print("No tinc aquest contacte")
```

**Exemple 2. Notes per assignatura**

```python
notes = {"Mates": 7, "Català": 8, "Anglès": 6}
for assignatura, nota in notes.items():
    print(f"{assignatura}: {nota}")
print(f"Mitjana: {round(sum(notes.values()) / len(notes), 2)}")
```

**Exemple 3. Comptar lletres**

```python
text = input("Text: ").lower()
comptador = {}
for lletra in text:
    if lletra != " ":
        comptador[lletra] = comptador.get(lletra, 0) + 1

for lletra, vegades in comptador.items():
    print(f"{lletra}: {vegades}")
```

**Exemple 4. Un traductor**

```python
traduccio = {"gat": "cat", "gos": "dog", "casa": "house"}
paraula = input("Paraula en català: ").lower().strip()
print(traduccio.get(paraula, "No ho sé traduir"))
```

**Exemple 5. Una llista d'alumnes**

```python
alumnes = [
    {"nom": "Anna", "edat": 15},
    {"nom": "Pere", "edat": 16},
]
for alumne in alumnes:
    print(f"{alumne['nom']} té {alumne['edat']} anys")
```

## Errors típics

!!! failure "Consultar una clau que no existeix"
    ```python
    edats = {"Anna": 15}
    print(edats["Marta"])
    ```

    - **Missatge (similar a):** `KeyError: 'Marta'`
    - **Què vol dir:** la clau `"Marta"` no és al diccionari.
    - **Com es corregeix:** comprova-ho abans (`if "Marta" in edats:`) o fes servir `edats.get("Marta", valor_per_defecte)`.

!!! failure "Fer servir `append` en un diccionari"
    ```python
    edats = {"Anna": 15}
    edats.append("Pere")
    ```

    - **Missatge (similar a):** `AttributeError: 'dict' object has no attribute 'append'`
    - **Què vol dir:** `append` és un mètode de les llistes. Els diccionaris no en tenen.
    - **Com es corregeix:** afegeix una parella amb `edats["Pere"] = 16`.

!!! failure "Fer servir una llista com a clau"
    ```python
    dades = {[1, 2]: "punt"}
    ```

    - **Missatge (similar a):** `TypeError: unhashable type: 'list'`
    - **Què vol dir:** les claus han de ser d'un tipus que no es pugui modificar.
    - **Com es corregeix:** fes servir una tupla: `{(1, 2): "punt"}`.

!!! failure "Repetir una clau (sense missatge d'error)"
    ```python
    edats = {"Anna": 15, "Anna": 16}
    print(edats)
    ```

    - **Resultat:** mostra `{'Anna': 16}`.
    - **Què vol dir:** les claus no es poden repetir, i el segon valor sobreescriu el primer, sense cap avís.
    - **Com es corregeix:** fes servir claus diferents.

!!! failure "Modificar el diccionari mentre el recorres"
    ```python
    notes = {"Mates": 7, "Català": 3}
    for assignatura in notes:
        if notes[assignatura] < 5:
            del notes[assignatura]
    ```

    - **Missatge (similar a):** `RuntimeError: dictionary changed size during iteration`
    - **Què vol dir:** no es poden afegir ni eliminar elements mentre es fa un `for` sobre el mateix diccionari.
    - **Com es corregeix:** guarda en una llista les claus que vols eliminar i elimina-les després del bucle.

## Activitats guiades

### Activitat 1. Prediu: consultes i modificacions

```python
edats = {"Anna": 15, "Pere": 16}
edats["Laia"] = 14
edats["Anna"] = 16
print(len(edats))
print(edats["Anna"])
print("Pere" in edats)
print(edats.get("Marta", 0))
```

??? success "Solució"
    Mostra `3`, `16`, `True` i `0`. S'afegeix la Laia (3 claus) i l'Anna passa de 15 a 16. «Marta» no existeix, així que `get` retorna el valor per defecte.

### Activitat 2. Prediu: recorreguts

```python
preus = {"pa": 2, "llet": 1, "ous": 3}
total = 0
for producte, preu in preus.items():
    total += preu
print(total)
print(max(preus.values()))
for clau in preus:
    print(clau)
```

??? success "Solució"
    Mostra `6`, `3` i després, en línies separades, `pa`, `llet` i `ous`. Un `for` directe sobre el diccionari recorre només les **claus**.

### Activitat 3. Corregeix el codi

Aquest programa té dos errors. Corregeix-los **un per un**.

```python
agenda = {"Anna": "612345678"}
agenda.append("Pere")
print(agenda["Marta"])
```

??? success "Solució"
    ```python
    agenda = {"Anna": "612345678"}
    agenda["Pere"] = "698765432"
    print(agenda.get("Marta", "Contacte no trobat"))
    ```

    Errors: (1) els diccionaris no tenen `append`; s'hi afegeix una parella assignant un valor a una clau nova (i cal indicar el telèfon); (2) `agenda["Marta"]` dona `KeyError` perquè la clau no existeix; amb `get` es pot indicar un valor per defecte.

### Activitat 4. Completa el codi

Completa el programa, que compta quantes vegades apareix cada resposta.

```python
respostes = ["si", "no", "si", "si", "no"]
comptador = {}
for resposta in respostes:
    comptador[resposta] = comptador.___(resposta, ___) + 1
print(comptador)
```

??? success "Solució"
    ```python
    respostes = ["si", "no", "si", "si", "no"]
    comptador = {}
    for resposta in respostes:
        comptador[resposta] = comptador.get(resposta, 0) + 1
    print(comptador)       # {'si': 3, 'no': 2}
    ```

### Activitat 5. Escriu-ho tu (consultes)

Tens el diccionari `{"Catalunya": "Barcelona", "França": "París", "Itàlia": "Roma"}`. Demana un país: si hi és, mostra'n la capital; si no hi és, **demana l'usuari quina és la capital i afegeix-la** al diccionari.

??? success "Solució"
    ```python
    capitals = {"Catalunya": "Barcelona", "França": "París", "Itàlia": "Roma"}
    pais = input("País: ")
    if pais in capitals:
        print(f"La capital és {capitals[pais]}")
    else:
        capital = input("No ho sé. Quina és la capital? ")
        capitals[pais] = capital
        print(f"Gràcies! Ara sé que la capital de {pais} és {capital}")
    ```

### Activitat 6. Escriu-ho tu (llista de diccionaris)

Tens aquesta llista. Mostra el **nom de qui té la millor nota**.

```python
alumnes = [
    {"nom": "Anna", "nota": 8},
    {"nom": "Pere", "nota": 5},
    {"nom": "Marta", "nota": 9},
]
```

??? success "Solució"
    ```python
    millor = alumnes[0]
    for alumne in alumnes:
        if alumne["nota"] > millor["nota"]:
            millor = alumne
    print(f"La millor nota és de {millor['nom']} ({millor['nota']})")
    ```

## Repte opcional

**L'inventari, amb un diccionari.** Refés el projecte E de la unitat 7 (inventari d'una botiga) fent servir **un sol diccionari** `producte: unitats` en lloc de dues llistes paral·leles. Mantén el menú: veure l'inventari, afegir un producte, vendre unitats (sense deixar l'estoc en negatiu) i sortir. Quan acabis, compara les dues versions: quina és més curta? Quina és més fàcil de llegir?

## Xuleta

| Vull... | Escric... |
| --- | --- |
| Crear un diccionari / un de buit | `{"a": 1, "b": 2}` / `{}` |
| Consultar una clau | `d[clau]` |
| Consultar sense risc d'error | `d.get(clau, valor_per_defecte)` |
| Afegir o modificar | `d[clau] = valor` |
| Eliminar | `del d[clau]` o `d.pop(clau)` |
| Saber si una clau hi és | `clau in d` |
| Quantes parelles té | `len(d)` |
| Recórrer claus / valors / parelles | `for k in d` / `d.values()` / `d.items()` |
| Comptar freqüències | `d[x] = d.get(x, 0) + 1` |
| Un element d'una llista de diccionaris | `alumnes[0]["nom"]` |
