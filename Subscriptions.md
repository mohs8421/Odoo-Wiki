---
title: Abonnements
description: Wiederkehrende Rechnungsstellung und Management von Abonnenten auf einfache Art und Weise.
tags:
- HowTo
prev: ./
---
# Abonnements

![icons_odoo_account_invoicing](attachments/icons_odoo_account_invoicing.png)

{{ $frontmatter.description }}

Website: <https://www.odoo.com/de_DE/app/subscriptions>

## Verwendung

### Abonnement-Vorlage erstellen

Rufen Sie die Ansicht *Abonnements > Konfiguration > Vorlage für Abonnements* auf. Erstellen Sie einen neuen Eintrag. Geben Sie einen Namen beispielsweise *Jahresabonnment* ein. Legen Sie den *Abrechnungszeitraum* und einen *Code* fest.

![](attachments/Abonnements%20Vorlage.png)

### Abonnement erstellen

Im Normalfall wird beim [Angebot bestätigen](Sale.md#Angebot%20bestätigen) ein Abonnement generiert. Wenn Sie ein Abonnment ohne Verkaufsauftrag erstellen möchten, navigieren Sie nach *Abonnement* und klicken auf *Neu*.

### Abonnement-Laufzeit mit Produktvariante verknüpfen

Öffnen Sie ein Abonnent-Produkt unter *Abonnements > Abonnements > Produkte*. Zeigen Sie den Tab *Preis* an. Legen Sie in der Spalte *Produktvarianten* fest, welche Laufzeit zu welcher Variante gehört. Dazu ein Beispiel.

![](attachments/Abonnements%20Produktvarainten.png)

### Abonnement-Laufzeit mit Produktvariante und Preisliste verknüpfen

Wenn Sie [Preislisten aktivieren](Sale%20Price.md#Preislisten%20aktivieren) und eine [Abonnement-Laufzeit mit ein Produktvariante verknüpfen](#Abonnement-Laufzeit%20mit%20Produktvariante%20verknüpfen), können Sie zusätzlich eine Preislisteliste auswählen.

Wenn Sie die ausgewählte [Preisliste anzeigen](Sale%20Price.md#Preisliste%20anzeigen) sehen Sie im Tab *Zeitbasierte Regel* die erstellten Verknüpfungen.