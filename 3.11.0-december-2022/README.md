# NCV Data
### Versie 3.11.0, december 2022
In de sqlite database in deze map is de structuur van de data van het NCV project te vinden, en in de map "tabellen" de data zelf, zoals deze eind december 2022 was, en is verschenen in versie 3.11.0 van de app, uitgebracht op 23 december 2022. De data bevat de NCV vertaling, het interlineair bij de Griekse en Hebreeuwse grondtekst, structuren, commentaar, voetnoten en meer. Onder is per tabel in de database beschreven wat de data inhoudt.

Een pdf bestand van de papieren uitgave zoals die in deze tijd is klaargemaakt is ook te vinden in de map. In dat bestand is de vertaling van het NT te vinden, samen met een uitgebreide verantwoording van de vertaling en meer. Uiteindelijk zijn er voor de papieren versie nog enkele verbeteringen aan de data gedaan, en versie 3.12.0 komt overeen met de uiteindelijke gedrukte papieren uitgave.

Aan het gebruik van de data zijn voorwaarden verbonden, zoals beschreven in het LICENSE bestand. Voor delen van de data zijn aanvullende eisen en/of copyright statements van kracht, zie hieronder het gedeelte onder "Bronnen".

### Status data
In deze versie is het volledige interlineair bij de CGT en de bhs opgenomen, NCV van het NT, Structuren en commentaar bij het NT, voetnoten nog vooral bij Galaten en 2Korinte, woordenboekomschrijving van maar een paar woorden. De vertaling is vergeleken met de versie van 3.10.0 een stuk verfijnder, fouten zijn eruitgehaald, veel keuzes verbeterd.

## Structuur van de data
Hieronder een korte uitleg van de structuur van de data, hoe zaken aan elkaar gekoppeld zijn of hoe verschillende tabellen elkaar aanvullen.

### Koppeling aan versnummers
Omdat veel van de data gekoppeld is aan een boek, hoofdstuk en vers in de Bijbel, is hiervoor een "versindex" bedacht, in de database kortweg "vid", waarmee deze informatie in een getal opgeslagen kan worden, dat makkelijk te herleiden is en op volgorde gesorteerd kan worden. Dit getal is te berekenen door de bijbelboeken van 1 tot 66 te nummeren, en dan de volgende berekening te doen:
```javascript
let vid = boeknummer * 1000000 + hoofdstuknummer * 1000 + versnummer;
```

### Interlineair bij de Griekse grondtekst
Voor elk Grieks woord is een vertaalwoord gekozen, het trefwoord, en is bepaald hoe dit woord is opgebouwd uit Griekse elementen, die in de stamvorm zijn weergeven. Deze informatie is per Grieks lexeem opgeslagen in de tabel "GriNe", en de lexemen zijn daar uniek genummerd met "GriUniekeId". Elk woord is opgebouwd uit elementen, en in de tabel "GE" staan de afzonderlijke Griekse elementen met hun betekenis opgeslagen. In de tabel "CGT" wordt gekoppeld welk Grieks woord in welk vers en als zoveelste woord in de tekst staat. De afzonderlijke Griekse woorden met alle informatie over vervoegde trefwoord, stamvorm, grammaticale informatie, Strongnummer en meer staat in de tabel "GrWoorden". Wat de grammaticale codes betekenen staat verder uitgewerkt in de tabel "GrParsings". In de tabel "strongGR" staat bij elk Strongnummer nog de omschrijving uit het Strong lexicon en andere woordenboeken. in "StrongLink" worden Strongnummers met GriUniekeids gekoppeld. In GrVertaal is opgeslagen bij elk lexeem met welke vertaalwoorden dit woord vertaald is. In de tabel "CGT" wordt bij elk Grieks woord gelinkt naar een vertaalwoord.

### Interlineair bij de Hebreeuwse grondtekst
Eenzelfde opzet is er voor het Oude Testament, met de lexemen in "HebNe", de elementen of wortels in "HE", de tekst in "bhs", de afzonderlijke Hebreeuwse woorden in "HeWoorden", de uitleg van de grammaticale codes in "HeParsings" en woordenboeken per Strongnummer in "strongHb". In "bhs_qre" staan de qre woorden bij qtib/qre lezingen, en in "bhs_tk" staat welke qtib woorden door welke qre woorden vervangen worden.

### De NCV vertaling
De NCV vertaling is per woord opgeslagen in de "NCV" tabel, om koppeling per woord met de grondtekst op te kunnen slaan. In "NCVpar" is de opmaak van paragrafen, citaten e.d. opgelsagen. Hoe een specifieke grammaticale vorm in de vertaling weergegeven kan worden is met uitleg opgeslagen in "Vertalingen", en bij welk Grieks woord een bepaalde vertaling toegepast is is opgeslagen in "VertalingenLink".

### Overige tabellen
Structuuroverzichten van boeken en tekstgedeelten zijn ook opgeslagen in de database. Elke structuur is opgeslagen in "Struct", de regels bij elke structuur weer afzonderlijk in "Structregels".

In "Bijbels" is de Schriftwoordvertaling opgeslagen per vers en is bij elk vers ook een aantal versverwijzingen te vinden.

In "com" is het Concordant Commentaar bij het NT door A.E.Knoch te vinden, zoals die ook bij de Schriftwoordvertaling is gepubliceerd. In "vidToCom" zijn versverwijzingen in het commentaar apart opgeslagen, zodat het commentaar op ververwijzingen doorzocht kan worden.

In "voetnoten" zijn de voetnoten bij de vertaling te vinden (vooralsnog vooral bij Galaten en 2Korinte), die uitleg geven over vertaalkeuzes, achtergrondinformatie en meer.

In "woordenboek" is van een paar woorden een woordstudie opgelsagen, die dan bij het klikken op dat woord bekeken kan worden, met informatie over gebruik in Oud Grieks, in de Septuagint, in het NT, over de woordfamilie etc.

In "woordenboek2" is een begin gemaakt met een betere woordenboekomschrijving met uitleg over elke vertaalkeuze per lexeem. Dit is nog neit voor alle lexemen gedaan.

## Uitleg tabellen
Hieronder is per tabel aangegeven welke velden de tabel bevat en wat die velden betekenen.

### CGT
| Veld  | Uitleg  |
| ------------ | ------------ |
| vid  | Versindex  |
| Woord  | Zoveelste woord van het vers  |
| vertaalwoord  | Koppeling met "id" van "GrVertaal". Voor koppeling is ook GriUniekeid nodig, op te halen via tabel "GrWoorden"  |
| role  | Rol dat het zinsgedeelte in de zin heeft, zoals onderwerp of lijdend voorwerp.  |
| id  | Koppeling met "id" van "GrWoorden".  |

### GE
| Veld  | Uitleg  |
| ------------ | ------------ |
| id  | index van de Griekse elementen  |
| Gri  | Weergave van het element in Griekse letters  |
| translit  | Transliteratie van deze letters in latijnse letters, naar uitspraak.  |
| GriZ  | Een één op één overzetting van de Griekse letters naar latijnse letters om het zoeken te faciliteren.  |
| stamgegevens  | De betekenis van het Griekse element  |
| parent  | Eventueel is het element zelf ook weer opgebouwd uit een ander element, een parent.  |
| vergelijk  | Indien vergelijkbaar met een ander element, hier het id ervan.  |

### GrParsings
| Veld  | Uitleg  |
| ------------ | ------------ |
| parsT  | Traditionele grammaticale parsing  |
| pars  | Grammaticale parsing gebruikt door het NCV project  |
| vv  | Voorvoegsel dat de woordsoort aangeeft, zoals "V" voor werkwoord  |
| aspect  | Aspect van de werkwoordsvorm, zoals in traditionele parsing gegeven, zoals "A" voor aorist.  |
| tijd  | De tijd van de werkwoordsvorm, zoals "P" voor verleden tijd  |
| toestand  | De toestand van de werkwoordsvorm, zoals "I" voor voortdurende handeling. |
| vorm  | Of een werkwoord actief, mediaal of passief is.  |
| modus  | De modus van het werkwoord, zoals "I" voor indicatief.  |
| persoon  | Of het woord 1e, 2e of 3e persoon is.  |
| naamval  | Naamval van het woord.  |
| getal  | Of het woord enkelvoud of meervoud is.  |
| geslacht  | Of het woord mannelijk, vrouwelijk of onzijdig is.  |
| extra  | Extra informatie over het woord.  |

### GrVertaal
| Veld  | Uitleg  |
| ------------ | ------------ |
| griUniekeid  | Het unieke id voor het Griekse lexeem, koppelt aan "id" van "GriNe"  |
| id  | Per griUniekeid, nummer voor zoveelste vertaling vna het woord  |
| sterretjeNodig  | Of de vertaling wordt gezien als een afwijking van het trefwoord, en er in de vertaling dus een sterretje of teken nodig is  |
| vertaling  | De vertaling van het lexeem  |
| omschrijving  | Een uitleg bij deze vertaling van het lexeem, niet gebruikt in deze versie  |

### GrWoorden
| Veld  | Uitleg  |
| ------------ | ------------ |
| id | Het unieke id van het Griekse woord |
| grieks | De Griekse weergave van het woord |
| translit | Transliteratie van deze letters in latijnse letters, naar uitspraak. |
| translitz | Aangepaste transliteratie die beter doorzoekbaar is |
| nedS | De vervoegde stamvorm van het woord |
| nedI | Het vervoegde trefwoord van het woord |
| nedSz | Een licht aangepaste versie van nedS die beter doorzoekbaar is |
| nedIz | Een licht aangepaste versie van nedI die beter doorzoekbaar is |
| strong | Het strongnummer van het woord |
| CGTparsing | De grammaticale code, koppelt aan "GrParsings" |
| CGTparsingT | De traditionele grammaticale code |
| griUniekeid | Het unieke id van het Griekse lexeem, gekoppeld aan "id" van "GriNe" |
| bijvolgende | Of het woord in het interlineair samen met een volgend woord als één samengesteld woord moet verschijnen |
| samen | Het unieke id van het samengestelde woord |

### GriNe
| Veld  | Uitleg  |
| ------------ | ------------ |
| id | Het unieke id van het lexeem |
| grieks | De Griekse weergave van het lexeem |
| translit | Transliteratie van deze letters in latijnse letters, naar uitspraak. |
| translitz | Aangepaste transliteratie die beter doorzoekbaar is |
| GrWrd | Aangepaste oude transliteratie die eerst als unieke index gebruikt werd |
| stamgegevens | De stamvorm van het lexeem, dat de opbouw uit elementen weergeeft |
| trefwoord | Het gekozen vertaalwoord voor dit lexeem |
| GE | De Griekse elementen waaruit het woord is opgebouwd, opgeslagen als de nummers van de lexemen met een 'a' ervoor en erachter om het makkelijk doorzoekbaar te maken. De afzonderlijke nummers koppelen het lexeem aan "id" van "GE" |
| strong | Strongnummer van het woord |
| aant | Hoe vaak het voorkomt in het interlineair |
| familieWB | Koppelt aan "id" in "woordenboek" |

### HE
| Veld  | Uitleg  |
| ------------ | ------------ |
| id | Het unieke id van het element |
| Heb | De weergave van het element in Hebreeuwse letters |
| translit | Transliteratie van deze letters in latijnse letters, naar uitspraak. |
| Hebz | Aangepaste transliteratie die beter doorzoekbaar is |
| stamgegevens  | De betekenis van het element  |
| parent  | Eventueel is het element zelf ook weer opgebouwd uit een ander element, een parent.  |
| vergelijk  | Indien vergelijkbaar met een ander element, hier het id ervan.  |
| taal | Taal van het element, Aramees, Hebreeuws of anders |

### HeParsings
| Veld  | Uitleg  |
| ------------ | ------------ |
| parsT  | Traditionele grammaticale parsing  |
| pars  | Grammaticale parsing gebruikt door het NCV project  |
| vv  | Voorvoegsel dat de woordsoort aangeeft, zoals "W" voor werkwoord  |
| binjan | De binjan van het werkwoord, zoals Qal |
| aspect | Het tradtitionele omschrijving van het aspect van het werkwoord, zoals Participium actief |
| tijd  | De tijd van de werkwoordsvorm, zoals "V" voor verleden tijd  |
| toestand  | De toestand van de werkwoordsvorm, zoals "O" voor voortdurende handeling. |
| stam | De werkwoordsstam waar het woord vanaf komt, zoals grondstam. |
| vorm  | Of een werkwoord actief, reflexief of passief is.  |
| modus  | De modus van het werkwoord, zoals "O" voor infinitief.  |
| persoon  | Of het woord 1e, 2e of 3e persoon is.  |
| geslacht  | Of het woord mannelijk, vrouwelijk of onzijdig is.  |
| getal  | Of het woord enkelvoud, tweevoud of meervoud is.  |
| status | Status van het woord, zoals status constructus |
| extra  | Extra informatie over het woord.  |

### HeWoorden
| Veld  | Uitleg  |
| ------------ | ------------ |
| id | Unieke id van het Hebreeuwse of Aramese woord |
| cons | Weergave van het woord in Hebreeuwse consonanten |
| voc | Weergave van het woord in consonanten en alle tekens |
| trailer | Of na het woor deen streepje, spatie of iets anders moet komen |
| translit | Transliteratie van deze letters in latijnse letters, naar uitspraak. |
| translitz | Aangepaste transliteratie die beter doorzoekbaar is |
| nedS | De vervoegde stamvorm van het woord |
| nedI | Het vervoegde trefwoord van het woord |
| nedSz | Een licht aangepaste versie van nedS die beter doorzoekbaar is |
| nedIz | Een licht aangepaste versie van nedI die beter doorzoekbaar is |
| strong | Het strongnummer van het woord |
| CHTparsing | De grammaticale code van het woord, zoals gebruikt in het NCV project. Koppelt aan "HeParsings" |
| CHTparsingT | De traditionele grammaticale code voor het woord |
| hebUniekeid | Unieke index van het lexeem van het woord, koppelt aan "HeNe" |
| bijvolgende | Of het woord in het interlineair samen met een volgend woord als één samengesteld woord moet verschijnen |
| samen | Het unieke id van het samengestelde woord |
| taal | Hebreeuws of Aramees |
| aant | Hoe vaak het woord voorkomt in het interlineair |

### HebNe
| Veld  | Uitleg  |
| ------------ | ------------ |
| id | Unieke id van het lexeem |
| language | Hebreeuws of Aramees |
| hebreeuws | Weergave van het lexeem in Hebreeuwse letters met tekens |
| cons | Weergave in alleen consonanten |
| translit | Transliteratie van deze Hebreeuwse weergave in latijnse letters, naar uitspraak. |
| translitz | Aangepaste transliteratie die beter doorzoekbaar is |
| trefwoord | Het gekozen vertaalwoord voor het lexeem |
| trefwoordB | Bij werkwoorden wordt hier opgeslagen als per binjan nog een ander trefwoord gekozen is |
| stamgegevens | De stamvorm van het lexeem, dat de opbouw uit elementen weergeeft  |
| HE | De Hebreeuwse/Aramese elementen waaruit het woord is opgebouwd, opgeslagen als de nummers van de lexemen met een 'h' ervoor en erachter om het makkelijk doorzoekbaar te maken. De afzonderlijke nummers koppelen het lexeem aan "id" van "HE" |
| strong | Het strongnummer van het lexeem |
| aant | Hoe vaak het lexeem voorkomt in het interlineair |

### NCV
| Veld  | Uitleg  |
| ------------ | ------------ |
| vid | Versindex |
| Woord | Zoveelste woord in de vertaling van het vers (loopt niet gelijk met Woord van CGT of bhs) |
| tekst | De tekst van het woord |
| supvoor | Verhoogde tekens voor het woord |
| supna | verhoogde tekens na het woord |
| tekstvoor | leestekens of spaties voor het woord |
| tekstna | leestekens of spaties na het woord |
| dun | Of het woord grijs gedrukt moet worden |
| GTbegin | Nummer van het Griekse woord dat dit woord vertaald, koppelt aan "Woord" van CGT bij dit vid |
| GTbeginOud | Niet gebruikt in deze uitgave |
| GTeind | Niet gebruikt in deze uitgave |

### NCVkopjes
| Veld  | Uitleg  |
| ------------ | ------------ |
| vid | Versindex |
| tekst | Tekst van de kopjes |

### NCVpar
| Veld  | Uitleg  |
| ------------ | ------------ |
| id | Unieke id van een opmaak element |
| vidBegin | Versindex waar het opmaakelement staat |
| Woord | Indien niet aan het begin van een vers maar halverwege, het woord in de vertaling waar het voor komt te staan. -1 is aan het eind van het vers. |
| type | Soort opmaakelement, een paragraaf of citaat etc. |
| par | Of het een paragraaf is |
| cit | Of het een citaat is |

### Struct
| Veld  | Uitleg  |
| ------------ | ------------ |
| id | Unieke id van een structuur |
| van | Begin vid van de structuur |
| tot | Eind vid van de structuur |
| titel | Titel boven de structuur |
| algemeen | Of het specifieke stukken bespreekt of groter, een boek of serie boeken |
| ruimte | Hoeveelheid ruimte die het in beslag neemt (?) |
| header | Of de structuur onder een header weergegeven moet worden (?) |

### Structregels
| Veld  | Uitleg  |
| ------------ | ------------ |
| id | Unieke id van de structuur regel |
| sid | Id van de structuur, koppelt aan "id" in "Struct" |
| van | Begin vid van de structuurregel |
| tot | Eind vid van de structuurregel |
| cl | Welke class de regel moet hebben, bepaald hoeveel tabs van links de regel weergegeven wordt |
| tekst | De tekst van de regel |

### Vertalingen
| Veld  | Uitleg  |
| ------------ | ------------ |
| id | Unieke id van de vertaling |
| parsing | Parsing van de vorm waarbij de vertaling geldt. Is alleen een woordsoort, of bij werkwoorden ook info over tijd, vorm, toestand, modus |
| num | Hoeveelste vertaling bij die parsing |
| syntax | Poging een conditie waaronder deze vertaling gedaan wordt te coderen, niet gebruikt in de app |
| vertaling | Hoe de vorm vertaald wordt, niet gebruikt in de app  |
| kort | Een korte omschrijving van de vertaling, gebruikt in het overzicht bij het klikken op een woord |
| opmerking | Een langere uitleg bij de vertalingen, ook wanneer de vorm zo vertaald wordt |

### VertalingenLink
| Veld  | Uitleg  |
| ------------ | ------------ |
| vid | Versindex |
| Woord | Zoveelste woord uit de grondtekst, koppelt met "vid" aan "Woord" in "CGT" |
| id | Id van de vertaling, koppelt aan "id" in "Vertalingen" |

### bhs
| Veld  | Uitleg  |
| ------------ | ------------ |
| vid | Versindex, nummering van de verzen zoals de vertaling aanhoudt |
| altvid | Alternatieve nummering van de verzen, zoals de BHS zelf doet |
| Woord | Zoveelste woord in het vers |
| role | Rol dat het zinsgedeelte in de zin heeft, zoals onderwerp of lijdend voorwerp.  |
| link | Koppeling aan het bijbehorende Griekse woord in de LXX. Deze tekst staat niet in deze database. |
| id  | Koppeling met "id" van "HeWoorden".  |

### bhs_qre
| Veld  | Uitleg  |
| ------------ | ------------ |
| vid | Versindex, nummering van de verzen zoals de vertaling aanhoudt |
| Woord | Zoveelste woord in het vers |
| id  | Koppeling met "id" van "HeWoorden".  |

### bhs_tk
| Veld  | Uitleg  |
| ------------ | ------------ |
| id | Unieke id van de tekstkwestie |
| tekst | Soort tekstkwestie, hier alleen Qetib/Qere |
| vid | versindex |
| WoordVan | Woord in bhs waar de tekstkwestie begint |
| WoordTot | Woord in bhs waar de tekstkwestie eindigt |
| WoordVan_v | Woord in bhs_qre waar de tekstkwestie begint |
| WoordTot_v | Woord in bhs_qre waar de tekstkwestie eindigt |

### bijbels
| Veld  | Uitleg  |
| ------------ | ------------ |
| vid | Versindex |
| vv | Versverwijzingen bij het vers |
| SW | De Schriftwoordvertaling van het vers |

### com
| Veld  | Uitleg  |
| ------------ | ------------ |
| id | Unieke code van het commentaar |
| vid | Versindex van het vers waar het commentaar bij hoort |
| code | Code dat de schrijvers van dit commentaar aanduidt |
| aand | Aanduiding van het commentaar |
| titel | Aparte titel die nog boven het commentaar kan staan |
| text | De tekst van het commentaar |

### strongGR
| Veld  | Uitleg  |
| ------------ | ------------ |
| num | Strongnummer |
| grieks | Griekse weergave van het woord |
| translit | Transliteratie van het woord |
| text | Omschrijving in het Strong Lexicon van het woord |
| Thayer | Omschrijving in het lexicon van Thayer (abriged) van het woord |
| Abott | Omschrijving in het lexicon van Abott van het woord |
| ThayerUA | Omschrijving in het lexicon van Thayer (unabriged) van het woord |

### strongHb
| Veld  | Uitleg  |
| ------------ | ------------ |
| num | Strongnummer |
| hebreeuws | Hebreeuwse weergave van het woord |
| text | Omschrijving in het Strong Lexicon van het woord |
| BDB | Omschrijving in het Brown Driver Briggs Lexicon (abridged) van het woord |
| pos | Afkorting van de woordsoort |

### strongLink
| Veld  | Uitleg  |
| ------------ | ------------ |
| strong | Strongnummer |
| griUniekeid | Unieke id van het lexeem, linkt aan "id" in "GriNe" |
| kan | Of deze link bruikbaar is, zeker is |
| uniek | Of deze link uniek is, of dat er meer strongnummers bij het lexeem horen |

### vidToCom
| Veld  | Uitleg  |
| ------------ | ------------ |
| vidvan | Vid van het begin van de verwijzing |
| vidtot | Vid van het eind van de verwijzing |
| textid | Id de tekst waaruit gerefereerd wordt, is boeknummer + 66 |
| referentie | Id van het commentaar, linkt naar "id" in "com" |

### voetnoten
| Veld  | Uitleg  |
| ------------ | ------------ |
| id | Unieke id voor de voetnoot |
| vid | Versindex waar de voetnoot bij hoort |
| tekst | Tekst van de voetnoot |
| type | Soort voetnoot (uitleg, alternatief etc.) |

### woordenboek
| Veld  | Uitleg  |
| ------------ | ------------ |
| id | Unieke id van woordenboekgedeelte |
| num | Id van het lexeem, linkt naar "id" in "GriNe", of, als getal > 10.000, nummer van de woordenboekenfamilie waar dit woord toe behoort |
| tekst | Tekst van het gedeelte |
| type | Type, dus gebruik in NT, in Oud Grieks etc. |

### woordenboek2
| Veld  | Uitleg  |
| ------------ | ------------ |
| griUniekeid | Unieke id van van het lexeem dat beschreven wordt, kopelt het aan "id" van GriNe |
| van | Id van het gedeelte van de woordenboekomschrijving |
| tot | Hoogste id van alle subkopjes die onder dit gedeelte vallen |
| indent | Hoeveel dit gedeelte moet verspringen |
| tekst | Tekst van het woordenboekgedeelte, omschrijving |
| grVertaalid | De vertaling van het lexeem die omschreven wordt, koppelt aan "id" van "GrVertaal" |

## Bronnen
De data van enkele tabellen is verkregen uit (verwerking van) data van andere bronnen.

De Concordant Greek tekst is oorspronkelijk uitgegeven door Concordant Publishing Concern uit Amerika, zie [https://www.concordant.org](https://www.concordant.org "https://www.concordant.org"). Deze tekst is gedigitaliseerd door André de Mol van Schripture4All, zie [https://www.scripture4all.org](https://www.scripture4all.org "https://www.scripture4all.org"). Hij heeft deze data vervolgens aan het NCV project verleend, waar het, met een enkele bewerking om meer in overeenstemming te komen met de papieren uitgave, de Griekse tekst van de CGT tabel vormt. Raadpleeg voor heruitgaven deze mensen.

De data uit de bhs tabellen is een verregaande verwerking van de data uit meerdere openbare bronnen, voornamelijk de [ETCBC](http://etcbc.nl/ "ETCBC") database en de [OSHB](https://hb.openscriptures.org/HomeFiles/Oshb.html "OSHB") database. Over de verwerking van de data uit deze databases is meer geschreven in [dit artikel](https://ncv-bijbelstudie.nl/achtergrond/het-hebreeuwse-interlineair-tekst-en-stam-en-trefwoorden/ "dit artikel").

De Schriftwoordvertaling is met toestemming overgenomen van [https://www.schriftwoord.nl/](https://www.schriftwoord.nl/ "https://www.schriftwoord.nl/"), zoals te vinden in de tabel "Bijbel". Daar komt ook de Nederlandse vertaling van het Concordant Commentaar voor het NT vandaan, dat te vinden is in de tabel "com". Voor eigen studiedoeleinden mag de tekst zonder toestemming vermenigvuldigd worden, voor commerciële uitgaven moet de uitgever benaderd worden, zie website.

## Database
De .sqlite database geeft de structuur weer van de data, hoe het in tabellen staat, wat de eigenschappen van de tabellen zijn en wat de indexes zijn. De data zelf is geëxporteerd in csv bestanden, te vinden in map "tabellen", waarna de data uit de database zelf gehaald is, omwille van het klein houden van het bestand. De data is verwijderd met de volgende queries:

```sql
DELETE FROM CGT;
DELETE FROM GE;
DELETE FROM GrParsings;
DELETE FROM GrVertaal;
DELETE FROM GrWoorden;
DELETE FROM GriNe;
DELETE FROM HE;
DELETE FROM HeParsings;
DELETE FROM HeWoorden;
DELETE FROM HebNe;
DELETE FROM NCV;
DELETE FROM NCVkopjes;
DELETE FROM NCVpar;
DELETE FROM Struct;
DELETE FROM Structregels;
DELETE FROM Vertalingen;
DELETE FROM VertalingenLink;
DELETE FROM bhs;
DELETE FROM bhs_qre;
DELETE FROM bhs_tk;
DELETE FROM bijbels;
DELETE FROM com;
DELETE FROM strongGR;
DELETE FROM strongHb;
DELETE FROM strongLink;
DELETE FROM vidToCom;
DELETE FROM voetnoten;
DELETE FROM woordenboek;
DELETE FROM woordenboek2;
VACUUM;
```

De oorspronkelijke database kan weer verkregen worden door alle csv bestanden in de juiste tabellen te importeren.