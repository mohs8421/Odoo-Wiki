---
title: Entwicklung Berichte
description: Eigene Berichte mit QWeb erstellen.
tags:
- HowTo
prev: ./development
---
# Entwicklung Berichte
![icons_odoo_web_studio](attachments/icons_odoo_web_studio.png)

{{ $frontmatter.description }}

## Ansicht

### Bericht als Webseite anzeigen

Eine Übersicht der wichtigsten Berichte und deren URL:

| Name                      | URL                                                                             |
|:------------------------- |:------------------------------------------------------------------------------- |
| Angebot / Auftrag         | `/report/html/sale.report_saleorder/$ID`                                        |
| Angebotsanfrage           | `/report/html/purchase.report_purchasequotation/$ID`                            |
| Attendance and Leave      | `/report/html/hr_employee_attendance_report.res_users/$ID`                      |
| Barcode EAN-13            | `/report/barcode/?type=EAN13&value=0769503968353width=600&height=150`           |
| Barcodes (PDF)            | `/report/html/stock.label_transfer_template_view_pdf/$ID`                       |
| Bordereau                 | `/report/html/report/html/mint_system.stock.report_bordero.basis57/$ID`         |
| Fertigungsauftrag         | `/report/html/mrp.report_mrporder/$ID`                                          |
| Kaufvertrag               | `/report/html/purchase_requisition.report_purchaserequisitions/$ID`             |
| Lieferschein              | `/report/html/stock.report_deliveryslip/$ID`                                    |
| Lohnabrechnung            | `/report/html/hr_payroll.report_payslip_lang/$ID`                               |
| Packvorgänge              | `/report/html/stock.report_picking/$ID`                                         |
| QR-Rechnung               | `/report/html/l10n_ch.qr_report_main/$ID`                                       |
| Rahmenauftrag             | `/report/html/sale_blanket_order.report_blanketorder/$ID`                       |
| Rechnung mit Zeitnachweis | `/report/html/account_sale_timesheet_report.report_invoice_with_timesheets/$ID` |
| Rechnungen                | `/report/html/account.report_invoice/$ID`                                       |
| Rechnungen mit Zahlung    | `/report/html/account.report_invoice_with_payments/$ID`                         |
| Vorschau externer Bericht | `/report/html/web.preview_externalreport/$ID`                                   |
| Vorschau interner Bericht | `/report/html/web.preview_internalreport/$ID`                                   |
| Zeitnachweis              | `/report/html/account_sale_timesheet_report.timesheet_report/$ID`               |
| Lieferschein (Aufgabe)    | `/report/html/forestry_timesheet.report_project_task_deliveryslip/$ID`          |

::: tip
Bestimmte Bericht können mehere Dokumente anzeigen. Für die HTML-Anzeige können Sie die Dokument-IDs Komma-getrennt übergeben: /report/html/**stock.report_deliveryslip**/**3,4,5**
:::

### Berichte als HTML anzeigen

Alle von Odoo generierten Berichte können unter einer bestimmten URL als HTML angezeigt werden. Diese URL besteht aus dem technischen Berichtsnamen und der ID des anzuzeigenden Geschäftsobjekt. Dazu ein Beispiel anhand des Lieferscheins.

Öffnen Sie einen Lieferschein via *Lager > Vorgänge > Transfers* und merken Sie sich die folgenden Elemente der angezeigeigten URL: /web#**id=3**&action=348&**model=stock.picking**&view_type=form&cids=1&menu_id=208

Navigieren Sie nun zu **Einstellungen > Technisch > Aktionen > Berichte**. Filtern Sie die Liste nach dem *Name* des Berichts oder dem *Modellname*.

![](attachments/Entwicklung%20Berichte%20filtern.png)

Wählen Sie den Bericht aus und notieren Sie den *Vorlagenname* des Berichts.

![](attachments/Entwicklung%20Bericht%20Vorlagenname.png)

Nun haben Sie alle Elemente um den Bericht als HTML anzuzeigen. Geben Sie die folgende URL ein: /report/html/**stock.report_deliveryslip**/**3**

![](attachments/Entwicklung%20Bericht%20angezeigt.png)

## Verwaltung

#### Benutzerdefinierter Bericht erstellen

In diesem Szenario möchten wir für Dokumente einen Bericht generieren.

Öffnen Sie *Einstellungen > Technisch > Berichtswesen > Berichte* und erstellen Sie einen neuen Bericht mit diesen Attributen:

* **Name**: `Kundenstandards`
* **Modellname**: `documents.document`
* **Papierformat**: `A4`
* **Berichtstyp**: `PDF`
* **Vorlagenname**: `documents.report_customer_standards`

Navigieren Sie nun nach *Einstellungen > Technisch > Benutzer-Interface > Ansichten* und erstellen sie Sie neue Ansicht gemäss [Ansicht erstellen](Develpment%20Views.md#Ansicht%20erstellen) mit diesen Attributen:

**Ansichtsbezeichnung**: `mint_system.documents.report_customer_standards`
**Modell**: `documents.document`\
**Sequenz**: `50`\
**Ansichtstyp**: `QWeb`\
**Architektur**:

```xml
<t t-name="report_customer_standards">
  <t t-call="web.html_container">
	  <t t-call="web.internal_layout">
  		<div class="page">
  				
		<table class="table o_report_block_table">
          <thead>
            <tr>
              <th>
                <span>Name</span>
              </th>
            </tr>
          </thead>
          <tbody>
            <tr t-foreach="docs" t-as="o">
              <td>
                <span t-field="o.name"/>
              </td>
            </tr>
          </tbody>
        </table>
    
  		</div>
	  </t>
	</t>
</t>
```

Kopieren Sie die *ID* der Ansicht via *Entwicklertools > Metadaten anzeigen* und erstellen Sie eine externe ID gemäss [Externe ID erfassen](Development.md#Externe%20ID%20erfassen) mit diesen Attributen:

* **Modul**: `documents`
* **Externe Identifikation**: `report_customer_standards`
* **Modellname**: `ir.ui.view`
* **Datensatz-ID**: `$ID`

Ihre Ansicht wird nun vom Bericht über den *Vorlagename* identifiziert. Kehren Sie zum Bericht zurück und wählen *Zum Druckmenü hinzufügen*

![](attachments/Entwicklung%20QWeb-Berichte%20Drucken%20Kundenstandards.png)

### Benutzerdefinierter Bericht kopieren

In diesem Szenario wird gezeigt wie Sie einen bestehenden Bericht übernehmen und anpassen.

Öffnen Sie *Einstellungen > Technisch > Berichtswesen > Berichte* und erstellen Sie einen neuen Bericht mit diesen Attributen:

* Name: `Barcodes $COMPANY (PDF)`
* Modellname: `stock.picking`
* Papierformat: `A4`
* Berichtstyp: `PDF`

Navigieren Sie nun nach *Einstellungen > Technisch > Benutzer-Interface > Ansichten*, suchen Sie eine bestehende Ansicht und duplizieren Sie diese.

* Ansichtsbezeichnung: `label_transfer_template_view_$COMPANY`
* Architektur:

```xml
<t t-name="stock.label_transfer_template_view_$COMPANY">
    <t t-call="web.basic_layout">
        <t t-foreach="docs" t-as="picking">
            <t t-foreach="picking.move_lines" t-as="move">

                <t t-foreach="move.move_line_ids" t-as="move_line">
                    <div class="page">
                        <div class="label">
                            <span class="text-uppercase" t-esc="move.product_id.name"/>
                        </div>
                        <p style="page-break-before:always;" />
                    </div>
                </t>

            </t>
        </t>
    </t>
</t>
```

Nun exportieren Sie die Ansicht um eine *XML ID* zu generieren.

![QWeb-Berichte XML ID generieren](attachments/QWeb-Berichte%20XML%20ID%20generieren.gif)

Setzen Sie als *Ansichtsbezeichnung* die *XML ID*, ersetzen Sie dabei `__export__` mit einer anderen Bezeichner beispielsweise `mint_system`. Öffnen Sie den Bericht und setzen Sie als *Vorlagenname* die *XML ID* ein.

![](attachments/QWeb-Berichte%20Vorlagenname%20setzen.png)

Wurde das Kontext-Menü mit der Aktion *Zum Druckmenü hinzufügen* erstellt, kann der Bericht entsprechend erstellt werden.

![](attachments/QWeb-Berichte%20Drucken.png)

::: tip
Odoo verlinkt das Ansichts- und Berichtsobjekt über die externe ID bzw. XML ID.
:::

### Option "Als Anhang speichern" deaktivieren

Verschiedene Standardberichte werden beim Erzeugen als das Geschäftsobjekt angehängt. Dies geschieht aufgrund der Option *Als Anhangsprefix speichern* auf dem Berichtsobjekt. Rufen Sie einen Bericht auf *Einstellungen > Technisch > Berichtswesen > Berichte* und entfernen Sie im Tab *Erweiterte Eigenschaften* den Eintrag im Feld *Als Anhangsprefix speichern*.

### Dateinamen für Berichte festlegen

Navigieren Sie nach  *Einstellungen > Technisch > Berichtswesen > Berichte* und legen Sie die Dateinamen gemäss folgender Tabelle fest:

| Name                  | Name des gedruckten Berichtes                      | Als Anhangsprefix speichern                        |
| --------------------- | -------------------------------------------------- | -------------------------------------------------- |
| Invoice with QR       | `'Rechnung_%s.pdf' % object.name.replace("/","_")` | `'Rechnung_%s.pdf' % object.name.replace("/","_")` |
| Originalrechnungen    | `'Rechnung_%s.pdf' % object.name.replace("/","_")` |                                                    |
| QR-bill               | `'QR-Rechnung_%s' % object.name`                   | `'QR-Rechnung_%s' % object.name`                   |
| Rechnung ohne Zahlung | `'Rechnung_%s.pdf' % object.name.replace("/","_")` | `'Rechnung_%s.pdf' % object.name.replace("/","_")` |
| Rechnungen            | `'Rechnung_%s.pdf' % object.name.replace("/","_")` | `'Rechnung_%s.pdf' % object.name.replace("/","_")` |
