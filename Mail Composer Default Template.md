---
title: Mail Composer Default Template
description: Standardvorlage für Mail-Dialog festlegen.
tags:
- HowTo
- Drittanbieter
prev: ./discuss
---
# Mail Composer Default Template
![icon_oms_box](attachments/icon_oms_box.png)

{{ $frontmatter.description }}
 
Technischer Name: `mail_composer_default_template`\
Repository: <https://github.com/Mint-System/Odoo-Apps-Social/tree/14.0/mail_composer_default_template>

## Verwendung

### Standardvorlage für Mail-Dialog definieren

Wenn Sie diese Erweiterung installiert haben und den Mail-Dialog auf einem Geschäftsobjekt öffnen, wird die erste Mail-Vorlage gemäss Sequenz und Filter geladen.

![Mail Composer Default Template](attachments/Mail%20Composer%20Default%20Template.gif)

::: tip
Beim Aufruf des Mail-Dialog wird die Vorlage in folgender Reihenfolge ausgewählt:
* Filterung nach Geschäftsobjekt
* Filterung nach Sequenz
* Filterung nach Domain
:::

### Sequenz der E-Mail-Vorlagen festlegen

Zeigen Sie die E-Mail-Vorlagen unter *Einstellungen > Technisch > Vorlagen* an. Sortieren Sie die Vorlagen mit dem *Handler*.

![Mail Composer Default Template Sequence](attachments/Mail%20Composer%20Default%20Template%20Sequence.gif)

### Domain-Filter auf E-Mail-Vorlage festlegen

Rufen Sie eine E-Mail-Vorlage unter *Einstellungen > Technisch > Vorlagen* auf. Legen Sie eien Filter im *Domain* für die ausgewählten Geschäftsobjekte fest.

![](attachments/Mail%20Composer%20Default%20Template%20Domain.png)