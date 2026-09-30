
# Unitat 1: Variables i Tipus de Dades

Una variable és com una caixa etiquetada on guardem informació. En Python, no cal dir-li quin tipus de dada guardarà; ell ho detecta sol.

## 1. Com crear variables

La sintaxi és: `nom_de_la_variable = valor`

!!! tip "Regles d'or per als noms"
    - Fes servir lletres minúscules i guions baixos (`_`). Ex: `edat_usuari`, `preu_final`.
    - No poden començar per número.
    - No facis servir accents ni caràcters especials (ñ, ç, etc.) en els noms de les variables, encara que sigui català.
    - Són sensibles a majúscules/minúscules: `Nom` i `nom` són dues coses diferents.

### Exemple bàsic

```python
# Això són comentaris. Python els ignora.
nom = "Anna"        # Text (str)
edat = 25           # Nombre sencer (int)
altura = 1.75       # Decimal (float)
esta_actiu = True   # Veritable/Fals (bool)

print(nom)
print(edat)

```

### 🛠️ Prova-ho tu mateix amb Thonny

Com que aquesta web no executa codi directament, hauràs d'utilitzar un editor de text local recomanat per al curs: **Thonny**.

1. Obre Thonny.
2. Crea un nou fitxer (`File > New`).
3. Copia i enganxa el següent codi:

```python
nom = "Anna"
edat = 25
altura = 1.75

print(f"Hola, sóc {nom}. Tinc {edat} anys.")
print(f"La meva altura és {altura} metres.")
```
4. Desa el fitxer com a exercici_1.py.
5. Executa'l fent clic al botó verd ▶️ o prement F5.
!!! tip "Què has de veure?"
A la consola inferior de Thonny hauria d'aparèixer:
text Hola, sóc Anna. Tinc 25 anys. La meva altura és 1.75 metres.
Si et surt algun error, revisa:
Les cometes (").
Els parèntesis tancats correctament.
Que hagis desat el fitxer abans d'executar-lo.



## **2. Els quatre tipus fonamentals**

Per ara, només ens centrarem en aquests quatre. Si entens aquests, ja tens gairebé tot el que necessites per començar.

| Tipus | Nom tècnic | Què guarda? | Exemple |
| --- | --- | --- | --- |
| **Text** | `str` (string) | Paraules, frases, símbols. Sempre entre cometes `' '` o `" "`. | `"Hola món"` |
| **Enter** | `int` (integer) | Nombres sense decimals. Positius o negatius. | `42`, `-7` |
| **Decimal** | `float` | Nombres amb decimals. El separador és el PUNT, no la coma. | `3.14`, `9.99` |
| **Booleà** | `bool` | Només dos valors possibles: `True` (cert) o `False` (fals). | `True` |

!!! warning "Atenció amb els floats!"
A Catalunya escrivim `3,14` (amb coma). En Python **NO**.

❌ Incorrecte: `pi = 3,14` (això ho interpreta com si no fos un nombre!)

✅ Correcte: `pi = 3.14`

## **3. Entrada de dades: `input()`**

Volem interactuar amb l'usuari. La funció `input()` sempre retorna un **text** (`str`), fins i tot si l'usuari escriu un número.
```python
nom = input("Com et dius? ")
print(f"Hola, {nom}!") 
```

El `f` davant de les cometes (`f"..."`) permet inserir variables directament dins del text mitjançant claudàtors `{}`. Això es diu *f-string* i és molt còmode.

## **4. Conversió de tipus (Casting)**

Si volem fer matemàtiques amb el que introdueix l'usuari, hem de convertir el text en nombre.

- `int(text)` → Converteix a enter.
- `float(text)` → Converteix a decimal.
- `str(nombre)` → Converteix a text.

### **L'error més freqüent**
```python
# MALAMENT: Intentar sumar text i nombre
edat_text = input("Quants anys tens? ")  # Retorna str, ex: "20"
resultat = edat_text + 1                 # ERROR! TypeError

# BÉ: Convertir primer
edat_num = int(input("Quants anys tens? ")) # Retorna int, ex: 20
resultat = edat_num + 1                     # OK! Resultat: 21
print(f"L'any vinent en faràs {resultat}")
```

> **Exercici:** Demana el nom i l'edat de l'usuari i imprimeix un missatge personalitzat.

```python
nom = input("Com et dius? ")
edat = int(input("Quants anys tens? "))

print(f"Hola {nom}, el proper any en faràs {edat + 1}.")
```


## **⚠️ Errors comuns a evitar**

1. **Oblidar les cometes:** `nom = Anna` ❌ (Python buscarà una variable anomenada `Anna` que no existeix). Correcte: `nom = "Anna"` ✅.
2. **Usar coma en decimals:** `preu = 9,99` ❌. Correcte: `preu = 9.99` ✅.
3. **No convertir `input()`:** Intentar fer sumes o restes directament amb el resultat d'un `input()` sense embolicar-lo amb `int()` o `float()`.

