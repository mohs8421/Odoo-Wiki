---
title: Aufwand Aktionen
description: Aktionen für Aufwand App einrichten.
tags:
- HowTo
prev: ./hr-attendance
---
# Aufwand Aktionen
![icons_odoo_hr_expense](attachments/icons_odoo_hr_expense.png)

{{ $frontmatter.description }}

## Aktionen

### Auslagenbericht zurücksetzen

Navigieren Sie nach *Einstellungen > Technisch > Server Aktionen* und erstellen Sie einen neuen Eintrag:

Name der Aktion: `Auslagenbericht zurücksetzen`\
Modell: `hr.expense.sheet`\
Folgeaktion: `Python-Code ausführen`

Kopieren Sie die folgenden Zeilen in das Feld *Python-Code*:

```python
for rec in records:  
  rec.action_unpost()
```

Die Aktion mit dem Knopf *Kontextuelle Aktion erstellen* bestätigen und speichern. In der Ansicht der Auslagenberichte können Sie *Aktion > Auslagenbericht zurücksetzen* anwählen.