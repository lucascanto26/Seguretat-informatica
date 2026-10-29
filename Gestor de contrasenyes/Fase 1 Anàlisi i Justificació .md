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

## 2. Comparativa tècnica

Bitwarden és l'alternativa **online (núvol)** i KeePassXC l'alternativa **offline (escriptori)**. Totes dues són de codi obert, xifren les dades amb algorismes forts i tenen extensió de navegador; la diferència principal és **on viu la base de dades i qui s'encarrega de sincronitzar-la**.

| Criteri | Bitwarden (núvol) | KeePassXC (escriptori) |
| --- | --- | --- |
| Model | Servei al núvol (també es pot autoallotjar). Clients per a web, escriptori, mòbil, extensió i CLI. | Aplicació d'escriptori local per a Windows, macOS i Linux. Sense servidor ni compte. |
| Emmagatzematge | La caixa forta xifrada es guarda als servidors de Bitwarden i es manté una còpia local a cada dispositiu. | Un únic arxiu local `.kdbx` (format KDBX 4) que l'usuari desa on vulgui. |
| Sincronització | Automàtica entre tots els dispositius connectats al mateix compte. | No en té de nativa. S'ha de fer a mà (còpia de l'arxiu) o amb eines externes (Syncthing, Nextcloud, OneDrive xifrat, etc.). |
| Xifratge i model de seguretat | Xifratge extrem a extrem de tipus *zero-knowledge*: la clau es deriva de la contrasenya mestra al dispositiu i el servidor només guarda dades xifrades (AES-256). KDF: PBKDF2-SHA256 o Argon2id. | Arxiu xifrat amb AES-256 (també ChaCha20 o Twofish). KDF Argon2id per defecte en KDBX 4. Clau composta: contrasenya + arxiu clau + YubiKey opcionals. |
| Segon factor | 2FA per al compte (app TOTP, correu, FIDO2/YubiKey segons pla). | No hi ha compte; es reforça l'arxiu amb arxiu clau o YubiKey (repte-resposta). |
| Accés multidispositiu | Molt fàcil: ordinador, mòbil i qualsevol navegador via web vault. | Més limitat: cal portar l'arxiu al dispositiu i usar una app compatible amb KDBX al mòbil (KeePassDX, KeePassium...). |
| Extensió de navegador | Oficial (Chrome, Firefox, Edge, Safari...). | KeePassXC-Browser (Chrome, Firefox, Edge...) connectada a l'aplicació d'escriptori, que ha d'estar oberta i desbloquejada. |
| Cost / model | *Freemium*: pla gratuït amb contrasenyes i dispositius il·limitats; Premium, Teams i Enterprise de pagament amb funcions extra (TOTP integrat, informes, gestió d'equips). | Gratuït, sense plans ni límits. |
| Codi obert | Sí (clients i servidor). Ha passat auditories de seguretat externes. | Sí (GPL). Desenvolupament comunitari actiu. |
| Independència del núvol | Depèn del servei (o de l'autoallotjament) i de la connexió per sincronitzar. Hi ha accés sense connexió amb la còpia local. | Total. Funciona sense Internet i sense cap tercer. |
| Portabilitat de l'arxiu | Exportació a CSV o JSON (aquest últim pot anar xifrat). | `.kdbx` es pot copiar, moure o obrir amb molts clients compatibles (KeePass, KeePassXC, KeePassDX, KeePassium). |
| Gestió d'equip / compartició | Col·leccions i organitzacions per compartir credencials amb permisos (plans de pagament). | No hi ha compartició centralitzada: s'ha de compartir l'arxiu, i això complica el control d'accessos. |
| Superfície d'atac | Cal confiar en el proveïdor i protegir el compte (la filtració del servidor no revela les claus, però un compte robat sí que és un risc). | Més petita, perquè no hi ha servei exposat. El risc és perdre l'arxiu, no fer-ne còpia o que es robi el dispositiu. |

**Nota sobre KeePassX:** KeePassX és el projecte original, però gairebé no rep actualitzacions. KeePassXC n'és la continuació activa i és el que cal usar avui (suporta KDBX 4, Argon2, TOTP i integració amb el navegador). Per això l'informe compara Bitwarden amb KeePassXC.

*Els preus i els límits dels plans poden canviar; cal comprovar-los a bitwarden.com/pricing abans de decidir.*

## 3. Avantatges i inconvenients: online vs offline
Cap model és millor en tots els aspectes: l'online guanya en comoditat i col·laboració, i l'offline en control i independència.

### 3.1 Model online (Bitwarden)

| Àmbit | Avantatges | Inconvenients |
| --- | --- | --- |
| Seguretat | Xifratge extrem a extrem; el proveïdor no pot llegir les dades. Codi obert i auditat. 2FA al compte. Actualitzacions gestionades pel proveïdor. | Les dades xifrades estan en un servidor de tercers. Si es roba el compte o la contrasenya mestra és feble, tota la caixa forta queda exposada. Cal confiar en el proveïdor. |
| Usabilitat | Sincronització immediata entre PC, mòbil i navegador. Instal·lació i alta molt senzilles. Bona experiència per a usuaris no tècnics. | Cal crear un compte i, en alguns plans, pagar per a les funcions avançades. |
| Continuïtat del negoci | Accés des de qualsevol lloc. Compartició per col·leccions i recuperació d'accés més fàcil en plans d'organització. | Depèn de la disponibilitat del servei i de la política del proveïdor (preus, canvis de pla). Es pot mitigar amb la còpia local o amb l'autoallotjament, que exigeix administrar un servidor. |

### 3.2 Model offline (KeePassXC)

| Àmbit | Avantatges | Inconvenients |
| --- | --- | --- |
| Seguretat | Cap dada surt de l'equip si no es vol. Superfície d'atac petita. Xifratge fort (AES-256, Argon2id) i arxiu clau o YubiKey opcionals. Sense dependència de tercers. | La seguretat depèn de l'usuari: on es guarda l'arxiu, si es fa còpia, si l'equip està infectat. L'extensió del navegador requereix l'aplicació oberta. |
| Usabilitat | Totalment gratuït i sense registre. Interfície completa (grups, camps personalitzats, TOTP, adjunts). | Sense sincronització automàtica; cal organitzar-la. El mòbil depèn d'apps de tercers compatibles amb KDBX. Corba d'aprenentatge una mica més alta. |
| Continuïtat del negoci | Funciona sense Internet i no pot deixar de funcionar per la caiguda o el tancament d'un servei. L'arxiu `.kdbx` és portable i obert. | Si es perd l'arxiu o la contrasenya mestra i no hi ha còpia, no hi ha recuperació possible. Difícil compartir credencials amb un equip amb control d'accés i traçabilitat. Risc de còpies desincronitzades. |


## 4. Recomanació

**Recomanem Bitwarden per al personal tècnic de l'empresa.**

**Motius:**

1. **Xifratge extrem a extrem i codi obert auditat.** El proveïdor no pot llegir les credencials, de manera que el model de seguretat és comparable al d'una base de dades local ben protegida.
2. **Sincronització automàtica i accés multidispositiu.** El personal tècnic treballa amb diversos equips i dispositius, i la caixa forta és la mateixa a tots, sense haver de copiar arxius a mà.
3. **Compartició amb control d'accessos.** Les col·leccions i organitzacions permeten compartir credencials d'equip (servidors, xarxa, comptes de servei) amb permisos i sense passar-se contrasenyes per canals insegurs.
4. **Ús des del navegador, sense instal·lació.** El web vault i l'extensió oficial permeten treballar des de qualsevol equip i redueixen el risc de phishing, perquè només omplen al domini correcte.
5. **Cost baix i model freemium.** El pla gratuït cobreix l'ús individual i els plans Teams o Enterprise són assequibles si l'empresa vol gestió centralitzada.
6. **Continuïtat.** L'accés no depèn d'un únic equip: si es perd o s'espatlla un dispositiu, la caixa forta continua disponible al núvol.

**Condicions per fer-ho bé (mitigació dels inconvenients):**

- Contrasenya mestra llarga (frase de pas) i segon factor (2FA) obligatori per a tots els usuaris.
- Còpia de seguretat periòdica amb exportació xifrada (.json Encrypted protegida amb contrasenya) guardada en una unitat xifrada fora del compte, tal com detalla la guia de la Fase 2.
- Valorar l'autoallotjament de Bitwarden si l'empresa vol que les dades xifrades no surtin de la seva infraestructura.

**Quan seria preferible KeePassXC:** per a credencials d'infraestructura molt crítiques que no han de dependre de cap servei extern, o en entorns sense connexió a Internet.