---
title: "DMVs f&#252;r SQL Server-R-Dienste | Microsoft Docs"
ms.custom: ""
ms.date: "11/29/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b3643ea0-d9f3-463f-8ece-572127f32a24
caps.latest.revision: 13
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 12
---
# DMVs f&#252;r SQL Server-R-Dienste

Das Thema umfasst die Katalogsichten und DMVs, die zusammengehören [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)]. 


Weitere Informationen zu erweiterten Ereignissen finden Sie unter [Erweiterte Ereignisse für SQL Server R Services](../../advanced-analytics/r-services/extended-events-for-sql-server-r-services.md).

> [!TIP]
> Das Produktteam hat benutzerdefinierte Berichte bereitgestellt, die Sie verwenden können, um Pakete und R-Services-Sitzungen zu überwachen. Weitere Informationen finden Sie unter [Monitor R Services mithilfe benutzerdefinierter Berichte in Management Studio](../../advanced-analytics/r-services/monitor-r-services-using-custom-reports-in-management-studio.md).
> 

## <a name="system-configuration-and-system-resources"></a>Systemkonfiguration und Systemressourcen

Sie können überwachen und analysieren Sie die Ressourcen, die mithilfe von R-Skripts verwendet [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Katalogsichten und DMVs.


**Allgemein**
+ [ Sys. dm_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)

  Gibt Informationen für benutzerverbindungen und systemsitzungen zurück. Bestimmen Sie die systemsitzungen durch einen Blick auf die *Session_id* Spalte; Werte größer als oder gleich dem 51 werden benutzerverbindungen und Werte, der niedriger als 51 Systemprozesse sind. 



+ [dm_os_performance_counters (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md)

  Gibt eine Zeile für jedes System Leistungsindikator, der vom Server verwendet wird.  Sie können diese Informationen verwenden, um festzustellen, wieviele-Skripts ausgeführt haben, welche Skripts ausgeführt wurden, mit welcher Authentifizierungsmodus oder wie viele R-Aufrufe für die gesamte Instanz ausgegeben wurden.

  In diesem Beispiel wird nur die Leistungsindikatoren, die im Zusammenhang mit R-Skript:

  ```SQL
  SELECT * from sys.dm_os_performance_counters WHERE object_name LIKE '%Extended Scripts%'
  ```

  Die folgenden Leistungsindikatoren werden von dieser DMV für externe Skripts pro Instanz gemeldet:

  + **Gesamtanzahl der Ausführungen**: Anzahl der R-Prozesse gestartet werden, lokal oder remote aufrufen
  + **Parallele Ausführung**: Anzahl der Fälle, in denen ein Skript enthalten die @parallel -Spezifikation und die [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] konnte zum Generieren und Verwenden von einem parallelen Abfrageplan
  + **Streaming Ausführungen**: Anzahl der Fälle, in denen die Medienstreaming-Funktion aufgerufen wurde. 
  + **SQL CC Ausführungen**: Anzahl der R-Skripts ausführen, in dem der Aufruf Remote instanziiert wurde und als computekontext verwendete SQL Server 
  + **Implizite auth. Anmeldungen**: Anzahl der Fälle, in denen eine ODBC-Loopback Puffermethode wurde mit impliziert, Authentifizierung, d. h., die [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] ausgeführt, den Aufruf im Auftrag des Benutzers, der die Skript-Anforderung senden
  + **Gesamtanzahl der Ausführungszeit (ms)**: verstrichene Zeit zwischen dem Aufruf und den Abschluss des Aufrufs.
  + **Fehler bei der Ausführung**: Anzahl der Skripts Fehler gemeldete. Diese Anzahl umfasst nicht die R-Fehler.


+ [dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md)

  Diese DMV gibt eine einzelne Zeile für jedes workerkonto, auf denen derzeit ein externes Skript ausgeführt wird. Beachten Sie, dass dieses workerkonto die Benutzeranmeldeinformationen der Person, die das Skript senden unterscheidet. Wenn ein einzelner Windows-Benutzer mehrere Anforderungen von Skript sendet, würde nur einen Worker-Konto zum Verarbeiten aller Anforderungen von diesem Benutzer zugewiesen werden. Wenn anderer Windows-Benutzer anmeldet, ein externes Skript auszuführen, würde die Anforderung von einem separaten workerkonto verarbeitet werden. 
  Diese DMV gibt keine Ergebnisse zurück, wenn derzeit keine Skripts ausgeführt werden; Daher ist es besonders hilfreich für die lang andauernde Überwachungsskripts. Es gibt folgende Werte zurück:
  + **External_script_request_id**: eine GUID, die auch als temporärer Name des Arbeitsverzeichnisses zum Speichern von Skripts und Zwischenergebnissen verwendet wird.  
  + **Sprache**: ein Wert z. B. `R` Wert, der die Sprache des externen Skripts bezeichnet.
  + **Degree_of_parallelism**: eine ganze Zahl, der angibt, die Anzahl der Parallel verarbeitet werden, die verwendet wurden. 
  + **External_user_name**: ein Konto des Launchpad-Worker, z. B. SQLRUser01. 
  

+ [dm_external_script_execution_stats (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md)

  Diese DMV wird bereitgestellt, für die interne Überwachung (Telemetrie), um nachzuverfolgen, wie viele R-Aufrufe auf eine Instanz ausgeführt werden. Der telemetriedienst beginnt, wenn [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] verfügt und erhöht einen Zähler datenträgerbasierte jedes Mal eine bestimmte R-Funktion wird aufgerufen.

  Pro Aufruf einer Funktion wird erhöht. Wenn `rxLinMod` z. B. parallel aufgerufen und ausgeführt wird, wird der Leistungsindikator um 1 erhöht.
  
  Leistungsindikatoren sind im Allgemeinen nur so lange gültig, wie der Prozess aktiv ist, der sie generiert hat. Daher kann eine Abfrage für eine DMV keine ausführlichen Daten für Dienste anzeigen, die beendet wurden. Angenommen, wenn das Launchpad wird mehrere parallele R-Aufträge erstellt und noch sie sehr schnell ausgeführt und dann durch die Windows-Auftragsobjekt bereinigt werden, eine DMV zeigt möglicherweise keine Daten.
 
  Allerdings bleiben die nachverfolgt werden, indem Sie diese DMV Leistungsindikatoren ausgeführt werden und Status für Dm_external_script _execution Leistungsindikator beibehalten wird, mithilfe von Schreibvorgängen auf den Datenträger, selbst wenn die Instanz heruntergefahren wird.
 
 Weitere Informationen zu verwendeten Systemleistungsindikatoren [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], finden Sie unter [verwenden, SQL Server-Objekten](../../relational-databases/performance-monitor/use-sql-server-objects.md).

**Sichten der Ressourcenkontrolle**

+ [resource_governor_resource_pools](../../relational-databases/system-catalog-views/sys-resource-governor-resource-pools-transact-sql.md)

  Gibt Informationen zum aktuellen Status der Ressourcenpools, zur aktuellen Konfiguration der Ressourcenpools sowie Statistiken zu den Ressourcenpools zurück.

  > [!IMPORTANT]
  > 
  > Sie müssen die Ressourcenpools ändern, die auf andere Serverdienste angewendet werden soll, bevor Sie R Services zusätzliche Ressourcen zuteilen können.


+ [Sys. resource_governor_external_resource_pools](../../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md)

  Eine neue Katalogsicht, die die aktuellen Konfigurationswerte für externen Ressourcenpools anzeigt.
  In der Enterprise Edition verwendet wird, konfigurieren Sie zusätzliche externen Ressourcenpools: beispielsweise könnten, behandeln Ressourcen für R-Aufträge auf [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] getrennt von den, die von einem Remoteclient aus stammen. 

  > [!NOTE]
  > 
  > In der Standard Edition werden alle R-Aufträge in der gleichen externen standardressourcenpool ausgeführt.

+ [resource_governor_workload_groups](../../relational-databases/system-catalog-views/sys-resource-governor-workload-groups-transact-sql.md)

  Gibt Statistiken zu Arbeitsauslastungsgruppen sowie die aktuelle Konfiguration der Arbeitsauslastungsgruppe an. Diese Sicht kann mit sys.dm_resource_governor_resource_pools verknüpft werden, um den Ressourcenpoolnamen abzurufen.
  Für externe Skripts wurde eine neue Spalte hinzugefügt, dass zeigt, dass die Id des externen Pools der Arbeitsauslastungsgruppe zugeordnet. 


+ [Sys. dm_resource_governor_external_resource_pool_affinity](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md)

  Ein neuer Katalog anzuzeigen, können Sie sehen, die Prozessoren und die Ressourcen, die einem bestimmten Ressourcenpool zugeordnet sind.

  Gibt eine Zeile pro Zeitplanungsmodul in [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] zurück, wobei jedes Zeitplanungsmodul einem einzelnen Prozessor zugeordnet ist. Mithilfe dieser Sicht können Sie den Zustand eines Zeitplanungsmoduls überwachen oder Endlostasks identifizieren.

  In der Standardkonfiguration arbeitsauslastungspools automatisch Prozessoren zugewiesen sind, und daher keine Affinitätswerte zurückzugebenden vorhanden sind.

  Die Affinity-Zeitplan ordnet den Ressourcenpool der [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Zeitpläne, die von den angegebenen IDs identifizierten. Diese IDs zuordnen, die Werte in der Scheduler_id-Spalte in DM_OS_SCHEDULERS (Transact-SQL).


> [!NOTE] 
> 
> Obwohl die Möglichkeit zum Konfigurieren und Anpassen von Ressourcenpools nur in Enterprise steht und Developer Edition, die Standard-Adresspools sowie die DMVs in allen Editionen verfügbar sind. Aus diesem Grund können Sie DMVs in der Standard Edition verwenden, um Ressource Caps für Ihre R-Aufträge zu bestimmen. 

Allgemeine Informationen zum Überwachen von [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Instanzen finden Sie unter [Katalogsichten](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md) und [Resource Governor verwandte dynamische Verwaltungssichten](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md).

## <a name="r-script-execution-and-monitoring"></a>Ausführung von R-Skripts und Überwachung

R-Skripts, die in [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] werden gestartet, indem die [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] Schnittstelle. Das Launchpad ist jedoch nicht Ressource kontrolliert oder separat überwacht werden, da angenommen wird, dass ein sicherer Dienst von Microsoft, die Ressourcen entsprechend verwaltet bereitgestellt werden.

Einzelne R-Skripts, die unter den Launchpad-Dienst ausgeführt werden verwaltet, mit der [Windows-Auftragsobjekt](https://msdn.microsoft.com/library/windows/desktop/ms684161.aspx). Ein Auftragsobjekt kann Gruppen von Prozessen an, als eine Einheit verwaltet werden. Einzelnen Auftragsobjekte ist hierarchisch aufgebaut und steuert die Attribute aller Prozesse, die mit ihm verknüpft sind. Vorgänge für ein Auftragsobjekt Auswirkungen auf alle Prozesse, die die Job-Objekt zugeordnet. 

Daher, wenn Sie eine Aufgabe, die einem Objekt zugeordneten beenden müssen, Bedenken Sie, dass alle verknüpften Prozesse wird auch beendet. Wenn Sie ein R-Skript, das ein Windows-Auftragsobjekt zugewiesen ist, und dieses Skript ausgeführt wird, eine verwandte ODBC-Auftrags, der beendet werden muss, wird auch das übergeordnete Element R-Skript-Prozess beendet. 

Wenn Sie ein R-Skript starten, die parallelen Verarbeitung verwendet wird, verwaltet ein einzelnes Windows-Auftragsobjekt alle parallelen untergeordnete Prozesse.

Um festzustellen, ob ein Prozess in einem Auftrag ausgeführt wird, verwenden die `IsProcessInJob` Funktion.

## <a name="see-also"></a>Siehe auch
[Verwaltung und Überwachung](../../advanced-analytics/r-services/managing-and-monitoring-r-solutions.md)

