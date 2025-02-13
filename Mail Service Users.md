---
title: Mail Service Users
description: Service-Benutzer von Lizenzvertrag ausschliessen.
tags:
- HowTo
- Drittanbieter
prev: ./settings-login
---
# Mail Service Users
![icon_oms_box](attachments/icon_oms_box.png)

{{ $frontmatter.description }}

Technischer Name: `mail_service_users`\
Repository: <https://github.com/Mint-System/Odoo-Apps-Server-Tools/tree/15.0/mail_service_users>

## Verwendung

### Benutzer als Service-Benutzer festlegen

Mit dieser Erweiterung können Sie bestimmte Benutzer als *Service-Benutzer* markieren. Diese Benutzer werden vom Lizenzvertrag von Odoo augeschlossen. Sie dürfen diese Benutzer nicht als persönliches Login verwenden.

Rufen Sie einen Benutzer via *Einstellungen > Benutzer und Unternehmen > Benutzer* auf. Setzen Sie die Checkbox wenn es sich um einen Service-Benutzer handelt.

![](attachments/Mail%20Service%20Users.png)

Unter Einstellungen wird die Zahl der aktiven Benutzer entsprechend angepasst.

![](attachments/Mail%20Service%20Users%20Einstellungen.png)

::: warning
Dieses Modul verändert die Berechnung der aktiven Benutzer auf dem System. Ist die Erweiterung aktiv verstossen Sie gegen die Bedingungen im Odoo Enterprise Lizenzvertrag. 
:::