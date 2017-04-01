---
title: "Ausf&#252;hren eines Abgleichsprojekts | Microsoft Docs"
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
  - "sql13.dqs.matchingproject.map.f1"
  - "sql13.dqs.matchingproject.matching.f1"
  - "sql13.dqs.matchingproject.export.f1"
ms.assetid: 6aa9d199-83ce-4b5d-8497-71eef9258745
caps.latest.revision: 36
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 36
---
# Ausf&#252;hren eines Abgleichsprojekts
  In diesem Thema wird beschrieben, wie ein Datenabgleich in [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) ausgeführt wird. Der Abgleichsprozess identifiziert anhand von Abgleichsregeln in der Abgleichsrichtlinie Cluster von übereinstimmenden Datensätzen, legt basierend auf einer Survivorship-Regel einen Datensatz von jedem Cluster als Survivor fest und exportiert die Ergebnisse. DQS führt den Abgleichsprozess, auch Deduplizierung genannt, in einem computerunterstützten Prozess aus, Sie erstellen die Abgleichsregeln jedoch interaktiv und wählen die Survivorship-Regel aus mehreren Optionen aus, so dass Sie den Abgleichsprozess selbst steuern können.  
  
 Der Abgleich erfolgt in drei Phasen: ein Zuordnungsprozess, in dem Sie die Datenquelle identifizieren und der Datenquelle Domänen zuordnen, ein Abgleichsprozess, in dem Sie die Abgleichsanalyse ausführen, und ein Survivorship- sowie Exportprozess, in denen Sie die Survivorship-Regel festlegen und die Abgleichsergebnisse exportieren. Jede dieser Prozesse wird auf einer separaten Seite des Abgleichsaktivitäts-Assistenten ausgeführt, sodass Sie zwischen den Seiten hin und her wechseln, den Prozess erneut auszuführen, einen bestimmten Abgleichsprozess schließen und dann zur gleichen Phase des Prozesses zurückkehren können. DQS stellt Ihnen Statistiken zu den Quelldaten, den Abgleichsregeln und den Abgleichsergebnissen bereit, die es Ihnen ermöglichen, informierte Entscheidungen zum Abgleich zu treffen und den Abgleichsprozess zu optimieren.  
  
 Sie müssen den Abgleich vorbereiten, indem Sie eine Abgleichsrichtlinie mit einer oder mehreren Abgleichsregeln erstellen und die Richtlinie für Beispieldaten ausführen. Der Abgleichsprojektprozess erfolgt getrennt vom Abgleichsrichtlinienprozess. Es wird keine Wissensdatenbank mit dem beim Abgleichsprojekt gewonnenen Abgleichswissen gefüllt. Weitere Informationen zum Erstellen von Abgleichsrichtlinie finden Sie unter [Create a Matching Policy](../data-quality-services/create-a-matching-policy.md).  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Prerequisites"></a> Erforderliche Komponenten  
  
-   Sie müssen eine Wissensdatenbank mit einer Abgleichsrichtlinie erstellt haben, die aus einer oder mehreren Abgleichsregeln besteht.  
  
-   Microsoft Excel muss auf dem [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] -Computer installiert sein, wenn sich die Quelldaten, die abgeglichen werden sollen, in einer Excel-Datei befinden. Andernfalls sind Sie nicht in der Lage, die Excel-Datei in der Zuordnungsphase auszuwählen. Die von Microsoft Excel erstellten Dateien können die Erweiterung .xlsx, .xls oder .csv haben. Wenn die 64-Bit-Version von Excel verwendet wird, werden nur Excel 2003-Dateien (.xls) unterstützt; Excel 2007- oder 2010-Dateien (.xlsx) werden nicht unterstützt. Wenn Sie die 64-Bit-Version von Excel 2007 oder 2010 verwenden, speichern Sie die Datei als XLS-Datei oder CSV-Datei, oder installieren Sie stattdessen eine 32-Bit-Version von Excel.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Sie müssen über die Rolle „dqs_kb_editor“ oder „dqs_administrator“ in der DQS_MAIN-Datenbank verfügen, um ein Abgleichsprojekt auszuführen.  
  
##  <a name="StartingaMatchingProject"></a> Erster Schritt: Starten eines Abgleichsprojekts  
 Sie führen die Abgleichsaktivität in einem Data Quality-Projekt aus, das Sie in der DQS-Clientanwendung erstellen.  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Ausführen der Data Quality-Clientanwendung](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Klicken Sie im Startbildschirm von [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] auf **Neues Data Quality-Projekt** , um den Abgleich in einem neuen Data Quality-Projekt auszuführen. Geben Sie unter einen Namen für das Data Quality-Projekt und eine Beschreibung ein, und wählen Sie unter **Wissensdatenbank verwenden**die Wissensdatenbank für den Abgleich aus. Klicken Sie für die Aktivität auf **Abgleich** . Klicken Sie auf **Weiter** , um zur Zuordnungsphase zu wechseln.  
  
3.  Klicken Sie auf **Data Quality-Projekt öffnen** , um einen Abgleich in einem vorhandenen Data Quality-Projekt auszuführen. Wählen Sie das Projekt aus, und klicken Sie dann auf **Weiter**. (Alternativ können Sie ein Projekt unter auf **Zuletzt verwendetes Data Quality-Projekt**.) Wenn Sie ein abgleichsprojekt, die geschlossen wurde öffnen, fahren Sie fort mit der Phase, die die abgleichsprojektaktivität geschlossen wurde (wie durch die **Zustand** Spalte in der Tabelle oder im Projektnamen unter **zuletzt verwendetes Data Quality-Projekt**). Wenn Sie ein abgleichsprojekt, das abgeschlossen wurde öffnen, gelangen Sie auf die **exportieren** Seite (und Sie nicht zu einem vorherigen Bildschirm zurück gehen).  
  
##  <a name="MappingStage"></a> Zuordnungsphase  
 In der Zuordnungsphase identifizieren Sie die Quelle der Daten, für die Sie die Abgleichsanalyse ausführen, und Sie ordnen Domänen Quellspalten zu, um die Domänen für die Abgleichsaktivität verfügbar zu machen.  
  
1.  Um den Abgleich für eine Datenbank auszuführen, übernehmen Sie auf der Seite **Zuordnen** für **Datenquelle** die Einstellung **SQL Server**, wählen Sie die Datenbank aus, für die Sie den Abgleich ausführen möchten, und wählen Sie dann die Tabelle aus. Die Quelldatenbank muss sich in der gleichen SQL Server-Instanz wie der DQS-Server befinden. Andernfalls wird sie nicht in der Dropdownliste angezeigt.  
  
2.  Um einen Abgleich für die Daten in einem Excel-Arbeitsblatt auszuführen, wählen Sie **Excel-Datei** für **Datenquelle**aus, klicken Sie auf **Durchsuchen** , und wählen Sie die Excel-Datei aus. Lassen Sie **Erste Zeile als Header verwenden** ggf. aktiviert. Wählen Sie in **Arbeitsblatt**das Arbeitsblatt in der Excel-Datei aus, das die Quelle der Daten ist. Excel muss auf dem [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] -Computer installiert sein, um eine Excel-Datei auswählen zu können. Wenn Excel auf dem [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] -Computer nicht installiert ist, ist die Schaltfläche **Durchsuchen** nicht verfügbar, und Sie werden unter diesem Textfeld benachrichtigt, dass Excel nicht installiert ist.  
  
3.  Wählen Sie unter **Zuordnungen**ein Feld in der Datenquelle für **Quellspalte**aus, und wählen Sie dann die entsprechende Domäne aus. Wiederholen Sie den Vorgang für alle Domänen, die Sie im Abgleichsprozess verwenden. Jede Domäne, die in der Abgleichsrichtlinie definiert ist, muss einer entsprechenden Quellspalte zugeordnet werden. Auf der Seite „Zuordnen“ werden die Domänen angezeigt, die in der Abgleichsrichtlinie und den Regeln in der Abgleichsrichtlinie im rechten Bereich definiert wurden.  
  
    > [!NOTE]  
    >  Sie können die Quelldaten nur dann einer DQS-Domäne zuordnen, wenn der Quelldatentyp in DQS unterstützt wird und mit dem DQS-Domänendatentyp übereinstimmt. Informationen zu in DQS unterstützten Datentypen finden Sie unter [Supported SQL Server and SSIS Data Types for DQS Domains](../data-quality-services/supported-sql-server-and-ssis-data-types-for-dqs-domains.md).  
  
4.  Klicken Sie auf der **plus (+)** Steuerelement eine Zeile der Zuordnungstabelle hinzu oder **minus (-)** -Steuerelement eine Zeile zu entfernen.  
  
5.  Klicken Sie auf **Vorschau der Datenquelle** , um die Daten in der ausgewählten SQL Server-Tabelle oder -Sicht oder im ausgewählten Excel-Arbeitsblatt anzuzeigen.  
  
6.  Klicken Sie auf **Verbunddomänen anzeigen/auswählen** eine Liste der in der Wissensdatenbank verfügbaren verbunddomänen anzuzeigen, und wählen Sie Optionen für die Zuordnung.  
  
7.  Klicken Sie auf **Weiter** , um zur Abgleichsphase zu wechseln.  
  
    > [!NOTE]  
    >  Klicken Sie auf **Schließen** , um die Phase des Abgleichsprojekts zu speichern und zur DQS-Startseite zurückzukehren. Wenn Sie dieses Projekt das nächste Mal öffnen, befindet es sich in derselben Phase. Klicken Sie auf **Abbrechen** , um die Abgleichsaktivität zu beenden, ohne Ihre Arbeit zu speichern, und kehren Sie zur DQS-Startseite zurück.  
  
##  <a name="MatchingStage"></a> Abgleichsphase  
 In dieser Phase führen Sie einen computerunterstützten Abgleichsprozess aus, der anzeigt, wie viele Übereinstimmungen basierend auf den Abgleichsregeln in den Quelldaten enthalten sind. Durch diesen Prozess wird eine Abgleichsergebnistabelle generiert, in der die von DQS identifizierten Cluster, jeder Datensatz im Cluster mit der zugehörigen Datensatz-ID und die Treffergenauigkeit sowie der anfänglich führende Datensatz für den Cluster angezeigt werden. Der führende Datensatz im Cluster wird zufällig ausgewählt. Sie bestimmen den überdauernden Datensatz durch Auswählen der Survivorship-Regel auf der Seite **Exportieren** , wenn Sie das Abgleichsprojekt ausführen. Jede zusätzliche Zeile in einem Cluster wird als Treffer angesehen, dessen Treffergenauigkeit (im Vergleich zum führenden Datensatz) in der Ergebnistabelle angegeben wird. Die Clusternummer ist mit der Datensatz-ID für den führenden Datensatz im Cluster identisch.  
  
 Sie können die Abgleichsergebnisse nach den gewünschten Daten filtern und unerwünschte Treffer ablehnen. Sie können Profilerstellungsdaten für den gesamten Abgleichsprozess, Details zu den angewendeten Abgleichsregeln und Statistiken zu den Abgleichsergebnissen im Ganzen anzeigen. Der Abgleichsprozess kann überlappende oder nicht überlappende Cluster identifizieren. wenn er mehrfach ausgeführt wird, kann er zudem auf Daten, die neu aus der Quelle kopiert und indiziert wurden, oder auf frühere Daten angewendet werden.  
  
1.  Auf der **Abgleich Seite**, Option **überlappende Cluster** aus der Dropdown-Liste an, die pivotdatensätze und die folgenden Datensätze für alle Cluster Wenn Abgleich ausgeführt wird, auch wenn Gruppen von Clustern gemeinsame Datensätze aufweisen. Wählen Sie **Nicht überlappende Cluster** aus, um Cluster anzuzeigen, die als einzelne Cluster gemeinsame Datensätze aufweisen, wenn der Abgleich ausgeführt wird.  
  
2.  Klicken Sie auf **erneut aus Datenquelle laden** (Standard) zum Kopieren von Daten aus der Datenquelle in die Stagingtabelle und neu zu indizieren, wenn Sie das abgleichsprojekt ausführen. Klicken Sie auf **für vorherige Daten ausführen** ein abgleichsprojekt auszuführen, ohne die Daten in die Stagingtabelle zu kopieren und neu zu indizieren. **Für vorherige Daten ausführen** ist für die erste Ausführung des Abgleichsprojekts deaktiviert. Dies gilt auch, wenn Sie die Zuordnung auf der Seite **Zuordnen** ändern und in der folgenden Meldung auf **Ja** klicken. In beiden Fällen müssen Sie die Daten erneut indizieren. Die Neuindizierung ist nicht erforderlich, wenn das Abgleichsprojekt nicht geändert wurde. Durch die Ausführung für vorherige Daten kann die Leistung verbessert werden.  
  
3.  Klicken Sie auf **Start** , um den Abgleich für die ausgewählte Datenquelle auszuführen.  
  
4.  Klicken Sie auf **Beenden** , wenn Sie das Abgleichsprojekt beenden und die Ergebnisse verwerfen möchten.  
  
5.  Überprüfen Sie nach Abschluss des Abgleichsprozesses, ob die Cluster in der Tabelle **Abgleichsergebnisse** angemessen sind. zeigen Sie außerdem die Statistiken in den Registerkarten **Profiler** und **Abgleichsergebnisse** an, um sicherzustellen, dass Sie die erforderlichen Ergebnisse erhalten. Zeigen Sie die übereinstimmenden Datensätze an, indem Sie für **Filter** die Option **Übereinstimmung** auswählen. Um die nicht übereinstimmenden Datensätze anzuzeigen, wählen Sie **Keine Übereinstimmung**aus.  
  
6.  Wenn Die Abgleichsrichtlinie mehrere Abgleichsregeln enthält, klicken auf die Registerkarte **Abgleichsregeln** , und geben Sie das Symbol für jede Regel an. Überprüfen Sie dann, welche Regel einen Datensatz als eine Übereinstimmung erkannt hat, indem Sie die Regel in der Spalte **Regel** der Tabelle **Abgleichsergebnisse** identifiziert.  
  
7.  Wenn Sie eine pivotdatensatz in der Tabelle wählen, und klicken Sie auf der **Details anzeigen** Symbol (oder doppelklicken Sie auf den Datensatz), zeigt DQS eine **Details zur Treffergenauigkeit** Popup, den Datensatz doppelgeklickt und dessen pivotdatensatz (und die Werte in allen ihren Feldern) angezeigt, das Ergebnis zwischen ihnen und einen Drilldown der übereinstimmenden bewerten Beiträge der einzelnen Felder. Wenn Sie auf einen Pivotdatensatz doppelklicken, wird kein Popupfenster angezeigt.  
  
8.  Klicken Sie auf das Symbol **Alle reduzieren** , um die in der Tabelle **Abgleichsergebnisse** angezeigten Datensätze auszublenden und nur den Pivotdatensatz, nicht die doppelten Datensätze anzuzeigen. Klicken Sie auf **Alle erweitern** , um die in der Tabelle „Abgleichsergebnisse„ angezeigten Datensätze einzublenden und alle doppelten Datensätze anzuzeigen.  
  
9. Um einen Datensatz aus den Abgleichsergebnissen auszuschließen, klicken Sie auf das Kontrollkästchen **Abgelehnt** für den Datensatz.  
  
10. So ändern die minimale treffergenauigkeit, die den Grad der Übereinstimmung bestimmt, die ein Datensatz angezeigt werden muss, wählen Sie die **Min. Treffergenauigkeit** Symbol oberhalb der rechten Seite der Tabelle, und geben Sie eine höhere Zahl. Die minimale Treffergenauigkeit ist standardmäßig auf 80% festgelegt. Klicken Sie auf **Aktualisieren** , um den Inhalt der Tabelle zu ändern.  
  
11. Nachdem die Analyse abgeschlossen wurde, wird die Schaltfläche **Start** zur Schaltfläche **Neustart** . Klicken Sie auf **Neustart** , um das Analyseprojekt erneut auszuführen. Wenn die Ergebnisse der vorherigen Analyse noch nicht gespeichert wurden, gehen beim Klicken auf **Neustart** jedoch die vorherigen Daten verloren. Klicken Sie zum Fortfahren in dem Popupfenster auf **Ja** . Verlassen Sie während der Ausführung der Analyse nicht die Seite, da ansonsten der Analyseprozess abgebrochen wird.  
  
12. Klicken Sie auf **Weiter** , um zur Survivorship- und Exportphase zu wechseln.  
  
##  <a name="SurvivorshipandExportStage"></a> Survivorship- und Exportphase  
 Im Survivorship-Prozess bestimmt Data Quality Services einen Survivor-Datensatz für jeden Cluster, der die anderen Datensätze ersetzt, die im Cluster mit ihm übereinstimmen. Anschließend werden die übereinstimmenden und/oder Survivorship-Ergebnisse in eine Tabelle in der SQL Server-Datenbank, in einer CSV-Datei oder in einer Excel-Datei exportiert.  
  
 Survivorship ist optional. Sie können die Ergebnisse auch ohne Ausführung von Survivorship exportieren. In diesem Fall verwendet DQS den Pivotdatensatz, der in der Abgleichsanalyse festgelegt wurde. Wenn zwei oder mehr Datensätze in einem Cluster die Survivorship-Regel erfüllen, wählt der Survivorship-Prozess die niedrigste Datensatz-ID in den konfliktverursachenden Datensätzen als Survivor aus. Sie können Survivor mit unterschiedlichen Survivorship-Regeln in verschiedene Dateien oder Tabellen exportieren.  
  
1.  Wählen Sie auf der Seite **Exportieren** unter **Zieltyp**das ziel aus, in das die übereinstimmenden Daten exportiert werden sollen: **SQL Server**, **CSV-Datei**oder **Excel-Datei**.  
  
    > [!IMPORTANT]  
    >  Wenn Sie die 64-Bit-Version von Excel verwenden, können Sie die übereinstimmenden Daten nicht in eine Excel-Datei exportieren; Sie können sie nur in eine SQL Server-Datenbank oder eine CSV-Datei exportieren.  
  
2.  Wenn Sie **SQL Server** für **Zieltyp**auswählten, geben Sie unter **Datenbankname**die Datenbank an, in die die Ergebnisse exportiert werden sollen.  
  
    > [!IMPORTANT]  
    >  Die Zieldatenbank muss sich in der gleichen SQL Server-Instanz wie der DQS-Server befinden. Andernfalls wird sie nicht in der Dropdownliste angezeigt.  
  
3.  Aktivieren Sie das Kontrollkästchen für **übereinstimmenden Ergebnisse** übereinstimmenden Ergebnisse (siehe oben erläutert) in die festgelegte Tabelle in einer SQL Server-Datenbank oder die festgelegte CSV- oder Excel-Datei exportieren. Aktivieren Sie das Kontrollkästchen für **Survivorship-Ergebnisse** Survivorship-Ergebnisse (siehe oben erläutert) in die festgelegte Tabelle in einer SQL Server-Datenbank oder die festgelegte CSV- oder Excel-Datei exportieren.  
  
     Für Abgleichsergebnisse wird Folgendes exportiert:  
  
    -   Eine Liste der Cluster und der übereinstimmenden Datensätze in jedem Cluster, einschließlich des Regelnamens und der Genauigkeit. Der Pivotdatensatz wird als „Pivot“ markiert. Die Cluster werden als erstes in der Exportliste angezeigt.  
  
    -   Eine Liste der nicht übereinstimmenden Datensätze mit dem Wert „NULL“ in der Spalte für die Genauigkeit und den Regelnamen. Diese Datensätze werden nach den Clustern an die Exportliste angefügt.  
  
     Für Survivorship-Ergebnisse wird Folgendes exportiert:  
  
    -   Eine Liste der durch den Survivorship-Prozess entsprechend der Survivorship-Regel bestimmten Survivor-Datensätze. Diese Datensätze werden als erstes in der Exportliste angezeigt.  
  
    -   Eine Liste der nicht übereinstimmenden Datensätze, die nicht in den Clustern übereinstimmender Datensätze enthalten sind. Diese Datensätze werden nach den Survivor-Ergebnissen angefügt.  
  
4.  Wenn Sie **SQL Server** für **Zieltyp**ausgewählt haben, geben Sie unter **Tabellenname**den Namen der Tabellen ein, in die die Ergebnisse exportiert werden sollen. Wenn Sie Abgleichsergebnisse und Survivorship-Ergebnisse exportieren, müssen die Zieltabellen unterschiedliche Namen haben, die für die Datenbank eindeutig sind.  
  
5.  Wenn Sie **CSV-Datei** für **Zieltyp**ausgewählt haben, geben Sie unter **Name der CSV-Datei**den Dateinamen und Pfad der CSV-Datei ein, in die die Ergebnisse exportiert werden sollen.  
  
6.  Wenn Sie **Excel-Datei** für **Zieltyp**ausgewählt haben, geben Sie unter **Name der Excel-Datei**den Dateinamen und Pfad der Excel-Datei ein, in die die Ergebnisse exportiert werden sollen. Wenn Sie die 64-Bit-Version von Excel verwenden, können Sie die Daten nicht in eine Excel-Datei exportieren.  
  
7.  Wählen Sie die Survivorship-Regel wie folgt aus:  
  
    -   Wählen Sie **Pivot-Datensatz** (Standard) um den survivor-Datensatz als den ursprünglichen pivotdatensatz von DQS willkürlich ausgewählt zu identifizieren.  
  
    -   Wählen Sie **Vollständigster und längster Datensatz** aus, um den Survivor-Datensatz als den mit der größten Anzahl ausgefüllter Felder und mit der größten Anzahl von Begriffen in jedem Feld zu identifizieren. Alle Quellfelder werden überprüft, auch die Felder, die auf der Seite **Zuordnen** keiner Domäne zugeordnet wurden.  
  
    -   Wählen Sie **Vollständigster Datensatz** aus, um den Survivor-Datensatz als den mit der größten Anzahl ausgefüllter Felder zu identifizieren. Ein ausgefülltes Feld enthält mindestens einen Wert (Zeichenfolge, numerisch oder beides). Alle Quellfelder werden überprüft, auch die Felder, die auf der Seite Zuordnen keiner Domäne zugeordnet wurden. Ein ausgefülltes Feld enthält mindestens einen Wert (Zeichenfolge, numerisch oder beides).  
  
    -   Wählen Sie **Längster Datensatz** aus, um den Survivor-Datensatz als den mit der größten Anzahl von begriffen in den Quellfeldern zu identifizieren. Um die Länge jedes Datensatzes zu bestimmen, überprüft DQS die Länge der Begriffe in allen Quellfeldern, einschließlich der Felder, die auf der Seite **Zuordnen** keiner Domäne zugeordnet wurden.  
  
8.  Zeigen Sie die Statistiken auf den Registerkarten **Profiler** an, um sicherzustellen, dass Sie die benötigten Ergebnisse erzielen.  
  
9. Klicken Sie auf **Exportieren** , um die Ergebnisse zu exportieren. Hierdurch wird das Dialogfeld „Export wird abgeglichen“ geöffnet, in dem der Fortschritt und anschließend die Ergebnisse des Exports angezeigt werden.  
  
    -   Wenn Sie **SQL Server** als Datenziel ausgewählt haben, wird eine neue Tabelle mit dem angegebenen Namen in der ausgewählten Datenbank erstellt.  
  
    -   Wenn Sie **CSV-Datei** als Datenziel ausgewählt haben, wird eine CSV-Datei in dem Ordner auf dem [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] -Computer mit dem Dateinamen erstellt, den Sie zuvor im Feld **Name der CSV-Datei** angegeben haben.  
  
    -   Wenn Sie **Excel-Datei** als Datenziel ausgewählt haben, wird eine XLSX-Datei in dem Ordner auf dem [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] -Computer mit dem Dateinamen erstellt, den Sie zuvor im Feld **Name der Excel-Datei** angegeben haben.  
  
10. Überprüfen Sie, ob der Export erfolgreich abgeschlossen wurde, und klicken Sie dann auf **Schließen**.  
  
11. Klicken Sie auf **Fertig stellen** , um das Abgleichsprojekt abzuschließen.  
  
    > [!NOTE]  
    >  Wenn Sie ein Abgleichsprojekt beendet haben und es dann erneut verwenden, verwendet es die Wissensdatenbank in dem Zustand, als es veröffentlicht wurde. Es werden keine Änderungen berücksichtigt, die Sie seit Abschluss des Projekts an der Wissensdatenbank vorgenommen haben. Um die Änderungen oder eine neue Wissensdatenbank zu verwenden, müssen Sie ein neues Abgleichsprojekt erstellen. Wenn Sie jedoch ein Abgleichsprojekt erstellt, aber noch nicht abgeschlossen haben, werden alle an der Abgleichsrichtlinie vorgenommenen und veröffentlichten Änderungen beim Ausführen des Abgleichs in dem Projekt verwendet.  
  
##  <a name="FollowUp"></a> Nachverfolgung: Ausführen eines Abgleichsprojekts  
 Nachdem Sie ein Abgleichsprojekt ausgeführt haben, können Sie die Abgleichsrichtlinie in der Wissensdatenbank ändern und ein anderes Abgleichsprojekt basierend auf der aktualisierten Abgleichsrichtlinie erstellen und ausführen. Weitere Informationen finden Sie unter [Create a Matching Policy](../data-quality-services/create-a-matching-policy.md).  
  
##  <a name="Profiler"></a> Registerkarten „Profiler“ und „Ergebnisse“  
 Die Registerkarten „Profiler“ und „Ergebnisse“ enthalten Statistiken für den Abgleichsprozess.  
  
### Registerkarte „Profiler“  
 Klicken Sie auf die Registerkarte **Profiler** , um Statistiken für die Quelldatenbank und für alle in der Richtlinienregel enthaltenen Felder anzuzeigen. Die Statistiken werden aktualisiert, wenn die Richtlinienregel ausgeführt wird. Die Profilerstellung hilft Ihnen, die Effektivität vom Deduplizierungsprozess zu bewerten und zu ermitteln, inwieweit der Prozess die Datenqualität verbessert. Die Genauigkeit der Profilerstellung ist für ein Abgleichsprojekt irrelevant.  
  
 Die Quelldatenbankstatistiken umfassen Folgendes:  
  
-   **Datensätze**: Die Gesamtzahl der Datensätze in der Datenbank  
  
-   **Gesamtwerte**: Die Gesamtzahl der Werte in den Feldern  
  
-   **Neue Werte**: Die Gesamtzahl der Werte, die seit der vorherigen Ausführung neu sind, und ihr prozentualer Anteil am Ganzen  
  
-   **Eindeutige Werte**: Die Gesamtzahl der eindeutigen Werte in den Feldern und ihr prozentualer Anteil am Ganzen  
  
-   **Neue eindeutige Werte**: Die Gesamtzahl der eindeutigen Werte, die neu in den Feldern sind, und ihr prozentualer Anteil am Ganzen  
  
 Die Feldstatistiken umfassen Folgendes:  
  
-   **Feld**: Name des Felds, das in die Zuordnungen eingeschlossen wurde  
  
-   **Domäne**: Name der Domäne, die dem Feld zugeordnet wurde  
  
-   **Neu**: Die Anzahl der neuen Übereinstimmungen und ihr prozentualer Anteil am Gesamtwert  
  
-   **Eindeutig**: Die Gesamtzahl der eindeutigen Datensätze in den Feldern und ihr prozentualer Anteil am Ganzen  
  
-   **Vollständigkeit**: Der Prozentsatz, zu dem die Regelausführung abgeschlossen wurde  
  
### Abgleichsrichtlinienbenachrichtigungen  
 Für die Abgleichsrichtlinienaktivität führen die folgenden Bedingungen zu Benachrichtigungen:  
  
-   Das Feld ist in allen Datensätzen leer; Sie sollten es aus der Zuordnung entfernen.  
  
-   Das Feldvollständigkeitsergebnis ist sehr niedrig; Sie sollten es aus der Zuordnung entfernen.  
  
-   Alle Werte in einem Feld sind ungültig; Sie sollten die Zuordnung und die Relevanz von Domänenregeln für den Feldinhalt überprüfen.  
  
-   Es gibt nur wenige gültige Werte im Feld; Sie sollten die Zuordnung und die Relevanz von Domänenregeln für den Feldinhalt überprüfen.  
  
-   Es gibt einen hohen Eindeutigkeitsgrad in diesem Feld. Das Verwenden dieses Felds in Abgleichsrichtlinien kann die Abgleichsergebnisse reduzieren.  
  
### Registerkarte „Abgleichsregeln“  
 Klicken Sie auf diese Registerkarte, um eine Liste der Regeln in der Abgleichsrichtlinie und die Bedingungen für eine Regel anzuzeigen.  
  
 **Liste „Regeln“**  
 Zeigt eine Liste aller Abgleichsregeln in der Abgleichsrichtlinie an. Wählen Sie eine der Regeln aus, um die Bedingungen in der Regel in der Tabelle „Abgleichsregel“ anzuzeigen.  
  
 **Tabelle „Abgleichsregel“**  
 Zeigt jede Bedingung in der ausgewählten Regel an, einschließlich Domäne, Ähnlichkeitswerts, Gewichtung und erforderlicher Auswahl.  
  
### Registerkarte „Abgleichsergebnisse“  
 Klicken Sie auf die Registerkarte **Abgleichsergebnisse** , um Statistiken für die Analyse der Datenquelle anhand der für das Projekt ausgewählten Daten und der Abgleichsregel oder den Regeln in der Wissensdatenbank anzuzeigen. Die Statistiken umfassen Folgendes:  
  
-   Die Gesamtzahl der Datensätze in der Datenbank  
  
-   Die Gesamtzahl der übereinstimmenden Datensätze in der Datenbank  
  
-   Die Anzahl von Datensätzen in der Datenbank, die nicht als Duplikate angesehen werden  
  
-   Die Anzahl der ermittelten Cluster  
  
-   Die durchschnittliche Clustergröße (die Anzahl doppelter Datensätze geteilt durch die Anzahl der Cluster)  
  
-   Die geringste Anzahl von Duplikaten in einem Cluster  
  
-   Die größte Anzahl von Duplikaten in einem Cluster  
  
  