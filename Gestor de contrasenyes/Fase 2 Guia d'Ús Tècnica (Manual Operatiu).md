__Fase 2: Guia d'Ús Tècnica (Manual Operatiu)__



## 1. Instal·lació i configuració inicial

Aquesta guia explica com configurar Bitwarden des del navegador: el **web vault** (la caixa forta a vault.bitwarden.com) i l'**extensió oficial**, que s'instal·la al navegador. No cal instal·lar cap programa d'escriptori.

### 1.1 Accés al web vault

1. Obre el navegador i ves a **vault.bitwarden.com**.
2. Prem **Create account** per crear el compte.

![crear compte bitwarden](img/Captura%20de%20pantalla%202026-10-29%20161955.png)


### 1.2 Creació del compte

1. Omple el formulari:
   - **Email:** l'adreça de correu de l'empresa.
   - **Name:** el teu nom.
   - **Master password:** una frase de pas llarga (mínim 12 caràcters; recomanat 20 o més) que només coneguis tu.
   - **Master password hint:** opcional. No hi posis la contrasenya ni cap pista evident.
2. Accepta les condicions i prem **Create account**.
3. Verifica el correu electrònic amb l'enllaç que rebràs i inicia sessió.

![m'envien correu](img/Captura%20de%20pantalla%202026-10-29%20164331.png)


### 1.3 Instal·lació de l'extensió del navegador

A l'entrar m'ha sortit per afegir l'extensió de google.

![plugin chrome](img/Captura%20de%20pantalla%202026-10-29%20164539.png)

En "add extension" em fica a la pagina de google per posar l'opció "afegir a chrome".

![afegir a chrome](img/Captura%20de%20pantalla%202026-10-29%20164854.png)

I en obrir l'extensió tenim la nostre caixa forta, està buida perquè es la primera vegada que l'utilitzem.

![la nostra extensió oberta](img/Captura%20de%20pantalla%202026-10-29%20165110.png)

### 1.4 Activar el segon factor (2FA)

A la web vault anirem a configuracó, seguretat, autentificació en dues passes.
![mfa](img/Captura%20de%20pantalla%202026-10-29%20165321.png)

I entrarem a Aplicació d'autenticació (Bitwarden Authenticator) i l'activarem a la web.

![activacio mfa](img/Captura%20de%20pantalla%202026-10-29%20165809.png)


## 2. Generació de contrasenyes segures

El generador de Bitwarden crea contrasenyes aleatòries amb els paràmetres que triïs. La regla bàsica és que **cada servei ha de tenir una contrasenya diferent, llarga i generada, no escrita a mà**.

### 2.1 On és el generador

Entrarem a eines, generador.

![generador](img/Captura%20de%20pantalla%202026-10-29%20170123.png)

### 2.2 Paràmetres de la contrasenya (Password)

| Paràmetre | Què fa | Valor recomanat |
| --- | --- | --- |
| Length | Nombre de caràcters. És el factor que més augmenta la seguretat. | 20 com a mínim; 24-32 per a administració, servidors i correu. |
| A-Z | Inclou majúscules. | Activat |
| a-z | Inclou minúscules. | Activat |
| 0-9 | Inclou números. | Activat |
| !@#$%^&* | Inclou caràcters especials. | Activat, llevat que el servei no els accepti. |
| Minimum numbers / Minimum special | Força un mínim de xifres i símbols. | 2 i 2 |
| Avoid ambiguous characters | Evita caràcters que es confonen (`O/0`, `l/1`). | Activat si s'ha de teclejar a mà. |

![generació contrasenya](img/Captura%20de%20pantalla%202026-10-29%20170305.png)


### 2.3 Frase de pas (Passphrase)

Per a una contrasenya que hagis de **recordar** (la contrasenya mestra o el login de Windows), canvia el tipus a **Passphrase**:

![generació passphrase](img/Captura%20de%20pantalla%202026-10-29%20170454.png)

