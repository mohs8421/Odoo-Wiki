---
title: Devisenhandel
description: Eine einfache und umfassende Odoo-Dokumentation.
tags:
- Best-Practice
prev: ./best-practice
---
# Devisenhandel

## Geld von einem Bankkonto mit unterschiedlicher Währung auf ein anderes transferieren

Haben Sie [Mehrere Währungen aktiviert](Finance%20Multicurrency.md#Mehrere%20Währungen%20aktivieren) und möchten beispielsweise vom USD-Bankkonto zum CHF-Bankkonto Geld transferieren, können Sie das mit internen Überweisungen erledigen.

Als erstes müssen Sie auf dem CHF-Bankjournal eine [interne Überweisung erstellen](Finance%20Accounting.md#Interne%20Überweisung%20erstellen). Wählen Sie als *Zahlungsart* die Option *Geld schicken*.

Auf dem USD-Bankjournal erstellen Sie eine interne Überweisung mit der Optional *Geld erhalten* als *Zahlungsart*.

Nun führen Sie die entsprechende Überweisung im eBanking bzw. Portal für den Devisenhandel aus.

Wurde die Überweisung ausgeführt, können Sie für beide Bankjournale eine [Abstimmung durchführen](Finance%20Reconcile.md#Abstimmung%20durchführen).

Beispiel CHF-Konto:

![](attachments/Best%20Practice%20Devisenhandel%20Abgleich%20CHF.png)

Beispiel USD-Konto:

![](attachments/Best%20Practice%20Devisenhandel%20Abgleich%20USD.png)

Odoo übernimmt jeweils die Umrechnung der Währungen.