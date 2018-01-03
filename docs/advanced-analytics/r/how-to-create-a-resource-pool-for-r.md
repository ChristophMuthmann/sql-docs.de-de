---
title: "Erstellen eines Ressourcenpools für Machine Learning | Microsoft Docs"
ms.custom: 
ms.date: 11/13/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c7f7f6e4-774d-4b45-b94a-f06c51718475
caps.latest.revision: "19"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: f5699ed583f0fd40657f3be5f132b879681a7942
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/20/2017
---
# <a name="create-a-resource-pool-for-machine-learning"></a>Erstellen eines Ressourcenpools für Machine learning

In diesem Thema wird beschrieben, wie Sie einen Ressourcenpool speziell für die Verwaltung von Machine Learning-Arbeitslasten in SQL Server erstellen können. Es wird davon ausgegangen, dass Sie bereits installiert und aktiviert die Machine learning-Funktionen und die Instanz für die Unterstützung von Ressourcen von einem externen Prozess, z. B. R oder Python Weitere differenzierte Management neu konfigurieren möchten.

Der Vorgang umfasst mehrere Schritte:

1.  Überprüfen Sie den Status eines vorhandenen Ressourcenpools. Es ist wichtig zu wissen, welche Dienste auf vorhandene Ressourcen verwendet werden.
2.  Ändern Sie die Server-Ressourcenpools hinzu.
3.  Erstellen Sie einen neuen Ressourcenpool für externe Prozesse.
4.  Erstellen Sie eine Klassifizierungsfunktion, um externe Skripts Anforderungen zu identifizieren.
5.  Stellen Sie sicher, dass die neuen externen Ressourcenpool R oder Python Aufträge aus der angegebenen Clients oder Konten erfasst.

**Gilt für:** [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] [!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)] und [!INCLUDE[sscurrent-md](../../includes/sscurrent-md.md)][!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

##  <a name="bkmk_ReviewStatus"></a>Überprüfen des Status der vorhandenen Ressourcenpools
  
1.  Verwenden Sie eine Anweisung ähnlich der folgenden, um die Ressourcen, die an den Pool "Default" für den Server zu überprüfen.
  
    ```sql
    SELECT * FROM sys.resource_governor_resource_pools WHERE name = 'default'
    ```

    **Beispielergebnisse**

    |pool_id|NAME|min_cpu_percent|max_cpu_percent|min_memory_percent|max_memory_percent|cap_cpu_percent|min_iops_per_volume|max_iops_per_volume|
    |-|-|-|-|-|-|-|-|-|
    |2|default|0|100|0|100|100|0|0|

2.  Überprüfen Sie die Ressourcen, die dem **externen** Standardressourcenpool zugeordnet sind.
  
    ```sql
    SELECT * FROM sys.resource_governor_external_resource_pools WHERE name = 'default'
    ```

    **Beispielergebnisse**

    |external_pool_id|NAME|max_cpu_percent|max_memory_percent|max_processes|version|
    |-|-|-|-|-|-|
    |2|default|100|20|0|2|
 
3.  Diese Standardeinstellungen Server müssen wahrscheinlich nicht genügend Ressourcen für die meisten Aufgaben die externe Common Language Runtime. Um dies zu ändern, müssen Sie die Nutzung der Serverressourcen wie folgt ändern:
  
    -   Reduzieren des maximale Arbeitsspeichers, der vom Datenbankmodul verwendet werden kann.
  
    -   Erhöhen des maximale Arbeitsspeichers, der von der externe Prozess verwendet werden kann.

## <a name="modify-server-resource-usage"></a>Ändern der Nutzung von Serverressourcen

1.  Führen Sie in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] folgende Anweisung aus, um die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Arbeitsspeicherauslastung auf **60%** des Werts in der Einstellung „max Server Memory“ zu begrenzen.

    ```sql
    ALTER RESOURCE POOL "default" WITH (max_memory_percent = 60);
    ```
  
2.  Führen Sie analog dazu die folgende Anweisung aus, um die Verwendung des Arbeitsspeichers durch externe Prozesse auf **40%** der gesamten Computerressourcen zu begrenzen.
  
    ```sql
    ALTER EXTERNAL RESOURCE POOL "default" WITH (max_memory_percent = 40);
    ```
  
3.  Um diese Änderung zu erzwingen, müssen Sie die Ressourcenkontrolle wie folgt neu konfigurieren und neu starten:
  
    ```sql
    ALTER RESOURCE GOVERNOR RECONFIGURE;
    ```
  
    > [!NOTE]
    >  Dies sind nur vorgeschlagene Einstellungen, mit; Sie sollten Ihrer für maschinelles lernen von Aufgaben im Hinblick auf andere Serverprozesse, um zu bestimmen, das richtige Gleichgewicht für Ihre Umgebung und die Arbeitslast ausgewertet werden.

## <a name="create-a-user-defined-external-resource-pool"></a>Erstellen eines benutzerdefinierten externen Ressourcenpools
  
1.  Jede Änderung an der Konfiguration der Ressourcenkontrolle betrifft den Server als Ganzes und wirkt sich auf Arbeitslasten aus, die die Standardpools für den Server verwenden, sowie auf Arbeitslasten, die die externen Pools verwenden.
  
     Um eine präzisere Kontrolle bereitzustellen, bei der Arbeitslasten Vorrang haben, können Sie einen neuen benutzerdefinierten externen Ressourcenpool erstellen. Sie sollten zudem auch eine Klassifizierungsfunktion definieren und sie dem externen Ressourcenpool zuweisen. Die **EXTERNEN** Schlüsselwort ist neu.
  
     Erstellen Sie zunächst einen neuen *benutzerdefinierten externen Ressourcenpool*. Im folgenden Beispiel erhält der Pool den Namen **ds_ep**.
  
    ```sql
    CREATE EXTERNAL RESOURCE POOL ds_ep WITH (max_memory_percent = 40);
    ```

2.  Erstellen Sie eine Arbeitsauslastungsgruppe mit dem Namen `ds_wg`, die Sie für die Verwaltung von Sitzungsanforderungen verwenden. Verwenden Sie für SQL-Abfragen den Standardpool und für alle externen Prozessabfragen den `ds_ep`-Pool.
  
    ```sql
    CREATE WORKLOAD GROUP ds_wg WITH (importance = medium) USING "default", EXTERNAL "ds_ep";
    ```
  
     Anforderungen werden der Standardgruppe zugewiesen, wenn die Anforderung nicht klassifiziert werden kann, oder wenn ein sonstiger Klassifizierungsfehler aufgetreten ist.
  
     Weitere Informationen finden Sie unter [Resource Governor Workload Group (Arbeitsauslastungsgruppe der Ressourcenkontrolle)](../../relational-databases/resource-governor/resource-governor-workload-group.md) und [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md).
  
## <a name="create-a-classification-function-for-machine-learning"></a>Erstellen Sie eine Klassifizierungsfunktion für Machine learning
  
Eine Klassifizierungsfunktion untersucht eingehenden Aufgaben und bestimmt, ob sie mithilfe des aktuellen Ressourcenpools ausgeführt werden können. Aufgaben, die die Kriterien der Klassifizierungsfunktion nicht erfüllen, werden wieder an den Standardressourcenpool des Servers zurückgewiesen.
  
1. Gibt an, dass eine Klassifizierungsfunktion von Resource Governor verwendet werden soll, Ermitteln von Ressourcenpools, um zu beginnen. Sie können Zuweisen einer **null** als Platzhalter für die Klassifizierungsfunktion.
  
    ```sql
    ALTER RESOURCE GOVERNOR WITH (classifier_function = NULL);
    ALTER RESOURCE GOVERNOR RECONFIGURE;
    ```
  
     Weitere Informationen finden Sie unter [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md).
  
2.  Definieren Sie in der Klassifizierungsfunktion zu jedem Ressourcenpool den Typ von Anweisungen oder eingehende Anforderungen, die dem Ressourcenpool zugewiesen werden soll.
  
     Beispielsweise gibt die folgende Funktion den Namen des Schemas zurück, der dem benutzerdefinierten externen Ressourcenpool zugewiesen wurde, wenn es sich bei der Anwendung, die die Anforderung gesendet wird, um Microsoft R Host oder RStudio handelt. Andernfalls wird der Standardressourcenpool zurückgegeben.
  
    ```sql
    USE master
    GO
    CREATE FUNCTION is_ds_apps()
    RETURNS sysname
    WITH schemabinding
    AS
    BEGIN
        IF program_name() in ('Microsoft R Host', 'RStudio') RETURN 'ds_wg';
        RETURN 'default'
        END;
    GO
    ```
  
3.  Konfigurieren Sie nach dem Erstellen der Funktion die Ressourcengruppe, um die neue Klassifizierungsfunktion der externen Ressourcengruppe zuweisen, die Sie zuvor definiert haben.
  
    ```sql
    ALTER RESOURCE GOVERNOR WITH  (classifier_function = dbo.is_ds_apps);
    ALTER RESOURCE GOVERNOR WITH reconfigure;
    GO
    ```

## <a name="verify-new-resource-pools-and-affinity"></a>Überprüfen des neuen Ressourcenpools und der Affinität

Um sicherzustellen, dass die Änderungen vorgenommen wurden, sollten Sie die Konfiguration des Serverarbeitsspeicher und maximalem CPU-aller Arbeitsauslastungsgruppen, die dieser Instanz Ressourcenpools zugeordnet zu überprüfen:

+ der Standardpool für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Server
+ standardressourcenpool für externe Prozesse
+ die benutzerdefinierten Pool für externe Prozesse

1. Führen Sie die folgende Anweisung aus, um alle Arbeitsauslastungsgruppen anzuzeigen:

    ```sql
    SELECT * FROM sys.resource_governor_workload_groups;
    ```

    **Beispielergebnisse**

    |group_id|NAME|importance|request_max_memory_grant_percent|request_max_cpu_time_sec|request_memory_grant_timeout_sec|max_dop|group_max_requests pool_id|pool_idd|external_pool_id|
    |-|-|-|-|-|-|-|-|-|-|
    |1|Interner Pool (internal)|Medium|25|0|0|0|0|1|2|
    |2|default|Medium|25|0|0|0|0|2|2|
    |256|ds_wg|Medium|25|0|0|0|0|2|256|
  
2.  Verwenden Sie die neue Katalogsicht [Sys. resource_governor_external_resource_pools &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md), um alle externen Ressourcenpools anzuzeigen.
  
    ```sql
    SELECT * FROM sys.resource_governor_external_resource_pools;
    ```

    **Beispielergebnisse**
    
    |external_pool_id|NAME|max_cpu_percent|max_memory_percent|max_processes|version|
    |-|-|-|-|-|-|
    |2|default|100|20|0|2|
    |256|ds_ep|100|40|0|1|
  
     Weitere Informationen finden Sie unter [Resource Governor Catalog Views &#40;Transact-SQL&#41; (Resource Governor-Katalogsichten (Transact-SQL))](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md).
  
3.  Führen Sie die folgende Anweisung zum Zurückgeben von Informationen zu den Ressourcen des Computers, die an den externen Ressourcenpool zugeordnet werden, sofern zutreffend:
  
    ```sql
    SELECT * FROM sys.resource_governor_external_resource_pool_affinity;
    ```
  
     Da die Pools mit der Affinität „AUTO“ erstellt wurden, wird in diesem Fall keine Informationen angezeigt. Weitere Informationen finden Sie unter [sys.dm_resource_governor_resource_pool_affinity &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pool-affinity-transact-sql.md).

## <a name="see-also"></a>Siehe auch

Weitere Informationen zum Verwalten von Serverressourcen finden Sie unter:

+  [Ressourcenkontrolle](../../relational-databases/resource-governor/resource-governor.md) 
+ [Die Ressourcenkontrolle in Verbindung mit dynamischen Verwaltungssichten &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md)

Einen Überblick über die Ressourcenkontrolle für den Machine learning finden Sie unter:

+  [Die Ressourcenkontrolle für Machine Learning-Dienste](../../advanced-analytics/r/resource-governance-for-r-services.md)
