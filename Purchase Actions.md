---
title: Einkauf Aktionen
description: Arbeitsflüsse in Einkauf automatisieren.
tags:
- HowTo
prev: ./
---
# Einkauf Aktionen
![icons_odoo_purchase](attachments/icons_odoo_purchase.png)

{{ $frontmatter.description }}

## Automatische Aktionen

### Bestellfrist festlegen

Mit Aktionen können Felder mit einem bestimmten Default-Wert beschrieben werden. Im folgenden Beispiel wird das Feld *Order Deadline* auf Angebotsanfragen auf das Datum *heute + 5 Tage* gesetzt.

Navigieren Sie nach *Einstellungen > Technisch > Automation > Automatische Aktionen* und erstellen Sie den folgenden Eintrag:

* Name der Aktion: `Bestellfrist festlegen`
* Modell: `Beschaffungsauftrag`
* Auslöser: `Bei Erstellung`
* Folgeaktion: `Den Datensatz aktualisieren`
* Feld: `Order Deadline (purchase.order)`
* Wert: `datetime.datetime.today() + datetime.timedelta(days=5)`

## Automatische Aktionen

### Aktivität Rechnung prüfen für Käufer erstellen

Mit dieser automatischen Aktion wird beim anwählen der Option *Zum Überprüfen* auf einer Rechnung mit einem Einkauf eine Aktivität zur Prüfung der Rechnung dem Käufer zugeordnet.

Erstellen Sie unter *Einstellungen > Technisch > Automation > Automatische Aktionen* einen Eintrag mit diesen Werten:

Name der Aktion: `Aktivität Rechnung prüfen für Käufer erstellen`\
Modell: `acclount.move`\
Auslöser: Beim Aktualisieren\
Trigger-Felder: `to_check`
Anzuwenden auf: `[("to_check", "=", True),("purchase_order_count",">",0)]`
Folgeaktion: Python-Code ausführen\
Python-Code:

```python
for rec in records:
  user_id = rec.line_ids.purchase_line_id.order_id.user_id[0]
  if user_id:
    env['mail.activity'].create({
      'activity_type_id': env.ref('mail.mail_activity_data_todo').id,
      'summary': 'Rechnung prüfen',
      'note': 'Das ist eine Rechnung zu einer Bestellung von Ihnen. Bitte überprüfen die Rechunung und wählen Sie "Als geprüft markieren".',
      'res_id': rec.id,
      'res_model_id': env.ref('account.model_account_move').id,
      'user_id': user_id.id,
    })
```