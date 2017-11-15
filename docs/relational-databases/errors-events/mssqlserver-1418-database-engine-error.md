---
title: MSSQLSERVER_1418 | Microsoft-Dokumentation
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 1418 (Database Engine error)
ms.assetid: 6e9c7241-0201-44e0-9f8b-b3c4e293f0f6
caps.latest.revision: "24"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: af047f866172b233fd18f803eb67e9f77da1ae43
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver1418"></a>MSSQLSERVER_1418
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|Ereignis-ID|1418|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|DBM_PARTNERNOTFOUND|  
|Meldungstext|Die Server-Netzwerkadresse "%.*ls" ist nicht erreichbar oder nicht vorhanden. Überprüfen Sie den Namen der Netzwerkadresse, und dass die Ports für die lokalen und Remoteendpunkte betriebsbereit sind.|  
  
## <a name="explanation"></a>Erklärung  
Der Endpunkt des Servernetzwerks hat nicht reagiert, da die angegebene Server-Netzwerkadresse nicht erreichbar oder nicht vorhanden ist.  
  
> [!NOTE]  
> Standardmäßig blockiert das [!INCLUDE[msCoName](../../includes/msconame-md.md)]-Betriebssystem alle Ports.  
  
## <a name="user-action"></a>Benutzeraktion  
Überprüfen Sie den Namen der Netzwerkadresse, und führen Sie den Befehl erneut aus.  
  
Möglicherweise sind korrigierende Maßnahmen auf beiden Partnern erforderlich. Wird beispielsweise diese Fehlermeldung beim Ausführen der SET PARTNER-Anweisung auf der Prinzipalserverinstanz ausgelöst, wird mit der Meldung der Eindruck erweckt, die Ausführung korrigierender Maßnahmen auf der Spiegelserverinstanz wäre ausreichend. Möglicherweise sind jedoch korrigierende Maßnahmen auf beiden Partnern erforderlich.  
  
### <a name="additional-corrective-actions"></a>Zusätzliche korrigierende Maßnahmen  
  
-   Stellen Sie sicher, dass die Spiegeldatenbank für die Spiegelung bereit ist.  
  
-   Stellen Sie sicher, dass der Name und der Port der Spiegelserverinstanz richtig sind.  
  
-   Stellen Sie sicher, dass sich die Ziel-Spiegelserverinstanz nicht hinter einer Firewall befindet.  
  
-   Stellen Sie sicher, dass sich die Prinzipalserverinstanz nicht hinter einer Firewall befindet.  
  
-   Stellen Sie mithilfe der **state**- oder **state_desc**-Spalte in der **sys.database_mirroring_endpoints**-Katalogsicht sicher, dass die Endpunkte auf den Partnern gestartet wurden. Wurde einer der Endpunkte nicht gestartet, führen Sie zum Starten eine ALTER ENDPOINT-Anweisung aus.  
  
-   Stellen Sie sicher, dass die Prinzipalserverinstanz am Port lauscht, der dem Endpunkt der Datenbankspiegelung zugewiesen wurde, und dass die Spiegelserverinstanz an ihrem Port lauscht. Weitere Informationen finden Sie im Abschnitt zum Überprüfen der Verfügbarkeit von Ports weiter unten in diesem Thema. Lauscht einer der Partner an den ihm zugewiesenen Port nicht, ändern Sie den Endpunkt der Datenbankspiegelung so, dass er an einen anderen Port lauscht.  
  
    > [!IMPORTANT]  
    > Fehlerhaft konfigurierte Sicherheit kann zu einem allgemeinen Setupfehler führen. In der Regel löscht die Serverinstanz einfach die fehlerhafte Verbindungsanforderung, ohne zu reagieren. Für den Aufrufer könnte der Eindruck entstehen, dass ein Sicherheitskonfigurationsfehler aufgrund einer Vielzahl anderer Gründe aufgetreten ist, wie z. B. einer nicht vorhandenen Spiegeldatenbank oder aufgrund des mangelhaften Zustands der Datenbank oder unzureichender Berechtigungen usw.  
  
### <a name="using-the-error-log-file-for-diagnosis"></a>Verwenden der Fehlerprotokolldatei für die Diagnose  
In einigen Fällen kann die Ursache nur anhand der Fehlerprotokolldateien untersucht werden. Ermitteln Sie in diesen Fällen, ob im Fehlerprotokoll die Fehlermeldung 26023 für den TCP-Port des Endpunkts für die Datenbankspiegelung enthalten ist. Dieser Fehler mit Schweregrad 16 kann darauf hinweisen, dass der Endpunkt der Datenbankspiegelung nicht gestartet wurde. Diese Meldung kann auch dann ausgegeben werden, wenn **sys.database_mirroring_endpoints** den Status des Endpunkts als STARTED anzeigt.  
  
Nach dem Beheben möglicher Probleme versuchen Sie erneut, die Anweisung ALTER DATABASE *Datenbank_Name* SET PARTNER auf dem Prinzipalserver auszuführen.  
  
### <a name="verifying-port-availability"></a>Überprüfen der Verfügbarkeit von Ports  
Stellen Sie beim Konfigurieren des Netzwerks für eine Datenbankspiegelungssitzung sicher, dass der Endpunkt der Datenbankspiegelung der einzelnen Serverinstanzen nur vom Datenbankspiegelungsprozess verwendet wird. Wenn an dem einem Datenbank-Spiegelungsendpunkt zugeordneten Port von einem anderen Prozess gelauscht wird, können die Datenbankspiegelungsprozesse der anderen Serverinstanzen keine Verbindung mit dem Endpunkt herstellen.  
  
Mithilfe des Eingabeaufforderungs-Hilfsprogramms **netstat** können Sie alle Ports anzeigen, die ein Windows-basierten Server überwacht. Die **netstat**-Syntax ist von der Version des Windows-Betriebssystems abhängig. Weitere Informationen finden Sie in der Dokumentation zum Betriebssystem.  
  
#### <a name="windows-server-2003-service-pack-1-sp1"></a>Windows Server 2003 Service Pack 1 (SP1)  
Geben Sie an der Windows-Eingabeaufforderung den folgenden Befehl ein, um eine Liste der Ports, an denen gelauscht wird, sowie der Prozesse anzuzeigen, die diese Ports geöffnet haben:  
  
**netstat -abn**  
  
#### <a name="windows-server-2003-pre-sp1"></a>Windows Server 2003 (vor SP1)  
Gehen Sie zum Identifizieren der Ports, an denen gelauscht wird sowie der Prozesse, die diese Ports geöffnet haben, folgendermaßen vor:  
  
1.  Rufen Sie die Prozess-ID ab.  
  
    Die Prozess-ID einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] können Sie ermitteln, indem Sie eine Verbindung mit der Instanz herstellen und die folgende [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung verwenden:  
  
    ```  
    SELECT SERVERPROPERTY('ProcessID')   
    ```  
  
    Weitere Informationen finden Sie unter "SERVERPROPERTY (Transact-SQL)" in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Onlinedokumentation.  
  
2.  Gleichen Sie die Prozess-ID mit der Ausgabe des folgenden **netstat**-Befehls ab:  
  
    **netstat -ano**  
  
## <a name="see-also"></a>Siehe auch  
[ALTER ENDPOINT &#40;Transact-SQL&#41;](~/t-sql/statements/alter-endpoint-transact-sql.md)  
[Der Datenbankspiegelungs-Endpunkt &#40;SQL Server&#41;](~/database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)  
[Vorbereiten einer Spiegeldatenbank auf die Spiegelung &#40;SQL Server&#41;](~/database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md)  
[SERVERPROPERTY &#40;Transact-SQL&#41;](~/t-sql/functions/serverproperty-transact-sql.md)  
[Angeben einer Servernetzwerkadresse &#40;Datenbankspiegelung&#41;](~/database-engine/database-mirroring/specify-a-server-network-address-database-mirroring.md)  
[sys.database_mirroring_endpoints &#40;Transact-SQL&#41;](~/relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql.md)  
[Problembehandlung für die Datenbankspiegelungskonfiguration &#40;SQL Server&#41;](~/database-engine/database-mirroring/troubleshoot-database-mirroring-configuration-sql-server.md)  
  
