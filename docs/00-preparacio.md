# Unitat 0. Preparació de l'entorn

!!! abstract "Resum"
    **Sessions:** 1 · **Lliurament a Classroom:** `u0_cognom_nom.py`

## Objectius

En acabar aquesta unitat sabràs:

- Explicar què és Python i per a què serveix.
- Obrir Thonny i reconèixer-ne les parts principals.
- Escriure, desar i executar el teu primer programa.
- Llegir un missatge d'error senzill i corregir-lo.
- Posar nom als fitxers i escriure comentaris seguint les convencions del curs.

## Punt de partida

!!! question "Ho recordes?"
    Quan treballàveu amb activitats desendollades, escriviu **instruccions ordenades i sense ambigüitats** (per exemple, per dibuixar a la quadrícula). Un programa és exactament això, però escrit en un llenguatge que l'ordinador entén.

    Compara el pseudocodi i Python:

    | Pseudocodi | Python |
    | --- | --- |
    | `Escriu "Hola"` | `print("Hola")` |

    Python s'assembla molt al pseudocodi: per això és un bon primer llenguatge.

## Teoria

### 1. Què és Python?

Python és un **llenguatge de programació** d'alt nivell: està pensat perquè els humans el puguem llegir i escriure amb facilitat. És **interpretat**, és a dir, l'ordinador executa el programa línia a línia, de dalt a baix. Es fa servir en ciència de dades, automatització, desenvolupament web i intel·ligència artificial.

### 2. Thonny, el nostre editor

Farem servir **Thonny**, un editor pensat per aprendre. Ja porta Python incorporat, així que **només cal instal·lar Thonny** (a [thonny.org](https://thonny.org)) i no cal instal·lar Python a part.

Quan l'obres, veuràs dues zones principals:

| Zona | On és | Per a què serveix |
| --- | --- | --- |
| **Editor** | A dalt | Escrius i desas els teus programes (fitxers `.py`). |
| **Shell** | A baix | Aquí apareix el resultat del programa i també pots provar instruccions soltes. |

També tens el botó verd **▶ Executa** (o la tecla **F5**) per fer córrer el programa.

!!! tip "Veure les variables"
    Al menú **Visualitza → Variables** (*View → Variables* si Thonny està en anglès) s'obre un panell que et mostra què guarda el programa en cada moment. Ens serà molt útil a partir de la unitat 1.

### 3. El primer programa

```python
print("Hola, món!")
```

- `print` és una **funció**: una ordre que mostra alguna cosa per pantalla.
- Els **parèntesis** `( )` envolten el que volem mostrar.
- Les **cometes** `" "` indiquen que és text.

Per executar-lo:

1. Escriu el codi a l'editor.
2. Desa el fitxer: **Fitxer → Desa com...** i posa-li un nom, per exemple `u0_hola.py`.
3. Prem **▶ Executa**.
4. Mira el resultat a la **Shell**.

!!! tip "Per recordar"
    L'editor és per als programes que vols desar; la Shell és per veure resultats i fer proves ràpides que no es guarden.

### 4. Convencions del curs

**Noms de fitxer**

- Sempre acaben en `.py`.
- En minúscules, **sense espais, accents ni caràcters especials**: `u0_hola.py` ✅, `Unitat 0 Hola!.py` ❌.

**Comentaris.** Tot el que va després d'un `#` és una nota per als humans: Python l'ignora.

```python
# Aquest programa saluda l'usuari
print("Hola, món!")   # Això també és un comentari
```

**Capçalera.** Tots els fitxers que lliuris començaran així:

```python
# Nom i cognoms: Anna Serra
# Data: 15/10/2026
# Unitat 0 - Lliurament
```

**Indentació.** En Python, els espais al començament d'una línia **tenen significat**. De moment no n'usarem, així que cada línia comença a la primera columna. A la unitat 3 veurem per què és tan important.

## Exemples resolts

Copia'ls a Thonny, executa'ls i **modifica'ls** per veure què canvia.

**Exemple 1. Diverses línies**

```python
print("Bon dia")
print("Això és Python")
print("Ens veiem a classe")
```

Python executa les instruccions **en ordre**, una darrere l'altra.

**Exemple 2. Una línia buida**

```python
print("Primera part")
print()
print("Segona part")
```

`print()` sense res dins mostra una línia en blanc.

**Exemple 3. Text amb cometes simples o dobles**

```python
print("Hola")
print('Hola')
```

Tots dos donen el mateix resultat. Tria'n un i **sigues coherent**.

## Errors típics

Equivocar-se és normal, i és la millor manera d'aprendre. Quan Python troba un error, t'ho diu a la Shell: mira sempre **el número de línia** i **la darrera frase** del missatge.

!!! failure "Falta tancar les cometes"
    ```python
    print("Hola, món!)
    ```

    - **Missatge (similar a):** `SyntaxError: unterminated string literal (detected at line 1)`
    - **Què vol dir:** has obert un text amb cometes però no l'has tancat.
    - **Com es corregeix:** afegeix les cometes que falten: `print("Hola, món!")`.

!!! failure "`print` mal escrit"
    ```python
    Print("Hola")
    ```

    - **Missatge (similar a):** `NameError: name 'Print' is not defined`
    - **Què vol dir:** Python no coneix cap ordre anomenada `Print`. Distingeix **majúscules i minúscules**.
    - **Com es corregeix:** `print("Hola")`.

!!! failure "Falten els parèntesis"
    ```python
    print "Hola"
    ```

    - **Missatge (similar a):** `SyntaxError: Missing parentheses in call to 'print'`
    - **Què vol dir:** `print` necessita parèntesis.
    - **Com es corregeix:** `print("Hola")`.

## Activitats guiades

### Activitat 1. Prediu la sortida

Abans d'executar-lo, escriu en un paper què creus que mostrarà aquest programa. Després comprova-ho a Thonny.

```python
print("Bon dia")
print()
print("Adéu")
```

??? success "Solució"
    Mostra tres línies: `Bon dia`, una línia **buida** i `Adéu`. El `print()` sense res dins és el que crea l'espai en blanc.

### Activitat 2. Corregeix el codi

Aquest programa té tres errors. Troba'ls i arregla'ls **un per un**: Python només et mostra un error cada vegada.

```python
Print("Hola")
print("Com estàs?)
print "Adéu"
```

??? success "Solució"
    ```python
    print("Hola")
    print("Com estàs?")
    print("Adéu")
    ```

    Errors: (1) `Print` amb majúscula, (2) cometes sense tancar a la segona línia, (3) falten els parèntesis a la tercera.

### Activitat 3. Completa el codi

Substitueix cada `___` perquè el programa funcioni.

```python
___("Hola, sóc el meu primer programa")
print("Estic aprenent ___")
```

??? success "Solució"
    ```python
    print("Hola, sóc el meu primer programa")
    print("Estic aprenent Python")
    ```

    A la primera línia falta l'ordre `print`; a la segona, el text que vulguis (per exemple, `Python`).

## Lliurament (Classroom)

!!! example "Què has de lliurar"
    **Fitxer:** `u0_cognom_nom.py`

    Escriu un programa que mostri per pantalla **quatre línies**:

    1. El teu nom i cognoms.
    2. El teu curs.
    3. Una frase que comenci amb `Vull aprendre a programar per...`
    4. Una línia en blanc i, a continuació, la frase `Aquest és el meu primer programa!`

    **Abans de lliurar, comprova que:**

    1. El fitxer té la capçalera amb el teu nom, la data i la unitat.
    2. El nom del fitxer segueix el format indicat (minúscules, sense espais ni accents).
    3. El programa inclou almenys un comentari propi.
    4. S'executa sense errors.

    **Com lliurar-lo:** obre la tasca a Classroom, prem **Afegeix o crea → Fitxer**, puja el teu `.py` i prem **Lliura**.

## Repte opcional

Fes servir només `print` per dibuixar a la Shell un **rectangle de 5 files** fet d'asteriscs (`*`). Després, prova de dibuixar les inicials del teu nom.

## Xuleta

| Vull... | Escric... |
| --- | --- |
| Mostrar text | `print("text")` |
| Deixar una línia en blanc | `print()` |
| Escriure un comentari | `# això és un comentari` |
| Executar el programa | Botó **▶** o tecla **F5** |
| Desar el fitxer | **Ctrl + S** |
