---
title: Verkauf Projekt
description: Dienstleistungen mit Verkauf und Projekt abwickeln.
tags:
- HowTo
prev: ./sale
---
# Verkauf Projekt
![icons_odoo_sale](attachments/icons_odoo_sale.png)

{{ $frontmatter.description }}

## Abrechnung

### Dienstleistung für Zeiterfassung konfigurieren

Mit Verkauf, Projekt und Zeiterfassung können Sie Dienstleistung mit Zeiterfassung erstellen. Navigieren Sie nach *Verkauf > Produkte > Produkte* erstellen oder öffnen Sie ein Dienstleistungs-Produkt. Hier die wichtigsten Konfigurationen:

![](attachments/Produkt%20Dienstleistung.png)

* **Produktart**: Muss als Dienstleistung festgelegt sein.
* **Fakturierungsregel**: Basis für Abrechnung der Dienstleistungseinheiten.
* **Eine Bestellung erstellen**: Projekt, Aufgabe oder beides bei Bestätigungs des Auftrags erstellen. 
* * **Projekt**: Projekt in welchem die Aufgabe erstellt wird.
* **Projekt-Vorlage**: Projekt welches als Vorlage kopiert wird.

### Bestehendes Projekt verknüpfen

Wenn Sie ein bestehendes Projekt mit Dienstleistungen aus einem Verkaufsauftrag verknüpfen möchten, müssen Sie mindestes eine Dienstleistung als Auftragszeile hinzugefügt haben.

![Verkauf Projekt Verknüpfung](attachments/Verkauf%20Projekt%20Verknüpfung.gif)