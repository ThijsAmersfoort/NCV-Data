# NCV Data
### Versie 3.10.0, december 2021
In de sqlite database in deze map is de data van het NCV project te vinden zoals deze eind december 2021 was, en is verschenen in versie 3.10.0 van de app, uitgebracht op 8 januari 2022. De database bevat de NCV vertaling, het interlineair bij de Griekse en Hebreeuwse grondtekst, structure, commentaar, voetnoten en meer. Onder is per tabel in de database beschreven wat de data inhoudt.

Aan het gebruik van de data zijn voorwaarden verbonden, zoals beschreven in het LICENSE bestand.

(onderstaande kopjes worden nog verder uitgewerkt)

## Bronnen
(waar de data vandaan komt)

## Structuur van de data
(uitleg vid, vertaling uit verschillende tabellen, interlineair uit verschillende tabellen etc)

## Uitleg tabellen
(per tabel welke info de velden bevatten)

## Indexes
Om de grootte van de database te verkleinen zijn de indexes eruit gehaald en bevat de database puur de data. Om bruikbaar te zijn is het aan te raden de indexes weer toe te voegen. Van de indexes die zijn verwijderd staan hieronder de queries.

```sql
CREATE INDEX IF NOT EXISTS CGTvertaal ON "CGT" ("vertaalwoord");

CREATE INDEX IF NOT EXISTS CGTindex7 ON "CGT" ("role");

CREATE INDEX IF NOT EXISTS CGTind ON "CGT" ("id");

CREATE INDEX IF NOT EXISTS index8 ON "GrWoorden" ("translitz");

CREATE INDEX IF NOT EXISTS index7 ON "GrWoorden" ("griUniekeid");

CREATE INDEX IF NOT EXISTS index6 ON "GrWoorden" ("strong");

CREATE INDEX IF NOT EXISTS index5 ON "GrWoorden" ("grieks");

CREATE INDEX IF NOT EXISTS index4 ON "GrWoorden" ("nedSz");

CREATE INDEX IF NOT EXISTS index3 ON "GrWoorden" ("nedIz");

CREATE INDEX IF NOT EXISTS index2 ON "GrWoorden" ("CGTparsingT");

CREATE INDEX IF NOT EXISTS index1 ON "GrWoorden" ("CGTparsing");

CREATE INDEX IF NOT EXISTS index9 ON "GrWoorden" ("samen");

CREATE INDEX IF NOT EXISTS HEWindex1 ON "HeWoorden" ("CHTparsing");

CREATE INDEX IF NOT EXISTS HEWindex2 ON "HeWoorden" ("CHTparsingT");

CREATE INDEX IF NOT EXISTS HEWindex3 ON "HeWoorden" ("cons");

CREATE INDEX IF NOT EXISTS HEWindex4 ON "HeWoorden" ("translitz");

CREATE INDEX IF NOT EXISTS HEWindex5 ON "HeWoorden" ("nedSz");

CREATE INDEX IF NOT EXISTS HEWindex6 ON "HeWoorden" ("nedIz");

CREATE INDEX IF NOT EXISTS HEWindex7 ON "HeWoorden" ("strong");

CREATE INDEX IF NOT EXISTS HEWindex8 ON "HeWoorden" ("hebUniekeid");

CREATE INDEX IF NOT EXISTS NCVinde ON "NCV" ("vid", "GTbegin");

CREATE INDEX IF NOT EXISTS bhsindex1 ON "bhs" ("id");
```

Deze indexes zijn verwijderd met de volgende queries:

```sql
DROP INDEX CGTvertaal;

DROP INDEX CGTindex7;

DROP INDEX CGTind;

DROP INDEX index8;

DROP INDEX index7;

DROP INDEX index6;

DROP INDEX index5;

DROP INDEX index4;

DROP INDEX index3;

DROP INDEX index2;

DROP INDEX index1;

DROP INDEX index9;

DROP INDEX HEWindex1;

DROP INDEX HEWindex2;

DROP INDEX HEWindex3;

DROP INDEX HEWindex4;

DROP INDEX HEWindex5;

DROP INDEX HEWindex6;

DROP INDEX HEWindex7;

DROP INDEX HEWindex8;

DROP INDEX NCVinde;

DROP INDEX bhsindex1;
```
