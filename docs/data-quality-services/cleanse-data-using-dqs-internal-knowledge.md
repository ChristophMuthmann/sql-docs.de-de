---
title: Bereinigen von Daten mit (internem) DQS-Wissen | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: data-quality-services
ms.service: 
ms.component: data-quality-services
ms.reviewer: 
ms.suite: sql
ms.technology:
- data-quality-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dqs.dqproject.interactivecleansing.f1
- sql13.dqs.dqproject.map.f1
- sql13.dqs.dqproject.correction.f1
- sql13.dqs.dqproject.export.f1
ms.assetid: c96b13ad-02a6-4646-bcc7-b4a8d490f5cc
caps.latest.revision: 26
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 8aa5b0fdf2771d83310e503f2fdd8770bf9cf324
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="cleanse-data-using-dqs-internal-knowledge"></a>Bereinigen von Daten mit (internem) DQS-Wissen
  In diesem Thema wird beschrieben, wie die Daten mithilfe eines Data Quality-Projekts in [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) gereinigt werden. Die Datenbereinigung wird mithilfe einer Wissensdatenbank, die in DQS gegen ein hochwertiges Dataset erstellt wurde, für die Quelldaten ausgeführt. Weitere Informationen finden Sie unter [Aufbau einer Wissensdatenbank](../data-quality-services/building-a-knowledge-base.md).  
  
 Die Datenbereinigung wird in vier Phasen ausgeführt: eine *Zuordnungsphase* , in der Sie die zu reinigende Datenquelle identifizieren und den erforderlichen Domänen in einer Wissensdatenbank zuordnen, einer *computerunterstützten Bereinigungsphase* , in der DQS die Wissensdatenbank auf die zu bereinigenden Daten anwendet und Änderungen an den Quelldaten vorschlägt/vornimmt, eine *interaktive Bereinigungsphase* , in der Data Stewards die Datenänderungen analysieren und annehmen/ablehnen können, und schließlich die *Exportphase* , in der die Sie die bereinigten Daten exportieren können. Jeder dieser Prozesse wird auf einer separaten Seite des Bereinigungsaktivitäts-Assistenten ausgeführt, sodass Sie zwischen den Seiten hin und her wechseln, den Prozess erneut auszuführen, einen bestimmten Bereinigungsprozess schließen und dann zur gleichen Phase des Prozesses zurückkehren können. DQS stellt Ihnen Statistiken zu den Quelldaten und den Bereinigungsergebnissen bereit, die es Ihnen ermöglichen, informierte Entscheidungen zur Datenbereinigung zu treffen.  
  
## <a name="before-you-begin"></a>Vorbereitungen  
  
###  <a name="Prerequisites"></a> Erforderliche Komponenten  
  
-   Sie müssen entsprechende Schwellenwerte für die Bereinigungsaktivität angegeben haben. Weitere Informationen dazu finden Sie unter [Konfigurieren der Schwellenwerte für Bereinigung und Abgleich](../data-quality-services/configure-threshold-values-for-cleansing-and-matching.md).  
  
-   Eine DQS-Wissensdatenbank muss auf [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] verfügbar sein, um Ihre Quelldaten vergleichen und bereinigen zu können. Darüber hinaus muss die Wissensdatenbank Wissen zum Typ von Daten enthalten, die Sie bereinigen möchten. Wenn Sie z. B. die Quelldaten bereinigen, die US-Adressen enthalten, benötigen Sie eine Wissensdatenbank, die gegen „hochwertige“ Beispieldaten für US-Adressen erstellt wurde.  
  
-   Microsoft Excel muss auf dem [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] -Computer installiert sein, wenn sich die Quelldaten, die bereinigt werden sollen, in einer Excel-Datei befinden. Andernfalls sind Sie nicht in der Lage, die Excel-Datei in der Zuordnungsphase auszuwählen. Die von Microsoft Excel erstellten Dateien können die Erweiterung .xlsx, .xls oder .csv haben. Wenn die 64-Bit-Version von Excel verwendet wird, werden nur Excel 2003-Dateien (.xls) unterstützt; Excel 2007- oder 2010-Dateien (.xlsx) werden nicht unterstützt. Wenn Sie die 64-Bit-Version von Excel 2007 oder 2010 verwenden, speichern Sie die Datei als XLS-Datei oder CSV-Datei, oder installieren Sie stattdessen eine 32-Bit-Version von Excel.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Sie müssen über die Rolle "dqs_kb_editor" oder "dqs_kb_operator" für die Datenbank DQS_MAIN verfügen, um eine Datenbereinigung auszuführen.  
  
##  <a name="Create"></a> Erstellen eines Data Quality-Bereinigungsprojekts  
 Sie müssen den Datenbereinigungsvorgang mithilfe eines Data Quality-Projekts ausführen. So erstellen Sie ein Data Quality-Bereinigungsprojekt:  
  
1.  Führen Sie die Schritte 1-3 im Thema [Erstellen eines Data Quality-Projekts](../data-quality-services/create-a-data-quality-project.md)aus.  
  
2.  Wählen Sie in Schritt 3.d die **Bereinigungsaktivität** aus.  
  
3.  Klicken Sie auf **Erstellen** , um ein Data Quality-Bereinigungsprojekt zu erstellen.  
  
 Dies erstellt ein Data Quality-Bereinigungsprojekt und öffnet die Seite **Karte** des Data Quality-Bereinigungs-Assistenten.  
  
##  <a name="Mapping"></a> Zuordnungsphase  
 In der Zuordnungsphase geben Sie die Verbindung zu den zu bereinigenden Quelldaten an und ordnen die Spalten in den Quelldaten den entsprechenden Domänen in der ausgewählten Wissensdatenbank zu.  
  
1.  Wählen Sie auf der Seite **Struktur** des Data Quality-Bereinigungs-Assistenten die zu bereinigenden Quelldaten aus: **SQL Server** oder **Excel-Datei**:  
  
    1.  **SQL Server**: Wählen Sie **DQS_STAGING_DATA** als Quelldatenbank aus, wenn Sie die Quelldaten in diese Datenbank kopiert haben, und wählen Sie dann die entsprechende Tabelle/Sicht aus, die die Quelldaten enthält. Wählen Sie andernfalls die Quelldatenbank und die entsprechende Tabelle/Sicht aus. Die Quelldatenbank muss sich in der gleichen SQL Server-Instanz wie [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] befinden, um in der Dropdownliste **Datenbank** verfügbar zu sein.  
  
    2.  **Excel-Datei**: Klicken Sie auf **Durchsuchen**, und wählen Sie die Excel-Datei aus, die die Daten enthält, die gereinigt werden sollen. Microsoft Excel muss auf dem [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] -Computer installiert sein, um eine Excel-Datei auswählen zu können. Andernfalls ist die Schaltfläche **Durchsuchen** nicht verfügbar, und Sie werden unter diesem Textfeld benachrichtigt, dass Microsoft Excel nicht installiert ist. Lassen Sie außerdem das Kontrollkästchen **Erste Zeile als Header verwenden** aktiviert, wenn die erste Zeile der Excel-Datei Headerdaten enthält.  
  
2.  Ordnen Sie unter **Zuordnungen**die Datenspalten in den Quelldaten den entsprechenden Domänen in der Wissensdatenbank zu, indem Sie eine Quellspalte aus der Dropdownliste in der Spalte **Quellspalte** auswählen und dann eine Domäne aus der Dropdownliste in der Spalte **Domäne** in der gleichen Zeile auswählen. Wiederholen Sie diesen Schritt, um alle Spalten in den Quelldaten entsprechenden Domänen in der Wissensdatenbank zuzuordnen. Klicken Sie ggf. auf das Symbol **Spaltenzuordnung hinzufügen** , um der Zuordnungstabelle Zeilen hinzuzufügen.  
  
    > [!NOTE]  
    >  Sie können die Quelldaten zum Durchführen der Datenbereinigung einer DQS-Domäne nur zuordnen, wenn der Quelldatentyp in DQS unterstützt wird und mit dem DQS-Domänendatentyp übereinstimmt. Informationen zu unterstützten Quelldatentypen finden Sie unter [Unterstützte SQL Server- und SSIS-Datentypen für DQS-Domänen](../data-quality-services/supported-sql-server-and-ssis-data-types-for-dqs-domains.md).  
  
3.  Klicken Sie auf das Symbol **Vorschau der Datenquelle** , um die Daten in der ausgewählten SQL Server-Tabelle oder -Sicht oder im ausgewählten Excel-Arbeitsblatt anzuzeigen.  
  
4.  Klicken Sie auf **Verbunddomänen anzeigen/auswählen** , um eine Liste der Verbunddomänen anzuzeigen, die einer Quellspalte zugeordnet sind. Diese Schaltfläche ist nur verfügbar, wenn Sie mindestens eine Verbunddomäne haben, die einer Quellspalte zugeordnet ist.  
  
5.  Klicken Sie auf **Weiter** , um zur computerunterstützten Bereinigungsphase (Seite**Bereinigen** ) zu wechseln.  
  
##  <a name="ComputerAssisted"></a> Computerunterstützte Bereinigungsphase  
 In der computerunterstützten Bereinigungsphase führen Sie einen automatisierten Datenbereinigungsprozess aus, der Quelldaten im Hinblick auf die zugeordneten Domänen in der Wissensdatenbank analysiert und Datenänderungen vornimmt/vorschlägt.  
  
1.  Klicken Sie auf der Seite **Bereinigen** des Data Quality-Assistenten auf **Start** , um den computerunterstützten Bereinigungsprozess auszuführen. DQS verwendet erweiterte Algorithmen und Vertrauensgrade auf Grundlage der angegebenen Schwellenwertebenen, um die Daten im Hinblick auf die ausgewählte Wissensdatenbank zu analysieren und dann zu bereinigen. Weitere Informationen zur computerunterstützten Bereinigung in DQS finden Sie unter [Computerunterstützte Bereinigung](../data-quality-services/data-cleansing.md#ComputerAssisted) in [Datenbereinigung](../data-quality-services/data-cleansing.md).  
  
    > [!IMPORTANT]  
    >  -   Nachdem die Datenanalyse abgeschlossen wurde, wird die Schaltfläche **Start** zur Schaltfläche **Neustart** . Wenn die Ergebnisse der vorherigen Analyse noch nicht gespeichert wurden, gehen beim Klicken auf **Neustart** die vorherigen Daten verloren. Verlassen Sie während der Ausführung der Analyse nicht die Seite, da ansonsten der Analyseprozess abgebrochen wird.  
    > -   Wenn die für das Bereinigungsprojekt verwendete Wissensdatenbank nach dem Erstellen des Bereinigungsprojekts aktualisiert und veröffentlicht wurde, werden Sie beim Klicken auf **Start** gefragt, ob die neueste Wissensdatenbank für die Bereinigung verwendet werden soll. Dies kann in der Regel geschehen, wenn Sie ein Data Quality-Projekt mithilfe einer Wissensdatenbank erstellt haben, das Bereinigungsprojekt zwischendurch durch Klicken auf **Schließen**geschlossen haben und das Data Quality-Projekt dann später wieder geöffnet haben, um die Bereinigung auszuführen. Inzwischen wurde die im Bereinigungsprojekt verwendete Wissensdatenbank aktualisiert und veröffentlicht.  
    >   
    >      Wenn die für das Bereinigungsprojekt verwendete Wissensdatenbank nach der letzten Ausführung der computerunterstützten Bereinigung aktualisiert und veröffentlicht wurde, werden Sie beim Klicken auf **Neustart** gefragt, ob die neueste Wissensdatenbank für die Bereinigung verwendet werden soll.  
    >   
    >      Klicken Sie in beiden Fällen auf **Ja** , um die aktualisierte Wissensdatenbank für die computerunterstützte Bereinigung zu verwenden. Wenn es darüber hinaus Konflikte zwischen aktuellen Zuordnungen und der aktualisierten Wissensdatenbank gibt (wenn z. B. Domänen gelöscht wurden oder der Domänendatentyp geändert wurde) gibt, fordert die Meldung Sie auch auf, die aktuellen Zuordnungen zu korrigieren, um die aktualisierte Wissensdatenbank zu verwenden. Wenn Sie auf **Ja** klicken, gelangen Sie zur Seite **Struktur** , wo Sie die Zuordnungen korrigieren können, bevor Sie mit der computerunterstützten Bereinigung fortfahren.  
  
2.  Während der computerunterstützten Bereinigungsphase können Sie den Profiler einschalten, indem Sie auf die Registerkarte **Profiler** klicken, um Echtzeitdaten zur Profilerstellung und zu Benachrichtigungen anzuzeigen. Weitere Informationen finden Sie unter [Profiler-Statistik](#Profiler).  
  
3.  Wenn Sie mit den Ergebnissen nicht zufrieden sind, klicken Sie auf **Zurück** , um zur Seite **Struktur** zurückzukehren, ändern Sie ggf. eine oder mehrere Zuordnungen, kehren Sie zur Seite **Bereinigen** zurück, und klicken Sie dann auf **Neustart**.  
  
4.  Nachdem der computerunterstützte Bereinigungsprozess abgeschlossen wurde, klicken Sie auf **Weiter** , um zur interaktiven Bereinigungsphase zu gelangen (Seite**Ergebnisse verwalten und anzeigen** ).  
  
##  <a name="Interactive"></a> Interaktive Bereinigungsphase  
 In der interaktiven Bereinigungsphase können Sie die von DQS vorgeschlagenen Änderungen anzeigen und durch Annehmen oder Ablehnen der Änderungen entscheiden, ob sie implementiert werden sollen. Im linken Bereich der Seite **Ergebnisse verwalten und anzeigen** zeigt DQS eine Liste aller Domänen an, die Sie zuvor in der Zuordnungsphase zusammen mit der Anzahl der Werte in den Quelldaten, die gegen alle Domänen während der computerunterstützten Bereinigungsphase analysiert wurden, zugeordnet haben. Im dem rechten Bereich der Seite **Ergebnisse verwalten und anzeigen** kategorisiert DQS auf Grundlage des Einhaltens der Domänenregeln, Syntaxfehlerregeln und erweiterter Algorithmen die Daten auf fünf Registerkarten mithilfe des *Vertrauensgrads*. Der Vertrauensgrad gibt die DQS-Sicherheitsstufe der Korrektur oder des Vorschlags an und basiert auf den folgenden Schwellenwerten:  
  
-   **Schwellenwert für die automatische Korrektur**: Jeder Wert mit einem Vertrauensgrad oberhalb dieses Schwellenwerts wird von DQS automatisch korrigiert. Der Data Steward kann die Änderung jedoch während der interaktiven Bereinigung überschreiben. Sie können den automatischen Korrekturschwellenwert auf der Registerkarte **Allgemeine Einstellungen** auf dem Bildschirm **Konfiguration** angeben. Weitere Informationen finden Sie unter [Konfigurieren der Schwellenwerte für Bereinigung und Abgleich](../data-quality-services/configure-threshold-values-for-cleansing-and-matching.md).  
  
-   **Schwellenwert für automatische Vorschläge**: Jeder Wert mit einem Vertrauensgrad oberhalb dieses Schwellenwerts, jedoch unterhalb des Schwellenwerts für die automatische Korrektur, wird als Ersetzungswert vorgeschlagen. DQS nimmt die Änderung nur vor, wenn sie vom Data Steward genehmigt wird. Sie können den automatischen Vorschlagsschwellenwert auf der Registerkarte **Allgemeine Einstellungen** auf dem Bildschirm **Konfiguration** angeben. Weitere Informationen finden Sie unter [Konfigurieren der Schwellenwerte für Bereinigung und Abgleich](../data-quality-services/configure-threshold-values-for-cleansing-and-matching.md).  
  
-   **Sonstige**: Jeder Wert unterhalb des Schwellenwerts für automatische Vorschläge wird von DQS unverändert gelassen.  
  
 Abhängig vom Vertrauensgrad werden die Werte auf einer der folgenden fünf Registerkarten angezeigt:  
  
|Registerkarte|Beschreibung|  
|---------|-----------------|  
|**Vorgeschlagen**|Zeigt die Domänenwerte an, für die DQS die vorgeschlagenen Werte gefunden hat, die einen Vertrauensgrad aufweisen, der höher als der *automatisch vorgeschlagene Schwellenwert* , aber niedriger als der *Schwellenwert für die automatische Korrektur* ist.<br /><br /> Die vorgeschlagenen Werte werden in der Spalte **Korrigieren in** im Vergleich zum ursprünglichen Wert angezeigt. Sie können auf das Optionsfeld in der Spalte **Genehmigen** oder **Ablehnen** für einen Wert im oberen Raster klicken, um den Vorschlag für alle Instanzen des Wertes anzunehmen oder abzulehnen. In diesem Fall wird der angenommene Wert auf die Registerkarte **Korrigiert** verschoben, und der abgelehnte Wert wird auf die Registerkarte **Ungültig** verschoben.|  
|**Neu**|Zeigt die gültige Domäne an, für die DQS nicht genug Informationen aufweist, und die daher keiner anderen Registerkarte zugeordnet werden kann. Außerdem enthält diese Registerkarte auch Werte, die einen Vertrauensgrad aufweisen, der unterhalb des *automatisch vorgeschlagenen Schwellenwerts* liegt, aber hoch genug ist, um als gültig markiert zu werden.<br /><br /> Wenn Sie glauben, dass der Wert richtig ist, klicken Sie auf das Optionsfeld in der Spalte **Genehmigen** . Klicken Sie andernfalls auf das Optionsfeld in der Spalte **Ablehnen** . Der angenommene Wert wird auf die Registerkarte **Richtig** verschoben, und der abgelehnte Wert wird auf die Registerkarte **Ungültig** verschoben. Sie können den richtigen Wert auch manuell als Ersatz für den ursprünglichen Wert in der Spalte **Korrigieren in** eingeben und dann auf das Optionsfeld in der Spalte **Genehmigen** klicken, um die Änderung anzunehmen. In diesem Fall wird der Wert auf die Registerkarte **Korrigiert** verschoben.|  
|**Ungültig**|Zeigt die Domänenwerte an, die in der Domäne in der Wissensdatenbank als ungültig markiert wurden, oder zeigt Werte an, die eine Domänenregel verletzt haben. Diese Registerkarte enthält auch Werte, die vom Benutzer auf einer der anderen vier Registerkarten abgelehnt wurden.<br /><br /> Wenn Sie aber glauben, dass der Wert richtig ist, klicken Sie auf das Optionsfeld in der Spalte **Genehmigen** . Der angenommene Wert wird auf die Registerkarte **Richtig** verschoben. Sie können den richtigen Wert auch manuell als Ersatz für den ursprünglichen Wert in der Spalte **Korrigieren in** eingeben und dann auf das Optionsfeld in der Spalte **Genehmigen** klicken, um die Änderung anzunehmen. In diesem Fall wird der Wert auf die Registerkarte **Korrigiert** verschoben.|  
|**Korrigiert**|Zeigt die Domänenwerte an, die von DQS während des automatisierten Bereinigungsprozesses korrigiert wurden, da für den Wert eine Korrektur mit einem Vertrauensgrad oberhalb des Schwellenwerts für die automatische Korrektur gefunden wurde.<br /><br /> Die korrigierten Werte werden in der Spalte **Korrigieren in** im Vergleich zum ursprünglichen Wert angezeigt. Standardmäßig ist das Optionsfeld in der Spalte **Genehmigen** für den Wert aktiviert. Wenn erforderlich, können Sie die vorgeschlagene Korrektur ablehnen, indem Sie in der Spalte **Ablehnen** auf das Optionsfeld klicken, um den Wert auf die Registerkarte **Ungültig** zu verschieben, oder Sie geben den richtigen Wert in die Spalte **Korrigieren in** ein und klicken dann auf das Optionsfeld in der Spalte **Genehmigen** , um die Änderung anzunehmen und auf die Registerkarte **Korrigiert** zu verschieben.|  
|**Richtig**|Zeigt die Domänenwerte an, die als richtig gefunden wurden. Beispielsweise stimmt der Wert mit dem Domänenwert überein. Diese Registerkarte enthält auch Werte, die vom Benutzer durch Klicken auf das Optionsfeld in der Spalte **Genehmigen** auf den Registerkarten **Neu** und **Ungültig** genehmigt wurden.<br /><br /> Standardmäßig ist das Optionsfeld in der Spalte **Genehmigen** für den Wert aktiviert. Wenn Sie aber glauben, dass ein Wert auf dieser Registerkarte falsch ist, können Sie entweder in der Spalte **Ablehnen** auf das Optionsfeld für den Wert klicken, um ihn auf die Registerkarte **Ungültig** zu verschieben, oder Sie geben den richtigen Wert manuell als Ersatz für den Wert in der Spalte **Korrigieren in** ein und klicken dann auf das Optionsfeld in der Spalte **Genehmigen** , um die Änderung anzunehmen und auf die Registerkarte **Korrigiert** zu verschieben.|  
  
 Zu bereinigen Sie die Daten interaktiv:  
  
1.  Klicken Sie auf der Seite **Ergebnisse verwalten und anzeigen** des Data Quality-Bereinigungs-Assistenten im linken Bereich auf einen Domänennamen.  
  
2.  Überprüfen Sie die Domänenwerte auf den fünf Registerkarten, und ergreifen Sie die entsprechende Aktion, wie zuvor erklärt.  
  
    -   Im Bereich rechts oben werden die folgenden Informationen für jeden Wert in der ausgewählten Domäne angezeigt: ursprünglicher Wert, Anzahl von Instanzen (Datensätze), ein Feld, um einen anderen (richtigen) Wert anzugeben, den Vertrauensgrad (nicht verfügbar für die Werte auf der Registerkarte **Richtig** ), der Grund für die DQS-Aktion für den Wert und die Option, um die Korrekturen und Vorschläge für den Wert zu genehmigen und abzulehnen.  
  
        > [!TIP]  
        >  Sie können alle Werte in der ausgewählten Domäne im rechten oberen Bereich durch Klicken auf das Symbol **Alle Begriffe genehmigen** oder **Alle Begriffe ablehnen** genehmigen oder ablehnen. Sie können auch mit der rechten Maustaste auf einen Wert in der ausgewählten Domäne klicken und dann im Kontextmenü auf **Alle annehmen** oder **Alle ablehnen** klicken.  
  
    -   Im unteren Bereich werden einzelne Vorkommen des Domänenwerts angezeigt, der im Bereich rechts oben ausgewählt wurde. Die folgenden Informationen werden angezeigt: ein Feld, um einen anderen (richtigen) Wert anzugeben, den Vertrauensgrad (nicht verfügbar für die Werte auf der Registerkarte **Richtig** ), der Grund für die DQS-Aktion für den Wert und die Option, um die Korrekturen und Vorschläge für den Wert zu genehmigen und abzulehnen, und der ursprüngliche Wert.  
  
3.  Wenn Sie beim Erstellen einer Domäne die Funktion **Rechtschreibprüfung** aktiviert haben, werden wellige rote Unterstriche für solche Domänenwerte angezeigt, die als potenzielle Fehler identifiziert werden. Der Unterstrich wird für den ganzen Wert angezeigt. Wenn „New York“ z. B. falsch als „Neu York“ buchstabiert wurde, zeigt die Rechtschreibprüfung einen roten Unterstrich unter „Neu York“ und nicht nur unter „Neu“ an. Wenn Sie mit der rechten Maustaste auf den Wert klicken, sehen Sie vorgeschlagene Korrekturen. Wenn es mehr als 5 Vorschläge gibt, können Sie im Kontextmenü auf **Weitere Vorschläge** klicken, um die restlichen Vorschläge anzuzeigen. Wie bei der Fehleranzeige ersetzen die Vorschläge den ganzen Wert. „New York“ wird so im vorherigen Beispiel als Vorschlag angezeigt, nicht nur „Neu“. Sie können einen der Vorschläge auswählen oder dem Wörterbuch einen Wert hinzufügen, der für diesen Wert angezeigt werden soll. Werte werden im Wörterbuch auf Benutzerkontoebene gespeichert. Wenn Sie einen Vorschlag im Kontextmenü der Rechtschreibprüfung auswählen, wird der Spalte **Korrigieren in** der ausgewählte Vorschlag hinzugefügt. Wenn Sie jedoch in der Spalte **Korrigieren in** einen Vorschlag auswählen, wird der Wert in der Spalte durch den ausgewählten Vorschlag ersetzt.  
  
     Die Rechtschreibprüfungsfunktion ist standardmäßig in der interaktiven Bereinigungsphase aktiviert. Sie können die Rechtschreibprüfung in der interaktiven Bereinigungsphase deaktivieren, indem Sie auf das Symbol **Rechtschreibprüfung aktivieren/deaktivieren** klicken oder mit der rechten Maustaste in den Domänenwertebereich klicken und dann im Kontextmenü auf **Rechtschreibprüfung** klicken. Um sie wieder zu aktivieren, gehen Sie genau so vor.  
  
    > [!NOTE]  
    >  Die Rechtschreibprüfungsfunktion ist nur im oberen Bereich (Domänenwerte) verfügbar. Darüber hinaus können Sie die Rechtschreibprüfung nicht für Verbunddomänen aktivieren oder deaktivieren. Für die untergeordneten Domänen in einer Verbunddomäne, die von einem Zeichenfolgentyp sind und für die die Rechtschreibprüfungsfunktion aktiviert wurde, ist die Rechtschreibprüfungsfunktion in der interaktiven Bereinigungsphase standardmäßig aktiviert.  
  
4.  Während der interaktiven Bereinigungsphase können Sie den Profiler einschalten, indem Sie auf die Registerkarte **Profiler** klicken, um Echtzeitdaten zur Profilerstellung und zu Benachrichtigungen anzuzeigen. Weitere Informationen finden Sie unter [Profiler-Statistik](#Profiler).  
  
5.  Nachdem Sie alle Domänenwerte überprüft haben, klicken Sie auf **Weiter** , um zur Exportphase zu gelangen.  
  
##  <a name="Export"></a> Exportphase  
 In der Exportphase geben Sie die Parameter zum Exportieren der bereinigten Daten an: was wohin exportiert werden soll.  
  
1.  Wählen Sie auf der Seite **Exportieren** des Data Quality-Bereinigungs-Assistenten den Zieltyp für das Exportieren der bereinigten Daten aus: **SQL Server**, **CSV-Datei**oder **Excel-Datei**.  
  
    > [!IMPORTANT]  
    >  Wenn Sie die 64-Bit-Version von Excel verwenden, können Sie die bereinigten Daten nicht in eine Excel-Datei exportieren; Sie können sie nur in eine SQL Server-Datenbank oder eine CSV-Datei exportieren.  
  
    1.  **SQL Server**Wählen Sie **DQS_STAGING_DATA** als Zieldatenbank aus, wenn Sie die Daten hierher exportieren möchten, und geben Sie dann einen Namen für die Tabelle an, die erstellt wird, um die exportierten Daten zu speichern. Wählen Sie andernfalls eine andere Datenbank aus, wenn Sie Daten in eine andere Datenbank exportieren möchten, und geben Sie dann einen Namen für die Tabellen an, die erstellt wird, um die exportierten Daten zu speichern. Die Zieldatenbank muss sich in der gleichen SQL Server-Instanz wie [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] befinden, um in der Dropdownliste **Datenbank** verfügbar zu sein.  
  
    2.  **CSV-Datei**: Klicken Sie auf **Durchsuchen**, und geben Sie den Namen und den Speicherort der CSV-Datei an, in die Sie die bereinigten Daten exportieren möchten. Sie können auch den Dateinamen für die CSV-Datei, in die Sie die bereinigten Daten exportieren möchten, zusammen mit dem vollständigen Pfad eingeben. Zum Beispiel „c:\ExportedData.csv“. Die Datei wird auf dem Computer gespeichert, auf dem [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] installiert ist.  
  
    3.  **Excel-Datei**: Klicken Sie auf **Durchsuchen**, und geben Sie den Namen und den Speicherort der Excel-Datei an, in die Sie die bereinigten Daten exportieren möchten. Sie können auch den Dateinamen für die Excel-Datei, in die Sie die bereinigten Daten exportieren möchten, zusammen mit dem vollständigen Pfad eingeben. Zum Beispiel „c:\ExportedData.xlsx“. Die Datei wird auf dem Computer gespeichert, auf dem [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] installiert ist.  
  
2.  Aktivieren Sie das Kontrollkästchen **Ausgabe standardisieren** , um die Ausgabe auf Grundlage des für die Domäne ausgewählten Ausgabeformats zu standardisieren. Ändern Sie z. B. den Zeichenfolgenwert in Großbuchstaben, oder schreiben Sie den ersten Buchstaben des Worts groß. Informationen zum Angeben des Ausgabeformats einer Domäne finden Sie in der Liste **Formatausgabe** in [Domäne-Eigenschaften festlegen](../data-quality-services/set-domain-properties.md).  
  
3.  Wählen Sie danach die Datenausgabe aus: Exportieren Sie nur die bereinigten Daten, oder exportieren Sie die bereinigten Daten zusammen mit den Bereinigungsinformationen.  
  
    -   **Nur Daten**: Klicken Sie auf das Optionsfeld, um nur die bereinigten Daten zu exportieren.  
  
    -   **Informationen zu Daten und Bereinigung**: Klicken Sie auf das Optionsfeld, um die folgenden Daten für jede Domäne zu exportieren:  
  
        -   **\<Domäne>_Quelle**: Der ursprüngliche Wert in der Domäne.  
  
        -   **\<Domäne>_Ausgabe**: Die bereinigten Werte in der Domäne.  
  
        -   **\<Domäne>_Ursache**: Die für die Korrektur des Werts angegebene Ursache.  
  
        -   **\<Domäne>_Vertrauen**: Der Vertrauensgrad für alle korrigierten Begriffe. Der angezeigte Wert ist ein Dezimalwert, der dem Prozentwert entspricht. Ein Vertrauensgrad von 95 % wird z. B. als .9500000 angezeigt.  
  
        -   **\<Domäne>_Status**: Der Status des Domänenwerts nach der Datenbereinigung. Beispiele sind **Vorgeschlagen**, **Neu**, **Ungültig**, **Korrigiert**oder **Richtig**.  
  
        -   **Datensatzstatus**: Abgesehen von einem Statusfeld für jede zugeordnete Domäne **(\<Domänenname>_Status**) wird im Feld **Datensatzstatus** der Status eines Datensatzes angezeigt. Wenn einer der Statuswerte der Domäne im Datensatz *Neu* oder *Korrigiert*lautet, wird der **Datensatzstatus** auf *Richtig*festgelegt. Wenn einer der Statuswerte der Domäne im Datensatz *Vorgeschlagen*, *Ungültig*oder *Korrigiert*lautet, wird **Datensatzstatus** auf den entsprechenden Wert festgelegt. Wenn beispielsweise einer der Statuswerte der Domäne im Datensatz *Vorgeschlagen*lautet, wird **Datensatzstatus** auf *Vorgeschlagen*festgelegt.  
  
            > [!NOTE]  
            >  Wenn Sie den Verweisdatendienst für den Bereinigungsvorgang verwenden, stehen auch zusätzliche Daten zum Domänenwert für das Exportieren zur Verfügung. Weitere Informationen finden Sie unter [Bereinigen von Daten mit &#40;externem&#41; Verweisdaten-Wissen](../data-quality-services/cleanse-data-using-reference-data-external-knowledge.md).  
  
4.  Klicken Sie auf **Exportieren** , um die Daten in das ausgewählte Ziel zu exportieren. Optionen:  
  
    -   Wenn Sie**SQL Server** als Datenziel ausgewählt haben, wird eine neue Tabelle mit dem angegebenen Namen in der ausgewählten Datenbank erstellt.  
  
    -   Wenn Sie**CSV-Datei** als Datenziel ausgewählt haben, wird eine CSV-Datei in dem Ordner auf dem [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] -Computer mit dem Dateinamen erstellt, den Sie zuvor im Namensfeld **CSV-Datei** angegeben haben.  
  
    -   Wenn Sie**Excel-Datei** als Datenziel ausgewählt haben, wird eine Excel-Datei in dem Ordner auf dem [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] -Computer mit dem Dateinamen erstellt, den Sie zuvor im Namensfeld **Excel-Datei** angegeben haben.  
  
5.  Klicken Sie auf **Fertig stellen** , um das Data Quality-Projekt zu schließen.  
  
##  <a name="Profiler"></a> Profiler Statistics  
 Die Registerkarte **Profiler** stellt Statistiken bereit, die die Qualität der Quelldaten angeben. Mithilfe der Profilerstellung können Sie die Effektivität der Datenbereinigungsaktivität bewerten und potenziell bestimmen, inwiefern die Datenbereinigung die Qualität der Daten verbessern konnte.  
  
 Die Registerkarte **Profiler** stellt die folgenden Statistiken für die Quelldaten, nach Feld und Domäne geordnet, bereit:  
  
-   **Datensätze**: Wie viele Datensätze im Datenbeispiel wurden für die Datenbereinigungsaktivität analysiert?  
  
-   **Richtige Datensätze**: Wie viele Datensätze wurden als richtig gefunden?  
  
-   **Korrigierte Datensätze**: Wie viele Datensätze wurden korrigiert?  
  
-   **Vorgeschlagene Datensätze**: Wie viele Datensätze wurden vorgeschlagen?  
  
-   **Ungültige Datensätze**: Wie viele Datensätze waren ungültig?  
  
 Die Feldstatistiken umfassen Folgendes:  
  
-   **Feld**: Name des Felds in den Quelldaten  
  
-   **Domäne**: Name der Domäne, die dem Feld zugeordnet ist  
  
-   **Korrigierte Werte**: Die Anzahl der Domänenwerte, die korrigiert wurden  
  
-   **Vorgeschlagene Werte**: Die Anzahl der Domänenwerte, die vorgeschlagen wurden  
  
-   **Vollständigkeit**: Die Vollständigkeit jedes Quellfelds, das für die Bereinigungsaktivität zugeordnet ist  
  
-   **Genauigkeit**: Die Genauigkeit jedes Quellfelds, das für die Bereinigungsaktivität zugeordnet ist  
  
 DQS-Profilerstellung stellt zwei Data Quality-Dimensionen bereit: *Vollständigkeit* (das Ausmaß des Vorhandenseins von Daten) und *Genauigkeit* (das Ausmaß, in dem Daten für den beabsichtigten Zweck verwendet werden können). Wenn die Profilerstellung Ihnen sagt, dass ein Feld relativ unvollständig ist, sollten Sie es aus der Wissensdatenbank eines Data Quality-Projekts entfernen. Die Profilerstellung kann keine zuverlässigen Vollständigkeitsstatistiken für Verbunddomänen bereitstellen. Wenn Sie Vollständigkeitsstatistiken benötigen, verwenden Sie Einzeldomänen anstatt Verbunddomänen. Wenn Sie Verbunddomänen verwenden möchten, sollten Sie eine Wissensdatenbank mit Einzeldomänen für die Profilerstellung erstellen, um die Vollständigkeit zu bestimmen, und eine weitere Domäne mit einer Verbunddomäne für den Bereinigungsprozess erstellen. Die Profilerstellung kann z. B. 95 % Vollständigkeit für Adressendatensätze anzeigen, die eine Verbunddomäne verwenden, aber es kann einen viel höheren Grad der Unvollständigkeit für eine der Spalten geben, z. B. für eine Postleitzahlspalte. In diesem Beispiel möchten Sie die Vollständigkeit der Postleitzahlspalte mit einer Einzeldomäne messen. Die Profilerstellung stellt wahrscheinlich zuverlässige Genauigkeitsstatistiken für Verbunddomänen bereit, da Sie die Genauigkeit für mehrere Spalten gemeinsam messen können. Der Wert dieser Daten liegt in der zusammengesetzten Aggregation, daher sollten Sie die Genauigkeit mit einer Verbunddomäne messen.  
  
 Genauigkeitsstatistiken erfordern wahrscheinlich mehr Interpretation, wenn Sie keinen Verweisdatendienst verwenden. Wenn Sie einen Verweisdatendienst für die Datenbereinigung verwenden, haben Sie eine Vertrauensebene in den Genauigkeitsstatistiken. Weitere Informationen zur Datenbereinigung mithilfe von Reference Data Service finden Sie unter [Bereinigen von Daten mit &#40;externem&#41; Verweisdaten-Wissen](../data-quality-services/cleanse-data-using-reference-data-external-knowledge.md).  
  
### <a name="cleansing-notifications"></a>Bereinigungsbenachrichtigungen  
 Die folgenden Bedingungen führen zu Benachrichtigungen:  
  
-   Es gibt keine Korrekturen oder Vorschläge für ein Feld. Sie sollten das Feld aus der Zuordnung entfernen und zuerst die Wissensermittlung ausführen oder eine andere Wissensdatenbank verwenden.  
  
-   Es gibt relativ wenige Korrekturen oder Vorschläge für ein Feld. Sie sollten das Feld aus der Zuordnung entfernen und zuerst die Wissensermittlung ausführen oder eine andere Wissensdatenbank verwenden.  
  
-   Die Genauigkeitsstufe des Felds ist sehr niedrig. Sie sollten die Zuordnung überprüfen, oder erwägen, die Wissensermittlung zuerst auszuführen.  
  
 Weitere Informationen zur Profilerstellung finden Sie unter [Datenprofilerstellung und Benachrichtigungen in DQS](../data-quality-services/data-profiling-and-notifications-in-dqs.md).  
  
  

