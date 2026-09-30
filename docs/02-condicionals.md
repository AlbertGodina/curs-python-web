
# Unitat 2: Presa de Decisions (Condicionals)

Fins ara, els nostres programes han seguit sempre el mateix camí de dalt a baix. Amb els condicionals, podem fer que el programa prengui decisions: *"Si passa això, fes allò; sinó, fes una altra cosa"*.

## L'estructura `if`

La paraula clau és `if` (si). Després va una condició que ha de ser veritable (`True`) o falsa (`False`).

```python
edat = 18

if edat >= 18:
    print("Ets major d'edat.")
```

!!! warning "Atenció! Indentació"
    Les línies dins del `if` han d'estar indentades (normalment 4 espais o 1 tabulador). 
    Si no indentes, Python donarà un error `IndentationError`.

## Afegint alternatives: `else`

Què fem si la condició NO es compleix? Utilitzem `else` (sinó).

```python
temperatura = 15

if temperatura > 25:
    print("Fa calor.")
else:
    print("No fa tanta calor.")
```

## Múltiples opcions: `elif`

Si tenim diverses possibilitats intermitges, fem servir `elif` (abreviatura d'"else if").

```python
nota = 7

if nota >= 9:
    print("Excel·lent")
elif nota >= 7:
    print("Notable")
elif nota >= 5:
    print("Suficient")
else:
    print("Insuficient")
```

!!! tip "Ordre importa!"
    Python comprova les condicions de dalt a baix. Quan troba la primera que és certa, executa aquell bloc i salta la resta. Per això posem les condicions més restrictives primer (ex: `>= 9` abans que `>= 7`).

---

## 🛠️ Exercici Pràctic (Thonny)

1. Obre Thonny i crea un nou fitxer `exercici_condicionals.py`.
2. Escriu un programa que demani a l'usuari la seva **edat**.
3. El programa ha de imprimir:
   - "Ets menor d'edat" si té menys de 18 anys.
   - "Ets major d'edat" si en té 18 o més.

*(Pista: Recorda convertir l'entrada a `int()`)*

??? success "Solució"
    
    ```python
    edat_str = input("Quants anys tens? ")
    edat = int(edat_str)

    if edat < 18:
        print("Ets menor d'edat.")
    else:
        print("Ets major d'edat.")
    ```

## Errors freqüents

| Error | Causa | Solució |
| :--- | :--- | :--- |
| `SyntaxError: expected ':'` | Oblidar els dos punts `:` després de `if`. | Afegir `:` al final de la línia del `if`. |
| `IndentationError` | No indentar el bloc interior. | Usar Tab o 4 espais per a les línies interiors. |
| Comparar amb `=` en lloc de `==` | Confondre assignació amb comparació. | Per comparar, feu servir doble igual `==`. Ex: `if x == 5:` |
```
