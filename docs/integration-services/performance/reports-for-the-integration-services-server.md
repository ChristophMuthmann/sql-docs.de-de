---
title: "Berichte f&#252;r den Integration Services-Server | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.SWB.SUMMARY.RENDER.CUSTOM.REPORT.F1"
ms.assetid: e976e7c0-a805-4370-bf73-356c8e3becfb
caps.latest.revision: 17
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 17
---
# Berichte f&#252;r den Integration Services-Server
  In der aktuellen Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]sind Standardberichte in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] verfügbar, die zum Überwachen von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekten hilfreich sind, die auf dem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Server bereitgestellt wurden. Mit diesen Berichten können Sie den Paketstatus und -verlauf anzeigen und ggf. die Ursache von Paketausführungsfehlern identifizieren.  
  
 Im oberen Bereich jeder Berichtsseite werden die folgenden Symbole bereitgestellt: Zurück-Symbol (um zur vorherigen Seite zurückzukehren), Aktualisierungssymbol (um die auf der Seite angezeigten Informationen zu aktualisieren) und Druckersymbol (um die aktuelle Seite zu drucken).  
  
 Weitere Informationen zum Bereitstellen von Paketen auf dem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Server, finden Sie unter [Bereitstellen von Projekten auf dem Integration Services-Server](../../integration-services/packages/deploy-projects-to-integration-services-server.md).  
  
## Integration Services-Dashboard  
 Der Bericht **Integration Services-Dashboard** bietet eine Übersicht über alle Paketausführungen für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz. Im Dashboard können Sie die Informationen zu jedem auf dem Server ausgeführten Paket erweitern, um spezifische Details über möglicherweise aufgetretene Paketausführungsfehler zu suchen.  
  
 Der Bericht zeigt die folgenden Abschnitte von Informationen an.  
  
|Abschnitt|Description|  
|-------------|-----------------|  
|**Ausführungsinformationen**|Zeigt die Anzahl von Ausführungen an, die in den vergangenen 24 Stunden unterschiedliche Status (fehlerhaft, ausgeführt, erfolgreich, andere) aufgewiesen haben.|  
|**Paketinformationen**|Zeigt die Gesamtanzahl der Pakete, die in den letzten 24 Stunden ausgeführt wurden.|  
|**Verbindungsinformationen**|Zeigt die Verbindungen, die in den letzten 24 Stunden in fehlerhaften Ausführungen verwendet wurden.|  
|**Detaillierte Paketinformationen**|Zeigt die Details der abgeschlossenen Ausführungen an, die in den letzten 24 Stunden durchgeführt wurden. Dieser Abschnitt zeigt z. B. die Anzahl der fehlerhaften Ausführungen im Vergleich zur Gesamtzahl der Ausführungen, die Dauer der Ausführungen (in Sekunden) und die durchschnittliche Dauer der Ausführungen in den vergangenen drei Monaten an.<br /><br /> Sie können weitere Informationen für ein Paket anzeigen, indem Sie auf **Übersicht**, **Alle Meldungen**und **Ausführungsleistung**klicken.<br /><br /> Der Bericht **Ausführungsleistung** zeigt die Dauer der letzten Ausführungsinstanz sowie die Start- und Endzeiten und die Umgebung an, die angewendet wurde.<br /><br /> Das Diagramm und die zugeordnete Tabelle im Bericht **Ausführungsleistung** zeigen die Dauer der letzten 10 erfolgreichen Ausführungen des Pakets an. In der Tabelle wird auch die durchschnittliche Ausführungsdauer in einem Zeitraum von drei Monaten angezeigt. Unterschiedliche Umgebungen und Literalwerte wurden möglicherweise zur Laufzeit für diese 10 erfolgreichen Ausführungen des Pakets angewendet.<br /><br /> Schließlich wird im Bericht **Ausführungsleistung** die aktive Zeit und die Gesamtzeit für die Datenflusskomponenten des Pakets angezeigt. Die aktive Zeit bezieht sich auf die gesamte Zeit, die für die Ausführung der Komponente in allen Phasen benötigt wurde, und die Gesamtzeit bezieht sich auf die insgesamt verstrichene Zeit für eine Komponente. Der Bericht zeigt nur diese Informationen für Paketkomponenten an, wenn der Protokolliergrad der letzten Paketausführung auf "Leistung" oder "Ausführlich" festgelegt wird.<br /><br /> Der Bericht **Übersicht** zeigt den Status von Pakettasks an. Der Bericht **Meldungen** zeigt die Ereignismeldungen und die Fehlermeldungen für das Paket und die Tasks an, beispielsweise das Melden der Start- und Endzeiten sowie die Anzahl der geschriebenen Zeilen.<br /><br /> Sie können auch im Bericht **Übersicht** auf **Meldungen anzeigen** klicken, um zum Bericht **Meldungen** zu navigieren. Sie können auch im Bericht **Meldungen** auf **Übersicht anzeigen** klicken, um zum Bericht **Übersicht** zu navigieren.|  
  
 Sie können die auf einer beliebigen Seite angezeigte Tabelle filtern, indem Sie auf **Filtern** klicken und dann im Dialogfeld **Filtereinstellungen** die gewünschten Kriterien auswählen. Abhängig von den angezeigten Daten sind unterschiedliche Filterkriterien verfügbar. Sie können die Sortierreihenfolge des Berichts ändern, indem Sie im Dialogfeld **Filtereinstellungen** auf das Sortiersymbol klicken.  
  
## Bericht "Alle Ausführungen"  
 Der Bericht **Alle Ausführungen** zeigt eine Zusammenfassung aller [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Ausführungen, die auf dem Server ausgeführt wurden. Es kann mehrere Ausführungen des Beispielpakets geben. Im Gegensatz zum Bericht **Integration Services-Dashboard** können Sie den Bericht **Alle Ausführungen** so konfigurieren, dass Ausführungen angezeigt werden, die während eines Datumsbereichs gestartet wurden. Die Datumsangaben können mehrere Tage, Monate oder Jahre umfassen.  
  
 Der Bericht zeigt die folgenden Abschnitte von Informationen an.  
  
|Abschnitt|Description|  
|-------------|-----------------|  
|Filter|Zeigt den aktuellen Filter an, der für den Bericht verwendet wird, z. B. der Startzeitraum.|  
|Ausführungsinformationen|Zeigt die Startzeit, die Endzeit und die Dauer für jede Paketausführung an. Sie können eine Liste der Parameterwerte anzeigen, die bei einer Paketausführung verwendet wurden, z. B. Werte, die mit dem Task "Paket ausführen" an ein untergeordnetes Paket übergeben wurden. Um die Parameterliste anzuzeigen, klicken Sie auf "Übersicht".|  
  
 Weitere Informationen über das Verwenden des Tasks "Paket ausführen" zum Verfügbarmachen von Werten für untergeordnete Pakete finden Sie unter [Execute Package Task](../../integration-services/control-flow/execute-package-task.md).  
  
 Weitere Informationen zu Parametern finden Sie unter [Integration Services-Paket- und -Projektparameter (SSIS)](../../integration-services/integration-services-ssis-package-and-project-parameters.md).  
  
## Alle Verbindungen  
 Der Bericht **Alle Verbindungen** enthält die folgenden Informationen für Verbindungen, die nicht hergestellt werden konnten, und für Ausführungen, die in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz aufgetreten sind.  
  
 Der Bericht zeigt die folgenden Abschnitte von Informationen an.  
  
|Abschnitt|Description|  
|-------------|-----------------|  
|Filtern|Zeigt den aktuellen Filter an, der für den Bericht verwendet wird, z. B. Verbindungen mit einer angegebenen Zeichenfolge und dem Bereich **Uhrzeit des letzten Fehlers** .<br /><br /> Sie legen den Bereich **Uhrzeit des letzten Fehlers** fest, um lediglich Verbindungsfehler anzuzeigen, die während eines Datumsbereichs aufgetreten sind. Der Bereich kann mehrere Tage, Monate oder Jahre umfassen.|  
|Details|Zeigt die Verbindungszeichenfolge, die Anzahl der Ausführungen, bei denen eine Verbindung nicht hergestellt werden konnte, und das Datum an, wann die Verbindung zuletzt nicht hergestellt werden konnte.|  
  
## Bericht "Alle Vorgänge"  
 Der Bericht **Alle Vorgänge** zeigt eine Zusammenfassung aller [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Vorgänge an, die auf dem Server ausgeführt wurden, einschließlich Paketbereitstellung, Validierung und Ausführung sowie anderer administrativer Vorgänge. Wie in dem Integration Services-Dashboard können Sie einen Filter auf die Tabelle anwenden, um die angezeigten Informationen einzugrenzen.  
  
## Bericht "Alle Überprüfungen"  
 Der Bericht **Alle Überprüfungen** zeigt eine Zusammenfassung aller [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Überprüfungen, die auf dem Server ausgeführt wurden. Die Zusammenfassung enthält Informationen für jede Überprüfungen, z. B. Status, Startzeit und Endzeit. Jeder Zusammenfassungseintrag enthält einen Link zu den Meldungen, die während der Überprüfungen generiert wurden. Wie in dem Integration Services-Dashboard können Sie einen Filter auf die Tabelle anwenden, um die angezeigten Informationen einzugrenzen.  
  
## Benutzerdefinierte Berichte  
 Sie können dem **SSISDB**-Katalogknoten unter dem Knoten **Integration Services-Kataloge** in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] einen benutzerdefinierten Bericht (RDL-Datei) hinzufügen. Stellen Sie vor dem Hinzufügen des Berichts sicher, dass Sie eine Konvention für dreiteilige Namen verwenden, um die Objekte, auf die Sie verweisen, z. B. eine Quelltabelle, vollständig zu qualifizieren. Andernfalls meldet [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] einen Fehler. Die Namenskonvention ist \<Datenbank>.\<Besitzer>.\<Objekt>. Ein Beispiel wäre SSISDB.internal.executions.  
  
> [!NOTE]  
>  Wenn Sie dem **SSISDB**-Knoten unter dem Knoten **Datenbanken** benutzerdefinierte Berichte hinzufügen, ist das SSISDB-Präfix nicht erforderlich.  
  
 Anweisungen zum Erstellen und Hinzufügen eines benutzerdefinierten Berichts finden Sie unter [Add a Custom Report to Management Studio](../../ssms/object/add-a-custom-report-to-management-studio.md).  
  
## Verwandte Aufgaben  
 [Anzeigen von Berichten für den Integration Services-Server](../../integration-services/performance/view-reports-for-the-integration-services-server.md)  
  
## Verwandte Inhalte  
[Überwachen der Ausführung von Paketen und anderen Vorgängen](../../integration-services/performance/monitor-running-packages-and-other-operations.md)
  
  