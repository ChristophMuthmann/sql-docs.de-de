---
title: "Gewusst wie: Erstellen eines Ressourcenpools f&#252;r R | Microsoft Docs"
ms.custom: ""
ms.date: "10/17/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c7f7f6e4-774d-4b45-b94a-f06c51718475
caps.latest.revision: 19
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 19
---
# Gewusst wie: Erstellen eines Ressourcenpools f&#252;r R
  In diesem Thema wird beschrieben, wie Sie einen Ressourcenpool speziell für die Verwaltung von R-Arbeitslasten in erstellen können [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]. Es wird vorausgesetzt, dass Sie R-Services (In der Datenbank) bereits installiert haben und neu konfigurieren, um die [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Instanz zur Unterstützung der weitere abgestimmte Verwaltung der Ressourcen von R.  
  
 Weitere Informationen zum Verwalten von Serverressourcen, finden Sie unter [Ressourcenkontrolle](../../relational-databases/resource-governor/resource-governor.md) und [Resource Governor zugehörigen Dynamic Management Views &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md).  
  
 **Schritte**  
  
1.  Überprüfen Sie den Status der vorhandenen Ressourcenpools  
  
2.  Ändern Sie die Server-Ressourcenpools  
  
3.  Erstellen eines neuen Ressourcenpools für externe Prozesse  
  
4.  Erstellen Sie eine Klassifizierungsfunktion, um R-Anforderungen zu identifizieren.  
  
5.  Stellen Sie sicher, dass neue externe Ressourcenpool R-Aufträge erfasst  
  
##  <a name="bkmk_ReviewStatus"></a> Überprüfen Sie den Status der vorhandenen Ressourcenpools  
  
1.  Überprüfen Sie zunächst die Standard-Adresspool für den Server zugeordneten Ressourcen.  
  
    ```  
    SELECT * FROM sys.resource_governor_resource_pools WHERE name = 'default'  
    ```  
     **Ergebnisse**

    |pool_id|name|min_cpu_percent|max_cpu_percent|min_memory_percent|max_memory_percent|cap_cpu_percent|min_iops_per_volume|max_iops_per_volume|  
    |-|-|-|-|-|-|-|-|-|  
    |2|default|0|100|0|100|100|0|0|  

2.  Überprüfen Sie die Ressourcen auf den Standardwert **externe** Ressourcenpool.  
  
    ```  
    SELECT * FROM sys.resource_governor_external_resource_pools WHERE name = 'default'  
    ```  
     
    **Ergebnisse**

    |external_pool_id|name|max_cpu_percent|max_memory_percent|max_processes|version|  
    |-|-|-|-|-|-|  
    |2|default|100|20|0|2|  
 
3.  Diese Server-Standardeinstellungen werden die R-Laufzeit wahrscheinlich nicht über genügend Ressourcen für die meisten Aufgaben verfügen. Um dies zu ändern, müssen Sie die Nutzung von Serverressourcen wie folgt ändern:  
  
    -   Reduzieren der maximale Arbeitsspeicher, die von verwendet werden können [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
    -   Erhöhen der maximalen Arbeitsspeicher, die von der externe Prozess verwendet werden können  
  
## Ändern Sie die Nutzung von Serverressourcen  
  
1.  In [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], führen Sie folgende Anweisung beschränken [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Speicherverwendung auf **60 %** des Werts in der Einstellung 'max Server Memory'.  
  
    ```  
    ALTER RESOURCE POOL "default" WITH (max_memory_percent = 60);  
    ```  
  
2.  Auf ähnliche Weise führen die folgende Anweisung aus, um die Verwendung des Arbeitsspeichers von externen Prozessen zu beschränken **40 %** insgesamt Computerressourcen.  
  
    ```  
    ALTER EXTERNAL RESOURCE POOL "default" WITH (max_memory_percent = 40);  
    ```  
  
3.  Um diese Änderung zu erzwingen, müssen Sie neu konfigurieren und neu starten der Ressourcenkontrolle wie folgt:  
  
    ```  
    ALTER RESOURCE GOVERNOR reconfigure;  
    ```  
  
    > [!NOTE]  
    >  Dies sind nur vorgeschlagene Einstellungen, mit zu starten. Sie sollten die R-Anforderungen für andere Serverprozesse, um das richtige Gleichgewicht für Ihre Umgebung und Arbeitslast festzustellen auswerten.  
  
## Erstellen eines externen Ressourcenpools  
  
1.  Jede Änderung an der Konfiguration der Ressourcenkontrolle auf den Server als Ganzes gelten und wirken sich Arbeitslasten, die die Standard-Adresspools für den Server zu verwenden sowie Arbeitslasten, die die externen Pools zu verwenden.  
  
     Um eine präzisere Kontrolle bereitzustellen, über die Arbeitslasten Vorrang haben sollten, können Sie daher einen neuen benutzerdefinierten externen Ressourcenpool erstellen. Sie sollten auch eine Klassifizierungsfunktion definieren und externen Ressourcenpool zuweisen.  
  
     Zunächst erstellen Sie ein neues *externe Ressourcenpool*. Im folgenden Beispiel wird der Pool namens **Ds_ep**.  
  
    ```  
    CREATE EXTERNAL RESOURCE POOL ds_ep WITH (max_memory_percent = 40);  
    ```  
  
     Beachten Sie die neue **EXTERNE** Schlüsselwort.  
  
2.  Erstellen Sie eine Arbeitsauslastungsgruppe `ds_wg` bei der Verwaltung von sitzungsanforderungen verwenden. SQL-Abfragen verwenden Sie die Standard-Pool; für alle externen Abfragen verwenden die `ds_ep` Pool.  
  
    ```  
    CREATE WORKLOAD GROUP ds_wg WITH (importance = medium) USING "default", EXTERNAL "ds_ep";  
    ```  
  
     Anforderungen werden der Standardgruppe zugewiesen, wenn die Anforderung kann nicht klassifiziert werden, oder wenn es einen beliebigen anderen Klassifizierung Fehler.  
  
     Weitere Informationen finden Sie unter [Arbeitsauslastungsgruppe der Ressourcenkontrolle](../../relational-databases/resource-governor/resource-governor-workload-group.md) und [CREATE WORKLOAD GROUP &#40; Transact-SQL &#41;](../../t-sql/statements/create-workload-group-transact-sql.md).  
  
## Erstellen Sie eine Klassifizierungsfunktion für R  
  
1.  Eine Klassifizierungsfunktion eingehende Aufgaben untersucht und bestimmt, ob die Aufgabe ist, die mit dem aktuellen Ressourcenpool ausgeführt werden können. Aufgaben, die die Kriterien der Klassifizierungsfunktion nicht erfüllen, werden zurück an den Server Standard-Ressourcenpool zugewiesen.  
  
     Beginnen Sie, indem Sie angeben, dass eine Classifier-Funktion von der Ressourcenkontrolle verwendet werden soll-Ressourcenpools bestimmen. Sie können einen NULL-Wert als Platzhalter für die Klassifizierungsfunktion zuweisen.  
  
    ```  
    ALTER RESOURCE GOVERNOR WITH (classifier_function = NULL);  
    ALTER RESOURCE GOVERNOR reconfigure;  
    ```  
  
     Weitere Informationen finden Sie unter [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md).  
  
2.  In der Klassifizierungsfunktion für jeden Ressourcenpool definieren Sie den Typ der-Anweisungen oder eingehende Anforderungen, die dem Ressourcenpool zugewiesen werden soll.  
  
     Beispielsweise gibt die folgende Funktion den Namen des Schemas in den externen Ressourcenpool zugewiesen werden, wenn die Anwendung, die die Anforderung gesendet wird, 'Microsoft R Host' oder 'RStudio'; Andernfalls wird der standardressourcenpool zurückgegeben.  
  
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
  
3.  Wenn die Funktion erstellt wurde, konfigurieren die Ressourcengruppe, um die neue Klassifizierungsfunktion externe Ressource zuweisen, die Sie zuvor definiert.  
  
    ```  
    ALTER RESOURCE GOVERNOR WITH  (classifier_function = dbo.is_ds_apps);  
    ALTER RESOURCE GOVERNOR WITH reconfigure;  
    go  
    ```  
  
## Überprüfen Sie die neuen Ressourcenpools und Affinität  
  
1.  Um sicherzustellen, dass die Änderungen vorgenommen wurden, überprüfen Sie die Konfiguration von Server-Arbeitsspeicher und CPU aller Arbeitsauslastungsgruppen alle Instanz Ressourcenpools zugeordnet: den Standardpool für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Server, dem Standard-Ressourcenpool für externe Prozesse und den benutzerdefinierten Pool für externe Prozesse.  
  
    ```  
    SELECT * FROM sys.resource_governor_workload_groups;  
    ```  

    **Ergebnisse**

    |group_id|name|importance|request_max_memory_grant_percent|request_max_cpu_time_sec|request_memory_grant_timeout_sec|max_dop|GROUP_MAX_REQUESTS pool_id|pool_idd|external_pool_idd|  
    |-|-|-|-|-|-|-|-|-|-|  
    |1|Interner Pool (internal)|Medium|25|0|0|0|0|1|2|  
    |2|default|Medium|25|0|0|0|0|2|2|  
    |256|ds_wg|Medium|25|0|0|0|0|2|256|  
  
2.  Können Sie die neue Katalogansicht [sys.resource_governor_external_resource_pools &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md), um alle externen Ressourcenpools anzuzeigen.  
  
    ```  
    SELECT * FROM sys.resource_governor_external_resource_pools;  
    ```  
    **Ergebnisse**
    
    |external_pool_id|name|max_cpu_percent|max_memory_percent|max_processes|version|  
    |-|-|-|-|-|-|  
    |2|default|100|20|0|2|  
    |256|ds_ep|100|40|0|1|  
  
     Weitere Informationen finden Sie unter [Katalogsichten der Ressourcenkontrolle &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md).  
  
3.  Die folgende Anweisung gibt Informationen zu den Ressourcen des Computers, die zugeordnet werden in den externen Ressourcenpool zurück.  
  
    ```  
    SELECT * FROM sys.resource_governor_external_resource_pool_affinity;  
    ```  
  
     Da die Pools mit der Affinität Auto erstellt wurden, wird in diesem Fall keine Informationen angezeigt. Weitere Informationen finden Sie unter [sys.dm_resource_governor_resource_pool_affinity &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pool-affinity-transact-sql.md).  
  
## Siehe auch  
 [Ressourcenkontrolle](../../relational-databases/resource-governor/resource-governor.md)   
 [Ressourcenkontrolle für R-Dienste](../../advanced-analytics/r-services/resource-governance-for-r-services.md)  
  
  