---
title: E-Mails verarbeiten
description: Eine einfache und umfassende Odoo-Dokumentation.
tags:
- Best-Practice
prev: ./best-practice
---
# E-Mails verarbeiten

## Allgemein

Auf bestimmten Odoo-Objekten können Sie E-Mail-Adressen einrichten. Wenn E-Mails im Postfach von Odoo mit der entsprechenden Adresse eintreffen, ordnet Odoo den Inhalt und Ahänge des E-Mails dem entsprechenden Odoo-Objekt zu.

### E-Mail Kopfzeilen

Odoo koordiniert die Kommunikation zwischen Geschäftsobjekten und den E-Mail-Empfängen mit Headern im E-Mail. Dazu die wichtigsten:

* **reply-to**: Antworten an den E-Mail-Absender werden an diese Adresse umgeleitet. Es handelt sich um die sog. Catchall-Adresse.
* **from**: Normalerweise der/die BenutzerIn, welche die E-Mail verschickt hat.
* **x-odoo-objects**: Eindeutige Referenz auf das Geschäftsobjekt.

 Dazu ein Beispiel:

![](attachments/Infomaniak%20Kopfzeilen.png)

Diese Header werden beim Empfang der Antwort-Mail von Odoo verarbeitet und dem entsprechenden Geschäftsobjekt zugeordnet.

## Rechnungen empfangen

Es macht Sinn, dass man Rechnungen per E-Mail empfangen kann. Dazu braucht es zwei Einstellungen. Erstens muss man den [eingehenden Mail-Server konfigurieren](Discuss%20E-Mail.md#Eingehender%20Mail-Server%20konfigurieren).
Zweitens muss man [Rechnung per E-Mail empfangen](Finance.md#Rechnung%20per%20E-Mail%20empfangen) einrichten.

Wenn alles eingerichtet ist, können Sie mit [Verarbeiten von eingehenden E-Mails ausführen](Discuss%20E-Mail.md#Verarbeiten%20von%20eingehenden%20E-Mails%20ausführen) den Abruf der E-Mails anstossen.

