# Allgemein

-   [Bestellungen auf dem Dashboard](#dashboard)
    -   [Anzahl Bestellungen](#count)
    -   [Typ Bestellungen](#type)
    -   [Sortierung](#sort)
    -   [Bestellungen ausschließen](#exclude)
    -   [Bestellinfos](#infos)
    -   [Zusätzliche Optionen für die Bulk-Erstellung](#bulk-options)
-   [Einstellung Bulk-Verarbeitung](#settings-bulk)
    -   [Anzahl Artikel als Bulk-Grenze](#items-count)
    -   [Sortierung als Bulk-Versandlabels](#sort-bulk)
    -   [Bulk-Ergebnis per E-Mail versenden](#email-bulk)
    -   [Staffelung der Stapelverarbeitung](#chunk-bulk)
-   [Dokumente sortiert zusammenführen](#merge)
-   [Weitere Options](#more-options)
-   [FAQ](#faq)

<a name="dashboard"></a>

## Bestellungen auf dem Dashboard

Konfiguriere, wie Bestellungen auf dem Dashboard dargestellt werden sollen. <a class="video">https://youtu.be/zUGuI1ka880</a>

<a name="count"></a>

### Anzahl Bestellungen

Lege fest, wieviele Bestellungen maximal im Dashboard angezeigt werden sollen.

<a name="type"></a>

### Typ Bestellungen

Wähle, ob alle offenen oder nur bezahlte Bestellungen geladen werden sollen.

<a name="sort"></a>

### Sortierung

Wähle, ob Bestellungen nach Datum auf- oder absteigend sortiert angezeigt werden sollen.

<a name="exclude"></a>

### Bestellungen ausschließen

Trage einen oder mehrere Tags ein, anhand derer Bestellungen aus dem Dashboard ausgeschlossen werden sollen.

<a name="infos"></a>

### Bestellinfos

Wähle, welche Informationen zu den Bestellungen im Dashboard angezeigt werden sollen.

<a name="bulk-options"></a>

### Zusätzliche Optionen für die Bulk-Erstellung

#### Wunschdatum

Blende das Eingabefeld für die Wunschzustellung im Dashboard ein.

#### Blätterfunktion

Aktiviere die Blätterfunktion im Dashboard.

<a name="settings-bulk"></a>

## Einstellung Bulk-Verarbeitung

Konfiguriere, wie die Bulk-Verarbeitung durchgeführt werden soll. <a class="video">https://youtu.be/2DhmAx5W5hQ</a>

<a name="items-count"></a>

### Anzahl Artikel als Bulk-Grenze

Lege fest, ob ab einer gewissen Artikelanzahl die Erstellung eines Labels über die Bulkverarbeitung verhindert wird. Dies insbesondere nützlich, wenn bei vielen Artikeln innerhalb einer Bestellung mehrere Labels erstellt werden sollen.

<a name="sort-bulk"></a>

### Sortierung als Bulk-Versandlabels

Stelle ein, wie Versandlabels bei der Bulk-Ausführung sortiert werden sollen. Mit Standard wird die Selektion aus dem Dashboard übernommen. Sortierung nach SKU und Artikel/SKU erfolgt anhand des ersten Artikels in der Bestellung.

<a name="email-bulk"></a>

### Bulk-Ergebnis per E-Mail versenden

Wenn Du hier eine E-Mail-Adresse hinterlegst, wird der Link zum Ergebnis (Downloadseite) anschließend an diese E-Mail-Adresse gesendet.

<a name="chunk-bulk"></a>

### Staffelung der Stapelverarbeitung

Wir empfehlen hier nicht mehr als 250 auszuwählen. Als Bespiel: Ist hier 50 eingestellt, werden bei einer Auswahl von 80 Bestellungen für die Stapelverarbeitung, diese in zwei Ergenisse aufgeteilt und zwar zu 50 und 30 Bestellungen / Versandlabels.

<a name="merge"></a>

## Dokumente sortiert zusammenführen

Aktiviere diese Option, um alle Dokumente (Labels, Zollerklärungen, Lieferscheine und Rechnungen) sortiert nach Bestellnummer in einem PDF zu erhalten. <a class="video">https://youtu.be/epstS88Gn94</a>

Neben dem Download kann das gesamte Dokument per Mail an die angegebene Adresse verschickt werden.

<a name="more-options"></a>

## Weitere Optionen

Lege fest, ob erstelltes Label direkt heruntergeladen werden soll.

<a name="faq"></a>

## FAQ

<div class="faq-list">
<dl class="space-y-8">
<div>
<dt><h4>Statt der Name unserer Firma wird einfach unsere Firmenadresse (Straße) angezeigt. Wie können wir das ändern?</h4></dt>
<dd>In dem Fall werdet ihr voraussichtlich keine Absender Referenz verwenden und zwar die Adressen, die ihr in Shopify hinterlegt habt. dazu müsst ihr einmal in die Shopify Einstellungen unten links im Shopify Admin und dann unter Standorte beziehungsweise in Englisch Locations eure Adressen überprüfen. Dort ist oft als Standort Name die Straße oder Adresse eingetragen. Hier bitte die Standorte entsprechend korrigieren. Dann einen Moment warten und wieder in die App easy DHL unter Einstellungen Versand wechseln. Dort habt ihr dann in einem dropdown eure Standorte zur Auswahl. Sollten die Änderung noch nicht sichtbar sein, dann bitte einmal eine halbe Minute warten und einen browser-reload der App durchführen</dd>
</div>

<div>
<dt><h4>Benutzername und Password stimmen aber ich kann mich nicht anmelden, woran liegt das?</h4></dt>
<dd>Solltest du die 2FA Authentifizierung im DHL Geschäftskunden Portal aktiviert haben, dann wird es höchstwahrscheinlich am gewählten Sicherheitsproblem liegen. Hier entweder die 2FA komplett deaktiviert oder aber das Sicherheitsprofil wie folgt geändert werden, siehe Screenshot - "Absicherung sicherheitsrelevanter Änderungen"

![DHL-2fa-Problem](https://media.247apps.de/storage/faq/dhl-2fa-problem.png)

</dd>
</dl>
</div>
</div>
