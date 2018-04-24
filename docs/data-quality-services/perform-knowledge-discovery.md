---
title: Durchführen der Wissensermittlung | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/04/2013
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
f1_keywords:
- sql13.dqs.kb.kbterms.f1
- sql13.dqs.kb.viewselectcd.f1
- sql13.dqs.kb.kbanalyze.f1
- sql13.dqs.kb.kbmap.f1
ms.assetid: 34a0ea16-02e6-46ed-90bc-dede68687f63
caps.latest.revision: 38
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cd936e2ceeba5b2b20f922bbd6a59d430c44de4b
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="perform-knowledge-discovery"></a>Durchführen der Wissensermittlung

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  In diesem Thema wird beschrieben, wie eine Wissensdatenbank über die Wissensermittlung erstellt wird. Im Wissensermittlungsprozess werden die Daten in einer Beispieldatenquelle in [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) über einen computergestützten Prozess analysiert, und das gewonnene Wissen wird zur Wissensdatenbank hinzugefügt. Dieses Wissen kann im Schritt **Domänenwerte verwalten** der Wissensermittlungsaktivität oder in der Domänenverwaltungsaktivität geändert und verbessert werden.  
  
 Die Wissensermittlung ist ein über einen Assistenten ausgeführter Prozess mit drei Schritten, die vollständig abgeschlossen werden müssen.  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungsmaßnahmen  
  
###  <a name="Prerequisites"></a> Erforderliche Komponenten  
 Microsoft Excel muss auf dem [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] -Computer installiert sein, wenn sich die Quelldaten, für die Sie den Ermittlungsprozess ausführen, in einer Excel-Datei befinden. Andernfalls sind Sie nicht in der Lage, die Excel-Datei in der Zuordnungsphase auszuwählen. Die von Microsoft Excel erstellten Dateien können die Erweiterung .xlsx, .xls oder .csv haben. Wenn die 64-Bit-Version von Excel verwendet wird, werden nur Excel 2003-Dateien (.xls) unterstützt; Excel 2007- oder 2010-Dateien (.xlsx) werden nicht unterstützt. Wenn Sie die 64-Bit-Version von Excel 2007 oder 2010 verwenden, speichern Sie die Datei als XLS-Datei oder CSV-Datei, oder installieren Sie stattdessen eine 32-Bit-Version von Excel.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Sie müssen über die dqs_kb_editor- oder dqs_administrator-Rolle in der DQS_MAIN-Datenbank verfügen, um eine Wissensdatenbank zu erstellen.  
  
##  <a name="FirstStep"></a> Erster Schritt: Starten der Wissensermittlung  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Ausführen der Data Quality-Clientanwendung](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Wenn Sie die Wissensermittlung für eine neue Wissensdatenbank durchführen möchten, klicken Sie auf **Neue Wissensdatenbank**, geben Sie den Namen und die Beschreibung ein, und geben Sie ggf. an, auf welcher Grundlage Sie die Wissensdatenbank erstellen. Wenn Sie die Wissensermittlung für eine vorhandene Wissensdatenbank durchführen möchten, klicken Sie auf **Wissensdatenbank öffnen**, und wählen Sie dann eine Wissensdatenbank aus.  
  
3.  Wählen Sie die Aktivität **Wissensermittlung** aus, und klicken Sie dann auf **Erstellen** , um die neue Wissensdatenbank zu erstellen, oder auf **Öffnen** , um eine vorhandene Wissensdatenbank zu öffnen.  
  
##  <a name="Mapping"></a> Zuordnungsphase  
  
1.  Wählen Sie im Feld **Datenquelle** die Option **SQL Server** (Standard) oder **Excel-Datei**aus.  
  
    > [!NOTE]  
    >  Auf dieser Seite stellen Sie eine Verbindung zu einer SQL Server- oder einer Excel-Datenquelle her und ordnen dann Spalten in der Datenquelle einer Domäne in der Wissensdatenbank zu. In der Tabelle Zuordnungen werden alle Spalten in der Quelldatenbank angezeigt, die analysiert werden, um Wissen zu den entsprechenden Domänen hinzuzufügen. Zuordnungen erfolgen zwischen den Spalten in der Datenquelle und einer Domäne in der ausgewählten Wissensdatenbank.  
  
2.  Wenn die Datenquelle **SQL Server**ist, gehen Sie wie folgt vor:  
  
    1.  Wählen Sie im Feld **Datenbank** die Quelldatenbank aus, die Sie analysieren möchten, um die Wissensdatenbank zu erstellen. Die Dropdownliste des Textfelds enthält die verfügbaren Datenbanken. Die Quelldatenbank muss sich in der gleichen SQL Server-Instanz wie [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]befinden. Andernfalls wird sie nicht in der Dropdownliste angezeigt.  
  
    2.  Wählen Sie im Feld **Tabelle/Sicht** die Tabelle oder Sicht aus, die Sie analysieren möchten, um die Wissensdatenbank zu erstellen. Bei dieser Tabelle oder Sicht sollte es sich um Beispieldaten handeln und nicht um eine vollständige Quelldatenbank, für die Sie eine Datenbereinigung oder einen Abgleich ausführen. Die Dropdownliste des Textfelds enthält die Tabellen und Sichten, die für die ausgewählte Datenbank verfügbar sind.  
  
3.  Wenn die Datenquelle **Excel**ist, gehen Sie wie folgt vor:  
  
    1.  Klicken Sie auf **Durchsuchen** , und wählen Sie die Excel-Datei aus, die Sie analysieren möchten, um die Wissensdatenbank zu erstellen. Excel muss auf dem [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] -Computer installiert sein, um eine Excel-Datei auswählen zu können. Wenn Excel auf dem [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] -Computer nicht installiert ist, ist die Schaltfläche Durchsuchen nicht verfügbar, und Sie werden unter diesem Textfeld benachrichtigt, dass Excel nicht installiert ist.  
  
    2.  Aktivieren Sie das Kontrollkästchen **Erste Zeile als Header verwenden** , wenn die erste Zeile der Excel-Datei Headerdaten enthält.  
  
4.  Ordnen Sie in der Tabelle **Zuordnungen** jede Quellspalte, für die die Wissensermittlung durchgeführt werden soll, einer Domäne in der Wissensdatenbank wie folgt zu:  
  
    1.  Erstellen Sie eine Zuordnung, indem Sie eine Quellspalte aus der Dropdownliste für die Spalte **Quellspalte** einer leeren Zeile auswählen und dann eine Domäne aus der Dropdownliste für die Spalte **Domäne** in der gleichen Zeile auswählen (wenn eine Domäne vorhanden ist). Wenn keine Domäne vorhanden ist, klicken Sie auf **Domäne erstellen** oder **Verbunddomäne erstellen** , um eine Domäne zu erstellen. Weitere Informationen finden Sie unter [Create a Domain Rule](../data-quality-services/create-a-domain-rule.md) oder [Create a Composite Domain](../data-quality-services/create-a-composite-domain.md).  
  
    2.  Wiederholen Sie den vorherigen Schritt für jede Zuordnung. Um die Anzahl der Zeilen in der Tabelle zu ändern, klicken Sie auf **Spaltenzuordnung hinzufügen**, oder wählen Sie eine Zeile aus, und klicken Sie auf **Ausgewählte Spaltenzuordnung entfernen**. Wenn Sie auf **Ausgewählte Spaltenzuordnung entfernen** klicken, während eine aufgefüllte Zeile ausgewählt ist, wird die ausgewählte Zeile gelöscht, auch wenn es eine nicht aufgefüllte Zeile gibt.  
  
        > [!NOTE]  
        >  Sie können die Quelldaten zum Durchführen der Wissensermittlung einer DQS-Domäne nur zuordnen, wenn der Quelldatentyp in DQS unterstützt wird und mit dem DQS-Domänendatentyp übereinstimmt. Weitere Informationen zu den unterstützten Datentypen finden Sie unter [Supported SQL Server and SSIS Data Types for DQS Domains](../data-quality-services/supported-sql-server-and-ssis-data-types-for-dqs-domains.md).  
  
    3.  Klicken Sie auf **Verbunddomänen anzeigen/auswählen** aus, um die Verbunddomänen anzuzeigen, die definiert wurden. Wenn keine Verbunddomänen definiert wurden, ist das Steuerelement nicht verfügbar.  
  
    4.  Klicken Sie auf **Vorschau der Datenquelle** , um alle Daten in der Datenquelle in einem Popupfenster anzuzeigen, die Sie im Textfeld **Tabelle/Sicht** oder **Excel-Datei** ausgewählt haben.  
  
5.  Klicken Sie auf **Weiter** , um im Wissensermittlungs-Assistenten auf die Seite **Ermitteln** zu wechseln. Sie können auch Folgendes auswählen:  
  
    -   Klicken Sie auf **Abbrechen** , um die Wissensermittlung abzubrechen, ohne die Ergebnisse zu speichern, und um zur DQS-Homepage zurückzukehren.  
  
    -   Klicken Sie auf **Schließen** , um die Ergebnisse zu speichern und zur DQS-Homepage zurückzukehren. Die Wissensdatenbank wird für Sie gesperrt, und der Status der Wissensdatenbank wird in der Wissensdatenbanktabelle auf der Seite **Wissensdatenbank öffnen** als **Ermittlung – Zuordnung**angezeigt. Nachdem Sie auf **Schließen**geklickt haben, um die Domänenverwaltung durchzuführen, müssen Sie im Fenster **Wissensdatenbank öffnen** auf **Wissensermittlung** klicken, die Seite **Wissensdatenbank-Verwaltung: Domänenbegriffe verwalten** öffnen, auf **Fertig stellen**klicken und anschließend auf **Ja** (um die Wissensdatenbank zu veröffentlichen) oder **Nein** (um die Arbeit in der Wissensdatenbank zu speichern und zu beenden) klicken.  
  
##  <a name="Discover"></a> Ermittlungsphase  
  
1.  Klicken Sie auf **Start** , um die Datenquelle zu analysieren.  
  
    > [!NOTE]  
    >  Die Ermittlung wird für die Spalten ausgeführt, die auf der Seite **Zuordnen** in der Tabelle **Zuordnungen** eingegeben wurden. Die Domäne, die der jeweiligen Spalte zugeordnet ist, wird mit dem in der Ermittlung gewonnenen Wissen aufgefüllt. Wenn die Domäne eine Verbunddomäne ist, wird das Wissen den einzelnen Domänen hinzugefügt, aus denen die Verbunddomäne besteht.  
  
2.  Während der Ermittlungsprozess ausgeführt wird, überprüfen Sie den Abschlussstatus, der für jeden Schritt der Ermittlung angezeigt wird: **Datensätze werden vorverarbeitet**, **Domänenregeln werden ausgeführt**und **Ermittlung wird ausgeführt**. Für jede dieser Phasen werden der prozentuale Anteil und der Abschlussstatus angezeigt.  
  
3.  Wenn die Analyse abgeschlossen ist, überprüfen Sie, ob in der Statuszeile unter der Abschlussstatistik angegeben ist, dass sie erfolgreich abgeschlossen wurde.  
  
    > [!NOTE]  
    >  Wenn Sie die Seite schließen, bevor die Datei hochgeladen wurde, wird der Dateiuploadprozess beendet.  
  
4.  Wenn die Analyse abgeschlossen ist, überprüfen Sie auf der Registerkarte **Profiler** in der Statistik den Status der Daten. Weitere Informationen finden Sie unter **Datenprofilerstellung und Benachrichtigungen in DQS**.  
  
5.  Nachdem die Analyse abgeschlossen wurde, wird die Schaltfläche **Start** zur Schaltfläche **Neustart** . Klicken Sie auf **Neustart** , um den Analyseprozess erneut auszuführen. Wenn die Ergebnisse der vorherigen Analyse noch nicht gespeichert wurden, gehen beim Klicken auf **Neustart** jedoch die vorherigen Daten verloren. Klicken Sie zum Fortfahren in dem Popupfenster auf **Ja** . Verlassen Sie während der Ausführung der Analyse nicht die Seite, da ansonsten der Analyseprozess abgebrochen wird.  
  
6.  Klicken Sie auf **Weiter** , um im Wissensermittlungs-Assistenten auf die Seite **Domänenwerte verwalten** zu wechseln. Auf dieser Seite können Sie die Informationen ändern, die in den Domänen der Wissensdatenbank hinzugefügt wurden. Sie können auch Folgendes auswählen:  
  
    -   Klicken Sie auf **Abbrechen** , um die Wissensermittlung abzubrechen, ohne die Ergebnisse zu speichern, und um zur DQS-Homepage zurückzukehren.  
  
    -   Klicken Sie auf **Schließen** , um die Ergebnisse zu speichern und zur DQS-Homepage zurückzukehren. Die Wissensdatenbank wird für Sie gesperrt, und der Status der Wissensdatenbank wird in der Wissensdatenbanktabelle auf der Seite **Wissensdatenbank öffnen** als **Ermittlung – Ermitteln**angezeigt. Nachdem Sie auf **Schließen**geklickt haben, um die Domänenverwaltung durchzuführen, müssen Sie im Fenster **Wissensdatenbank öffnen** auf **Wissensermittlung** klicken, die Seite **Wissensdatenbank-Verwaltung: Domänenbegriffe verwalten** öffnen, auf **Fertig stellen**klicken und anschließend auf **Ja** (um die Wissensdatenbank zu veröffentlichen) oder **Nein** (um die Arbeit in der Wissensdatenbank zu speichern und zu beenden) klicken.  
  
    -   Klicken Sie auf diese Schaltfläche, um zur Seite **Ermitteln** zurückzukehren.  
  
##  <a name="Manage"></a> Phase für die Verwaltung der Datenermittlungsergebnisse  
 Nachdem Sie die Wissensermittlungsaktivität ausgeführt haben, können Sie Werte wie folgt ändern:  
  
-   Hinzufügen eines Domänenwerts zur Wertliste oder Auswählen eines Werts und Löschen des Werts aus der Liste  
  
-   Ändern des Status eines Domänenwerts, der durch den DQS-Erkennungsprozess festgelegt wurde, in „Richtig“, „Fehler“ oder „Ungültig“  
  
-   Geben Sie einen Ersetzungswert für einen fehlerhaften oder ungültigen Wert ein.  
  
-   Legen Sie zwei oder mehr Werte als Synonyme fest, und ändern Sie den vom Erkennungsprozess festgelegten führenden Wert, so dass der führende Wert den Synonymwert ersetzt, wenn die Eigenschaft **Führenden Wert verwenden** beim Erstellen der Domäne festgelegt wurde.  
  
-   Importieren Sie Domänenwerte aus einer Excel-Datei.  
  
 In der Tabelle **Wert** wird der Wissensdatenbank für eine einzelne Domäne hinzugefügtes Wissen angezeigt. Sie können diese Domäne in der Domänenliste im linken Bereich auswählen. Das Feld enthält die folgenden Spalten:  
  
-   In der Spalte **Wert** werden alle Werte angezeigt, die während des Ermittlungsprozesses der ausgewählten Domäne aus einem Feld im Datenbeispiel hinzugefügt wurden. Alle Werte, die als Fehler projiziert werden, werden als Synonym zu einem Wert angezeigt, der als richtig projiziert wird.  
  
-   In der Spalte **Häufigkeit** wird die Anzahl der Instanzen des Werts im Beispieldatenbankfeld angezeigt, dem die Domäne zugeordnet ist. Für eine Verbunddomäne werden nur Werte mit einer Frequenz größer gleich 20 angezeigt. Die Häufigkeitsdaten sind verfügbar, da der Wissensermittlungsprozess immer noch über eine Verbindung mit der Beispieldatenbank verfügt. In der Domänentabelle im Fenster Domänenverwaltung auf der Registerkarte Domänenwerte sind keine Häufigkeitsdaten verfügbar, weil der Domänenverwaltungsprozess über keine Verbindung mit der Beispielsdatenbank verfügt.  
  
-   In der Spalte **Typ** wird der Status des Werts angezeigt, wie vom Ermittlungsprozess bestimmt. Ein grünes Häkchen zeigt an, dass der Wert richtig ist oder korrigiert wurde. Ein rotes Kreuz zeigt an, dass der Wert einen Fehler aufweist. Ein orangefarbenes Dreieck mit einem Ausrufezeichen zeigt an, dass der Wert nicht gültig ist. Ein Wert, der nicht gültig ist, entspricht nicht den Datenanforderungen für die Domäne. Ein Wert, der einen Fehler aufweist, kann gültig sein, ist aber aus Datengründen nicht der richtige Wert.  
  
-   In der Spalte **Korrigieren in** wird ein richtiger Wert angezeigt, in den der Originalwert geändert wird, der als fehlerhaft oder ungültig gekennzeichnet wurde. DQS kann in Folge des Ermittlungsprozesses den richtigen Wert vorschlagen.  
  
 Verwalten Sie die Ermittlungsergebnisse folgendermaßen:  
  
1.  Wählen Sie im Bereich **Domänenliste** auf der linken Seite eine Domäne aus, für die Domänenwerte festgelegt werden sollen. Gehen Sie wie folgt vor, um die angezeigten Werte zu ändern:  
  
    -   Zeigen Sie die Ergebnisse, die in der Tabelle angezeigt werden sollen, basierend auf deren Status an, indem Sie in der Liste **Filter** den Status auswählen.  
  
    -   Suchen Sie die Daten, die Sie prüfen oder ändern möchten, indem Sie einen oder mehrere zu suchende Buchstaben in das Textfeld Suchen eingeben. Hierdurch werden die Buchstaben hervorgehoben, wenn diese in einem beliebigen angezeigten Wert vorkommen.  
  
    -   Klicken Sie aus **Nur neue anzeigen** , um die in der Tabelle angezeigten Werte auf die Werte zu beschränken, die in der aktuellen Sitzung ermittelt wurden, und um vorherige Werte auszuschließen.  
  
    -   Klicken Sie auf die Schaltfläche **Alle erweitern** , um alle Werte in einer beliebigen Gruppe von Synonymen anzuzeigen, wenn der aktuelle Status reduziert ist, oder auf die Schaltfläche **Alle reduzieren** , um alle Werte außer dem führenden Wert in einer beliebigen Gruppe von Synonymen auszublenden, wenn der aktuelle Status erweitert ist.  
  
    -   Klicken Sie auf die Schaltfläche **Bereich mit dem Verlauf der Domänenwertänderungen anzeigen/ausblenden** , um unterhalb der Werttabelle den Vorschaubereich einzublenden, in dem die letzten Änderungen an der Domänenwertsammlung angezeigt werden.  
  
2.  Suchen Sie alle von Data Quality Services vorgeschlagenen Korrekturen, indem Sie **Filter** auf **Fehler**festlegen. Überprüfen Sie, ob der Wert tatsächlich ein Fehler ist und ob der Wert in der Spalte **Korrigieren in** geeignet ist.  
  
3.  Legen Sie **Filter** auf **Alle Werte** fest, und überprüfen Sie, ob der Status der Werte geeignet ist. Um den Status eines Werts zu ändern, wählen Sie den Wert aus, und klicken Sie dann auf die Schaltfläche **Ausgewählte Domänenwerte als korrigiert festlegen** (Häkchen), die Schaltfläche **Ausgewählte Domänenwerte als Fehler festlegen** (Kreuz) oder auf die Schaltfläche **Ausgewählte Domänenwerte als ungültig festlegen** (Dreieck).  
  
4.  Um den Status eines Werts zu ändern, gehen Sie wie folgt vor:  
  
    1.  **Ausgewählte Domänenwerte als korrigiert festlegen**: Um den Status eines Werts von „Fehler“ oder „Ungültig“ in „Richtig“ zu ändern, wählen Sie den Wert aus, und klicken Sie dann nach Auswahl des Abwärtspfeils in der Symbolleiste oder in der Dropdownliste „Typ“ auf das Symbol **Ausgewählte Domänenwerte als korrigiert festlegen** (Häkchen). Wenn der fehlerhafte oder ungültige Wert mit einem richtigen Wert gruppiert ist, löschen Sie diesen Wert nach dem Vorgang.  
  
    2.  **Ausgewählte Domänenwerte als Fehler festlegen**: Um den Status eines Werts von „Richtig“ oder „Ungültig“ in „Fehler“ zu ändern, wählen Sie den Wert aus, und klicken Sie dann nach Auswahl des Abwärtspfeils in der Symbolleiste oder in der Dropdownliste „Typ“ auf das Symbol **Ausgewählte Domänenwerte als Fehler festlegen** (Kreuz). Sie können eine Korrektur in die Spalte **Korrigieren in** eingeben oder diese leer lassen.  
  
    3.  **Ausgewählte Domänenwerte als ungültig festlegen**: Um den Status eines Werts von „Richtig“ oder „Fehler“ in „Ungültig“ zu ändern, wählen Sie den Wert aus, und klicken Sie dann nach Auswahl des Abwärtspfeils in der Symbolleiste oder in der Dropdownliste „Typ“ auf das Symbol **Ausgewählte Domänenwerte als ungültig festlegen** (Dreieck). Sie können eine Korrektur in die Spalte **Korrigieren in** eingeben oder diese leer lassen.  
  
    4.  **Korrigieren in**: Nachdem Sie einen Wert als fehlerhaft oderungültig festgelegt haben, geben Sie in die Spalte **Korrigieren in** einen neuen Wert ein. DQS fügt eine neue Zeile für den Ersatzwert hinzu, legt diesen als richtig fest und gruppiert dann die zwei Werte. Der neue Wert wird als führender Wert angezeigt. Dabei wird der führende Wert fett und der fehlerhafte oder ungültige Wert eingezogen dargestellt.  
  
5.  Um Werte als Gruppe von Synonymen festzulegen, wählen Sie mehrere richtige Werte aus, und gehen Sie dann wie folgt vor:  
  
    -   **Ausgewählte Domänenwerte als Synonyme festlegen**: Klicken Sie auf diese Option, um die ausgewählten Werte als Synonyme festzulegen. DQS legt einen der Werte als führenden Wert fest, durch den die anderen Werte ersetzt werden.  
  
        > [!NOTE]  
        >  Wenn Sie zwei oder mehr Werte in einer Gruppe und einen anderen Wert außerhalb der Gruppe auswählen und diese dann als Synonyme festlegen, erhalten Sie eine falsche Fehlermeldung. Die Werte werden ordnungsgemäß als Synonyme festgelegt, nachdem Sie die Fehlermeldung geschlossen haben.  
  
    -   **Beziehung zwischen ausgewählten Synonymen aufheben**: Klicken Sie auf diese Option, um die Synonymzuordnung rückgängig zu machen.  
  
    -   **Ausgewählten Domänenwert als führenden Wert der zugehörigen Gruppe festlegen**: Ändern Sie den führenden Wert der Gruppe, indem Sie einen Wert in der Gruppe auswählen, der nicht als führender Wert festgelegt ist, und klicken Sie dann auf die Schaltfläche **Ausgewählten Domänenwert als führenden Wert der zugehörigen Gruppe festlegen** .  
  
6.  **Rechtschreibprüfung**: Wenn Sie die Rechtschreibprüfung auf der Seite Domäneneigenschaften aktiviert haben, suchen Sie alle Werte mit einem welligen roten Unterstrich, da dadurch anzeigt wird, dass die Rechtschreibprüfung eine Korrektur vorschlägt. Klicken Sie mit der rechten Maustaste auf den unterstrichenen Wert, und wählen Sie eine Korrektur aus, sofern zutreffend. Als Werttyp wird „Fehler“ festgelegt (oder beibehalten), und die Korrektur wird zur Spalte **Korrigieren in** hinzugefügt. Klicken Sie auf den Abwärtspfeil, um weitere vorgeschlagene Korrekturen anzuzeigen. Geben Sie eine Korrektur manuell ein, um sie dem Rechtschreibprüfungswörterbuch hinzuzufügen und als Korrektur auswählen zu können. Weitere Informationen finden Sie unter [Use the DQS Speller](../data-quality-services/use-the-dqs-speller.md) und [Set Domain Properties](../data-quality-services/set-domain-properties.md).  
  
    > [!NOTE]  
    >  Um die Rechtschreibprüfung zu verwenden, können Sie diese auf der Seite **Domäneneigenschaften** aktivieren. Wenn sie auf der Seite **Domäneneigenschaften** deaktiviert ist, können Sie auf der Seite **Datenermittlungsergebnisse verwalten** auf das Symbol **Rechtschreibprüfung aktivieren/deaktivieren** klicken, um sie auf dieser Seite zu aktivieren.  
  
7.  **Neuen Domänenwert hinzufügen**: Fügen Sie einen neuen Wert zur Domäne hinzu, indem Sie auf die Schaltfläche **Neuen Domänenwert hinzufügen** klicken, um eine Zeile am Ende der Tabelle hinzuzufügen. Nachdem Sie einen Wert eingegeben haben, wird die Zeile in alphabetischer Reihenfolge neu angeordnet.  
  
8.  **Domänenwerte aus Excel importieren**: Fügen Sie neue Werte aus einer Excel-Tabellenkalkulation hinzu, indem Sie auf den Abwärtspfeil für das Symbol **Werte importieren** klicken und dann **Domänenwerte aus Excel importieren**auswählen. Geben Sie den Dateinamen ein, wählen Sie **Erste Zeile als Header verwenden** aus, sofern zutreffend, und klicken Sie dann auf **OK**. Weitere Informationen finden Sie unter [Import Values from an Excel File into a Domain](../data-quality-services/import-values-from-an-excel-file-into-a-domain.md).  
  
9. **Projektwerte importieren**: Fügen Sie neue Werte aus einem Data Quality-Projekt hinzu, indem Sie auf den Abwärtspfeil für das Symbol **Werte importieren** klicken und dann **Projektwerte importieren**auswählen. Geben Sie den Dateinamen ein, wählen Sie **Erste Zeile als Header verwenden** aus, sofern zutreffend, und klicken Sie dann auf **OK**. Wählen Sie das Projekt aus, aus dem Sie Werte importieren möchten, und klicken Sie auf **OK**. Die importierten Werte werden angezeigt. Klicken Sie auf **Fertig stellen**. Weitere Informationen finden Sie unter „Importieren von Projektwerten in eine Domäne“.  
  
10. **Ausgewählte Domänenwerte löschen**: Entfernen Sie einen oder mehrere vorhandene Werte aus einer Domäne, indem Sie die Werte auswählen und dann auf das Symbol **Ausgewählte Domänenwerte löschen** klicken. Ein Eintrag von DQS_NULL kann nicht gelöscht werden. Wenn Sie mehrere zu löschende Werte auswählen und einer davon DQS_NULL ist, schlägt der Vorgang daher fehl.  
  
11. Klicken Sie auf **Fertig stellen** , um den Wissensermittlungsaktivität abzuschließen. Ein Popupfenster wird angezeigt, wenn Sie nicht jede einzelne Domäne überprüft haben. Klicken Sie auf **Ja** , um weiterhin zu überprüfen, oder auf **Nein** , um fortzufahren. Wenn Sie auf Nein klicken, wird ein anderes Popupfenster mit den folgenden Optionen angezeigt:  
  
    1.  **Veröffentlichen**: Die Wissensdatenbank wird veröffentlicht und kann vom aktuellen Benutzer oder von anderen Benutzern verwendet werden. Die Wissensdatenbank wird nicht gesperrt, der Status der Wissensdatenbank (in der Wissensdatenbanktabelle) wird auf leer festgelegt, und die Aktivitäten für die Domänenverwaltung sowie die Wissensermittlung sind verfügbar. Sie kehren zur Startseite zurück. Um den Prozess abzuschließen, klicken Sie auf **Ja** .  
  
    2.  **Nein**: Ihre Arbeit wird gespeichert, die Wissensdatenbank bleibt gesperrt, und der Status der Wissensdatenbank wird auf "In Arbeit" festgelegt. Sowohl die Domänenverwaltungs- als auch die Wissensermittlungsaktivitäten sind verfügbar. Sie kehren zur Startseite zurück.  
  
    3.  **Abbrechen**: Das Popupfenster wird geschlossen, und Sie kehren zum Fenster **Domänenwerte verwalten** zurück.  
  
12. Sie können auch auf eine der folgenden Schaltflächen klicken:  
  
    -   Klicken Sie auf**Abbrechen** , um die Wissensermittlung abzubrechen, ohne die Ergebnisse zu speichern, und um zur DQS-Homepage zurückzukehren.  
  
    -   Klicken Sie auf**Schließen** , um die Ergebnisse zu speichern und zur DQS-Homepage zurückzukehren. Die Wissensdatenbank wird für Sie gesperrt, und der Status der Wissensdatenbank wird in der Wissensdatenbanktabelle auf der Seite **Wissensdatenbank öffnen** als **Ermittlung – Werteverwaltung**angezeigt.  
  
    -   Klicken Sie auf **Zurück** , um zur Seite **Ermitteln** zurückzukehren. Nachdem Sie auf **Schließen**geklickt haben, um die Domänenverwaltung durchzuführen, müssen Sie im Fenster **Wissensdatenbank öffnen** auf **Wissensermittlung** klicken, die Seite **Wissensdatenbank-Verwaltung: Domänenbegriffe verwalten** öffnen, auf **Fertig stellen**klicken und anschließend auf **Ja** (um die Wissensdatenbank zu veröffentlichen) oder **Nein** (um die Arbeit in der Wissensdatenbank zu speichern und zu beenden) klicken.  
  
##  <a name="FollowUp"></a> Nachverfolgung: Nach dem Ausführen der Wissensermittlung  
 Nachdem Sie mithilfe des computergestützten Wissensermittlungsprozesses Wissen zur Wissensdatenbank hinzugefügt haben, können Sie die Wissensdatenbank sofort für ein Bereinigungsprojekt verwenden oder die Domänenverwaltung vor der Bereinigung durchführen. Weitere Informationen zur Datenbereinigung oder Domänenverwaltung finden Sie unter [Datenbereinigung](../data-quality-services/data-cleansing.md) oder [Verwalten einer Domäne](../data-quality-services/managing-a-domain.md).  
  
##  <a name="Meaning"></a> Die Bedeutung von richtigen, fehlerhaften und ungültigen Werten  
 Jedem Wert in der Tabelle **Wert** der Seite **Domänenwerte** wird eine Einstellung für **Typ** von **Richtig**, **Fehler**oder **Ungültig**zugewiesen. Der Typ des Werts wird anfänglich von der Wissensermittlungsaktivität generiert, Sie können diesen jedoch nach Bedarf ändern. Der abschließende sowohl auf der Ermittlung als auch auf interaktiven Änderungen basierende Typ wird durch die Bereinigungsaktivität generiert. Diese Einstellungen haben die folgenden Bedeutungen:  
  
-   **Richtig:** Dieser Wert gehört zur Domäne und weist keine Syntaxfehler auf. Beispielsweise ist „Chicago“ in einer Ortsdomäne richtig.  
  
-   **Fehler:** Dieser Wert gehört zur Domäne, ist aber fehlerhaft. beispielsweise ist „Shicago“ statt „Chicago“ in einer Ortsdomäne ein Fehler. DQS kennzeichnet einen Wert als fehlerhaft, wenn ein Syntaxfehler und eine zugehörige Korrektur im Ermittlungsprozess erkannt wird. Syntaxfehler schließen auch orthographische Fehler ein.  
  
-   **Ungültig:** Dieser Wert gehört nicht zur Domäne, und es ist keine Korrektur vorhanden. Beispielsweise ist der Wert „12345“ in einer Ortsdomäne ungültig. DQS kennzeichnet einen Wert als ungültig, wenn er eine Domänenregel nicht erfüllt.  
  
 Sie können den Typ eines Werts manuell in einen der beiden anderen Werte ändern. DQS erzwingt bei manuellen Vorgängen keine Gültigkeits- und Fehlersemantik. Sie können eine Korrektur für einen ungültigen Wert eingeben, ohne den Status zu ändern. Sie können einen Wert als ungültig festlegen, auch wenn er keiner Domänenregel widerspricht. Sie können einen Wert als fehlerhaft festlegen, auch wenn der Ermittlungsprozess nicht angegeben hat, dass er einen Syntaxfehler aufweist. Sie können außerdem eine Korrektur eines fehlerhaften Werts entfernen, der als richtig markiert wurde, ohne den Status zu ändern.  
  
 Wenn Sie eine interaktive Datenbereinigung auf der Seite **Ergebnisse verwalten und anzeigen** der Aktivität **Bereinigung** ausführen, werden sowohl ungültige als auf fehlerhafte Werte auf der Registerkarte **Ungültig** der Seite **Ergebnisse verwalten und anzeigen** angezeigt.  
  
##  <a name="Display"></a> How to Display the Appropriate Values  
 Sie können die Anzeige wie folgt ändern:  
  
-   **Filtern** Sie die Ergebnisse, die in der Tabelle angezeigt werden sollen, basierend auf deren Status, indem Sie in der Dropdownliste **Filter** den Status auswählen.  
  
-   **Suchen** Sie die Daten, die Sie prüfen oder ändern möchten, indem Sie einen oder mehrere zu suchende Buchstaben in das Textfeld **Suchen** eingeben. Hierdurch werden die Buchstaben hervorgehoben, wenn diese in einem beliebigen angezeigten Wert vorkommen.  
  
-   Klicken Sie aus **Nur neue anzeigen** , um die in der Tabelle angezeigten Werte auf die Werte zu beschränken, die in der aktuellen Sitzung ermittelt wurden, und um vorherige Werte auszuschließen.  
  
-   Klicken Sie die Schaltfläche **Alle erweitern** , um alle Werte in einer beliebigen Gruppe von Synonymen anzuzeigen, wenn der aktuelle Status reduziert ist.  
  
-   Klicken Sie die Schaltfläche **Alle reduzieren** , um alle Werte mit Ausnahme des führenden Werts in einer beliebigen Gruppe von Synonymen auszublenden, wenn der aktuelle Status erweitert ist.  
  
-   Klicken Sie auf die Schaltfläche **Bereich mit dem Verlauf der Domänenwertänderungen anzeigen/ausblenden** , um unterhalb der Werttabelle den Vorschaubereich einzublenden, in dem die letzten Änderungen an der Domänenwertsammlung angezeigt werden.  
  
##  <a name="Profiler"></a> Profiler-Statistik  
 Die Registerkarte <ui>Profiler</ui> stellt Statistiken bereit, die die Qualität der Quelldaten angeben. Die Statistiken messen nicht die Qualität der Wissensdatenbank. Die Profilerstellung bei der Wissensermittlung gibt Einblicke in Vollständigkeit und Eindeutigkeit. Die Profilerstellung bei der Wissensermittlung misst keine Genauigkeit. Mithilfe der Profilerstellung für die Wissensverwaltung können Sie bewerten, in welchem Maß die Datenquelle für die Erstellung und Verbesserung des Wissens in einer Wissensdatenbank nützlich ist.  
  
 Die Registerkarte **Profiler** stellt die folgenden Statistiken für den Ermittlungsprozess, nach Feld und Domäne geordnet, bereit:  
  
-   **Datensätze**: Wie viele Datensätze wurden im Datenbeispiel ermittelt?  
  
-   **Gesamtwerte**: Wie viele Gesamtwerte wurden für jedes Feld und insgesamt gefunden?  
  
-   **Neue Werte**: Wie viele der Gesamtwerte für jedes Feld und alle zugeordneten Felder wurden seit dem letzten Ermittlungsprozess neu gefunden, und wie hoch ist ihr prozentualer Anteil an den Gesamtwerten?  
  
-   **Eindeutige Werte**: Wie viele der Gesamtwerte für jedes Feld und alle zugeordneten Felder sind eindeutige Werte, und wie hoch ist ihr prozentualer Anteil an den Gesamtwerten?  
  
-   **Neue eindeutige Werte**: Wie viele der eindeutigen Werte für jedes Feld und alle zugeordneten Felder wurden seit dem letzten Ermittlungsprozess neu gefunden, und wie hoch ist ihr prozentualer Anteil an den Gesamtwerten?  
  
-   **In Domänenwerten gültig**: Wie viele der Gesamtwerte für jedes Feld und alle zugeordneten Felder sind gültig, und wie hoch ist ihr prozentualer Anteil an den Gesamtwerten?  
  
 Die Feldstatistiken umfassen Folgendes:  
  
-   **Feld**: Name des Felds in den Quelldaten  
  
-   **Domäne**: Name der Domäne, die dem Feld zugeordnet ist  
  
-   **Neu**: Die Anzahl der neuen Werte und der prozentuale Anteil neuer Werte im Vergleich zu vorhandenen Werten im Feld  
  
-   **Eindeutig**: Die Gesamtzahl der eindeutigen Datensätze in den Feldern und ihr prozentualer Anteil am Ganzen  
  
-   **In Domäne gültig**: Die Anzahl der gültigen Domänenwerte und ihr prozentualer Anteil am Gesamtwert  
  
-   **Vollständigkeit**: Die Vollständigkeit jedes Quellfelds, das für den Abgleich zugeordnet ist  
  
 Die Profilerstellung bei der Wissensermittlung gibt Einblicke in die Vollständigkeit. Wenn die Profilerstellung Ihnen sagt, dass ein Feld relativ unvollständig ist, sollten Sie es aus der Wissensdatenbank eines Data Quality-Projekts entfernen. Die Profilerstellung kann keine zuverlässigen Vollständigkeitsstatistiken für Verbunddomänen bereitstellen. Wenn Sie Vollständigkeitsstatistiken benötigen, verwenden Sie Einzeldomänen anstatt Verbunddomänen. Wenn Sie Verbunddomänen verwenden möchten, sollten Sie eine Wissensdatenbank mit Einzeldomänen für die Profilerstellung erstellen, um die Vollständigkeit zu bestimmen, und eine weitere Domäne mit einer Verbunddomäne für den Bereinigungsprozess erstellen. Die Profilerstellung kann z. B. 95 % Vollständigkeit für Adressendatensätze anzeigen, die eine Verbunddomäne verwenden, aber es kann einen viel höheren Grad der Unvollständigkeit für eine der Spalten geben, z. B. für eine Postleitzahlspalte. In diesem Beispiel möchten Sie die Vollständigkeit der Postleitzahlspalte mit einer Einzeldomäne messen. Die Profilerstellung stellt wahrscheinlich zuverlässige Genauigkeitsstatistiken für Verbunddomänen bereit, da Sie die Genauigkeit für mehrere Spalten gemeinsam messen können. Der Wert dieser Daten liegt in der zusammengesetzten Aggregation, daher sollten Sie die Genauigkeit mit einer Verbunddomäne messen.  
  
 Statistiken werden auf der Registerkarte Profiler in den folgenden Phasen angezeigt:  
  
-   In der Phase **Datensätze werden vorverarbeitet** lädt DQS die Daten und indiziert sie. Dieser Vorgang wird für einen Datensatz nach dem anderen oder Batch nach dem anderen durchgeführt, deshalb kann der Verlauf nach Datensätzen angezeigt werden. Während der Ausführung dieses Schritts können die meisten Profilerstellungsdaten generiert werden – mit Ausnahme der Werte unter **In Domäne gültig** .  
  
-   In der Phase **Domänenregeln werden ausgeführt** wird die Spalte **In Domäne gültig** aufgefüllt, da alle Domänenregeln als unteilbare Einheit jedes Domänenwerts ausgeführt werden.  
  
-   In der Phase **Ermittlung wird ausgeführt** werden keine neuen Daten auf der Registerkarte Profiler aktualisiert. Alle aufgetretenen Syntaxfehler können im nächsten Schritt des Assistenten, in der Phase **Domänenwerte verwalten**, angezeigt werden.  
  
 Bei der Wissensermittlungsaktivität führen die folgenden Bedingungen zu Benachrichtigungen:  
  
-   In einem Feld sind keine neuen Werte enthalten; Sie sollten es aus der Zuordnung entfernen.  
  
-   In einem Feld sind wenige neue Werte enthalten; Es könnte besser sein, es aus der Zuordnung zu entfernen.  
  
-   Ein Feld ist leer; Sie sollten es aus der Zuordnung entfernen.  
  
-   Das Feldvollständigkeitsergebnis ist sehr niedrig; Sie sollten es aus der Zuordnung entfernen.  
  
-   Alle Werte in einem Feld sind ungültig; Sie sollten die Zuordnung und die Relevanz von Domänenregeln für den Feldinhalt überprüfen.  
  
-   Es gibt nur wenige gültige Werte im Feld; Sie sollten die Zuordnung und die Relevanz von Domänenregeln für den Feldinhalt überprüfen.  
  
 Weitere Informationen zur Profilerstellung finden Sie unter [Datenprofilerstellung und Benachrichtigungen in DQS](../data-quality-services/data-profiling-and-notifications-in-dqs.md).  
  
  
