# VO-TGSS_VIDA_LABORAL

## INDEX

- [1. Introducció](#1)
- [2. Transmissions de dades disponibles](#2)
- [3. Missatgeria del servei](#3)
   * [3.1 Consulta de vida laboral del darrer any (VIDA_LABORAL)](#3.1)
        * [3.1.1 Petició – dades genèriques](#3.1.1)
		* [3.1.2 Resposta – dades específiques](#3.1.2)
   * [3.2 Consulta de vida laboral dels darrers 5 anys (VIDA_LABORAL5)](#3.2)
        * [3.2.1 Petició – dades genèriques](#3.2.1)
		* [3.2.2 Petició – dades específiques](#3.2.2)
		* [3.2.3 Resposta – dades específiques](#3.2.3)
   * [3.3 Consulta de números d’afiliació (NUMEROS_AFILIACIO)](#3.3)
		* [3.3.1 Petició – dades genèriques](#3.3.1)
		* [3.3.2 Resposta – dades específiques](#3.3.2)
	- [4. Joc de proves](#4)




# 1 Introducció <a name="1"></a>

Aquest document detalla la missatgeria associada al servei de consulta d’informació de Vida Laboral de la Tesorería General de la Seguridad Social.

Per poder realitzar la integració cal conèixer prèviament la següent documentació:

- [Document de Missatgeria Genèrica de la PCI del Consorci AOC.][PCI]

[PCI]:https://github.com/ConsorciAOC/PCI


# 2	Transmissions de dades disponibles <a name="2"></a>
Les dades disponibles a través del servei són les que es presenten a continuació:

Emissor: Tesoreria General de la Seguridad Social.

Producte: TGSS_Vida_Laboral

|**MODALITAT** | **DESCRIPCIO** |
| --- | --- |
| VIDA_LABORAL | VIDA_LABORAL | Consulta de vida laboral del darrer any des de la data de consulta. |
| VIDA_LABORAL5 | Consulta d'un període de la vida laboral dels darrers 5 anys. |
| NUMEROS_AFILIACIO | Consulta de números d’afiliació. |

Les modalitats disposen de versió imprimible del resultat de la consulta en format PDF. Per més detalls adreceu-vos a l’apartat *Extensions de missatgeria* del document de missatgeria genèrica.

# 3	Missatgeria del servei <a name="3"></a>
A continuació es detalla la missatgeria corresponent al bloc de dades específiques de les modalitats de consum del producte.

>L’emissor de les dades requereix que s’informin les dades del funcionari que realitza la consulta. Així, cal informar els següents camps de l’element Funcionario del bloc de dades genèriques:
> */Peticion/Funcionario/NombreCompletoFuncionario,
> /Peticion/Funcionario/NifFuncionario,
> //SolicitudTransmision/DatosGenericos/Solicitante/Funcionario/NombreCompletoFuncionario
> //SolicitudTransmision/DatosGenericos/Solicitante/Funcionario/NifFuncionario*

## 3.1	Consulta de vida laboral del darrer any (VIDA_LABORAL) <a name="3.1"></a>

Consulta de vida laboral del darrer any des de la data de consulta. 

### 3.1.1	Petició – dades genèriques <a name="3.1.1"></a>

| _Element_ | _Descripció_ |
| --- | --- |
| //DatosGenericos/Titular/TipoDocumentacion | Tipus de documentació (DNI, NIE). |
| //DatosGenericos/Titular/Documentacion | Documentació. |

### 3.1.2	Resposta – dades específiques <a name="3.1.2"></a>

Vegeu [apartat 3.2.3] (#3.1.2) d’aquest mateix document.

## 3.2	Consulta de vida laboral dels darrers 5 anys (VIDA_LABORAL5) <a name="3.2"></a>
Consulta d'un període de la vida laboral dels darrers 5 anys.

### 3.2.1	Petició – dades genèriques <a name="3.2.1"></a>

| _Element_ | _Descripció_ |
| --- | --- |
| //DatosGenericos/Titular/TipoDocumentacion | Tipus de documentació (DNI, NIE). |
| //DatosGenericos/Titular/Documentacion | Documentació. |

### 3.2.2	Petició – dades específiques <a name="3.2.2"></a>

![Dades especifiques](https://github.com/ConsorciAOC/VO-TGSS_VIDA_LABORAL/blob/main/images/3%202%202%20Petici%C3%B3%20%E2%80%93%20dades%20espec%C3%ADfiques.png)

| _Element_ | _Descripció_ |
| --- | --- |
| /peticioConsultaVidaLaboral/dataInici | Data d’inici. No pot ser anterior a 5 anys des de la data de la consulta. |
| /peticioConsultaVidaLaboral/dataFi | Data de fi. |



### 3.2.3	Resposta – dades específiques <a name="3.2.3"></a>

![Dades especifiques](https://github.com/ConsorciAOC/VO-TGSS_VIDA_LABORAL/blob/main/images/3%202%203%20Resposta%20%E2%80%93%20dades%20espec%C3%ADfiques.png)

| _Element_ | _Descripció_ |
| --- | --- |
| respostaConsultaVidaLaboral/resposta | Bloc de dades corresponent a la resposta a la consulta. |
| //resposta/consulta/dataInici | Dada des de la que s’ha realitzat la consulta. |
| //resposta/consulta/dataFi | Dada fins la que s’ha realitzat la consulta.<br/> <ul><li>NO_CANVIS_POSTERIORS</li><li>CANVIS_POSTERIORS</li></ul>|
| //resposta/vidaLaboral | Bloc de dades corresponent a les dades de la vida laboral. |
| //vidaLaboral/numeroSituacions | Número de situacions retornades pel període consultat. |
| //vidaLaboral/numerosAfiliacio/numeroAfiliacio | Número d’afiliació del titular consultat (fins a 10).  |
| //vidaLaboral/dataNaixement | Data de naixement. |
| //vidaLaboral/transferenciaDretsCEE | Indicador de transferència dels drets a països de la Unió Europea (S / N). En cas afirmatiu indica: *“Los días en situación de alta que constan en el presente informe únicamente son computables para el acceso a la prestación económica de incapacidad permanente derivada de contingencias comunes, por haberse transferido al sistema de previsión del personal de las Comunidades Europeas las fracciones de cuota destinadas a sufragar las prestaciones de jubilación y muerte y supervivencia, derivadas de contingencias comunes.”* |
| //vidaLaboral/resum | Bloc de dades corresponent al resum dels dies cotitzats en el període consultat. |
| //vidaLaboral/resum/totals | Resum dels dies totals d’alta en el període consultat incloent dies de pluriocupació i pluriactivitat. |
| //vidaLaboral/resum/totals/totalDiesAlta | Total de dies d’alta en el període consultat incloent dies de pluriocupació i pluriactivitat. |
| //vidaLaboral/resum/totals/diesPluriocupacio | Dies d’alta en els que la situació és de pluriocupació. |
| //vidaLaboral/resum/totals/anysAlta | Anys d’alta en el període consultat incloent els anys de pluriocupació o pluriactivitat. |
| //vidaLaboral/resum/totals/mesosAlta | Mesos d’alta en el període consultat incloent els mesos de pluriocupació o pluriactivitat. |
| //vidaLaboral/resum/totals/diesAlta | Dies d’alta en el període consultat incloent els dies de pluriocupació o pluriactivitat. |
| //vidaLaboral/resum/pluriocupacio | Resum dels dies totals d’alta en el període consultat sense incloure dies de pluriocupació i pluriactivitat. |
| //vidaLaboral/resum/pluriocupacio/totalDiesAlta | Total de dies d’alta en el període consultat sense incloure dies de pluriocupació i pluriactivitat. |
| //vidaLaboral/resum/pluriocupacio/anysAlta | Anys d’alta en el període consultat sense incloure els anys de pluriocupació o pluriactivitat. |
| //vidaLaboral/resum/pluriocupacio/mesosAlta | Mesos d’alta en el període consultat sense incloure els mesos de pluriocupació o pluriactivitat. |
| //vidaLaboral/resum/pluriocupacio/diesAlta | Dies d’alta en el període consultat sense incloure els mesos de pluriocupació o pluriactivitat. |
| //vidaLaboral/resum/situacions/situacio | Bloc de dades corresponent a una situació del titular consultat. </br> Si el règim ès AUTONOMOS: <ul><li> es retorna la província on exerceix el titular consultat.</li><li>es retorna la situació amb l'activitat econòmica que realitza l'autònom.</li></ul>|
| //situació/numeroAfiliacio | Número d’afiliació de la Seguretat Social de la situació. |
| //situació/regim | Règim de la Seguretat Social per la situació: GENERAL, REP.COMER., ARTISTAS, TAURINOS, AUTONOMOS, AGRARIO, MAR, CARBON, HOGAR i PROF. TAUR |
| //situació/empresa | Raó social / nom de l’empresa. |
| //situació/codiCompteCotitzacio | Codi compte cotització de l’empresa. |
| //situació/provincia | Província i codi compte cotització. Només es retorna si el codi de compte de cotització és: C.AJENA, C.PROPIA i si no s’especifica |
| //situació/dataAlta | Data d’inici de l’activitat laboral. |
| //situació/dataEfectes | Data a partir de la qual té efectes l’alta en ordre a causar dret, a les prestacions del sistema de Seguretat Social, llevat per les prestacions derivades d’accidents de treball i malalties professionals, atur y assistència sanitària derivada de malaltia comuna, maternitat i accident no laboral, en les quals la data d’efecte de l’alta coincideix, en qualsevol cas, amb la data d’alta. |
| //situació/dataBaixa | Data de finalització de l’activitat laboral. |
| //situació/contracteTreball | Identificador del contracte de treball. Per més detalls vegeu l’apartat 3.2.3.1 d’aquest document. |
| //situació/contracteTempsParcial | Identificador del % de jornada per contractes a temps parcial. Identifica el percentatge que, sobre la jornada a temps complert establerta en el Conveni Col·lectiu d’aplicació o, en el seu defecte, sobre la jornada ordinària màxima legal, realitza o ha realitzat el treballador/a. |
| //situació/grupCotitzacio | Grup de cotització. Per més detalls vegeu l’apartat 3.2.3.2 d’aquest document. |
| //situació/diesAlta | Dies donat d’alta per la situació retornada. Per més detalls, vegeu l’apartat 3.2.3.3 d’aquest document. |
| respostaConsultaVidaLaboral/resultat/codiResultat | Codi de resultat de la consulta: 0000: titular localitzat, 0001: titular no localitzat a la BBDD de la Seguretat Social, 0002: titular duplicat a la BBDD de la Seguretat Social, 0005: vida laboral amb massa situacions, 0502: error realitzant la consulta. |
| respostaConsultaVidaLaboral/resultat/descripcio | Descripció del resultat. |

#### 3.2.3.1	Relació de contractes de treball

| Clave | Característiques del contracte | Característiques del contracte | Característiques del contracte | Característiques del contracte |
| --- | --- | --- | ---- | --- |
| 100 | INDEFINIT | TEMPS COMPLERT | ORDINARI | - |
| 109 | INDEFINIT | TEMPS COMPLERT | FOMENT CONTRACTACIÓ INDEFINIDA | TRANSFORMACIÓ CONTRACTE TEMPORAL |
| 130 | INDEFINIT | TEMPS COMPLERT | PERSONES AMB DISCAPACITAT | - |
| 139 | INDEFINIT | TEMPS COMPLERT | PERSONES AMB DISCAPACITAT | TRANSFORMACIÓ CONTRACTE TEMPORAL |
| 150 | INDEFINIT | TEMPS COMPLERT | FOMENT CONTRACTACIÓ INDEFINIDA | INICIAL |
| 189 | INDEFINIT | TEMPS COMPLERT | - | TRANSFORMACIÓ CONTRACTE TEMPORAL |
| 200 | INDEFINIT | TEMPSPARCIAL | ORDINARI | - |
| 209 | INDEFINIT | TEMPSPARCIAL | FOMENT CONTRACTACIÓ INDEFINIDA | TRANSFORMACIÓ CONTRACTE TEMPORAL |
| 230 | INDEFINIT | TEMPSPARCIAL | PERSONES AMB DISCAPACITAT | - |
| 239 | INDEFINIT | TEMPSPARCIAL | PERSONES AMB DISCAPACITAT | TRANSFORMACIÓ CONTRACTE TEMPORAL |
| 250 | INDEFINIT | TEMPSPARCIAL | FOMENT CONTRACTACIÓ INDEFINIDA | INICIAL |
| 289 | INDEFINIT | TEMPSPARCIAL | - | TRANSFORMACIÓ CONTRACTE TEMPORAL |
| 300 | INDEFINIT | FIX DISCONTINU | - | - |
| 309 | INDEFINIT | FIX DISCONTINU | FOMENT CONTRACTACIÓ INDEFINIDA | TRANSFORMACIÓ CONTRACTE TEMPORAL |
| 330 | INDEFINIT | FIX DISCONTINU | PERSONES AMB DISCAPACITAT | - |
| 339 | INDEFINIT | TEMPS PARCIAL | PERSONES AMB DISCAPACITAT | TRANSFORMACIÓ CONTRACTE TEMPORAL |
| 350 | INDEFINIT | FIX DISCONTINU | FOMENT CONTRACTACIÓ INDEFINIDA | INICIAL |
| 389 | INDEFINIT | FIX DISCONTINU | - | TRANSFORMACIÓ CONTRACTE TEMPORAL |
| 401 | DURACIÓ DETERMINADA | TEMPS COMPLERT | OBRA O SERVICIO DETERMINADO | - |
| 402 | DURACIÓ DETERMINADA | TEMPS COMPLERT | EVENTUAL CIRCUMSTÀNCIESDELAPRODUCCIÓ | - |
| 408 | TEMPORAL | TEMPS COMPLERT | - | CARÀCTER ADMINISTRATIU |
| 410 | DURACIÓ DETERMINADA | TEMPSCOMPLERT | INTERINITAT | - |
| 418 | DURACIÓ DETERMINADA | TEMPS COMPLERT | INTERINITAT | CARÀCTER ADMINISTRATIU |
| 420 | TEMPORAL | TEMPS COMPLERT | PRÀCTIQUES | - |
| 421 | TEMPORAL | TEMPS COMPLERT | FORMACIÓ I APRENENTATGE | - |
| 430 | TEMPORAL | TEMPS COMPLERT | PERSONES AMB DISCAPACITAT | - |
| 441 | TEMPORAL | TEMPS COMPLERT | RELLEU | - |
| 450 | TEMPORAL | TEMPS COMPLERT | FOMENT CONTRACTACIÓ INDEFINIDA | - |
| 452 | TEMPORAL | TEMPS COMPLERT | EMPRESES D'INSERCIÓ | - |
| 501 | DURACIÓ DETERMINADA | TEMPS PARCIAL | OBRAOSERVEIDETERMINAT | - |
| 502 | DURACIÓ DETERMINADA | TEMPS PARCIAL | EVENTUAL CIRCUMSTÀNCIES DE LA PRODUCCIÓ | - |
| 508 | TEMPORAL | TEMPS PARCIAL | - | CARÀCTER ADMINISTRATIU |
| 510 | DURACIÓ DETERMINADA | TEMPS PARCIAL | INTERINITAT | - |
| 518 | DURACIÓ DETERMINADA | TEMPS PARCIAL | INTERINITAT | CARÀCTER ADMINISTRATIU |
| 520 | TEMPORAL | TEMPS PARCIAL | PRÀCTIQUES | - |
| 530 | TEMPORAL | TEMPS PARCIAL | PERSONES AMB DISCAPACITAT | - |
| 540 | TEMPORAL | TEMPS PARCIAL | JUBILAT PARCIAL | - |
| 541 | TEMPORAL | TEMPS PARCIAL | RELLEU | - |
| 550 | TEMPORAL | TEMPS PARCIAL | FOMENT CONTRACTACIÓ INDEFINIDA | - |
| 552 | TEMPORAL | TEMPS PARCIAL | EMPRESES D'INSERCIÓ | - |

#### 3.2.3.2	Grups de cotització

| _Grup_ | _Descripció_ |
| --- | --- |
| 01 | INGENIEROS Y LICENCIADOS. PERSONAL DE ALTA DIRECCIÓN NO INCLUIDO EN EL ARTÍCULO 1.3. c) DEL ESTATUTO DE LOS TRABAJADORES |
| 02 | INGENIEROS TÉCNICOS, PERITOS Y AYUDANTES TITULADOS |
| 03 | JEFES ADMINISTRATIVOS Y DE TALLER |
| 04 | AYUDANTES NO TITULADOS |
| 05 | OFICIALES ADMINISTRATIVOS |
| 06 | SUBALTERNOS |
| 07 | AUXILIARES ADMINISTRATIVOS |
| 08 | OFICIALES DE PRIMERA Y SEGUNDA |
| 09 | OFICIALES DE TERCERA Y ESPECIALISTAS |
| 10 | PEONES |
| 11 | TRABAJADORES MENORES DE DIECIOCHO AÑOS, CUALQUIERA QUE SEA SU CATEGORÍA PROFESIONAL |

#### 3.2.3.3	Aclariment dels dies d’alta d’una situació

El dies d’alta d’una situació tindran les següents excepcions i aclariments. Número de dies compresos entre la data d’efecte de l’alta i la data de baixa
* En situacions d’alta el número de dies es computa entre la data d’efecte de l’alta i la data d’emissió de l’informe.

Peculiaritats dels contractes a temps parcial

Al numero resultant de la diferència entre la data d’efecte de l’alta i la data de baixa s’ha aplicat el percentatge sobre la jornada habitual de l’empresa.

* En el supòsit de que en un període el treballador hagi tingut diferents jornades de treball pel que fa a la seva durada, en el càlcul dels dies s’han tingut en compte totes elles.

* El càlcul del número de dies en situació d’alta en períodes amb contracte a temps parcial es provisional.

* El càlcul definitiu es realitzarà en el moment que s’efectuï una sol·licitud per a l’accés a una prestació del sistema de la Seguretat Social.

Peculiaritats del conveni especial de funcionaris de la Unió Europea dels contractes a temps parcial

* Els dies en situació d’alta en aquest conveni especial únicament són computables per a l’accés a la prestació econòmica d’incapacitat permanent derivada de contingències comunes.

Peculiaritats del sistema especial de fruites, hortalisses i conserves vegetals

* Si en l’informe consten les dades de COEFICIENT DE PERMANÈNCIES, DIES DE TREBALL i/o DIES ALS QUE NO ES D’APLICACIÓ EL COEFICIENT DE PERMANÈNCIES, el número de dies en situació d’alta es calcula multiplicant els DIES DE TREBALL pel COEFICIENT DE PERMANÈNCIES, sumant-se al resultat obtingut els DIES ALS QUE NO ÉS D’APLICACIÓ EL COEFICIENT DE PERMANÈNCIES.

* La situació d’alta de forma simultània en dos o més Règims del citat sistema –pluriactivitat- sent una de les empreses del Sistema Especial de Fruites, Hortalisses i Conserves Vegetals, impedeix determinar si al número de dies calculats segons s’ha indicat en el paràgraf anterior se li han de restar dies per existir una superposició de períodes cotitzats. El càlcul definitiu es realitzarà en el moment en que s’efectuï una sol·licitud per a l’accés a una prestació econòmica del sistema de la Seguretat Social.

## 3.3	Consulta de números d’afiliació (NUMEROS_AFILIACIO) <a name="3.3"></a>
Consulta dels números d’afiliació.

### 3.3.1	Petició – dades genèriques <a name="3.3.1"></a>

| _Element_ | _Descripció_ |
| --- | --- |
| //DatosGenericos/Titular/TipoDocumentacion | Tipus de documentació (DNI, NIE). |
| //DatosGenericos/Titular/Documentacion | Documentació. |

### 3.3.2	Resposta – dades específiques <a name="3.3.2"></a>

![Dades escifiques](https://github.com/ConsorciAOC/VO-TGSS_VIDA_LABORAL/blob/main/images/3%203%202%20Resposta%20%E2%80%93%20dades%20espec%C3%ADfiques.png)

| _Element_ | _Descripció_ |
| --- | --- |
| respostaConsultaNumerosAfiliacio/resposta | Bloc de dades corresponent a la resposta a la consulta. |
| //resposta/numerosAfiliacio/numeroAfiliacio | Número d’afiliació (fins a un màxim de 10). |
| respostaConsultaNumerosAfiliacio/resultat/codiResultat | Codi de resultat de la consulta: 0000: titular localitzat, 0001: titular no localitzat a la BBDD de la Seguretat Social, 0002: titular duplicat a la BBDD de la Seguretat Social, 0005: error realitzant la consulta, 0010: titular sense cap número d’afiliació i 0502: error realitzant la consulta. |
| respostaConsultaNumerosAfiliacio/resultat/descripcio | Descripció del resultat. |


# 4 Joc de proves <a name="4"></a>



L&#39;emissor final publica els següent [joc de proves a l&#39;entorn de pre-producció][proves] 

[proves]: https://administracionelectronica.gob.es/ctt/svd/descargas#.YvOZNXbP2Ul
![image](https://user-images.githubusercontent.com/32306731/137281698-9dfc2044-94f7-487f-a7d6-9a4e0707feb3.png) En cas de tindre problemes per accedir als jocs de proves, si us plau, obre un tiquet a través del [formulari][form]

[form]:https://www.aoc.cat/portal-suport/peticio-integradors/idservei/integracio/
