<h1 align="center"> Curs de Python: De Zero a Hero</h1>

<p align="center">
  <strong>Material docent per aprendre a programar en Python des de zero.</strong><br>
  Pensat per a alumnat de 4t d'ESO que ja té una base de pensament computacional.
</p>

<p align="center">
  <a href="https://albertgodina.github.io/curs-python-web/"><img alt="Web en directe" src="https://img.shields.io/badge/web-en%20directe-4f46e5?style=for-the-badge"></a>
</p>

<p align="center">
  <img alt="Python 3" src="https://img.shields.io/badge/Python-3-3776AB?logo=python&logoColor=white">
  <img alt="MkDocs Material" src="https://img.shields.io/badge/MkDocs-Material-526CFE?logo=materialformkdocs&logoColor=white">
  <img alt="Idioma: català" src="https://img.shields.io/badge/idioma-catal%C3%A0-red">
  <img alt="Nivell: iniciació" src="https://img.shields.io/badge/nivell-iniciaci%C3%B3-brightgreen">
  <a href="https://creativecommons.org/licenses/by-sa/4.0/deed.ca"><img alt="Llicència CC BY-SA 4.0" src="https://img.shields.io/badge/llic%C3%A8ncia-CC%20BY--SA%204.0-lightgrey"></a>
</p>

<p align="center">
  <a href="https://albertgodina.github.io/curs-python-web/"><strong>➡️ Obre el curs</strong></a>
</p>

---

##  Què és això?

Un curs complet i en català per aprendre **Python** pas a pas. Està format per **8 unitats** (unes **18 sessions**) més una secció d'**extres** per a qui vol anar més lluny.

Cada unitat té teoria curta, exemples per executar, errors típics explicats, activitats amb solucions desplegables i un lliurament. Tot el codi es treballa amb **[Thonny](https://thonny.org)**, un editor pensat per aprendre, i els lliuraments es fan a **Google Classroom**.

> [!TIP]
> No cal tenir cap coneixement previ de programació. Només Thonny i ganes d'aprendre.

##  Contingut

| # | Unitat | Sessions | Què s'hi aprèn |
| :-: | --- | :-: | --- |
| 0 | Preparació de l'entorn | 1 | Què és Python, Thonny i el primer programa |
| 1 | Variables i entrada/sortida | 2 | `print`, `input`, variables, tipus i f-strings |
| 2 | Operadors i text bàsic | 2 | Càlculs, comparacions, operadors lògics i text |
| 3 | Condicionals | 3 | `if`, `elif`, `else`, depuració i `random` |
| 4 | Bucles | 4 | `while`, `for`, `range`, comptadors i acumuladors |
| 5 | Funcions | 2 | `def`, paràmetres, `return` i àmbit de les variables |
| 6 | Llistes | 2 | Crear, recórrer, cercar i modificar llistes |
| 7 | Projecte final | 2 | Un programa propi de principi a fi |

###  Extres (ampliació)

Per a l'alumnat que acaba abans o vol aprofundir. No tenen lliurament: porten activitats amb solució desplegable.

| # | Extra | Estat |
| :-: | --- | :-: |
| 1 | Gestió d'errors (`try/except`) | ✅ |
| 2 | Text avançat (*slicing* i mètodes) | ✅ |
| 3 | Tuples i conjunts | ✅ |
| 4 | Diccionaris | 🔜 |
| 5 | Fitxers | 🔜 |
| 6 | Classes i objectes | 🔜 |

##  Com és cada unitat

Totes les unitats segueixen la mateixa estructura perquè sempre se sàpiga on buscar què:

1. **Objectius**: què sabràs fer en acabar.
2. **Punt de partida**: l'enllaç amb el pensament computacional i els algorismes.
3. **Teoria**: explicacions curtes, cadascuna amb un exemple.
4. **Exemples resolts**: per executar a Thonny i modificar.
5. **Errors típics**: amb el missatge de Python i com corregir-lo.
6. **Activitats guiades**: predir, corregir i completar codi, amb solucions desplegables.
7. **Lliurament**: l'activitat que es puja a Classroom.
8. **Repte opcional** i **xuleta** de resum.

##  Estructura del repositori

```text
curs-python-web/
├── docs/
│   ├── index.md                  # Portada del curs
│   ├── 00-preparacio.md          # Unitats 0 a 7
│   ├── ...
│   ├── 07-projecte-final.md
│   ├── extres/                   # Extres d'ampliació
│   └── stylesheets/extra.css     # Estils propis
├── mkdocs.yml                    # Configuració i menú del web
└── .github/workflows/            # Publicació automàtica
```

El web es genera amb **[MkDocs](https://www.mkdocs.org)** i el tema **[Material for MkDocs](https://squidfunk.github.io/mkdocs-material/)**, i es publica automàticament a **GitHub Pages** amb **GitHub Actions** a cada canvi a la branca `main`.

##  Executar-lo en local

Si vols veure el web al teu ordinador mentre l'edites:

```bash
# 1. Clona el repositori
git clone https://github.com/albertgodina/curs-python-web.git
cd curs-python-web

# 2. Instal·la les dependències
pip install "mkdocs<2" mkdocs-material

# 3. Arrenca el servidor local
mkdocs serve
```

Després obre <http://127.0.0.1:8000> al navegador. Els canvis es veuen en directe.

> [!NOTE]
> El desplegament fa servir `mkdocs build --strict`: si hi ha algun avís (per exemple, un enllaç a una pàgina que no existeix), la publicació falla. Comprova-ho en local amb `mkdocs build --strict` abans de pujar canvis.

## Suggeriments i errades

Has trobat una errada, un exemple que no funciona o tens una idea per millorar el curs? Obre una **[issue](https://github.com/albertgodina/curs-python-web/issues)** i explica-ho. Totes les aportacions són benvingudes.

## Llicència

Aquest material es distribueix amb llicència **[Creative Commons Reconeixement-CompartirIgual 4.0 (CC BY-SA 4.0)](https://creativecommons.org/licenses/by-sa/4.0/deed.ca)**: pots utilitzar-lo, adaptar-lo i compartir-lo, citant-ne l'autoria i mantenint la mateixa llicència.

## Autoria

Creat per **Albert Godina Lapaz**.

---

<p align="center">
  <sub>Fet amb ❤️ i molta paciència per aprendre a programar.</sub>
</p>
