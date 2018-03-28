---
title: Importieren von Domänen aus einer Excel-Datei in eine Wissensermittlung | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: data-quality-services
ms.service: ''
ms.component: data-quality-services
ms.reviewer: ''
ms.suite: sql
ms.technology:
- data-quality-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 4d3a3940-6c2a-4dc4-90eb-86f26012c165
caps.latest.revision: ''
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3bf3c6cad727ffb358dacfd2f2f401ca1902e806
ms.sourcegitcommit: 34766933e3832ca36181641db4493a0d2f4d05c6
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/22/2018
---
# <a name="import-domains-from-an-excel-file-in-knowledge-discovery"></a>Importieren von Domänen aus einer Excel-Datei in eine Wissensermittlung
  In diesem Thema wird beschrieben, wie eine oder mehrere Domänen in einer Excel-Datei in die [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS)-Wissensermittlungsaktivität importiert werden. Der Importvorgang vereinfacht den Wissensgenerierungsprozess und spart Zeit und Aufwand. Auf diese Weise können Personen, die über Daten in einer Excel-Datei oder Textdatei verfügen, eine Wissensdatenbank mit diesen Daten erstellen. (Weitere Informationen zum Importieren von Werten in eine Domäne einer vorhandenen Wissensdatenbank finden Sie unter [Importieren von Werten aus einer Excel-Datei in eine Domäne](../data-quality-services/import-values-from-an-excel-file-into-a-domain.md).) Das Exportieren in eine Excel-Datei wird nicht unterstützt.  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungsmaßnahmen  
  
###  <a name="Prerequisites"></a> Erforderliche Komponenten  
 Um Domänen aus einer Excel-Datei zu importieren, muss Excel auf dem Computer installiert sein, auf dem [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] installiert ist; Sie müssen eine Excel-Datei mit Domänenwerten erstellt haben (siehe [How the import works](#How)) und Sie müssen eine Wissensdatenbank erstellt und geöffnet haben, um die Domäne zu importieren.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Sie müssen über die dqs_kb_editor- oder die dqs_administrator-Rolle in der DQS_MAIN-Datenbank verfügen, um Domänen aus einer Excel-Datei zu importieren.  
  
##  <a name="Import"></a> Importieren von Domänen aus einer Excel-Datei in eine Wissensdatenbank  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Ausführen der Data Quality-Clientanwendung](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Führen Sie im [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] -Startbildschirm einen der folgenden Schritte aus:  
  
    -   Erstellen Sie eine neue Wissensdatenbank, in die die Daten importiert werden sollen, indem Sie auf **Neue Wissensdatenbank**klicken, einen Namen für die Wissensdatenbank eingeben, unter **Wissensdatenbank erstellen aus** die Option **Keine**auswählen, anschließend die Aktivität **Wissensermittlung** auswählen und auf **Erstellen**klicken.  
  
    -   Öffnen Sie eine vorhandene Wissensdatenbank für den Import der Daten, indem Sie auf **Wissensdatenbank öffnen**klicken, die Wissensdatenbank und dann die Aktivität **Wissensermittlung**auswählen und auf **Weiter**klicken.  
  
3.  Wählen Sie auf der Seite **Zuordnen** für **Datenquelle** die Option **Excel-Datei**aus.  
  
4.  Klicken Sie in der **Excel-Datei** -Zeile auf **Durchsuchen** .  
  
5.  Wechseln Sie im Dialogfeld **Excel-Datei auswählen** zum Ordner, der die Excel-Datei enthält, aus der Sie die Daten importieren möchten, wählen Sie die Excel-Datei aus, und klicken Sie dann auf **Öffnen**.  
  
6.  Wählen Sie in der Dropdownliste **Arbeitsblatt** das Arbeitsblatt in der Excel-Datei aus, aus dem Sie importieren möchten.  
  
7.  Wählen Sie **Erste Zeile als Header verwenden** aus, wenn die erste Zeile als Kopfzeile angesehen werden soll und die Werte in der ersten Zeile als Spaltennamen verwendet werden sollen. Heben Sie die Auswahl von **Erste Zeile als Header verwenden** auf, wenn die erste Zeile als Datenwert angesehen werden soll. In dem Fall verwendet DQS die Excel-Überschriften (Buchstaben) für die Spalte.  
  
8.  Wählen Sie eine Spalte aus, und ordnen Sie dann der Spalte eine vorhandene Domäne zu, oder erstellen Sie eine neue Domäne, indem Sie auf das Symbol **Domäne erstellen** klicken und im Dialogfeld **Domäne erstellen** eine Domäne erstellen und die Domäne der Spalte zuordnen. Der Datentyp der Domäne muss mit dem Datentyp der Spalte übereinstimmen. Wiederholen Sie diesen Vorgang für alle Spalten des Arbeitsblatts.  
  
9. Klicken Sie auf **Weiter**.  
  
10. Klicken Sie auf der Seite **Ermitteln** auf **Start** , um die Daten im Excel-Arbeitsblatt zu analysieren.  
  
    > [!NOTE]  
    >  Wenn Sie die Seite schließen, bevor die Daten hochgeladen wurden, wird der Dateiuploadprozess beendet.  
  
11. Überprüfen Sie, ob die Analyse erfolgreich abgeschlossen wurde, und klicken Sie dann auf **Weiter**.  
  
12. Überprüfen Sie auf der Seite **Domänenwerte verwalten** , ob die richtigen Domänen in der Liste **Domänen** aufgeführt sind und ob die Domänentabelle Werte enthält.  
  
13. Klicken Sie auf **Fertig stellen**und anschließend auf **Veröffentlichen** , um die Wissensdatenbank zu veröffentlichen, oder klicken Sie auf **Nein** , wenn diese nicht veröffentlicht werden soll.  
  
14. Überprüfen Sie, ob die Wissensdatenbank veröffentlicht wurde, und klicken Sie dann auf **OK**.  
  
##  <a name="FollowUp"></a> Nachverfolgung: Nach dem Importieren von Domänen aus einer Excel-Datei  
 Nachdem Sie Domänen aus einer Excel-Datei importiert haben, können Sie den Domänen Wissen hinzufügen oder die Domänen in einem Bereinigungs- oder Abgleichsprojekt verwenden – je nach den Inhalten der Domänen. Weitere Informationen finden Sie unter [Durchführen der Wissensermittlung](../data-quality-services/perform-knowledge-discovery.md), [Verwalten einer Domäne](../data-quality-services/managing-a-domain.md), [Verwalten einer Verbunddomäne](../data-quality-services/managing-a-composite-domain.md), [Erstellen einer Abgleichsrichtlinie](../data-quality-services/create-a-matching-policy.md), [Datenbereinigung](../data-quality-services/data-cleansing.md) oder [Datenabgleich](../data-quality-services/data-matching.md).  
  
##  <a name="How"></a> How the import works  
 Beim Importvorgang interpretiert DQS eine Excel-Datei wie folgt:  
  
-   Eine Spalte stellt eine Domäne dar.  
  
-   Eine Zeile stellt einen Datensatz dar.  
  
-   Die erste Zeile stellt entweder Domänennamen dar oder ist der erste Datenwert oder der Datensatz, je nach der Einstellung des Kontrollkästchens **Erste Zeile als Header verwenden** .  
  
 Für den Importvorgang gelten die folgenden Regeln:  
  
-   Dieser Vorgang importiert Domänenwerte in eine Wissensdatenbank. Domänenregeln oder eine Abgleichsrichtlinie werden dabei nicht importiert.  
  
-   Die Excel-Datei kann die Erweiterung .xlsx, .xls oder .csv haben. Microsoft Excel muss auf dem [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] -Computer installiert sein, um Domänenwerte oder eine vollständige Domäne zu importieren. Die Excel-Versionen 2003 und höher werden unterstützt. Wenn die 64-Bit-Version von Excel verwendet wird, werden nur Excel 2003-Dateien unterstützt; Excel 2007- oder 2010-Dateien werden nicht unterstützt.  
  
-   Excel-Dateien vom Typ .xlsx werden nicht für eine Excel-64-Bit-Installation unterstützt. Wenn Sie die 64-Bit-Version von Excel verwenden, speichern Sie die Arbeitsblattdatei mit der Erweiterung .xls.  
  
-   Der Datentyp der Spalte wird in XLSX- und XLS-Dateien vom häufigsten Datentyp in den ersten acht Zeilen bestimmt. Wenn eine Zelle diesem Datentyp nicht entspricht, erhält sie einen NULL-Wert.  
  
-   In CSV-Dateien wird der Datentyp vom häufigsten Datentyp in den ersten acht Zeilen bestimmt.  
  
-   Ein Wert in einem Excel-Arbeitsblatt, der einer Domänenregel nicht entspricht, wird als ungültiger Wert importiert.  
  
-   Wenn die Excel-Datei nicht im richtigen Format vorliegt oder beschädigt ist, führt der Importvorgang zu einem Fehler.  
  
  
