---
title: "Auftragsschritt-Eigenschaften – Neuer Auftragsschritt (Seite „Allgemein“) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.ag.job.stepgeneral.f1
ms.assetid: 8d1885ba-4386-4528-8f2b-68c16852720c
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: fbe2a44b573d05bbf4b9b1eed79595e3a771bcf4
ms.lasthandoff: 04/11/2017

---
# <a name="job-step-properties---new-job-step-general-page"></a>Auftragsschritt-Eigenschaften – Neuer Auftragsschritt (Seite „Allgemein“)
Mithilfe dieser Seite können Sie die Eigenschaften eines [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]-Agent-Auftragsschritts anzeigen und ändern oder einen neuen Auftragsschritt definieren.  
  
Erweitern Sie im Objekt-Explorer von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] den [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent, klicken Sie mit der rechten Maustaste auf **Aufträge**, klicken Sie auf **Neuer Auftrag**, wählen Sie die Seite **Schritte** aus, und klicken Sie auf **Neu**, um zu dieser Seite zu navigieren. Sie können auch zu dieser Seite navigieren, indem Sie mit der rechten Maustaste auf einen Auftrag im Objekt-Explorer klicken, auf **Eigenschaften**klicken, die Seite **Schritte** auswählen, und auf **Neu**, **Einfügen**oder **Bearbeiten**klicken.  
  
## <a name="options"></a>enthalten  
**Schrittname**  
Legt den Namen des Auftrags fest.  
  
**Typ**  
Legt das durch den Auftrag verwendete Subsystem fest. Basierend auf dem von Ihnen ausgewählten Subsystem ändern sich die für das Definieren des Auftragsschritts angezeigten Optionen.  
  
**Ausführen als**  
Legt das Proxykonto für den Auftragsschritt fest. Mitglieder der festen Serverrolle „sysadmin“ können auch das **SQL-Agent-Dienstkonto**angeben.  
  
**Datenbank**  
Legt die Datenbank fest, in der der Auftragsschritt ausgeführt wird. Diese Option ist nicht für alle Auftragsschritttypen verfügbar.  
  
**Befehl**  
Legt den durch den Auftrag ausgeführten Befehl fest.  
  
## <a name="options-for-transact-sql-job-steps"></a>Optionen für Transact-SQL-Auftragsschritte  
**Öffnen**  
Lädt den Befehl aus einer Datei.  
  
**Alles auswählen**  
Markiert den Text des Befehls.  
  
**Kopieren**  
Kopiert den ausgewählten Text in die Zwischenablage.  
  
**Einfügen**  
Fügt die Inhalte aus der Zwischenablage ein.  
  
**Analysieren**  
Überprüft die Syntax des Befehls.  
  
## <a name="options-for-activex-script-job-steps"></a>Optionen für Auftragsschritte von ActiveX-Skript  
  
> [!IMPORTANT]  
> Das ActiveX Scripting-Subsystem wird in einer zukünftigen Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] aus dem [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]-Agent entfernt. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird.  
  
**VBScript**  
Gibt [!INCLUDE[msCoName](../../includes/msconame_md.md)] VBScript als Sprache für die Auftragsschritte an.  
  
**JScript**  
Gibt JScript als Sprache für die Auftragsschritte an.  
  
**Andere**  
Geben Sie den Namen der Sprache für Auftragsschritte ein, die in einer anderen Skriptsprache geschrieben wurden.  
  
**Öffnen**  
Lädt den Befehl aus einer Datei.  
  
**Alles auswählen**  
Markiert den Text des Befehls.  
  
**Kopieren**  
Kopiert den markierten Text.  
  
**Einfügen**  
Fügt die Inhalte aus der Zwischenablage ein.  
  
## <a name="options-for-operating-system-cmdexec-job-steps"></a>Optionen für Auftragsschritte des Betriebssystems (CmdExec)  
**Prozessexitcode eines erfolgreichen Befehls**  
Geben Sie den Exitcode ein, den der Befehl zurückgibt, um einen Erfolg zu melden.  
  
**Öffnen**  
Lädt den Befehl aus einer Datei.  
  
**Alles auswählen**  
Markiert den Text des Befehls.  
  
**Kopieren**  
Kopiert den markierten Text.  
  
**Einfügen**  
Fügt die Inhalte aus der Zwischenablage ein.  
  
## <a name="options-for-powershell-job-steps"></a>Optionen für PowerShell-Auftragsschritte  
**Öffnen**  
Lädt das Skript aus einer Datei.  
  
**Alles auswählen**  
Markiert den Text des Skripts.  
  
**Kopieren**  
Kopiert den markierten Text.  
  
**Einfügen**  
Fügt die Inhalte aus der Zwischenablage ein.  
  
## <a name="options-for-replication-distributor-job-steps"></a>Optionen für Replikationsverteiler-Auftragsschritte  
**Alles auswählen**  
Markiert den Text des Befehls.  
  
**Kopieren**  
Kopiert den markierten Text.  
  
**Einfügen**  
Fügt die Inhalte aus der Zwischenablage ein.  
  
## <a name="options-for-replication-merge-job-steps"></a>Optionen für Replikationsmerge-Auftragsschritte  
**Alles auswählen**  
Markiert den Text des Befehls.  
  
**Kopieren**  
Kopiert den markierten Text.  
  
**Einfügen**  
Fügt die Inhalte aus der Zwischenablage ein.  
  
## <a name="options-for-replication-queue-reader-job-steps"></a>Optionen für Auftragsschritte des Replikation-Warteschlangenlesers  
**Datenbank**  
Die Datenbank, die für den Auftragsschritt verwendet werden soll.  
  
**Alles auswählen**  
Markiert den Text des Befehls.  
  
**Kopieren**  
Kopiert den markierten Text.  
  
**Einfügen**  
Fügt die Inhalte aus der Zwischenablage ein.  
  
## <a name="options-for-replication-snapshot-job-steps"></a>Optionen für Replikationsmomentaufnahme-Auftragsschritte  
**Alles auswählen**  
Markiert den Text des Befehls.  
  
**Kopieren**  
Kopiert den markierten Text.  
  
**Einfügen**  
Fügt die Inhalte aus der Zwischenablage ein.  
  
## <a name="options-for-replication-transaction-log-reader-job-steps"></a>Optionen für Auftragsschritte des Replikationstransaktionsprotokoll-Lesers  
**Alles auswählen**  
Markiert den Text des Befehls.  
  
**Kopieren**  
Kopiert den markierten Text.  
  
**Einfügen**  
Fügt die Inhalte aus der Zwischenablage ein.  
  
## <a name="options-for-sql-server-analysis-services-command-job-steps"></a>Optionen für Auftragsschritte von SQL Server Analysis Services-Befehlen  
**Server**  
Wählt den Server aus, auf dem der Auftragsschritt ausgeführt wird.  
  
**Öffnen**  
Lädt den Befehl aus einer Datei.  
  
**Alles auswählen**  
Markiert den Text des Befehls.  
  
**Kopieren**  
Kopiert den markierten Text.  
  
**Einfügen**  
Fügt die Inhalte aus der Zwischenablage ein.  
  
## <a name="options-for-sql-server-analysis-services-query-job-steps"></a>Optionen für Auftragsschritte von SQL Server Analysis Services-Abfragen  
**Server**  
Wählt den Server aus, auf dem der Auftragsschritt ausgeführt wird.  
  
**Datenbank**  
Die Datenbank, die für den Auftragsschritt verwendet werden soll.  
  
**Öffnen**  
Lädt den Befehl aus einer Datei.  
  
**Alles auswählen**  
Markiert den Text des Befehls.  
  
**Kopieren**  
Kopiert den markierten Text.  
  
**Einfügen**  
Fügt die Inhalte aus der Zwischenablage ein.  
  
## <a name="options-for-integration-services-package-execution-job-steps"></a>Optionen für Auftragsschritte von Integration Services-Paketausführungen  
  
### <a name="general-tab"></a>Registerkarte Allgemein  
Gibt den Speicherort des [!INCLUDE[ssISnoversion](../../includes/ssisnoversion_md.md)] ([!INCLUDE[ssIS](../../includes/ssis_md.md)])-Pakets an, und welche Authentifizierungsmethode verwendet werden soll. Die folgenden Optionen sind verfügbar, wenn Sie diese Registerkarte auswählen.  
  
**Paketquelle**  
Gibt den Speicherort des [!INCLUDE[ssIS](../../includes/ssis_md.md)] -Pakets an. Wählen Sie einen der folgenden Speicherorte aus:  
  
-   **SQL Server**  
  
-   **File system**  
  
-   **SSIS-Paketspeicher**  
  
**Server**  
Geben Sie den Namen des Servers ein, auf dem das [!INCLUDE[ssIS](../../includes/ssis_md.md)] -Paket gespeichert ist. Diese Option ist nur verfügbar, wenn **SQL Server** oder **SSIS-Paketspeicher** für **Paketquelle**angegeben ist.  
  
**Windows-Authentifizierung verwenden**  
Für Anmeldungen bei [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] wird die [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows-Authentifizierung verwendet.  
  
**SQL Server-Authentifizierung verwenden**  
Für Anmeldungen an [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] wird die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Authentifizierung verwendet. Wenn diese Authentifizierungsmethode ausgewählt wurde, geben Sie entsprechend **Benutzername** und **Kennwort**ein.  
  
> [!IMPORTANT]  
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Authentifizierung wird aus Gründen der Abwärtskompatibilität bereitgestellt. Aus Sicherheitsgründen sollte möglichst die Windows-Authentifizierung verwendet werden.  
  
**Paket**  
Geben Sie den Speicherort des Pakets ein.  
  
> [!IMPORTANT]  
> Klicken Sie für kennwortgeschützte [!INCLUDE[ssIS](../../includes/ssis_md.md)] -Pakete auf die Registerkarte **Konfigurationen** , um das Kennwort im Dialogfeld **Paketkennwort** einzugeben. Andernfalls erzeugt der Auftrag des [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agents, der das kennwortgeschützte Paket ausführt, einen Fehler.  
  
### <a name="configurations-tab"></a>Registerkarte Konfigurationen  
Gibt Konfigurationsoptionen für das [!INCLUDE[ssIS](../../includes/ssis_md.md)] -Paket an. Wenn Sie diese Registerkarte auswählen, sind die folgenden Optionen verfügbar.  
  
**Konfigurationsdateien**  
Führt die Konfigurationsdateien für das Paket in einer Liste auf.  
  
**Hinzufügen**  
Fügt eine Konfigurationsdatei für das Paket hinzu.  
  
**Entfernen**  
Entfernt eine Konfigurationsdatei für das Paket.  
  
**Nach oben**  
Verschiebt die ausgewählte Konfigurationsdatei nach oben.  
  
**Nach oben**  
Verschiebt die ausgewählte Konfigurationsdatei nach unten.  
  
### <a name="command-files-tab"></a>Registerkarte Befehlsdateien  
Wählt Befehlsdateien für das Paket aus. Befehlsdateien werden entsprechend ihrer Reihenfolge in der Liste verarbeitet. Die folgenden Optionen sind verfügbar, wenn Sie diese Registerkarte auswählen.  
  
**Befehlsdateien**  
Führt die Befehlsdateien für das Paket in einer Liste auf.  
  
**Hinzufügen**  
Fügt eine Befehlsdatei hinzu.  
  
**Entfernen**  
Entfernt die ausgewählte Befehlsdatei.  
  
**Nach oben**  
Verschiebt die ausgewählte Befehlsdatei nach oben.  
  
**Nach oben**  
Verschiebt die ausgewählte Befehlsdatei nach unten.  
  
### <a name="data-sources-tab"></a>Registerkarte Datenquellen  
Zeigt die im Paket angegebenen Datenquellen auf dieser Registerkarte an.  
  
**Verbindungs-Manager**  
Zeigt den Namen der Datenquelle an.  
  
**Description**  
Zeigt die Beschreibung der Datenquelle an.  
  
**Verbindungszeichenfolge**  
Zeigt die Verbindungszeichenfolge für die Datenquelle an.  
  
### <a name="execution-options-tab"></a>Registerkarte Ausführungsoptionen  
Zeigt die Ausführungsoptionen für das Paket auf dieser Registerkarte an oder ändert die Werte.  
  
**Paket bei Überprüfungswarnungen fehlschlagen lassen**  
Wählen Sie diese Option aus, wenn die Paketausführung bei Überprüfungswarnungen fehlschlagen soll.  
  
**Paket ohne Ausführung überprüfen**  
Wählen Sie diese Option für den Auftragsschritt aus, wenn das Paket überprüft, nicht jedoch ausgeführt werden soll.  
  
**Maximale Anzahl von gleichzeitig ausführbaren Dateien**  
Die maximale Anzahl der gleichzeitig ausführbaren Dateien.  
  
**Paketprüfpunkte aktivieren**  
Wählen Sie diese Option für den Auftragsschritt aus, wenn Paketprüfpunkte verwendet werden sollen.  
  
**Prüfpunktdatei**  
Geben Sie den Namen der Prüfpunktdatei des Pakets ein.  
  
**...**  
Sucht nach der Prüfpunktdatei des Pakets.  
  
**Neustartoptionen überschreiben**  
Wenn Sie diese Option auswählen, können Sie für diesen Auftragsschritt Neustartoptionen angeben, die von den im Paket angegebenen Optionen abweichen.  
  
**Neustartoption**  
Wählt die Aktion aus, die bei einem Neustart des Pakets durchgeführt werden soll.  
  
### <a name="logging-tab"></a>Registerkarte Protokollierung  
Zeigt die Protokollanbieter für das Paket auf dieser Registerkarte an oder ändert diese.  
  
**Protokollanbieter**  
Wählt die ClassID für den Protokollanbieter aus.  
  
**Konfigurationszeichenfolge**  
Geben Sie die Konfigurationszeichenfolge für den Protokollanbieter ein.  
  
**Entfernen**  
Entfernt den Protokollanbieter.  
  
### <a name="set-values-tab"></a>Registerkarte Werte festlegen  
Zeigt die Eigenschaftswerte für das Paket auf dieser Registerkarte an oder ändert die Werte.  
  
**Eigenschaftspfad**  
Zeigt einen Pfad für die Eigenschaft an oder ändert diese.  
  
**Wert**  
Zeigt einen Wert für die Eigenschaft an oder ändert diesen.  
  
**Entfernen**  
Entfernt die Eigenschaft.  
  
### <a name="verification-tab"></a>Registerkarte Überprüfung  
Wählt die Überprüfungsoptionen für den Auftragsschritt auf dieser Registerkarte aus.  
  
**Nur signierte Pakete ausführen**  
Führt nur Pakete aus, die signiert wurden. Bei Auswahl dieser Option schlägt der Auftragsschritt fehlt, wenn das Paket nicht signiert ist.  
  
**Paketbuild überprüfen**  
Führt nur Pakete aus, die eine bestimmte Buildnummer besitzen. Bei Auswahl dieser Option schlägt der Auftragsschritt fehl, wenn das Paket nicht die angegebene Buildnummer besitzt.  
  
**Erstellen**  
Geben Sie die Buildnummer des Pakets ein.  
  
**Paket-ID überprüfen**  
Führt nur Pakete aus, die eine bestimmte ID besitzen. Bei Auswahl dieser Option schlägt der Auftragsschritt fehl, wenn das Paket nicht die angegebene ID besitzt.  
  
**Paket-ID**  
Geben Sie die Paket-ID ein.  
  
**Versions-ID überprüfen**  
Führt nur Pakete mit einer bestimmten Versions-ID aus. Bei Auswahl dieser Option schlägt der Auftragsschritt fehl, wenn das Paket nicht die angegebene Versions-ID besitzt.  
  
**Versions-ID**  
Geben Sie die Versions-ID ein.  
  
### <a name="command-line-tab"></a>Registerkarte Befehlszeile  
Gibt die Befehlszeilenoptionen für das Paket an. Wenn Sie diese Registerkarte auswählen, sind die folgenden Optionen verfügbar.  
  
**Die ursprünglichen Optionen wiederherstellen**  
Verwendet die in diesem Dialogfeld festgelegten Befehlszeilenoptionen.  
  
**Befehlszeile manuell bearbeiten**  
Gibt die Optionen im Befehlszeilenfenster an.  
  
**Befehlszeile**  
Geben Sie die für dieses Paket zu verwendenden Befehlszeilenoptionen ein.  
  
## <a name="see-also"></a>Siehe auch  
[Verwalten von Auftragsschritten](../../ssms/agent/manage-job-steps.md)  
[Aufträge des SQL Server-Agents für Pakete](http://msdn.microsoft.com/en-us/ecf7a5f9-b8a7-47f1-9ac0-bac07cb89e31)  
[Verwalten der Replikations-Agents](http://msdn.microsoft.com/en-us/f27186b8-b1b2-4da0-8b2b-91f632c2ab7e)  
  

