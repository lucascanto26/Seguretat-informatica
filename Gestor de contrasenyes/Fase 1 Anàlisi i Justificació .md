__Fase 1: Anàlisi i Justificació (Document d'Informe)__

## 1. Introducció i justificació

La Direcció ha decidit implantar un gestor de contrasenyes perquè les credencials febles o reutilitzades són una de les vies d'entrada més senzilles i barates per a un atacant: no cal explotar cap vulnerabilitat, només endevinar o reaprofitar una clau.

### 1.1 Per què són un risc crític

| Atac | Com funciona | Per què afecta l'empresa |
| --- | --- | --- |
| Atac de diccionari | L'atacant prova llistes de contrasenyes habituals (`123456`, `Password1`, noms, anys, variacions de l'empresa) contra un compte. | Una contrasenya "fàcil de recordar" cau en segons o minuts. |
| Força bruta | Prova totes les combinacions possibles, o ataca un hash robat fora de línia amb GPU. | Les contrasenyes curtes (menys de 12 caràcters) es poden trencar en temps assumible. |
| Credential stuffing | Utilitza parelles usuari/contrasenya filtrades en una altra web i les prova automàticament en serveis corporatius. | Si un empleat reutilitza la mateixa clau en un servei extern i en el correu de l'empresa, una filtració aliena compromet l'empresa. |
| Password spraying | Prova una o poques contrasenyes molt comunes contra molts usuaris, per evitar bloquejos de compte. | Amb prou usuaris, algun tindrà una clau feble. |
| Phishing | Pàgina falsa que captura la contrasenya que l'usuari escriu a mà. | Un gestor només omple la clau si l'URL coincideix, i això ajuda a detectar-lo. |

**Conseqüències:** accés al correu corporatiu, VPN, panells d'administració i serveis al núvol; moviment lateral dins la xarxa; instal·lació de ransomware; fuga de dades personals amb possibles sancions segons el RGPD; i pèrdua de reputació i continuïtat de negoci. En personal tècnic el risc és més alt, perquè els seus comptes tenen privilegis elevats.

**Causa de fons:** una persona no pot recordar desenes de contrasenyes llargues, úniques i aleatòries. El que fa a la pràctica és reutilitzar-les, fer-les curtes, escriure-les en notes o fulls de càlcul, o variar-les de manera previsible (`Empresa2025!`, `Empresa2026!`).

### 1.2 La funció del gestor de contrasenyes

Un gestor de contrasenyes elimina aquesta causa de fons, perquè l'usuari només ha de recordar **una contrasenya mestra** (millor una frase de pas llarga) i, opcionalment, un segon factor. La resta les gestiona l'eina:

- **Generació:** crea contrasenyes aleatòries, llargues i úniques per a cada servei, la qual cosa neutralitza el credential stuffing i redueix molt l'eficàcia del diccionari i la força bruta.
- **Emmagatzematge xifrat:** guarda les credencials en una base de dades xifrada; sense la clau mestra les dades no són llegibles.
- **Emplenament automàtic:** omple usuari i contrasenya només al domini correcte, la qual cosa limita el phishing i evita copiar i enganxar.
- **Organització i control:** agrupa les credencials per carpetes o etiquetes, permet auditar contrasenyes repetides o dèbils i facilita canviar-les si hi ha una filtració.
- **Còpia de seguretat:** permet restaurar l'accés si es perd el dispositiu.