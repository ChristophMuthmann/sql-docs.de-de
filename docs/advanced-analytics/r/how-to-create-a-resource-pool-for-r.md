---
title: "Vorgehensweise: Erstellen eines Ressourcenpools für R | Microsoft-Dokumentation"
ms.custom: 
ms.date: 10/17/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c7f7f6e4-774d-4b45-b94a-f06c51718475
caps.latest.revision: 19
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: be3afb3a1ff5175fbb3d0735cde59bd19bb47f6c
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="how-to-create-a-resource-pool-for-r"></a>Vorgehensweise: Erstellen eines Ressourcenpools für R
  In diesem Thema wird beschrieben, wie Sie einen Ressourcenpool speziell für die Verwaltung von R-Arbeitslasten in [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]. Es wird vorausgesetzt, dass Sie R Services (In-Database) bereits installiert haben und die [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]-Instanz neu konfigurieren möchten, um eine differenziertere Verwaltung der von R verwendeten Ressourcen zu unterstützen.  
  
 Weitere Informationen zum Verwalten von Serverressourcen, finden Sie unter [Resource Governor (Ressourcenkontrolle)](../../relational-databases/resource-governor/resource-governor.md) und [Resource Governor Related Dynamic Management Views &#40;Transact-SQL&#41; (Dynamische Verwaltungssichten im Zusammenhang mit der Ressourcenkontrolle)](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md).  
  
 **Schritte**  
  
1.  Überprüfen Sie den Status der vorhandenen Ressourcenpools.  
  
2.  Ändern Sie die Serverressourcenpools.  
  
3.  Erstellen Sie einen neuen Ressourcenpools für externe Prozesse.  
  
4.  Erstellen Sie eine Klassifizierungsfunktion, um R-Anforderungen zu identifizieren.  
  
5.  Stellen Sie sicher, dass der neue externe Ressourcenpool R-Aufträge erfasst.  
  
##  <a name="bkmk_ReviewStatus"></a>Überprüfen des Status der vorhandenen Ressourcenpools  
  
1.  Überprüfen Sie zunächst die Ressourcen, die dem Standardpool für den Server zugeordnet sind.  
  
    ```  
    SELECT * FROM sys.resource_governor_resource_pools WHERE name = 'default'  
    ```  
     **Ergebnisse**

    |pool_id|name|min_cpu_percent|max_cpu_percent|min_memory_percent|max_memory_percent|cap_cpu_percent|min_iops_per_volume|max_iops_per_volume|  
    |-|-|-|-|-|-|-|-|-|  
    |2|default|0|100|0|100|100|0|0|  

2.  Überprüfen Sie die Ressourcen, die dem **externen** Standardressourcenpool zugeordnet sind.  
  
    ```  
    SELECT * FROM sys.resource_governor_external_resource_pools WHERE name = 'default'  
    ```  
     
    **Ergebnisse**

    |external_pool_id|name|max_cpu_percent|max_memory_percent|max_processes|version|  
    |-|-|-|-|-|-|  
    |2|default|100|20|0|2|  
 
3.  Angesichts dieser Serverstandardeinstellungen wird die R-Laufzeit wahrscheinlich nicht über ausreichend Ressourcen verfügen, um die meisten Aufgaben abzuschließen. Um dies zu ändern, müssen Sie die Nutzung der Serverressourcen wie folgt ändern:  
  
    -   Reduzieren des maximalen Arbeitsspeichers, der von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet werden kann  
  
    -   Erhöhen des maximalen Arbeitsspeichers, der vom externen Prozess verwendet werden kann  
  
## <a name="modify-server-resource-usage"></a>Ändern der Nutzung von Serverressourcen  
  
1.  Führen Sie in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] folgende Anweisung aus, um die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Arbeitsspeicherauslastung auf **60%** des Werts in der Einstellung „max Server Memory“ zu begrenzen.  
  
    ```  
    ALTER RESOURCE POOL "default" WITH (max_memory_percent = 60);  
    ```  
  
2.  Führen Sie analog dazu die folgende Anweisung aus, um die Verwendung des Arbeitsspeichers durch externe Prozesse auf **40%** der gesamten Computerressourcen zu begrenzen.  
  
    ```  
    ALTER EXTERNAL RESOURCE POOL "default" WITH (max_memory_percent = 40);  
    ```  
  
3.  Um diese Änderung zu erzwingen, müssen Sie die Ressourcenkontrolle wie folgt neu konfigurieren und neu starten:  
  
    ```  
    ALTER RESOURCE GOVERNOR reconfigure;  
    ```  
  
    > [!NOTE]  
    >  Dies sind lediglich empfohlene Einstellungen, mit denen Sie beginnen können. Sie sollten die R-Anforderungen jedoch anhand anderer Serverprozesse bewerten, um das richtige Gleichgewicht für Ihre Umgebung und Arbeitslast bestimmen zu können.  
  
## <a name="create-a-user-defined-external-resource-pool"></a>Erstellen eines benutzerdefinierten externen Ressourcenpools  
  
1.  Jede Änderung an der Konfiguration der Ressourcenkontrolle betrifft den Server als Ganzes und wirkt sich auf Arbeitslasten aus, die die Standardpools für den Server verwenden, sowie auf Arbeitslasten, die die externen Pools verwenden.  
  
     Um eine präzisere Kontrolle bereitzustellen, bei der Arbeitslasten Vorrang haben, können Sie einen neuen benutzerdefinierten externen Ressourcenpool erstellen. Sie sollten zudem auch eine Klassifizierungsfunktion definieren und sie dem externen Ressourcenpool zuweisen.  
  
     Erstellen Sie zunächst einen neuen *benutzerdefinierten externen Ressourcenpool*. Im folgenden Beispiel erhält der Pool den Namen **ds_ep**.  
  
    ```  
    CREATE EXTERNAL RESOURCE POOL ds_ep WITH (max_memory_percent = 40);  
    ```  
  
     Beachten Sie das neue **EXTERNE** Schlüsselwort.  
  
2.  Erstellen Sie eine Arbeitsauslastungsgruppe mit dem Namen `ds_wg`, die Sie für die Verwaltung von Sitzungsanforderungen verwenden. Verwenden Sie für SQL-Abfragen den Standardpool und für alle externen Prozessabfragen den `ds_ep`-Pool.  
  
    ```  
    CREATE WORKLOAD GROUP ds_wg WITH (importance = medium) USING "default", EXTERNAL "ds_ep";  
    ```  
  
     Anforderungen werden der Standardgruppe zugewiesen, wenn die Anforderung nicht klassifiziert werden kann, oder wenn ein sonstiger Klassifizierungsfehler aufgetreten ist.  
  
     Weitere Informationen finden Sie unter [Resource Governor Workload Group (Arbeitsauslastungsgruppe der Ressourcenkontrolle)](../../relational-databases/resource-governor/resource-governor-workload-group.md) und [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md).  
  
## <a name="create-a-classification-function-for-r"></a>Erstellen einer Klassifizierungsfunktion für R  
  
1.  Eine Klassifizierungsfunktion untersucht eingehenden Aufgaben und bestimmt, ob sie mithilfe des aktuellen Ressourcenpools ausgeführt werden können. Aufgaben, die die Kriterien der Klassifizierungsfunktion nicht erfüllen, werden wieder an den Standardressourcenpool des Servers zurückgewiesen.  
  
     Beginnen Sie, indem Sie angeben, dass eine Classifier-Funktion von der Ressourcenkontrolle verwendet werden soll, um Ressourcenpools zu bestimmen. Sie können einen NULL-Wert als Platzhalter für die Klassifizierungsfunktion zuweisen.  
  
    ```  
    ALTER RESOURCE GOVERNOR WITH (classifier_function = NULL);  
    ALTER RESOURCE GOVERNOR reconfigure;  
    ```  
  
     Weitere Informationen finden Sie unter [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md).  
  
2.  In der Klassifizierungsfunktion für jeden Ressourcenpool definieren Sie den Typ der Anweisung oder der eingehenden Anforderungen, die dem Ressourcenpool zugewiesen werden soll.  
  
     Beispielsweise gibt die folgende Funktion den Namen des Schemas zurück, der dem benutzerdefinierten externen Ressourcenpool zugewiesen wurde, wenn es sich bei der Anwendung, die die Anforderung gesendet wird, um Microsoft R Host oder RStudio handelt. Andernfalls wird der Standardressourcenpool zurückgegeben.  
  
    ```  
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
  
    ```  
    ALTER RESOURCE GOVERNOR WITH  (classifier_function = dbo.is_ds_apps);  
    ALTER RESOURCE GOVERNOR WITH reconfigure;  
    go  
    ```  
  
## <a name="verify-new-resource-pools-and-affinity"></a>Überprüfen des neuen Ressourcenpools und der Affinität  
  
1.  Um sicherzustellen, dass die Änderungen vorgenommen wurden, überprüfen Sie die Konfiguration von des Serverarbeitsspeicher und der CPU jeder Arbeitsauslastungsgruppe, die allen Instanz-Ressourcenpools zugeordnet ist: den Standardpool für den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Server, den Standardressourcenpool für externe Prozesse und den benutzerdefinierten Pool für externe Prozesse.  
  
    ```  
    SELECT * FROM sys.resource_governor_workload_groups;  
    ```  

    **Ergebnisse**

    |group_id|name|importance|request_max_memory_grant_percent|request_max_cpu_time_sec|request_memory_grant_timeout_sec|max_dop|group_max_requests pool_id|pool_idd|external_pool_idd|  
    |-|-|-|-|-|-|-|-|-|-|  
    |1|Interner Pool (internal)|Medium|25|0|0|0|0|1|2|  
    |2|default|Medium|25|0|0|0|0|2|2|  
    |256|ds_wg|Medium|25|0|0|0|0|2|256|  
  
2.  Sie können die neue Katalogsicht [sys.resource_governor_external_resource_pools &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md) verwenden, um alle externen Ressourcenpools anzuzeigen.  
  
    ```  
    SELECT * FROM sys.resource_governor_external_resource_pools;  
    ```  
    **Ergebnisse**
    
    |external_pool_id|name|max_cpu_percent|max_memory_percent|max_processes|version|  
    |-|-|-|-|-|-|  
    |2|default|100|20|0|2|  
    |256|ds_ep|100|40|0|1|  
  
     Weitere Informationen finden Sie unter [Resource Governor Catalog Views &#40;Transact-SQL&#41; (Resource Governor-Katalogsichten (Transact-SQL))](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md).  
  
3.  Die folgende Anweisung gibt Informationen zu den Ressourcen des Computers zurück, die dem externen Ressourcenpool zugeordnet sind.  
  
    ```  
    SELECT * FROM sys.resource_governor_external_resource_pool_affinity;  
    ```  
  
     Da die Pools mit der Affinität „AUTO“ erstellt wurden, wird in diesem Fall keine Informationen angezeigt. Weitere Informationen finden Sie unter [sys.dm_resource_governor_resource_pool_affinity &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pool-affinity-transact-sql.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Resource Governor](../../relational-databases/resource-governor/resource-governor.md)   
 [Resource Governance for R Services (Ressourcenkontrolle für R Services](../../advanced-analytics/r-services/resource-governance-for-r-services.md)  
  
  

