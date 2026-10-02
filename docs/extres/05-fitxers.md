# Extra 5. Fitxers

!!! abstract "Resum"
    **Tipus:** ampliació opcional · **Requisits:** unitats 4, 5 i 6, i els extres de gestió d'errors i de text · **Sense lliurament:** fes les activitats i comprova-les amb les solucions.

## Objectius

En acabar aquest extra sabràs:

- **Guardar** dades en un fitxer de text i **recuperar-les** quan torni a començar el programa.
- Obrir fitxers amb `with open(...)` en els modes lectura (`"r"`), escriptura (`"w"`) i afegir (`"a"`).
- Llegir un fitxer línia a línia i netejar-ne les línies.
- Controlar el cas en què el fitxer no existeix.
- Guardar i llegir dades amb diversos camps (format CSV).

## Punt de partida

!!! question "Ho recordes?"
    Fins ara, quan el programa acabava, **totes les dades desapareixien**: les variables, les llistes i els diccionaris només viuen a la memòria mentre el programa s'executa. Per això el gestor de tasques del projecte final començava sempre buit.

    Per aconseguir que un programa **recordi** les dades, les hem de guardar en un **fitxer** al disc. A això se li diu **persistència**. És com passar a net el que tens a la memòria en un quadern.

## Teoria

### 1. Escriure en un fitxer

```python
with open("noms.txt", "w", encoding="utf-8") as fitxer:
    fitxer.write("Anna\n")
    fitxer.write("Pere\n")
```

Aquest programa crea el fitxer `noms.txt` amb dues línies. Què fa cada part:

- `open("noms.txt", "w", encoding="utf-8")` obre el fitxer. Té tres dades: el **nom**, el **mode** i la **codificació**.
- `with ... as fitxer:` obre el fitxer i el **tanca automàticament** en acabar el bloc. Dins del bloc l'anomenem `fitxer`.
- `fitxer.write(text)` escriu un text. **No salta de línia sol**: l'hem de posar nosaltres amb `\n`.
- `encoding="utf-8"` assegura que els accents i la `ç` es guardin bé. Posa-ho sempre.

Els **modes** més habituals:

| Mode | Què fa | Atenció |
| --- | --- | --- |
| `"r"` | Llegeix el fitxer | Dona error si no existeix |
| `"w"` | Escriu en un fitxer nou | **Esborra tot el contingut anterior** si ja existia |
| `"a"` | Afegeix al final del fitxer | Si no existeix, el crea |

!!! warning "El mode `w` esborra"
    Si obres un fitxer existent amb `"w"`, es buida immediatament. Si vols **afegir** dades sense perdre les que hi ha, fes servir `"a"`.

!!! info "On es desa el fitxer?"
    Si només escrius el nom (`"noms.txt"`), es crea a la mateixa carpeta que el programa. Per això, a Thonny, **desa primer el programa** i després executa'l. Allà trobaràs el fitxer.

`write` només accepta **text**. Si vols escriure un nombre, convertint-lo abans: `fitxer.write(str(15))` o amb una f-string.

### 2. Llegir un fitxer

Per llegir tot el contingut d'un cop:

```python
with open("noms.txt", "r", encoding="utf-8") as fitxer:
    contingut = fitxer.read()
print(contingut)
```

Però el més habitual és recórrer el fitxer **línia a línia** amb un `for`:

```python
with open("noms.txt", "r", encoding="utf-8") as fitxer:
    for linia in fitxer:
        print(linia.strip())
```

Cada línia llegida **inclou el salt de línia final** (`"Anna\n"`). Per això hi apliquem `strip()`, que vas veure a l'extra de text: sense ell, el `print` deixaria una línia en blanc entre cada nom, i comparacions com `linia == "Anna"` serien falses.

### 3. Si el fitxer no existeix

Obrir amb `"r"` un fitxer que no hi és dona un `FileNotFoundError`. Amb el que vas aprendre a l'extra de gestió d'errors, ho podem controlar:

```python
try:
    with open("noms.txt", "r", encoding="utf-8") as fitxer:
        for linia in fitxer:
            print(linia.strip())
except FileNotFoundError:
    print("Encara no hi ha cap fitxer de noms")
```

### 4. Guardar i recuperar una llista

Un patró molt útil és tenir dues funcions: una que **guarda** una llista en un fitxer (un element per línia) i una altra que la **carrega**. Si el fitxer no existeix, la càrrega retorna una llista buida:

```python
def guarda_llista(nom_fitxer, llista):
    with open(nom_fitxer, "w", encoding="utf-8") as fitxer:
        for element in llista:
            fitxer.write(element + "\n")

def carrega_llista(nom_fitxer):
    llista = []
    try:
        with open(nom_fitxer, "r", encoding="utf-8") as fitxer:
            for linia in fitxer:
                llista.append(linia.strip())
    except FileNotFoundError:
        print("Encara no hi ha cap fitxer: començo amb una llista buida")
    return llista
```

L'ús habitual en un programa és: **carregar** les dades en començar, treballar amb elles i **guardar-les** en acabar (o cada cop que canvien).

### 5. Dades amb diversos camps: CSV

Per guardar registres amb diverses dades (nom, edat, nota), cada línia pot tenir els **camps separats per comes**. Aquest format s'anomena **CSV** i es pot obrir també amb Excel o un full de càlcul.

```text
Anna,15,8
Pere,16,5
```

Per **escriure**, fem servir una f-string. Per **llegir**, `split(",")` separa els camps i el desempaquetat els reparteix en variables. Recorda convertir els nombres, perquè es llegeixen com a text:

```python
linia = "Anna,15,8"
nom, edat, nota = linia.strip().split(",")
edat = int(edat)
nota = int(nota)
```

!!! tip "Per recordar"
    Si el text pot contenir comes (per exemple, una adreça), tria un altre separador, com `;`.

## Exemples resolts

Copia'ls a Thonny, **desa el programa** i executa'ls. Després obre el fitxer que s'ha creat per veure'n el contingut.

**Exemple 1. Desar noms en un fitxer**

```python
with open("noms.txt", "w", encoding="utf-8") as fitxer:
    nom = input("Nom (fi per acabar): ")
    while nom != "fi":
        fitxer.write(nom + "\n")
        nom = input("Nom (fi per acabar): ")
print("Noms desats!")
```

**Exemple 2. Llegir-los i numerar-los**

```python
try:
    with open("noms.txt", "r", encoding="utf-8") as fitxer:
        numero = 1
        for linia in fitxer:
            print(f"{numero}. {linia.strip()}")
            numero += 1
except FileNotFoundError:
    print("Primer has d'executar l'exemple anterior")
```

**Exemple 3. Un diari: afegir sense esborrar**

```python
frase = input("Què vols apuntar? ")
with open("diari.txt", "a", encoding="utf-8") as fitxer:
    fitxer.write(frase + "\n")
```

Executa'l diverses vegades i comprova que cada frase s'afegeix al final.

**Exemple 4. Notes en format CSV**

```python
alumnes = [("Anna", 8), ("Pere", 5), ("Marta", 9)]

# Escriure
with open("notes.csv", "w", encoding="utf-8") as fitxer:
    for nom, nota in alumnes:
        fitxer.write(f"{nom},{nota}\n")

# Llegir i calcular la mitjana
total = 0
quantitat = 0
with open("notes.csv", "r", encoding="utf-8") as fitxer:
    for linia in fitxer:
        nom, nota = linia.strip().split(",")
        total += int(nota)
        quantitat += 1
print(f"Mitjana: {round(total / quantitat, 2)}")
```

**Exemple 5. Una llista de tasques que es recorda**

```python
def guarda_llista(nom_fitxer, llista):
    with open(nom_fitxer, "w", encoding="utf-8") as fitxer:
        for element in llista:
            fitxer.write(element + "\n")

def carrega_llista(nom_fitxer):
    llista = []
    try:
        with open(nom_fitxer, "r", encoding="utf-8") as fitxer:
            for linia in fitxer:
                llista.append(linia.strip())
    except FileNotFoundError:
        print("Encara no hi ha cap fitxer: començo amb una llista buida")
    return llista

# --- Programa principal ---
tasques = carrega_llista("tasques.txt")
print(f"Tens {len(tasques)} tasques guardades")

nova = input("Nova tasca (Intro per no afegir res): ")
if nova != "":
    tasques.append(nova)
    guarda_llista("tasques.txt", tasques)

for tasca in tasques:
    print("-", tasca)
```

Executa'l diverses vegades: **les tasques sobreviuen** d'una execució a l'altra.

## Errors típics

!!! failure "Obrir un fitxer que no existeix"
    ```python
    with open("dades.txt", "r", encoding="utf-8") as fitxer:
        print(fitxer.read())
    ```

    - **Missatge (similar a):** `FileNotFoundError: [Errno 2] No such file or directory: 'dades.txt'`
    - **Què vol dir:** Python no troba el fitxer a la carpeta del programa.
    - **Com es corregeix:** comprova el nom i que el fitxer és a la mateixa carpeta que el programa (i que has desat el programa abans d'executar-lo). Si el fitxer pot no existir, controla-ho amb `try/except`.

!!! failure "Perdre les dades amb el mode `w` (sense missatge d'error)"
    ```python
    with open("diari.txt", "w", encoding="utf-8") as fitxer:
        fitxer.write("Nova frase\n")
    ```

    - **Resultat:** el fitxer només conté l'última frase; les anteriors s'han esborrat.
    - **Què vol dir:** `"w"` buida el fitxer cada vegada que l'obres.
    - **Com es corregeix:** fes servir el mode `"a"` per afegir al final.

!!! failure "Oblidar el salt de línia (sense missatge d'error)"
    ```python
    with open("noms.txt", "w", encoding="utf-8") as fitxer:
        fitxer.write("Anna")
        fitxer.write("Pere")
    ```

    - **Resultat:** el fitxer té una sola línia: `AnnaPere`.
    - **Què vol dir:** `write` no afegeix cap salt de línia.
    - **Com es corregeix:** `fitxer.write("Anna\n")`.

!!! failure "Escriure un nombre directament"
    ```python
    with open("edats.txt", "w", encoding="utf-8") as fitxer:
        fitxer.write(15)
    ```

    - **Missatge (similar a):** `TypeError: write() argument must be str, not int`
    - **Què vol dir:** `write` només accepta text.
    - **Com es corregeix:** `fitxer.write(str(15))` o `fitxer.write(f"{15}\n")`.

!!! failure "Llegir fora del bloc `with`"
    ```python
    with open("noms.txt", "r", encoding="utf-8") as fitxer:
        print("Fitxer obert")
    print(fitxer.read())
    ```

    - **Missatge (similar a):** `ValueError: I/O operation on closed file.`
    - **Què vol dir:** en acabar el bloc `with`, el fitxer es tanca automàticament.
    - **Com es corregeix:** fes tot el que necessitis del fitxer **dins** del bloc `with`, o guarda el contingut en una variable abans de sortir.

!!! failure "No netejar les línies llegides (sense missatge d'error)"
    ```python
    with open("noms.txt", "r", encoding="utf-8") as fitxer:
        for linia in fitxer:
            if linia == "Anna":
                print("Hi ha l'Anna")
    ```

    - **Resultat:** no mostra mai res, encara que «Anna» sigui al fitxer.
    - **Què vol dir:** la línia llegida és `"Anna\n"`, que no és igual a `"Anna"`.
    - **Com es corregeix:** `if linia.strip() == "Anna":`.

## Activitats guiades

### Activitat 1. Prediu el contingut del fitxer

Quin contingut tindrà `prova.txt` en acabar el programa?

```python
with open("prova.txt", "w", encoding="utf-8") as fitxer:
    fitxer.write("un\n")
    fitxer.write("dos")
    fitxer.write("tres\n")

with open("prova.txt", "a", encoding="utf-8") as fitxer:
    fitxer.write("quatre\n")
```

??? success "Solució"
    ```text
    un
    dostres
    quatre
    ```

    A «dos» li falta el `\n`, així que «tres» s'escriu enganxat a la mateixa línia. El segon bloc, en mode `"a"`, afegeix «quatre» al final sense esborrar res.

### Activitat 2. Prediu la lectura

Si `prova.txt` té el contingut de l'activitat anterior, què mostra aquest programa? Com podries evitar-ho?

```python
with open("prova.txt", "r", encoding="utf-8") as fitxer:
    for linia in fitxer:
        print(linia)
```

??? success "Solució"
    Mostra cada línia seguida d'una **línia en blanc**: `un`, línia buida, `dostres`, línia buida, `quatre`, línia buida. Passa perquè cada línia llegida ja porta un `\n` i `print` n'afegeix un altre.

    Es resol amb `print(linia.strip())` o amb `print(linia, end="")`.

### Activitat 3. Corregeix el codi

Aquest programa hauria de crear `edats.txt` amb les línies `Anna,15` i `Pere,16`. Té dos errors. Corregeix-los **un per un**.

```python
nom1, edat1 = "Anna", 15
nom2, edat2 = "Pere", 16
with open("edats.txt", "w", encoding="utf-8") as fitxer:
    fitxer.write(nom1 + edat1)
    fitxer.write(nom2 + edat2)
```

??? success "Solució"
    ```python
    nom1, edat1 = "Anna", 15
    nom2, edat2 = "Pere", 16
    with open("edats.txt", "w", encoding="utf-8") as fitxer:
        fitxer.write(f"{nom1},{edat1}\n")
        fitxer.write(f"{nom2},{edat2}\n")
    ```

    Errors: (1) `nom1 + edat1` uneix un text i un nombre, i dona `TypeError`; una f-string ho resol; (2) faltaven la coma de separació entre camps i el salt de línia al final de cada registre.

### Activitat 4. Completa el codi

Completa el programa, que compta quantes vegades apareix «Anna» al fitxer `noms.txt`.

```python
comptador = 0
with open("noms.txt", "___", encoding="utf-8") as fitxer:
    for linia in fitxer:
        nom = linia.___()
        if nom == "Anna":
            comptador += 1
print(comptador)
```

??? success "Solució"
    ```python
    comptador = 0
    with open("noms.txt", "r", encoding="utf-8") as fitxer:
        for linia in fitxer:
            nom = linia.strip()
            if nom == "Anna":
                comptador += 1
    print(comptador)
    ```

    Cal el mode `"r"` per llegir, i `strip()` per treure el `\n` final abans de comparar.

### Activitat 5. Escriu-ho tu (escriure)

Escriu un programa que demani frases fins que l'usuari escrigui `fi`, les **afegeixi** a `frases.txt` i, al final, mostri **quantes línies** té el fitxer.

??? success "Solució"
    ```python
    frase = input("Frase (fi per acabar): ")
    with open("frases.txt", "a", encoding="utf-8") as fitxer:
        while frase != "fi":
            fitxer.write(frase + "\n")
            frase = input("Frase (fi per acabar): ")

    total = 0
    with open("frases.txt", "r", encoding="utf-8") as fitxer:
        for linia in fitxer:
            total += 1
    print(f"El fitxer té {total} línies")
    ```

### Activitat 6. Escriu-ho tu (llegir un CSV)

Suposant que existeix `notes.csv` (amb línies com `Anna,8`, com a l'exemple 4), escriu un programa que mostri **qui té la millor nota**. Si el fitxer no existeix, ha d'avisar l'usuari en lloc de petar.

??? success "Solució"
    ```python
    try:
        with open("notes.csv", "r", encoding="utf-8") as fitxer:
            millor_nom = ""
            millor_nota = -1
            for linia in fitxer:
                nom, nota = linia.strip().split(",")
                nota = int(nota)
                if nota > millor_nota:
                    millor_nota = nota
                    millor_nom = nom
        print(f"Millor nota: {millor_nom} ({millor_nota})")
    except FileNotFoundError:
        print("No existeix el fitxer notes.csv")
    ```

## Repte opcional

**Una agenda que es recorda.** Fes una agenda de contactes amb un **diccionari** (`nom: telèfon`) que es guardi en un fitxer. Al començar, ha de **carregar** els contactes del fitxer (si existeix); amb un menú, l'usuari pot afegir contactes, consultar-ne un i veure'ls tots; i en sortir, ha de **guardar-los** de nou.

*Pista:* guarda cada contacte en una línia amb el format `nom,telèfon`, i en carregar-los fes servir `split(",")` per separar-los.

## Xuleta

| Vull... | Escric... |
| --- | --- |
| Escriure (esborrant) | `with open("f.txt", "w", encoding="utf-8") as f:` |
| Afegir al final | `with open("f.txt", "a", encoding="utf-8") as f:` |
| Llegir | `with open("f.txt", "r", encoding="utf-8") as f:` |
| Escriure una línia | `f.write(text + "\n")` |
| Llegir tot el fitxer | `f.read()` |
| Recórrer les línies | `for linia in f:` |
| Treure el salt de línia | `linia.strip()` |
| Separar els camps d'una línia CSV | `linia.strip().split(",")` |
| Controlar que no existeixi | `except FileNotFoundError:` |
