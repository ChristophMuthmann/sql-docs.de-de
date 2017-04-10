---
title: "&#220;berwachen der DQS-Aktivit&#228;ten | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "data-quality-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dqs.administration.activitymonitoring.f1"
helpviewer_keywords: 
  - "monitoring activity"
  - "Aktivitätsüberwachung"
ms.assetid: 1d4c76f3-0d7b-498e-b792-4db4a0349814
caps.latest.revision: 16
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 16
---
# &#220;berwachen der DQS-Aktivit&#228;ten
  In diesem Thema wird beschrieben, wie die folgenden Aktivitäten in [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) zentral überwacht werden: Wissensermittlung, Domänenverwaltung, Abgleichsrichtlinie, Datenbereinigung, Datenabgleich und SSIS-Bereinigung.  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="LimitationsRestrictions"></a> Einschränkungen  
 Nur Benutzer mit der dqs_administrator-Rolle in der Datenbank DQS_Main können eine Aktivität oder einen Prozess innerhalb einer Aktivität beenden.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
  
-   Sie müssen über die dqs_kb_editor- oder dqs_kb_operator-Rolle in der Datenbank DQS_MAIN verfügen, um die DQS-Aktivitäten anzuzeigen.  
  
-   Sie müssen über die dqs_administrator-Rolle in der Datenbank DQS_MAIN verfügen, um die DQS-Aktivitäten anzuzeigen und außerdem eine Aktivität oder einen Prozess innerhalb einer Aktivität zu beenden.  
  
##  <a name="View"></a> Anzeigen von DQS-Aktivitäten  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Ausführen der Data Quality-Clientanwendung](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Klicken Sie auf dem [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] -Startbildschirm auf **Aktivitätsüberwachung**. Der Bildschirm Aktivitätsüberwachung wird geöffnet.  
  
     ![Bildschirm "Aktivitätsüberwachung"](../data-quality-services/media/dqs-activitymonitoring.gif "Bildschirm "Aktivitätsüberwachung"")  
  
3.  Auf dem Bildschirm Aktivitätsüberwachung werden Informationen zu jeder Aktivität in einem Aktivitätsraster angezeigt. Das Aktivitätsraster zeigt die folgenden Informationen zu jeder DQS-Aktivität an:  
  
     **ID**: einen ganzzahligen Wert. Eindeutige Aktivitätsnummer, die das System für die Aktivitätsüberwachung generiert.  
  
     **Namen**: der Name des Knowledge Base oder Data Quality-Projekts, die für diese Aktivität verwendet wird.  
  
     **Ist Active**: Gibt an, ob die Aktivität derzeit aktiv ist. Die folgenden Werte sind möglich:  
  
    -   **Aktiv**: Aktivität wird gerade ausgeführt.  
  
    -   **Abgeschlossen**: Die Aktivität wurde beendet.  
  
    -   **Beendet**: Die Aktivität wurde vom DQS-Administrator im Bildschirm Aktivitätsüberwachung beendet oder während der Ausführung im entsprechenden Funktionsbereich in [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]vom Benutzer abgebrochen.  
  
     **Typ**: Gibt den Typ der Aktivität an. **Der Untertyp** Gibt den jeweiligen Workflow, der für einen Aktivitätstyp ausgeführt wird. Die folgenden Aktivitätstypen werden überwacht:  
  
    -   **Knowledge Management** Untertypen:  
  
        -   **Wissensermittlung**  
  
        -   **Domänenverwaltung**  
  
        -   **Übereinstimmende Richtlinie**  
  
    -   **DQ-Projekt** Untertypen:  
  
        -   **Bereinigung**  
  
        -   **Abgleich**  
  
    -   **SSIS-Bereinigung** Untertypen:  
  
        -   **Bereinigung**  
  
     **Aktueller Status**: Zeigt den aktuellen Status einer Aktivität. Der Aktivitätsstatus wird durch den zuletzt durchgeführten Berechnungsprozess bestimmt. So wie der Ermittlungsprozess (im Rahmen der Wissensermittlungsaktivität) kann auch der Berechnungsprozess für eine Aktivität mehrmals ausgeführt werden. Aus diesem Grund kann sich der Status während der Lebensdauer einer Aktivität mehrere Male ändern.  
  
     **Aktueller Status** können die folgenden Werte aufweisen:  
  
    -   **Wird ausgeführt**: Der Berechnungsprozess wird ausgeführt.  
  
    -   **Erfolgreich**: dieser Status wird festgelegt, bevor ein Berechnungsprozess ausgeführt wurde und erneut nach einem rechnerischen erfolgreich verarbeiten endet.  
  
    -   **Fehler**: Im Berechnungsprozess ist ein Fehler aufgetreten.  
  
    -   **Beendet**: Der Berechnungsprozess wurde beendet.  
  
     **DQKB**: Name der Wissensdatenbank, die für die Aktivität verwendet wird.  
  
     **Benutzer**: der Name des Benutzers, der die Aktivität initiiert hat, oder der letzte Benutzer, der die Aktivität bearbeitet (falls sie nicht identisch sind).  
  
     **Startzeit der Aktivität**: Datum und Uhrzeit, wann die Aktivität gestartet wurde,  
  
     **Verstrichene Zeit**: die verstrichene Zeit seit dem Start der Aktivitäts. Dies wird in der Schreibweise HH:MM:SS angezeigt.  
  
     **Endzeit der Aktivität**: Datum und Uhrzeit, wann die Aktivität beendet wurde.  
  
##  <a name="Filter"></a> Filtern von DQS-Aktivitätsinformationen  
 Können Sie im Filterbereich (**Filtern nach**, **Wert**, **von Datum**, und **auf dem neuesten Stand**) in der BAM-Bildschirm filtern und die erforderlichen Aktivitäten, die basierend auf bestimmten Kriterien anzeigen. So filtern Sie Aktivitätsdatensätze:  
  
1.  Legen Sie das Filterkriterium fest: Sie können die Aktivitätsdatensätze basierend auf einem Wert in einer der Spalten im Aktivitätsraster (wertbasiert) und/oder basierend auf einem Datumsbereich filtern.  
  
    1.  **Filterung**: Wählen Sie ein Filterkriterium in der **Filtern nach** aus, und wählen Sie dann den entsprechenden Wert zum Filtern von in der **Wert** Liste. Wenn Sie in der Liste **Filtern nach** eine Option ausgewählt haben, wird die Liste **Wert** mit den möglichen Werten aktualisiert. Sie können in den Aktivitätsdatensätzen nach den folgenden Feldern filtern: **Ist aktiv**, **Typ**, **Untertyp**, **Aktueller Status**und **DQKB**und **Benutzer**.  
  
    2.  **Startdatum bereichsbasierte**: Auswählen der entsprechende Daten in der **von Datum** und **auf dem neuesten Stand** auswählen. Standardmäßig liegt das im Feld **Ab Datum** angezeigte Datum zwei Tage vor dem aktuellen Datum, und in **Bis Datum** ist das aktuelle Datum angegeben. Die Filterung erfolgt nicht basierend auf den *Ab* - und *Bis* -Daten, sondern basierend auf dem Datumsbereich. Dies bedeutet, dass jede Aktivität, die während des ausgewählten Datumsbereichs ausgeführt wurde, angezeigt wird.  
  
2.  Klicken Sie auf das Symbol **Aktivitätsliste aktualisieren** , um den Filter anzuwenden, und zeigen Sie nur die gefilterten DQS-Aktivitäten an.  
  
##  <a name="ActivityDetails"></a> Anzeigen von DQS-Aktivitätsdetails  
 Sie können ausführliche Informationen zu einer DQS-Aktivität, z. B. Aktivitätsschritte und Profiler-Informationen im Bildschirm Aktivitätsüberwachung anzeigen. Gehen Sie folgendermaßen vor:  
  
1.  Wählen Sie eine DQS-Aktivität im Aktivitätsraster (im oberen Bereich) aus.  
  
2.  Im unteren Bereich werden die Aktivitätsdetails der ausgewählten Aktivität auf den beiden folgenden Registerkarten angezeigt:  
  
    -   **Aktivitätsschritte**: Zeigt ein Raster mit den berechnungsprozessen (aktivitätsschritten), die der ausgewählten Aktivität zugeordnet sind. Auf dieser Registerkarte können mehrere Aktivitätsschritte für eine Aktivität angezeigt werden. Dies ist dann der Fall, wenn der gleiche Aktivitätsschritt innerhalb der Aktivität mehrere Male vom Benutzer ausgeführt wurde. Beispielsweise kann der Aktivitätsschritt beendet und wieder gestartet worden sein. Das Raster auf dieser Registerkarte zeigt die folgenden Informationen für jeden Aktivitätsschritt an, der dieser Aktivität zugeordnet ist: **Typ**, **Aktueller Status**, **Startzeit**, **Verstrichene Zeit**und **Beendigungszeit**.  
  
    -   **Profiler**: Zeigt die Informationen für die Profilerstellung für aktuelle und vergangene Aktivitäten an. Für aktuelle Aktivitäten werden die Informationen teilweise, jedoch konsistent, angezeigt. Die Profilerstellungsdaten einer Aktivität werden in eine Excel-Datei exportiert, wenn Sie die entsprechenden Aktivitätsdetails in eine Excel-Datei exportieren. Die Informationen sind in der exportierten Excel-Datei in den Arbeitsblättern **Profiler – Quelle** und **Profiler – Felder** verfügbar.  
  
##  <a name="Export"></a> Exportieren von DQS-Aktivitätsdetails  
 Sie können die Aktivitätseigenschaften, Aktivitätsprozesse und Profilerstellungsdaten einer Aktivität im Überwachungsbildschirm in eine Excel-Datei exportieren. Gehen Sie folgendermaßen vor:  
  
1.  Wählen Sie eine Aktivität im Aktivitätsraster (im oberen Bereich) aus.  
  
2.  Klicken Sie auf das Symbol **Ausgewählte Aktivität nach Excel exportieren** . Alternativ mit der rechten Maustaste auf eine Aktivität im aktivitätsraster, und klicken Sie dann auf **Aktivität exportieren** im Kontextmenü.  
  
3.  Sie werden aufgefordert, einen Namen und einen Speicherort für die zu speichernde Excel-Datei anzugeben. Die exportierte Excel-Datei enthält folgende Arbeitsblätter:  
  
    |Blattname|Beschreibung|  
    |----------------|-----------------|  
    |Aktivität|Enthält Informationen (Spalten) zur Aktivität wie das Aktivitätsraster.|  
    |Prozesse|Enthält Informationen (Spalten) über die Prozesse in der Aktivität wie die **Aktivitätsschritte** Registerkarte.|  
    |Profiler – Quelle|Für den Untertyp **Bereinigung** sind die folgenden Informationen zur Aktivität enthalten: Datensätze, Richtige Datensätze, Korrigierte Datensätze und Ungültige Datensätze.<br /><br /> Für die Untertypen **Wissensermittlung**, **Domänenverwaltung**, **Abgleichsrichtlinie**und **Abgleich** sind die folgenden Informationen zur Aktivität enthalten: Datensätze, Gesamtwerte, Neue Werte, Eindeutige Werte und Neue eindeutige Werte.|  
    |Profiler – Felder|Für die Untertypen **Bereinigung** und **SSIS-Bereinigung** sind die folgenden Informationen zur Aktivität enthalten: Feld, Domäne, Korrigierte Werte, Vorgeschlagene Werte, Vollständigkeit und Genauigkeit.<br /><br /> Für die Untertypen **Wissensermittlung**, **Domänenverwaltung**, **Abgleichsrichtlinie**und **Abgleich** sind die folgenden Informationen zur Aktivität enthalten: Feld, Domäne, Neu, Eindeutig, In Domäne gültig und Vollständigkeit.|  
  
##  <a name="Terminate"></a> Beenden einer DQS-Aktivität  
 DQS-Administratoren (Dqs_administrator-Rolle) können beendet eine ausgeführte (aktive) Aktivität, die nicht vom Typ **SSIS-Bereinigung**. Wenn eine Aktivität beendet wird, werden alle ausgeführten Prozesse in der Aktivität beendet und alle mit der Aktivität verbundenen Elemente entfernt. Dieser Vorgang kann nicht rückgängig gemacht werden. Das Beenden einer Aktivität im Bildschirm Aktivitätsüberwachung ist damit vergleichbar, die entsprechende Aktivität abzubrechen, indem Sie auf **Abbrechen** klicken, während die Aktivität im Funktionsbereich in [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]ausgeführt wird. So beenden Sie eine Aktivität:  
  
1.  Wählen Sie eine Aktivität, die ausgeführt wird, im Aktivitätsraster (im oberen Bereich) aus.  
  
2.  Klicken Sie auf das Symbol **Ausgewählte Aktivität beenden** . Alternativ mit der rechten Maustaste auf die Aktivität im aktivitätsraster, und klicken Sie dann auf **Aktivität beenden** im Kontextmenü.  
  
3.  Eine Meldung wird angezeigt, um die Aktion zu bestätigen. Klicken Sie auf **Ja**.  
  
##  <a name="Stop"></a> Beenden eines Prozesses in einer DQS-Aktivität  
 DQS-Administratoren (Dqs_administrator-Rolle) können einen Prozess ausgeführten (aktiven) in einer Aktivität, die nicht vom Typ beenden **SSIS-Bereinigung**. Das Beenden eines Prozesses im Bildschirm Aktivitätsüberwachung ist damit vergleichbar, den Prozess innerhalb der entsprechenden Aktivität im Funktionsbereich in [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]zu beenden. Beispiele: das Beenden des computergestützten Bereinigungsprozesses innerhalb einer Bereinigungsaktivität oder das Beenden des Abgleichsprozesses innerhalb einer Abgleichsaktivität. Ein beendeter Prozess kann nicht im Bildschirm Aktivitätsüberwachung neu gestartet werden. Sie müssen den Prozess im entsprechenden Funktionsbereich im [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]neu starten. In dem Fall wird auf der Registerkarte **Aktivitätsschritte** eine zusätzliche Zeile zum Prozessraster hinzugefügt. Der Status des beendeten Prozesses wird weiterhin als **Beendet**angezeigt. So beenden Sie einen Prozess:  
  
1.  Wählen Sie einen Prozess, der ausgeführt wird, im Raster Aktivitätsdetails (im unteren Bereich) aus.  
  
2.  Klicken Sie auf das Symbol **Ausgewählten Prozess beenden** . Alternativ mit der rechten Maustaste auf den Prozess im Raster Details Aktivität, und klicken Sie dann auf **Prozess beenden** im Kontextmenü.  
  
3.  Eine Meldung wird angezeigt, um die Aktion zu bestätigen. Klicken Sie auf **Ja**.  
  
  