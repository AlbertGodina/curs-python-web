# Unitat 3: Repetir accions (Bucles)

Fins ara, els nostres programes executaven les instruccions una vegada i s'aturaven. Què passa si volem repetir una tasca 10, 100 o fins i tot mil vegades? No podem copiar i pegar el codi mil vegades! Aquí entren els **bucles**.

Un bucle permet executar un bloc de codi múltiples vegades mentre es compleixi una condició o durant un nombre determinat d'iteracions.

## 1. El bucle `for`: Per quantes vegades?

El bucle `for` s'utilitza quan sabem exactament quantes vegades volem repetir alguna cosa, o quan volem recórrer una seqüència (com una llista de noms).

La sintaxi bàsica utilitza la funció `range()`.

### L'exemple clàssic: Comptar de l'1 al 5

```python
# range(6) genera els nombres 0, 1, 2, 3, 4, 5
for numero in range(6):
    print(numero)
```

!!! tip "Com funciona `range()`?"
    - `range(n)` comença a 0 i acaba a n-1.
    - `range(inici, fi)` comença a `inici` i acaba a `fi-1`.
    - `range(inici, fi, pas)` salta de `pas` en `pas`.

### Exemple: Taules de multiplicar

Imagina que vols imprimir la taula del 7. En lloc d'escriure 10 línies de `print`, fem servir un bucle:

```python
numero = 7

for i in range(1, 11):
    resultat = numero * i
    print(f"{numero} x {i} = {resultat}")
```

Aquí, `range(1, 11)` genera els nombres de l'1 al 10. El programa repeteix l'operació de multiplicació i impressió 10 vegades.

## 2. El bucle `while`: Mentre sigui cert

El bucle `while` s'utilitza quan **no sabem** quantes vegades caldrà repetir l'acció, però sí sabem quan hem de parar. Es repeteix **mentre** la condició sigui `True`.

### Exemple: Joc d'endevinança simplificat

Suposem que volem demanar a l'usuari un número fins que encerti el 42.

```python
intent = 0
secret = 42

while intent != secret:
    entrada = input("Endevina el número secret (pista: és petit): ")
    intent = int(entrada)
    
    if intent < secret:
        print("Més alt!")
    elif intent > secret:
        print("Més baix!")
    else:
        print("Encertat! Has guanyat.")
```

!!! warning "Perill de Bucle Infinit"
    Si oblides actualitzar la variable de control (`intent` en aquest cas) dins del `while`, el programa no s'aturarà mai i hauràs de tancar-lo forçosament. 
    Assegura't sempre que hi ha una manera de sortir del bucle (que la condició esdevingui `False`).

## 3. Comparativa ràpida: `for` vs `while`

| Característica | `for` | `while` |
| :--- | :--- | :--- |
| **Quan usar-lo?** | Quan coneixes el nombre d'iterations o recorres una col·lecció. | Quan depens d'una condició dinàmica (ex: fins que l'usuari encerti). |
| **Risc d'infinit?** | Baix (controlat per `range` o longitud de llista). | Alt (cal cuidar bé la condició de sortida). |
| **Sintaxi** | `for variable in seqüència:` | `while condicio:` |

---

## 🛠️ Exercici Pràctic (Thonny)

Obre Thonny i crea un fitxer nou anomenat `exercici_bucles.py`.

**Repte:** Crea un programa que demani a l'usuari un nombre enter positiu. Després, el programa ha d'imprimir tots els nombres des de l'1 fins a aquell nombre introduït.

*Exemple d'execució:*
> Introdueix un nombre: 5
> 1
> 2
> 3
> 4
> 5

*(Pista: Utilitza `input()`, converteix a `int()` i fes servir un bucle `for` amb `range()`).*

??? success "Solució"
    
    ```python
    # Demanar el nombre a l'usuari
    entrada = input("Introdueix un nombre: ")
    fi = int(entrada)

    # Recórrer des de l'1 fins al nombre introduït (inclòs)
    # Recorda: range(final) arriba fins a final-1, així que posem fi + 1
    for numero in range(1, fi + 1):
        print(numero)
    ```

## Errors freqüents

1. **Oblidar el dos punts (`:`):** Tant a `for ... :` com a `while ... :`. Sense ell, dona `SyntaxError`.
2. **No indentar el cos del bucle:** Les línies que s'han de repetir han d'estar dins del bloc (indentades).
3. **Confondre `range(n)` amb `1..n`:** `range(5)` és `[0, 1, 2, 3, 4]`. Si vols arribar al 5, has de fer `range(6)` o especificar `range(1, 6)`.
4. **Bucle infinit amb `while`:** No modificar la variable que controla la condició dins del bucle.
```


