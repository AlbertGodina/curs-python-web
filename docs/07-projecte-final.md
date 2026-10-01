# Unitat 7. Projecte final

!!! abstract "Resum"
    **Sessions:** 2 · **Lliurament a Classroom:** `u7_cognom_nom.py`

    - **Sessió 1:** triar el projecte, planificar-lo i fer-ne la primera versió (apartats 1 a 3).
    - **Sessió 2:** ampliar-lo, provar-lo, depurar-lo i lliurar-lo (apartats 4 i 5).

## Objectius

En acabar aquesta unitat sabràs:

- Planificar un programa abans d'escriure'l: dades, funcions i estructura.
- Construir un programa **per versions**, començant per una de mínima que funcioni.
- Combinar tot el que has après: variables, `input`, condicionals, bucles, funcions i llistes.
- Provar el teu programa amb casos diferents i depurar-lo.
- Explicar què has fet i què has après.

## Punt de partida

!!! question "Ho recordes?"
    Resoldre un problema gran amb un algorisme sempre segueix els mateixos passos que ja has practicat sense ordinador: **entendre** què es demana, **dividir-lo** en parts més petites, **dissenyar** cada part i **comprovar** que funciona.

    En aquest projecte farem exactament això, però amb un programa teu, de principi a fi. No hi ha cap codi nou per aprendre: **tot el que necessites ja ho saps**.

## Projectes a triar

Tria **un** dels projectes següents (o proposa'n un de teu, que haurà de ser aprovat pel professorat). Cada projecte té un **mínim** que has de fer i unes **ampliacions** per anar més lluny.

!!! example "Projecte A. Endevina el nombre"
    L'ordinador pensa un nombre i tu l'has d'endevinar.

    **Mínim**

    - L'ordinador tria un nombre secret entre 1 i 100 (amb `random.randint`).
    - L'usuari té un màxim de **7 intents**. Després de cada intent, el programa diu `Massa alt`, `Massa baix` o `Encertat!`.
    - Si s'acaben els intents, mostra el nombre secret.

    **Ampliacions**

    - Nivells de dificultat (rang de nombres i nombre d'intents diferents).
    - Guardar en una llista els intents d'una partida i mostrar-los al final.
    - Jugar diverses partides seguides amb un marcador (partides guanyades i perdudes).

!!! example "Projecte B. Pedra, paper, tisores"
    L'usuari juga contra l'ordinador.

    **Mínim**

    - L'ordinador tria a l'atzar entre `pedra`, `paper` i `tisores` (`random.choice`).
    - L'usuari escriu la seva jugada (validada) i el programa diu qui guanya la ronda.
    - Es juga fins que algú arriba a 3 victòries, amb un marcador visible.

    **Ampliacions**

    - Guardar l'historial de rondes en una llista i mostrar-lo al final.
    - Estadístiques: percentatge de rondes guanyades, empatades i perdudes.
    - Permetre triar a quantes victòries es juga.

!!! example "Projecte C. Gestor de tasques"
    Una llista de coses per fer, amb un menú.

    **Mínim**

    - Menú amb les opcions: **afegir** una tasca, **veure** les tasques (numerades), **eliminar** una tasca i **sortir**.
    - Les tasques es guarden en una llista.
    - Controla els casos límit: no es pot eliminar si la llista és buida, ni triar un número que no existeix.

    **Ampliacions**

    - Marcar tasques com a fetes (amb una segona llista paral·lela).
    - Mostrar quantes tasques queden pendents.
    - Ordenar les tasques alfabèticament.

!!! example "Projecte D. Mini qüestionari"
    Un test amb preguntes i puntuació.

    **Mínim**

    - Almenys **5 preguntes** guardades en una llista, amb les seves respostes en una altra llista (llistes paral·leles).
    - El programa fa les preguntes, comprova les respostes i compta els encerts.
    - Al final mostra la puntuació i un missatge diferent segons el resultat.

    **Ampliacions**

    - Preguntes amb opcions (`a`, `b`, `c`) i validació de la resposta.
    - Ordre aleatori de les preguntes amb `random.shuffle(llista)`.
    - Poder repetir el test sense tornar a obrir el programa.

!!! example "Projecte E. Inventari d'una botiga"
    Control d'estoc amb un menú.

    **Mínim**

    - Dues llistes paral·leles: els **productes** i les **unitats en estoc** de cada un.
    - Menú: **veure l'inventari**, **afegir** un producte nou, **vendre** unitats (restant-les de l'estoc, sense deixar-lo en negatiu) i **sortir**.

    **Ampliacions**

    - Una tercera llista amb els **preus** i el valor total de l'inventari.
    - Avisar quan l'estoc d'un producte és baix.
    - Cercar un producte pel nom.

!!! example "Projecte F. Proposta pròpia"
    Pots plantejar un projecte diferent, **sempre que ho consensuïs abans amb el professorat** i que compleixi els requisits mínims del lliurament (més avall).

## Com construir un projecte

### 1. Planifica abans de programar

Abans d'escriure codi, escriu un **pla** en comentaris al començament del fitxer. Així saps què has de fer i en quin ordre:

```python
# PROJECTE: Gestor de tasques
# Què fa: permet afegir, veure i eliminar tasques d'una llista
# Dades: tasques (llista de text)
# Funcions previstes:
#   - mostra_menu(): imprimeix les opcions
#   - afegeix_tasca(tasques): demana el text i l'afegeix a la llista
#   - mostra_tasques(tasques): mostra les tasques numerades
#   - elimina_tasca(tasques): demana un número i elimina la tasca
# Programa principal (pseudocodi):
#   mentre l'usuari no triï sortir:
#       mostrar el menú i demanar l'opció
#       cridar la funció que correspongui
```

### 2. Construeix-lo per versions

No intentis fer-ho tot d'un cop. Avança en passos petits, **provant cada pas**:

1. **Versió 1: el mínim que funciona.** Pot ser poc elegant i tenir poques funcions, però ha de funcionar.
2. **Versió 2: ordena-ho.** Separa el codi en funcions, afegeix el menú i valida les entrades.
3. **Versió 3: amplia'l.** Només quan la versió 2 funcioni, afegeix les ampliacions.

!!! tip "Per recordar"
    Primer fes que **funcioni**; després fes que sigui **ordenat**; després fes que sigui **més complet**. Si trenques alguna cosa, torna al darrer pas que funcionava.

### 3. Patrons que et poden servir

**Menú amb un bucle.** Un esquelet que serveix per als projectes C, D i E:

```python
def mostra_menu():
    print()
    print("=== MENÚ ===")
    print("1. Opció 1")
    print("2. Opció 2")
    print("0. Sortir")

opcio = -1
while opcio != 0:
    mostra_menu()
    opcio = int(input("Tria una opció: "))
    if opcio == 1:
        print("Has triat l'opció 1")
    elif opcio == 2:
        print("Has triat l'opció 2")
    elif opcio == 0:
        print("Adéu!")
    else:
        print("Opció no vàlida")
```

**Llistes paral·leles.** Dues llistes on la **mateixa posició** correspon al mateix element:

```python
productes = ["llapis", "goma", "regle"]
estoc = [20, 15, 8]

for i in range(len(productes)):
    print(f"{productes[i]}: {estoc[i]} unitats")
```

Per trobar la posició d'un valor, fes servir `llista.index(valor)`. Dona error si el valor no hi és, així que comprova-ho abans amb `in`:

```python
nom = input("Producte: ")
if nom in productes:
    posicio = productes.index(nom)
    print(f"Estoc: {estoc[posicio]}")
```

**Aleatorietat.** `random.randint(1, 100)` tria un nombre; `random.choice(llista)` en tria un element, i `random.shuffle(llista)` barreja una llista.

**Validar entrades.** Reutilitza la funció `demana_enter(missatge, minim, maxim)` de la unitat 5.

## Exemple resolt

Fixa't com es construeix un projecte per versions. Aquest és un **simulador de daus** (no és cap dels projectes que pots triar): tira un dau moltes vegades i compta quantes vegades surt cada cara.

**Versió 1: el mínim que funciona**

```python
import random

n = int(input("Quantes tirades? "))
comptadors = [0, 0, 0, 0, 0, 0]
for i in range(n):
    cara = random.randint(1, 6)
    comptadors[cara - 1] += 1

for i in range(len(comptadors)):
    print(f"Cara {i + 1}: {comptadors[i]}")
```

Funciona, però tot està barrejat i no es valida l'entrada.

**Versió 2: amb funcions, validació, menú i percentatges**

```python
import random

# --- Funcions ---
def demana_enter(missatge, minim, maxim):
    n = int(input(missatge))
    while n < minim or n > maxim:
        print(f"Ha de ser un nombre entre {minim} i {maxim}")
        n = int(input(missatge))
    return n

def tira_dau(tirades):
    # Retorna una llista amb les vegades que ha sortit cada cara
    # (la posició 0 correspon a la cara 1)
    comptadors = [0, 0, 0, 0, 0, 0]
    for i in range(tirades):
        cara = random.randint(1, 6)
        comptadors[cara - 1] += 1
    return comptadors

def mostra_resultats(comptadors):
    total = sum(comptadors)
    for i in range(len(comptadors)):
        percentatge = round(comptadors[i] / total * 100, 1)
        print(f"Cara {i + 1}: {comptadors[i]} vegades ({percentatge} %)")

def mostra_menu():
    print()
    print("=== SIMULADOR DE DAUS ===")
    print("1. Fer una simulació")
    print("0. Sortir")

# --- Programa principal ---
opcio = -1
while opcio != 0:
    mostra_menu()
    opcio = demana_enter("Tria una opció: ", 0, 1)
    if opcio == 1:
        tirades = demana_enter("Quantes tirades (1-10000)? ", 1, 10000)
        resultats = tira_dau(tirades)
        mostra_resultats(resultats)

print("Adéu!")
```

Observa que **cada funció fa una sola cosa** i que el programa principal queda curt i fàcil de llegir.

## Problemes habituals

!!! failure "El programa és gran i no funciona, i no saps on és l'error"
    - **Què passa:** has escrit molt codi seguit i no l'has anat provant.
    - **Com es resol:** aïlla el problema. Comenta parts del programa, fes servir `print` de seguiment i el **depurador de Thonny** (**Ctrl+F5**, **F6** i **F7**). I recorda: **prova cada funció per separat** abans de provar-ho tot junt.

!!! failure "`NameError` dins d'una funció"
    - **Missatge (similar a):** `NameError: name 'tasques' is not defined`
    - **Què vol dir:** la funció fa servir una variable del programa principal, però les variables d'una funció són locals.
    - **Com es corregeix:** passa-la com a **paràmetre**: `def mostra_tasques(tasques):`.

!!! failure "El menú no s'acaba mai (sense missatge d'error)"
    - **Què passa:** la variable de la condició del `while` no canvia, o la comprovació de l'opció de sortida és incorrecta.
    - **Com es corregeix:** comprova que la variable que controla el bucle (`opcio`) es torna a demanar a cada volta.

!!! failure "`ValueError` si l'usuari escriu text"
    - **Missatge (similar a):** `ValueError: invalid literal for int() with base 10: 'hola'`
    - **Què vol dir:** `int()` no pot convertir un text que no sigui un nombre.
    - **Com es corregeix:** per al projecte **no cal** controlar-ho (assumeix que l'usuari escriu nombres quan toca). Si t'interessa, més endavant hi ha un apartat d'**Extres** sobre `try/except`.

## Lliurament (Classroom)

!!! example "Què has de lliurar"
    **Fitxer:** `u7_cognom_nom.py`

    **Capçalera ampliada.** A més del nom, la data i la unitat, afegeix el **nom del projecte**, una **descripció breu** (2-3 línies) i **com s'utilitza**.

    **Requisits mínims** (a més del mínim del projecte que hagis triat):

    1. Almenys **3 funcions pròpies amb paràmetres**, i almenys una que retorni un valor.
    2. Almenys **una llista**.
    3. Almenys un bucle `for` i un bucle `while`.
    4. Condicionals (`if`/`elif`/`else`).
    5. **Validació** d'almenys una entrada de l'usuari.
    6. Interacció que es repeteix (un menú, rondes, partides...).
    7. Estructura ordenada: primer els `import`, després les funcions i al final el programa principal.
    8. Noms de variables i funcions clars, i comentaris que expliquin les parts importants.

    **Reflexió final.** Al final del fitxer, en comentaris, respon aquestes tres preguntes (1-2 línies cadascuna):

    ```python
    # REFLEXIÓ
    # 1. Què ha estat el més difícil del projecte?
    # 2. Quin error t'ha costat més de trobar i com l'has resolt?
    # 3. Què milloraries si tinguessis més temps?
    ```

    **Abans de lliurar, comprova que:**

    1. El programa s'executa de principi a fi sense errors.
    2. Has provat tots els camins possibles (cada opció del menú, valors límit, entrades no vàlides).
    3. Al fitxer hi ha el pla inicial (apartat 1) o una descripció clara de què fa.
    4. Has esborrat els `print` de depuració.

### Rúbrica orientativa

| Criteri | A. Excel·lent | A. Notable | A. Satisfactori | No Assoliment |
| --- | --- | --- | --- | --- |
| **Funcionament** | Fa tot el que demana el projecte i alguna ampliació, sense errors | Fa tot el mínim sense errors | Fa gairebé tot el mínim, amb algun error | No funciona o falta bona part del mínim |
| **Estructura i funcions** | Funcions ben dividides (una tasca cada una) i programa principal curt | Funcions correctes, algun bloc massa llarg | Poques funcions o poc útils | Tot el codi seguit, sense funcions |
| **Ús dels conceptes** | Combina llistes, bucles i condicionals amb criteri | Usa tots els requisits mínims | Falta algun requisit mínim | Falten diversos requisits |
| **Proves i robustesa** | Valida les entrades i controla els casos límit | Valida les entrades principals | Validació parcial | Cap validació |
| **Claredat** | Noms clars, comentaris útils, reflexió completa | Codi clar i reflexió feta | Codi poc clar o reflexió incompleta | Sense comentaris ni reflexió |

## Repte opcional

**Prova creuada.** Quan acabis, passa el teu programa a un company o companya perquè el provi **sense dir-li com funciona**. Que t'anoti: (1) què no ha entès, (2) algun error que ha trobat i (3) una idea per millorar-lo. Després, arregla'n almenys un.

## Xuleta

| Vull... | Escric... |
| --- | --- |
| Un menú que es repeteix | `while opcio != 0:` + `if/elif/else` |
| Validar un enter en un interval | `demana_enter(missatge, minim, maxim)` |
| Un nombre aleatori | `random.randint(1, 100)` |
| Triar un element a l'atzar | `random.choice(llista)` |
| Barrejar una llista | `random.shuffle(llista)` |
| Posició d'un valor en una llista | `llista.index(valor)` (comprova abans amb `in`) |
| Dues llistes paral·leles | `noms[i]` i `edats[i]` |
| Comptar partides o encerts | `comptador += 1` |
| Depurar pas a pas | **Ctrl+F5**, **F6**, **F7** a Thonny |
