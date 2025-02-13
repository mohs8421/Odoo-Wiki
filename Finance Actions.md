---
title: Finanzen Aktionen
description: Neue Aktionen für Buchungen und Abstimmungen.
tags:
- HowTo
- Aktionen
prev: ./finance
---
# Finanzen Aktionen
![icons_odoo_account_accountant](attachments/icons_odoo_account_accountant.png)

{{ $frontmatter.description }}

## Aktionen

### Als gesendet markieren

Navigieren Sie nach *Einstellungen > Technisch > Server Aktionen* und erstellen Sie einen neuen Eintrag:

Name der Aktion: `Als gesendet markieren`\
Modell: `account.move`\
Folgeaktion: `Python-Code ausführen`

```python
for record in records:
	record.write({ 'is_move_sent': True })
```

Die Aktion mit dem Knopf *Kontextuelle Aktion erstellen* bestätigen und dann speichern.

In der Liste der Buchungssätze erscheint nun in der Auswahl *Aktion* das Menu *Als gesendet markieren*.

### Als ungebucht markieren

Navigieren Sie nach *Einstellungen > Technisch > Server Aktionen* und erstellen Sie einen neuen Eintrag:

Name der Aktion: `Als ungebucht markieren`\
Modell: `account.move`\
Folgeaktion: `Python-Code ausführen`

```python
for record in records:
	if record.state != 'cancel':
		UserError('Can only unpost entry if it is cancelled.')
	record.write({ 'posted_before': False })
```

Die Aktion mit dem Knopf *Kontextuelle Aktion erstellen* bestätigen und dann speichern.

In der Liste der Buchungssätze erscheint nun in der Auswahl *Aktion* das Menu *Als ungebucht markieren*.

### Bankauszug zurücksetzen

Navigieren Sie nach *Einstellungen > Technisch > Server Aktionen* und erstellen Sie einen neuen Eintrag:

Name der Aktion: `Bankauszug zurücksetzen`\
Modell: `account.bank.statement`\
Folgeaktion: `Python-Code ausführen`

Kopieren Sie die folgenden Zeilen in das Feld *Python-Code*:

```python
for record in records:  
  record.button_reopen()
```

Die Aktion mit dem Knopf *Kontextuelle Aktion erstellen* bestätigen und dann speichern.

In der Liste der Belege erscheint nun in der Auswahl *Aktion* das Menu *Bankauszug zurücksetzen*.

### Bankauszug bestätigen

Navigieren Sie nach *Einstellungen > Technisch > Server Aktionen* und erstellen Sie einen neuen Eintrag:

Name der Aktion: `Bankauszug bestätigen`\
Modell: `account.bank.statement`\
Folgeaktion: `Python-Code ausführen`

Kopieren Sie die folgenden Zeilen in das Feld *Python-Code*:

```python
for record in records:  
  record.button_validate_or_action()
```

Die Aktion mit dem Knopf *Kontextuelle Aktion erstellen* bestätigen und dann speichern.

In der Liste der Belege erscheint nun in der Auswahl *Aktion* das Menu *Bankauszug bestätigen*.

![Finanzen Aktionen Bankauszug bestätigen](attachments/Finanzen%20Aktionen%20Bankauszug%20bestätigen.gif)

### Buchungszeilen aktualisieren

Navigieren Sie nach *Einstellungen > Technisch > Server Aktionen* und erstellen Sie einen neuen Eintrag:

Name der Aktion: `Buchungszeilen aktualisieren`\
Modell: `account.move`\
Folgeaktion: `Python-Code ausführen`

```python
for rec in records.filtered(lambda r: r.state == 'draft'):
  rec.with_context(check_move_validity=False)._move_autocomplete_invoice_lines_values()
```

Die Aktion mit dem Knopf *Kontextuelle Aktion erstellen* bestätigen und dann speichern.

In der Liste der Buchungssätze erscheint nun in der Auswahl *Aktion* das Menu *Buchungszeilen aktualisieren*.

![Finanzen Buchungszeilen aktualisieren](attachments/Finanzen%20Buchungszeilen%20aktualisieren.gif)

### Auf Entwurf zurücksetzen

Navigieren Sie nach *Einstellungen > Technisch > Server Aktionen* und erstellen Sie einen neuen Eintrag:

Name der Aktion: `Auf Entwurf zurücksetzen`
Modell: `account.move`
Folgeaktion: `Python-Code ausführen`

Kopieren Sie die folgenden Zeilen in das Feld *Python-Code*:

```python
for record in records:  
  record.button_draft()
```

Die Aktion mit dem Knopf *Kontextuelle Aktion erstellen* bestätigen und dann speichern.

In der Liste der Buchungssätze erscheint nun die Auswahl *Aktion > Auf Entwurf zurücksetzen*.

### Abstimmung zurücksetzen

Navigieren Sie nach *Einstellungen > Technisch > Server Aktionen* und erstellen Sie einen neuen Eintrag:

Name der Aktion: `Abstimmung zurücksetzen`\
Modell: `account.bank.statement.line`\
Folgeaktion: `Python-Code ausführen`

Kopieren Sie die folgenden Zeilen in das Feld *Python-Code*:

```python
for record in records:  
  record.button_undo_reconciliation()
```

Die Aktion mit dem Knopf *Kontextuelle Aktion erstellen* bestätigen und dann speichern.

In der Liste der Vorgänge erscheint nun in der Auswahl *Aktion* das Menu *Abstimmung zurücksetzen*.

### Als gebucht markieren

Navigieren Sie nach *Einstellungen > Technisch > Server Aktionen* und erstellen Sie einen neuen Eintrag:

Name der Aktion: `Als gebucht markieren`
Modell: `account.move`
Folgeaktion: `Python-Code ausführen`

Kopieren Sie die folgenden Zeilen in das Feld *Python-Code*:

```python
for record in records:
  record.write({'state': 'posted'})
```

Die Aktion mit dem Knopf *Kontextuelle Aktion erstellen* bestätigen und dann speichern.

In der Liste der Buchungssätze erscheint nun in der Auswahl *Aktion* das Menu *Als gebucht markieren*.

### Zahlung gesendet zurücksetzen

Navigieren Sie nach *Einstellungen > Technisch > Server Aktionen* und erstellen Sie einen neuen Eintrag:

Name der Aktion: `Zahlung gesendet zurücksetzen`\
Modell: `account.payment`\
Folgeaktion: `Python-Code ausführen`

Kopieren Sie die folgenden Zeilen in das Feld *Python-Code*:

```python
for record in records:  
  record.write({'is_move_sent': False})
```

Die Aktion mit dem Knopf *Kontextuelle Aktion erstellen* bestätigen und dann speichern.

In der Liste der Zahlung erscheint nun in der Auswahl *Aktion* das Menu *Zahlung gesendet zurücksetzen*.

### Mahnstufe anzeigen

Navigieren Sie nach *Einstellungen > Technisch > Server Aktionen* und erstellen Sie einen neuen Eintrag:

Name der Aktion: `Mahnstufe anzeigen`\
Modell: `res.partner`\
Folgeaktion: `Python-Code ausführen`

Kopieren Sie die folgenden Zeilen in das Feld *Python-Code*:

```python
records.ensure_one()
followup_level = records._query_followup_level()
raise UserError(followup_level.items())
```

Die Aktion mit dem Knopf *Kontextuelle Aktion erstellen* bestätigen und dann speichern.

### Analysekonto entfernen

Navigieren Sie nach *Einstellungen > Technisch > Server Aktionen* und erstellen Sie einen neuen Eintrag:

Name der Aktion: `Analysekonto entfernen`\
Modell: `account.move`\
Folgeaktion: `Python-Code ausführen`

Kopieren Sie die folgenden Zeilen in das Feld *Python-Code*:

```python
for rec in records:
	rec.line_ids.write({'analytic_account_id': False})
```

Die Aktion speichern und mit dem Knopf *Kontextuelle Aktion erstellen* bestätigen.

### Steuersätze aktualisieren

Navigieren Sie nach *Einstellungen > Technisch > Server Aktionen* und erstellen Sie einen neuen Eintrag:

Name der Aktion: `Steuersätze aktualisieren`\
Modell: `account.move`\
Folgeaktion: `Python-Code ausführen`

Kopieren Sie die folgenden Zeilen in das Feld *Python-Code*:

```python
for rec in records:
	rec.button_draft()
	for line in rec.line_ids.filtered(lambda l: l.product_id):
		line.write({'tax_ids': [line.product_id.taxes_id.id]})
	rec.action_post()
```

Die Aktion speichern und mit dem Knopf *Kontextuelle Aktion erstellen* bestätigen.

## Geplante Aktionen

### Rechnung mit Abrechnungsinterval generieren

Das ist eine einfach Lösung um wiederholgende Rechnung zu generieren. Mit dem zusätzlichen Feld `x_recurring_inverval` wird geprüft ob die Rechnung wieder fällig ist.

Navigieren Sie nach *Einstellungen > Technisch > Geplante Aktionen* und erstellen Sie einen neuen Eintrag:

Name der Aktion: `Rechnung mit Abrechnungsinterval generieren`\
Modell: `ir.actions.server`\
Ausführen alle: `1` Tage\
Nächstes Ausführungsdatum: `DD.MM.YYYY 06:00:00`\
Anzahl der Anrufe: `-1`\
Folgeaktion: `Python-Code ausführen`

Kopieren Sie die folgenden Zeilen in das Feld *Python Code*:

```python
today = datetime.datetime.today()

def add_month(date):
  
    # Determine the year and month for the new date
    new_year = date.year
    new_month = date.month + 1

    # If the new month is greater than 12, subtract 12 and increment the year
    if new_month > 12:
        new_month -= 12
        new_year += 1

    # Return the new date
    return datetime.datetime(new_year, new_month, date.day)

# Get posted invoices with recurring interval within the last 40 days
invoice_ids = env['account.move'].search([
  ('x_recurring_inverval', 'in', ['monthly']),
  ('invoice_date', '>=', (today - datetime.timedelta(days=32)).strftime('%Y-%m-%d'))
], order='invoice_date desc')

# Foreach invoice check if is due
refs = []
for invoice in invoice_ids:
  
  if invoice.x_recurring_inverval == 'monthly' and invoice.ref not in refs:
    # Update ref list to avoid multiple duplicates
    refs.append(invoice.ref)
    
    # Duplicate invoice
    invoice_date = invoice.invoice_date
    last_date = datetime.date(today.year, abs(today.month-1), today.day)
    if invoice_date <= last_date:
      new_invoice = invoice.copy({
        'invoice_date': add_month(invoice_date),
        'ref': invoice.ref,
      })
      env.cr.commit()
    
    # raise UserError([invoice.name, refs, invoice_date, last_date,  invoice_date <= last_date, add_month(invoice_date)])
```