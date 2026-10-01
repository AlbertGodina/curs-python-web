# Extra 2. Text avançat

!!! abstract "Resum"
    **Tipus:** ampliació opcional · **Requisits:** unitats 2, 4 i 6 · **Sense lliurament:** fes les activitats i comprova-les amb les solucions.

## Objectius

En acabar aquest extra sabràs:

- Tallar un text amb el *slicing* (`text[a:b]`) i invertir-lo.
- Fer servir els mètodes de text més útils: `upper`, `lower`, `strip`, `replace`, `count`, `find`...
- Convertir un text en una llista de paraules (`split`) i tornar-la a unir (`join`).
- Construir textos nous amb un bucle.
- Donar format als nombres i alinear el text amb les f-strings.

## Punt de partida

!!! question "Ho recordes?"
    A la unitat 2 vas aprendre que un text és una **seqüència de caràcters** amb posicions que comencen a 0, i que `text[0]` dona la primera lletra. Ara aprendràs a agafar **trossos** del text i a manipular-lo, igual que has fet amb les llistes a la unitat 6.

    | Lletra | P | y | t | h | o | n |
    | --- | --- | --- | --- | --- | --- | --- |
    | Índex | 0 | 1 | 2 | 3 | 4 | 5 |
    | Índex negatiu | -6 | -5 | -4 | -3 | -2 | -1 |

## Teoria

### 1. Talls de text: el *slicing*

Amb `text[inici:final]` agafem un tros del text, **des de `inici` fins a `final` sense incloure'l**:

```python
text = "Python"
print(text[0:2])     # Py
print(text[2:5])     # tho
```

Si ometem un dels dos valors, vol dir «des del principi» o «fins al final»:

| Expressió | Resultat | Comentari |
| --- | --- | --- |
| `text[:3]` | `Pyt` | Des del principi fins a la posició 3 (sense incloure-la) |
| `text[3:]` | `hon` | Des de la posició 3 fins al final |
| `text[-3:]` | `hon` | Les 3 últimes lletres |
| `text[:]` | `Python` | Tot el text |
| `text[::2]` | `Pto` | Una lletra de cada dues |
| `text[::-1]` | `nohtyP` | El text **invertit** |

El tercer valor opcional és el **pas**: `text[inici:final:pas]`. Un pas negatiu recorre el text cap enrere.

!!! tip "Per recordar"
    El *slicing* **no dona error** si et passes dels límits: `"Sol"[0:10]` dona simplement `"Sol"`. I funciona igual amb les llistes: `notes[1:3]` és una llista nova amb els elements de les posicions 1 i 2.

### 2. Mètodes de text

Els textos tenen mètodes, com les llistes. Els més útils:

| Mètode | Exemple | Resultat |
| --- | --- | --- |
| `upper()` | `"hola".upper()` | `"HOLA"` |
| `lower()` | `"HOLA".lower()` | `"hola"` |
| `capitalize()` | `"anna serra".capitalize()` | `"Anna serra"` |
| `title()` | `"anna serra".title()` | `"Anna Serra"` |
| `strip()` | `"  hola ".strip()` | `"hola"` (treu els espais dels extrems) |
| `replace(a, b)` | `"casa".replace("a", "e")` | `"cese"` |
| `count(x)` | `"banana".count("a")` | `3` |
| `find(x)` | `"banana".find("n")` | `2` (o `-1` si no hi és) |
| `startswith(x)` | `"Python".startswith("Py")` | `True` |
| `endswith(x)` | `"foto.png".endswith(".png")` | `True` |
| `isdigit()` | `"123".isdigit()` | `True` (només té xifres) |
| `isalpha()` | `"abc".isalpha()` | `True` (només té lletres) |

!!! danger "Els textos no es poden modificar"
    Els mètodes **no canvien** el text original: en **retornen un de nou**. Si vols conservar-lo, has de guardar-lo en una variable:

    ```python
    nom = "anna"
    nom.upper()            # No serveix de res: el resultat es perd
    nom = nom.upper()      # Així sí: ara nom val "ANNA"
    ```

    Tampoc pots canviar una lletra amb `nom[0] = "A"`: dona error. Per «canviar» una lletra, construeix un text nou: `nom = "A" + nom[1:]`.

**Encadenar mètodes.** Com que cada mètode retorna un text, en pots encadenar uns quants. És molt útil per **netejar el que escriu l'usuari**:

```python
resposta = input("Vols continuar (si/no)? ").strip().lower()
if resposta == "si":
    print("Continuem!")
```

Així tant `"SI"` com `"  Si "` són acceptats.

**Una aplicació pràctica.** Els catalans escrivim els decimals amb coma, i `float("3,5")` dona error. Ho podem resoldre amb `replace`:

```python
altura = float(input("Altura en metres: ").replace(",", "."))
```

### 3. `split` i `join`: de text a llista i a l'inrevés

`split()` talla un text en trossos i en fa una **llista**. Sense paràmetre, talla per espais; també pots indicar el separador:

```python
frase = "el cel és blau"
paraules = frase.split()
print(paraules)           # ['el', 'cel', 'és', 'blau']
print(len(paraules))      # 4

dades = "Anna,15,Girona"
print(dades.split(","))   # ['Anna', '15', 'Girona']
```

`join()` fa el camí invers: uneix els elements d'una llista (que han de ser **textos**) amb un separador:

```python
print(" ".join(["el", "cel", "és", "blau"]))    # el cel és blau
print("-".join(["01", "10", "2026"]))           # 01-10-2026
```

!!! tip "Per recordar"
    `split` i `join` són molt útils per **llegir línies de dades** d'un fitxer. Ho aprofitarem a l'extra de fitxers.

### 4. Construir un text nou amb un bucle

Podem anar «acumulant» lletres en un text buit, igual que acumulàvem nombres en una suma:

```python
text = "programació"
resultat = ""
for lletra in text:
    if lletra not in "aeiou":
        resultat += lletra
print(resultat)       # prgrmcó
```

Comença amb `""` (text buit), recorre el text original i va afegint amb `+=` només les lletres que volem.

### 5. Format amb f-strings

Dins de les claus d'una f-string, després de `:`, pots indicar com es mostra el valor:

| Format | Què fa | Exemple | Resultat |
| --- | --- | --- | --- |
| `:.2f` | 2 decimals | `f"{4.5:.2f}"` | `4.50` |
| `:<10` | Alinea a l'esquerra en 10 espais | `f"[{'Anna':<10}]"` | `[Anna      ]` |
| `:>8` | Alinea a la dreta en 8 espais | `f"[{15:>8}]"` | `[      15]` |

Per exemple, per fer una petita taula:

```python
print(f"{'Producte':<10}{'Preu':>8}")
print(f"{'Llapis':<10}{1.5:>8.2f}")
print(f"{'Goma':<10}{0.75:>8.2f}")
```

Mostra:

```text
Producte      Preu
Llapis        1.50
Goma          0.75
```

`:.2f` és, a més, la forma habitual de mostrar preus sense els decimals estranys que vam veure a la unitat 2.

## Exemples resolts

Copia'ls a Thonny, executa'ls i **modifica'ls** per veure què canvia.

**Exemple 1. Inicials**

```python
nom = input("Nom: ")
cognom = input("Cognom: ")
print(f"Inicials: {nom[0].upper()}{cognom[0].upper()}")
```

**Exemple 2. Entrada neta**

```python
resposta = input("T'agrada Python (si/no)? ").strip().lower()
if resposta == "si":
    print("Genial!")
else:
    print("Seguirem practicant")
```

**Exemple 3. Comptar paraules i trobar la més llarga**

```python
frase = input("Escriu una frase: ")
paraules = frase.split()
print(f"Té {len(paraules)} paraules")

llarga = paraules[0]
for paraula in paraules:
    if len(paraula) > len(llarga):
        llarga = paraula
print(f"La més llarga és {llarga}")
```

**Exemple 4. Palíndroms**

```python
paraula = input("Escriu una paraula o frase: ").lower().replace(" ", "")
if paraula == paraula[::-1]:
    print("És un palíndrom")
else:
    print("No és un palíndrom")
```

Prova-ho amb `anna`, `radar` i `python`.

**Exemple 5. Mostrar un preu**

```python
preu = float(input("Preu (pots escriure coma): ").replace(",", "."))
unitats = int(input("Unitats: "))
print(f"Total: {preu * unitats:.2f} €")
```

## Errors típics

!!! failure "Oblidar guardar el resultat d'un mètode (sense missatge d'error)"
    ```python
    nom = "anna"
    nom.upper()
    print(nom)
    ```

    - **Resultat:** mostra `anna`, no `ANNA`.
    - **Què vol dir:** els textos no es modifiquen; el mètode retorna un text nou que aquí es perd.
    - **Com es corregeix:** `nom = nom.upper()`.

!!! failure "Intentar canviar una lletra"
    ```python
    nom = "anna"
    nom[0] = "A"
    ```

    - **Missatge (similar a):** `TypeError: 'str' object does not support item assignment`
    - **Què vol dir:** els textos no es poden modificar posició a posició.
    - **Com es corregeix:** crea un text nou: `nom = "A" + nom[1:]`.

!!! failure "Un caràcter de més o de menys amb el *slicing* (sense missatge d'error)"
    ```python
    text = "Python"
    print(text[0:3])
    ```

    - **Resultat:** mostra `Pyt` (3 lletres), no `Pyth`.
    - **Què vol dir:** el límit final **no s'inclou**: `[0:3]` agafa les posicions 0, 1 i 2.
    - **Com es corregeix:** per agafar fins a la posició 3 inclosa, `text[0:4]`.

!!! failure "Oblidar els parèntesis del mètode (sense missatge d'error)"
    ```python
    nom = "anna"
    print(nom.upper)
    ```

    - **Resultat:** mostra una cosa com `<built-in method upper of str object at 0x...>`.
    - **Què vol dir:** sense parèntesis nomenes el mètode, però no l'executes.
    - **Com es corregeix:** `nom.upper()`.

!!! failure "Unir amb `join` elements que no són text"
    ```python
    nombres = [1, 2, 3]
    print(", ".join(nombres))
    ```

    - **Missatge (similar a):** `TypeError: sequence item 0: expected str instance, int found`
    - **Què vol dir:** `join` només uneix textos, i la llista té nombres.
    - **Com es corregeix:** converteix-los primer a text. Crea una llista nova amb un bucle, afegint-hi `str(n)` de cada element amb `append`, i fes el `join` d'aquesta llista.

## Activitats guiades

### Activitat 1. Prediu els talls

Quin resultat mostra cada línia?

```python
text = "programació"
print(text[0:3])
print(text[3:])
print(text[-4:])
print(text[::2])
print(text[::-1])
```

??? success "Solució"
    - `text[0:3]` → `pro`
    - `text[3:]` → `gramació`
    - `text[-4:]` → `ació`
    - `text[::2]` → `pormcó` (posicions 0, 2, 4, 6, 8 i 10)
    - `text[::-1]` → `óicamargorp`

### Activitat 2. Prediu els mètodes

```python
frase = "  Hola Pere  "
print(frase.strip())
print(frase.upper())
print(frase.replace("e", "3"))
print(len(frase))
print(frase.strip().split())
```

??? success "Solució"
    - `frase.strip()` → `Hola Pere`
    - `frase.upper()` → `  HOLA PERE  ` (els espais es mantenen)
    - `frase.replace("e", "3")` → `  Hola P3r3  `
    - `len(frase)` → `13` (els espais també compten)
    - `frase.strip().split()` → `['Hola', 'Pere']`

### Activitat 3. Corregeix el codi

Aquest programa té dos errors. Corregeix-los **un per un**.

```python
nom = "anna"
nom.upper()
print("Hola, " + nom)
nom[0] = "E"
print(nom)
```

??? success "Solució"
    ```python
    nom = "anna"
    nom = nom.upper()
    print("Hola, " + nom)
    nom = "E" + nom[1:]
    print(nom)
    ```

    Errors: (1) `nom.upper()` no guarda el resultat; cal `nom = nom.upper()`; (2) no es pot assignar a una posició d'un text (`nom[0] = "E"`); cal construir un text nou amb `"E" + nom[1:]`.

### Activitat 4. Completa el codi

Completa el programa, que mostra el nombre de paraules d'una frase i les paraules en ordre invers.

```python
frase = input("Escriu una frase: ")
paraules = frase.___()
print(f"Té {___(paraules)} paraules")
print(" ".___(paraules[::-1]))
```

??? success "Solució"
    ```python
    frase = input("Escriu una frase: ")
    paraules = frase.split()
    print(f"Té {len(paraules)} paraules")
    print(" ".join(paraules[::-1]))
    ```

    Amb la frase `el cel és blau` mostra `4` i `blau és cel el`.

### Activitat 5. Escriu-ho tu

Escriu un programa que demani un **nom complet** (per exemple, `anna serra puig`) i en mostri les **inicials en majúscula separades per punts** (`A.S.P.`).

??? success "Solució"
    ```python
    nom_complet = input("Nom complet: ")
    inicials = ""
    for paraula in nom_complet.split():
        inicials += paraula[0].upper() + "."
    print(inicials)
    ```

## Repte opcional

**Xifratge de Cèsar.** És un dels xifratges més antics: cada lletra es **desplaça 3 posicions** a l'alfabet (`a` → `d`, `b` → `e`... i `x` → `a`). Escriu un programa que demani un missatge en minúscules i en mostri la versió xifrada, deixant els espais com són.

*Pista:* investiga les funcions `ord(lletra)` (dona el codi numèric d'una lletra) i `chr(nombre)` (fa el camí invers), i fes servir l'operador `%` per «tornar a començar» l'alfabet.

## Xuleta

| Vull... | Escric... |
| --- | --- |
| Un tros de text | `text[2:5]` |
| Les últimes 3 lletres | `text[-3:]` |
| Invertir un text | `text[::-1]` |
| Passar a majúscules / minúscules | `text.upper()` / `text.lower()` |
| Treure els espais dels extrems | `text.strip()` |
| Substituir | `text.replace("a", "b")` |
| Comptar / cercar | `text.count("a")` / `text.find("a")` |
| Només xifres? | `text.isdigit()` |
| Text a llista de paraules | `frase.split()` |
| Llista a text | `" ".join(llista)` |
| Dos decimals | `f"{valor:.2f}"` |
