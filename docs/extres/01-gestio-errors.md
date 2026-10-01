# Extra 1. Gestió d'errors

!!! abstract "Resum"
    **Tipus:** ampliació opcional · **Requisits:** unitats 3 i 4 · **Sense lliurament:** fes les activitats i comprova-les amb les solucions.

## Objectius

En acabar aquest extra sabràs:

- Explicar què és una **excepció** i llegir el missatge d'error complet.
- Fer que un programa **no peti** quan l'usuari escriu un valor incorrecte, amb `try` i `except`.
- Capturar tipus d'error concrets (`ValueError`, `ZeroDivisionError`, `IndexError`).
- Crear funcions que demanin dades **de manera robusta**, repetint la pregunta fins que siguin correctes.
- Decidir quan fer servir `try/except` i quan és millor un `if`.

## Punt de partida

!!! question "Ho recordes?"
    Als algorismes, a vegades cal preveure un **pla B**: «intenta obrir la porta; si està tancada, truca al timbre». En pseudocodi:

    ```text
    Intenta
        convertir el text en un nombre
    Si falla llavors
        avisar l'usuari
    Fi
    ```

    Això és exactament el que fa `try/except` en Python.

    Fins ara, quan l'usuari escrivia text on es demanava un nombre, el programa **petava**. Ara aprendràs a evitar-ho.

## Teoria

### 1. Què és una excepció?

Quan Python no pot continuar executant una instrucció, **llança una excepció** i el programa s'atura mostrant un missatge com aquest:

```text
Traceback (most recent call last):
  File "programa.py", line 1, in <module>
    edat = int(input("Edat: "))
ValueError: invalid literal for int() with base 10: 'vint'
```

Com llegir-lo: mira **l'última línia** (el tipus d'error i què ha passat) i la línia on s'ha produït (`line 1`).

Alguns tipus d'excepció que ja coneixes:

| Excepció | Quan apareix |
| --- | --- |
| `ValueError` | `int("hola")`: el valor no és vàlid per a l'operació |
| `ZeroDivisionError` | `10 / 0` |
| `IndexError` | `notes[10]` en una llista de 3 elements |
| `TypeError` | `"5" + 3` |
| `NameError` | Fer servir una variable que no existeix |

!!! info "Els `SyntaxError` són diferents"
    Els errors de sintaxi (un `:` oblidat, unes cometes sense tancar...) es detecten **abans d'executar** el programa. No es poden capturar amb `try/except`: s'han de corregir al codi.

### 2. `try` i `except`

```python
try:
    edat = int(input("Edat: "))
    print(f"L'any vinent en faràs {edat + 1}")
except ValueError:
    print("Això no és un nombre enter")
```

Com funciona:

1. Python executa el bloc de `try` línia a línia.
2. Si **cap línia falla**, el bloc d'`except` es salta.
3. Si **alguna línia falla** amb un `ValueError`, Python abandona el `try` immediatament (les línies següents no s'executen) i salta al bloc d'`except`.
4. Després, el programa continua amb normalitat.

### 3. Capturar errors concrets

Pots tenir **diversos `except`**, un per cada tipus d'error, amb un missatge diferent per a cadascun:

```python
try:
    a = int(input("a: "))
    b = int(input("b: "))
    print(a / b)
except ValueError:
    print("Cal escriure nombres enters")
except ZeroDivisionError:
    print("No es pot dividir per zero")
```

Si vols veure el missatge original de Python, pots guardar l'error en una variable amb `as`:

```python
except ValueError as e:
    print("Error:", e)
```

!!! warning "Evita l'`except` sense tipus"
    Un `except:` sense cap tipus captura **tots** els errors, també els teus errors de programació (una variable mal escrita, per exemple). Així el programa deixa de petar, però **no t'adones que alguna cosa va malament**. Indica sempre el tipus d'error que esperes.

### 4. `else`: quan tot ha anat bé

Pots afegir un `else` que només s'executa si **no** hi ha hagut cap excepció:

```python
text = input("Escriu un nombre: ")
try:
    n = int(text)
except ValueError:
    print("No és un nombre")
else:
    print(f"Has escrit el {n}")
```

És una forma de deixar clar què és el que pot fallar (`try`) i què es fa si funciona (`else`).

### 5. El patró estrella: demanar una dada fins que sigui vàlida

Combinant un bucle amb `try/except` creem una funció reutilitzable que **mai peta**:

```python
def demana_enter(missatge):
    while True:
        try:
            return int(input(missatge))
        except ValueError:
            print("Valor no vàlid. Escriu un nombre enter.")
```

- Si l'usuari escriu un enter, el `return` surt de la funció amb el valor.
- Si escriu text, salta l'`except`, es mostra l'avís i el bucle torna a començar.

I la versió completa de la funció de la unitat 5, amb límits:

```python
def demana_enter(missatge, minim, maxim):
    while True:
        try:
            n = int(input(missatge))
        except ValueError:
            print("Cal escriure un nombre enter")
        else:
            if minim <= n <= maxim:
                return n
            print(f"Ha de ser un nombre entre {minim} i {maxim}")
```

### 6. `try/except` o `if`?

- Si pots **comprovar el problema abans** amb una condició senzilla, fes servir un `if` (per exemple, `if b != 0:` abans de dividir).
- Si no és fàcil de comprovar abans (per exemple, saber si un text es pot convertir a nombre), fes servir `try/except`.
- Mantén el bloc `try` **curt**: només les línies que poden fallar.

!!! tip "Per recordar"
    `try/except` no arregla el problema: només decideix **què fer** quan passa. Sempre cal avisar l'usuari o tornar-ho a demanar.

## Exemples resolts

Copia'ls a Thonny, executa'ls i **prova-los amb dades incorrectes** a posta.

**Exemple 1. Una edat que no peta**

```python
try:
    edat = int(input("Quants anys tens? "))
    print(f"L'any vinent en faràs {edat + 1}")
except ValueError:
    print("Cal escriure un nombre enter")
```

**Exemple 2. Una divisió segura**

```python
try:
    a = int(input("Dividend: "))
    b = int(input("Divisor: "))
    print(f"{a} / {b} = {a / b}")
except ValueError:
    print("Cal escriure nombres enters")
except ZeroDivisionError:
    print("No es pot dividir per zero")
```

**Exemple 3. Notes amb una funció robusta**

```python
def demana_decimal(missatge):
    while True:
        try:
            return float(input(missatge))
        except ValueError:
            print("Cal escriure un nombre (amb punt decimal)")

notes = []
for i in range(3):
    notes.append(demana_decimal(f"Nota {i + 1}: "))
print(f"Mitjana: {round(sum(notes) / len(notes), 2)}")
```

**Exemple 4. Una posició que pot no existir**

```python
colors = ["roig", "verd", "blau"]
try:
    posicio = int(input("Posició (0-2): "))
    print(colors[posicio])
except ValueError:
    print("Cal escriure un nombre enter")
except IndexError:
    print("Aquesta posició no existeix")
```

## Errors típics

!!! failure "L'`except` buit amaga els teus errors (sense missatge d'error)"
    ```python
    try:
        edat = int(inptu("Edat: "))
    except:
        print("Valor no vàlid")
    ```

    - **Resultat:** sempre mostra «Valor no vàlid», encara que l'usuari escrigui bé el nombre.
    - **Què passa:** hi ha una errada d'escriptura (`inptu`) que genera un `NameError`, però l'`except` buit la captura i el missatge enganya.
    - **Com es corregeix:** indica el tipus (`except ValueError:`). Així el `NameError` es mostraria i trobaries l'errada.

!!! failure "Fer servir una variable que no s'ha arribat a crear"
    ```python
    try:
        n = int(input("Nombre: "))
    except ValueError:
        print("Error")
    print(n * 2)
    ```

    - **Missatge (similar a):** `NameError: name 'n' is not defined`
    - **Què vol dir:** si la conversió falla, `n` no arriba a existir i la darrera línia no té res per fer servir.
    - **Com es corregeix:** posa en el `else` (o dins del `try`) el codi que necessita `n`, o fes servir una funció amb bucle que no surti fins que tingui un valor vàlid.

!!! failure "Capturar el tipus d'error equivocat"
    ```python
    try:
        print(10 / 0)
    except ValueError:
        print("Error")
    ```

    - **Missatge (similar a):** `ZeroDivisionError: division by zero`
    - **Què vol dir:** l'`except` només captura `ValueError`, i aquí l'error és un altre.
    - **Com es corregeix:** `except ZeroDivisionError:`.

## Activitats guiades

### Activitat 1. Prediu la sortida

Què mostra aquest programa? I si canviem `"x"` per `"5"`?

```python
try:
    print("A")
    n = int("x")
    print("B")
except ValueError:
    print("C")
print("D")
```

??? success "Solució"
    Amb `"x"`: mostra `A`, `C` i `D`. Quan falla `int("x")`, Python salta a l'`except` i la línia amb `B` no s'executa.

    Amb `"5"`: no hi ha cap error, així que mostra `A`, `B` i `D`; l'`except` es salta.

### Activitat 2. Quin `except` el captura?

Per a cada línia, indica quin tipus d'excepció llança.

- a) `int("hola")`
- b) `10 / 0`
- c) `[1, 2, 3][5]`
- d) `"a" + 1`

??? success "Solució"
    - a) `ValueError`
    - b) `ZeroDivisionError`
    - c) `IndexError`
    - d) `TypeError`

### Activitat 3. Corregeix el codi

Aquest programa té dos problemes: no diu què ha fallat i, si falla, l'última línia també peta. Arregla'l.

```python
try:
    n = int(input("Un nombre: "))
    resultat = 100 / n
except:
    print("Hi ha hagut un error")
print(f"El resultat és {resultat}")
```

??? success "Solució"
    ```python
    try:
        n = int(input("Un nombre: "))
        resultat = 100 / n
    except ValueError:
        print("Cal escriure un nombre enter")
    except ZeroDivisionError:
        print("No es pot dividir per zero")
    else:
        print(f"El resultat és {resultat}")
    ```

    Problemes: (1) l'`except` buit no distingeix entre error de conversió i divisió per zero; (2) si falla, `resultat` no existeix i la línia final dona `NameError`. Posant el `print` al `else`, només s'executa quan tot ha anat bé.

### Activitat 4. Completa el codi

Completa la funció perquè no deixi de preguntar fins que s'escrigui un enter.

```python
def demana_enter(missatge):
    while ___:
        try:
            return int(input(missatge))
        except ___:
            print("Valor no vàlid")
```

??? success "Solució"
    ```python
    def demana_enter(missatge):
        while True:
            try:
                return int(input(missatge))
            except ValueError:
                print("Valor no vàlid")
    ```

### Activitat 5. Escriu-ho tu

Escriu un programa que demani **dues notes decimals** i en mostri la mitjana. Si l'usuari escriu text en lloc d'un nombre, ha de **repetir la pregunta** en lloc de petar.

??? success "Solució"
    ```python
    def demana_decimal(missatge):
        while True:
            try:
                return float(input(missatge))
            except ValueError:
                print("Cal escriure un nombre (amb punt decimal)")

    nota1 = demana_decimal("Nota 1: ")
    nota2 = demana_decimal("Nota 2: ")
    print(f"Mitjana: {round((nota1 + nota2) / 2, 2)}")
    ```

## Repte opcional

**Calculadora robusta.** Fes una calculadora que demani dos nombres decimals i una operació (`+`, `-`, `*` o `/`) i mostri el resultat. Ha de controlar:

- Que els nombres siguin vàlids (repetint la pregunta).
- Que l'operació sigui una de les quatre permeses.
- La divisió per zero.

Quan ho tinguis, aplica la funció `demana_enter` robusta al teu **projecte final** perquè no peti si l'usuari escriu text.

## Xuleta

| Vull... | Escric... |
| --- | --- |
| Provar una cosa que pot fallar | `try:` |
| Què fer si falla | `except TipusError:` |
| Diversos tipus d'error | Diversos `except` seguits |
| Veure el missatge original | `except ValueError as e:` |
| Què fer si no ha fallat | `else:` |
| Demanar fins que sigui vàlid | `while True:` + `try` + `return` |
| Errors més habituals | `ValueError`, `ZeroDivisionError`, `IndexError`, `TypeError` |
