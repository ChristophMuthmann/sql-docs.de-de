---
title: Anzeigen des SQL Server-Agent-Fehlerprotokolls (SQL Server Management Studio) | Microsoft-Dokumentation
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-agent
ms.reviewer: 
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- logs [SQL Server], SQL Server Agent
- viewing SQL Server Agent error logs
- displaying SQL Server Agent error logs
- SQL Server Agent, errors
- errors [SQL Server Agent]
ms.assetid: de920425-fa44-469f-b83d-49e3f97e97f4
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: e34811ab5bdff948a59bcf69a7abc1f7d5b8827c
ms.sourcegitcommit: d8ab09ad99e9ec30875076acee2ed303d61049b7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/23/2018
---
# <a name="view-sql-server-agent-error-log-sql-server-management-studio"></a>View SQL Server Agent Error Log (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
In diesem Thema wird das Anzeigen des  [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Fehlerprotokolls in [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]beschrieben.  
  
Im Protokolldatei-Viewer können Protokollinformationen aus einer Vielzahl von Komponenten angezeigt werden. Wählen Sie im geöffneten Protokolldatei-Viewer im Bereich **Protokolle auswählen** die Protokolle aus, die angezeigt werden sollen. In jedem Protokoll werden dem Protokolltyp entsprechende Spalten angezeigt. Welche Protokolle verfügbar sind, ist davon abhängig, wie der Protokolldatei-Viewer geöffnet wird.  
  
**In diesem Thema**  
  
-   **Vorbereitungen:**  
  
    [Einschränkungen](#Restrictions)  
  
    [Security](#Security)  
  
-   [So zeigen Sie ein SQL Server-Agent-Fehlerprotokoll mithilfe von SQL Server Management Studio an](#SSMSProcedure)  
  
## <a name="BeforeYouBegin"></a>Vorbereitungen  
  
### <a name="Restrictions"></a>Einschränkungen  
Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Knoten wird nur im Objekt-Explorer angezeigt, wenn Sie die Berechtigung besitzen, ihn zu verwenden.  
  
### <a name="Security"></a>Security  
  
#### <a name="Permissions"></a>Berechtigungen  
Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent muss zur Verwendung der Anmeldeinformationen eines Kontos konfiguriert werden, das Mitglied der festen Serverrolle **sysadmin** in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]ist, um seine Funktionen ausführen zu können. Das Konto muss über die folgenden Windows-Berechtigungen verfügen:  
  
-   Anmelden als Dienst (SeServiceLogonRight)  
  
-   Ersetzen von Token auf Prozessebene (SeAssignPrimaryTokenPrivilege)  
  
-   Umgehen von durchsuchenden Prüfungen (SeChangeNotifyPrivilege)  
  
-   Anpassen des Arbeitsspeicherkontingents für einen Prozess (SeIncreaseQuotaPrivilege)  
  
Weitere Informationen zu den Windows-Berechtigungen, die für das [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Dienstkonto erforderlich sind, finden Sie unter [Auswählen eines Kontos für den SQL Server-Agent-Dienst](../../ssms/agent/select-an-account-for-the-sql-server-agent-service.md) und [Einrichten von Windows-Dienstkonten](http://msdn.microsoft.com/en-us/309b9dac-0b3a-4617-85ef-c4519ce9d014).  
  
## <a name="SSMSProcedure"></a>Verwenden von SQL Server Management Studio  
  
#### <a name="to-view-the-includessnoversionincludesssnoversionmdmd-agent-error-log"></a>So zeigen Sie das [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Fehlerprotokoll an  
  
1.  Klicken Sie im **Objekt-Explorer**auf das Pluszeichen, um den Server zu erweitern, der das [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Fehlerprotokoll enthält, das Sie anzeigen möchten.  
  
2.  Klicken Sie auf das Pluszeichen, um **SQL Server-Agent**zu erweitern.  
  
3.  Klicken Sie auf das Pluszeichen, um den Ordner **Fehlerprotokolle** zu erweitern.  
  
4.  Klicken Sie mit der rechten Maustaste auf das Fehlerprotokoll, das Sie anzeigen möchten, und wählen Sie **Agentprotokoll anzeigen**aus.  
  
    Die folgenden Optionen sind im Dialogfeld **Protokolldatei-Viewer >***Servername* verfügbar:  
  
    **Protokoll laden**  
    Öffnen Sie ein Dialogfeld, in dem Sie eine zu ladende Protokolldatei angeben können.  
  
    **Exportieren**  
    Öffnen Sie ein Dialogfeld, in dem Sie die im Raster **Protokolldateizusammenfassung** angezeigten Informationen in eine Textdatei exportieren können.  
  
    **Aktualisieren**  
    Aktualisieren Sie die Anzeige der ausgewählten Protokolle. Beim Übernehmen von Filtereinstellungen werden mithilfe der Schaltfläche **Aktualisieren** die ausgewählten Protokolle erneut vom Zielserver gelesen.  
  
    **Filter**  
    Öffnen Sie ein Dialogfeld, in dem Sie zum Filtern der Protokolldatei verwendete Einstellungen angeben können, z.B. Filterkriterien wie **Verbindung**, **Datum**oder **Allgemein** .  
  
    **Suchen**  
    Durchsuchen Sie die Protokolldatei nach bestimmtem Text. Das Suchen mit Platzhalterzeichen wird nicht unterstützt.  
  
    **Beenden**  
    Beendet das Laden der Protokolldateieinträge. Diese Option können Sie z. B. verwenden, wenn das Laden einer Remote- oder Offline-Protokolldatei eine lange Zeit in Anspruch nimmt und Sie nur die zuletzt erstellten Einträge anzeigen möchten.  
  
    **Protokolldateizusammenfassung**  
    In diesem Informationsbereich wird eine Zusammenfassung der Protokolldateifilterung angezeigt. Wenn die Datei nicht gefiltert wurde, wird folgender Text angezeigt: **Kein Filter angewendet**. Nach Anwendung eines Filters auf das Protokoll wird folgender Text angezeigt: **Protokolleinträge auf diesen Fall filtern:** <filter criteria>.  
  
    **Details für die ausgewählte Zeile**  
    Wählen Sie eine Zahl aus, um am unteren Rand der Seite zusätzliche Details zu der ausgewählten Ereigniszeile anzuzeigen. Die Spalten können durch Ziehen an neue Positionen im Raster neu angeordnet werden. Die Breite der Spalten kann durch Ziehen der Spaltentrennbalken in der Kopfzeile des Rasters nach links oder rechts geändert werden. Wenn Sie auf die Spaltentrennbalken in der Kopfzeile des Rasters doppelklicken, wird die Breite der Spalte automatisch an die Breite des Inhalts angepasst.  
  
    **Instanz**  
    Der Name der Instanz, bei der das Ereignis aufgetreten ist. Dieser wird im Format *Computername*\\*Instanzname*.  
  
    **Datum**  
    Zeigt das Datum des Ereignisses an.  
  
    **Quelle**  
    Zeigt die Ausgangsfunktion an, mit dem das Ereignis erstellt wurde, z. B. den Namen des Diensts (z. B. MSSQLSERVER). Dies wird nicht für alle Protokolltypen angezeigt.  
  
    **MessageBox**  
    Zeigt die Meldungen an, die dem Ereignis zugeordnet sind.  
  
    **Protokolltyp**  
    Zeigt den Typ des Protokolls an, zu dem das Ereignis gehört. Alle ausgewählten Protokolle werden im Fenster für die Protokolldateizusammenfassung angezeigt.  
  
    **Protokollquelle**  
    Zeigt eine Beschreibung des Quellprotokolls an, in dem das Ereignis aufgezeichnet wird.  
  
5.  Wenn Sie fertig sind, klicken Sie auf **Schließen**.  
  
