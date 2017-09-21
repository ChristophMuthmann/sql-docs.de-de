---
title: "Importieren von Werten aus einer Excel-Datei in eine Domäne | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- data-quality-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dqs.kb.importfailing.f1
- sql13.dqs.kb.importselect.f1
- sql13.dqs.kb.failingvalues.f1
ms.assetid: 04cde693-2043-477f-8417-fcc463ca7195
caps.latest.revision: 26
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c007da5bb365b81cd3a8bdd570c139077e44afbd
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="import-values-from-an-excel-file-into-a-domain"></a>Importieren von Werten aus einer Excel-Datei in eine Domäne
  In diesem Thema wird beschrieben, wie Werte in [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) aus einer Excel-Datei in eine Domäne importiert werden. Eine Excel-Datei zu verwenden, um Domänenwerte in die Anwendung [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] zu importieren, vereinfacht den Wissensgenerierungsprozess und spart Zeit und Aufwand. Es ermöglicht Personen, die eine Liste mit gültigen Datenwerten in einer Excel-Datei oder einer Textdatei haben, jene Werte in eine Domäne zu importieren. In einer Excel-Datei können Sie Domänenwerte in eine Domäne oder Domänen in eine Wissensdatenbank importieren. (Weitere Informationen zum Importieren von Domänen in eine Wissensdatenbank finden Sie unter [Importieren von Domänen aus einer Excel-Datei in eine Wissensermittlung](../data-quality-services/import-domains-from-an-excel-file-in-knowledge-discovery.md).) Das Exportieren in eine Excel-Datei wird nicht unterstützt.  
  
 Sie können Datenwerte auf zwei Weisen importieren:  
  
-   Erstellen Sie eine neue Domäne, und importieren Sie dann Werte aus einer Excel-Datei. In diesem Fall werden der Domäne alle Werte hinzugefügt.  
  
-   Importieren Sie Werte in eine vorhandene, aufgefüllte Domäne. In diesem Fall werden nur neue Werte importiert. Alle Werte, die bereits existieren, werden nicht importiert.  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Prerequisites"></a> Erforderliche Komponenten  
 Um Domänen aus einer Excel-Datei zu importieren, muss Excel auf dem Computer installiert sein, auf dem die [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] -Anwendung installiert ist, um Domänenwerte oder eine vollständige Domäne zu importieren; Sie müssen eine Excel-Datei mit Domänenwerten erstellt haben (siehe [How the import works](#How)) und Sie müssen eine Wissensdatenbank erstellt und geöffnet haben, um die Domäne zu importieren.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Sie müssen über die dqs_kb_editor- oder die dqs_administrator-Rolle in der DQS_MAIN-Datenbank verfügen, um Domänenwerte aus einer Excel-Datei zu importieren.  
  
##  <a name="Import"></a> Import values from an Excel file into a domain  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Ausführen der Data Quality-Clientanwendung](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Öffnen Sie im [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] -Startbildschirm in der Domänenverwaltungsaktivität eine Wissensdatenbank.  
  
3.  Wenn Sie einer neuen Domäne Werte hinzufügen, erstellen Sie eine neue Domäne mithilfe des Symbols **Domäne erstellen** und wählen Sie dann die neue Domäne in der Domänenliste aus.  
  
4.  Wenn Sie einer vorhandenen Domäne Werte hinzufügen, wählen Sie die Domäne in der Domänenliste aus.  
  
5.  Klicken Sie auf die Registerkarte **Domänenwerte** , klicken Sie auf das Symbol **Werte importieren** in der Symbolleiste, und klicken Sie auf **Gültige Werte aus Excel importieren**.  
  
6.  Klicken Sie im Dialogfeld **Domänenwerte importieren** auf **Durchsuchen**.  
  
7.  Wechseln Sie im Dialogfeld **Datei auswählen** in den Ordner, der die Excel-Datei enthält, aus der Sie Domänenwerte importieren möchten, wählen Sie die Datei (mit einer .xlsx-, .xls- oder .csv-Erweiterung) aus und klicken Sie dann auf **Öffnen**. Die Datei muss entweder auf dem Client vorhanden sein, von dem Sie DQS ausführen, oder in einer Freigabedatei, auf die der Benutzer Zugriff hat.  
  
8.  Wählen Sie in der Dropdownliste **Arbeitsblatt** das Arbeitsblatt aus, aus dem Sie importieren.  
  
9. Wählen Sie **Erste Zeile als Header verwenden** , wenn die erste Zeile im Arbeitsblatt den Domänennamen darstellt, und alle anderen Zeilen die gültigen Domänenwerte darstellen.  
  
10. Klicken Sie auf **OK**. Eine Statusanzeige wird angezeigt, die darauf hinweist, wie viele Werte erfolgreich importiert wurden, wie viele nicht importiert wurden sowie die Gesamtzahl der Werte. Klicken Sie auf die Schaltfläche **Abbrechen** , um den Prozess abzubrechen.  
  
11. Überprüfen Sie, dass "Importieren abgeschlossen" im Dialogfeld **Domänenwerte importieren** angezeigt wird. In diesem Dialogfeld sehen Sie, welche Werte erfolgreich importiert wurden und welche nicht. Es zeigt den Namen der Datei und den Dateipfad an, den Abschlussstatus des Vorgangs, wie viele Werte erfolgreich importiert wurden, wie viele Werte nicht importiert wurden sowie die Gesamtzahl der verarbeiteten Werte.  
  
12. Klicken Sie für die Werte, die nicht erfolgreich importiert wurden, auf **Protokoll** , um das Dialogfeld **Domänenwerte importieren - fehlerhafte Werte** anzuzeigen. Hier sehen Sie, weshalb der Importvorgang fehlgeschlagen ist. Die Spalte **Fehlerhafter Wert** zeigt die Werte an, die nicht aus einer Excel-Datei in eine Domäne importiert werden konnten, und die Spalte **Grund** erläutert, warum der Import fehlgeschlagen ist. Klicken Sie auf **In Zwischenablage kopieren** , um die Tabelle **Fehlerhafte Werte** in die Zwischenablage zu kopieren, aus der Sie sie in ein anderes Programm kopieren können, z. B. ein Excel-Arbeitsblatt oder eine Editor-Datei. Klicken Sie auf **OK** , um das Dialogfeld **Fehlerhafte Werte** zu schließen.  
  
13. Klicken Sie auf **OK** , um den Importvorgang abzuschließen, und schließen Sie das Dialogfeld. Wenn der Import erfolgreich abgeschlossen wurde, wird die Domänenwerteliste auf der Seite **Domänenwerte** aktualisiert und schließt die neuen importierten Werte ein. Der Filter wird in **Alle Werte** geändert und **Nur neue anzeigen** wird ausgewählt. Wenn **Nur neue anzeigen** nach dem Importvorgang ausgewählt wird, werden nur die aus der Excel-Datei importierten Werte angezeigt.  
  
14. Klicken Sie auf **Fertig stellen** , um der Wissensdatenbank die Werte hinzuzufügen.  
  
##  <a name="FollowUp"></a> Nachverfolgung: Nach dem Importieren von Werten aus einer Excel-Datei in eine Domäne  
 Nachdem Sie Werte in eine Domäne importiert haben, können Sie andere Domänenverwaltungstasks in der Domäne ausführen, Sie können die Wissensermittlung durchführen, um der Domäne Wissen hinzuzufügen, oder Sie können der Domäne eine Abgleichsrichtlinie hinzufügen. Weitere Informationen finden Sie unter [Durchführen der Wissensermittlung](../data-quality-services/perform-knowledge-discovery.md), [Verwalten einer Domäne](../data-quality-services/managing-a-domain.md) oder [Erstellen einer Abgleichsrichtlinie](../data-quality-services/create-a-matching-policy.md).  
  
##  <a name="Synonyms"></a> Importieren von Synonymen  
 Synonyme werden wie folgt importiert:  
  
-   Zuerst werden alle Werte importiert, dann wird die Synonymverbindung hergestellt.  
  
-   Wenn es unmöglich ist, Synonymwerte zu verbinden, tritt ein Fehler im Protokollbildschirm auf. Es ist möglich, dass die führenden Werte und die Synonyme in der Datei in die Domäne importiert, aber nicht als Synonyme festgelegt werden.  
  
 Folgendes gilt für den Prozess, Synonymverbindungen festzulegen:  
  
-   Wenn der führende Wert in der Excel-Datei bereits in der Domäne als Synonym eines anderen Werts vorhanden ist, müssen Sie die Synonyme manuell festlegen (z. B. soll in der Excel-Datei Wert A der führende Wert für Wert B sein, aber in der Domäne erscheint Wert A als Synonym von Wert C). Zusätzlich zum manuellen Festlegen von Synonymen nach Abschluss des Imports können Sie auch die Verknüpfung von Werten aufheben, die derzeit Synonyme sind (z. B. die Verknüpfung von Wert A und C aufheben), und dann die Datei importieren.  
  
-   Wenn das Synonym bereits mit einem anderen führenden Wert verbunden ist, müssen Sie die Synonyme manuell festlegen.  
  
-   Wenn die Werte in der Anwendung aus irgendeinem Grund nicht manuell verbunden werden können, ist dies auch im Importvorgang nicht anwendbar.  
  
##  <a name="How"></a> How the import works  
 Die folgenden Werte werden von diesem Vorgang importiert:  
  
 Beim Importvorgang importiert DQS aus einer Excel-Datei wie folgt:  
  
-   Richtige Werte und neue Werte werden importiert. Wenn einer oder mehrere der importierten Domänenwerte bereits vorhanden ist, werden die Werte nicht importiert.  
  
-   Ein Wert, der einer Domänenregel widerspricht, wird als ungültiger Wert importiert.  
  
-   Ein Wert wird nicht aus der Datei importiert, wenn der Wert nicht vom Datentyp der Domäne oder NULL ist.  
  
-   Die Werte werden in der Reihenfolge importiert, in der sie in der Datei angezeigt werden.  
  
-   Jede Zeile stellt einen Domänenwert dar.  
  
-   Die erste Zeile stellt entweder Domänennamen dar oder ist der erste Datenwert oder der Datensatz, je nach der Einstellung des Kontrollkästchens **Erste Zeile als Header verwenden** . Wenn Sie beim Verwenden einer XSLS- oder einer XLS-Datei **Use First Row as header** auswählen, werden alle Spaltennamen, die NULL sind, automatisch in F*n*konvertiert. An alle Spalten, die doppelt sind, wird eine Zahl angefügt.  
  
-   Wenn Sie den Importvorgang abbrechen, bevor er abgeschlossen wurde, wird ein Rollback für den Vorgang ausgeführt, und es werden keine Daten importiert.  
  
-   Die Werte in der ersten Spalte werden in die Domäne importiert. Wenn eine oder mehrere weitere Spalten zusätzlich zur ersten Spalte aufgefüllt werden, dann werden die Werte in diesen Spalten als Synonyme hinzugefügt (siehe [Importieren von Synonymen](#Synonyms)).  
  
    -   Das erwartete Format ist, dass die erste Spalte führende Werte und die zweite Spalte und höher Synonyme sind.  
  
    -   Sie können mehrere Synonyme in die gleiche Zeile oder in verschiedene Zeilen importieren. Wenn Sie z. B. "NYC" und "New York City" als Synonyme für "New York" importieren möchten, können Sie eine einzelne Zeile mit "New York" in Spalte 1, "NYC" in Spalte 2 und "New York City" in Spalte 3 importieren; oder Sie können eine Zeile mit "New York" in Spalte 1 und "NYC" in Spalte 2 und eine andere Zeile mit "New York" in Spalte 1 und "New York City" in Spalte 2 importieren. Beachten Sie, dass, wenn der Wert "New York" bereits in der Domäne vorhanden ist, nur die Synonyme hinzugefügt werden. Der Benutzer erhält während des Importvorgangs keinen Fehler, der ihm mitteilt, dass der Wert bereits vorhanden ist. Wenn der erste Wert nicht bereits vorhanden ist, wird er der Domäne hinzugefügt.  
  
 Die folgenden Regeln gelten für die Excel-Datei, die für den Import verwendet wird:  
  
-   Die Excel-Datei kann die Erweiterung .xlsx, .xls oder .csv haben. Microsoft Excel muss auf dem Computer installiert sein, auf dem die Anwendung [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] installiert ist, um Domänenwerte oder eine vollständige Domäne zu importieren. Die Excel-Versionen 2003 und höher werden unterstützt. Wenn die 64-Bit-Version von Excel verwendet wird, werden nur Excel 2003-Dateien unterstützt; Excel 2007- oder 2010-Dateien werden nicht unterstützt.  
  
-   Excel-Dateien vom Typ .xlsx werden nicht für eine Excel-64-Bit-Installation unterstützt. Wenn Sie 64-Bit-Excel verwenden, speichern Sie die Arbeitsblattdatei als XLS-Datei oder CSV-Datei, oder installieren Sie stattdessen eine Excel-32-Bit-Installation.  
  
-   Der Datentyp der Spalte wird in XLSX- und XLS-Dateien von den ersten acht Zeilen bestimmt. Falls der Datentyp der ersten acht Zeilen gemischt ist, handelt es sich um einen string-Spaltentyp (Zeichenfolge). Wenn eine Zelle für Zeile 9 und höher diesem Datentyp nicht entspricht, erhält sie einen NULL-Wert.  
  
-   In CSV-Dateien wird der Datentyp vom häufigsten Datentyp in den ersten acht Zeilen bestimmt.  
  
-   Wenn die Excel-Datei nicht im richtigen Format vorliegt oder beschädigt ist, führt der Importvorgang zu einem Fehler.  
  
  
