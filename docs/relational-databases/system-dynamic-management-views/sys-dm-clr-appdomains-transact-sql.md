---
title: dm_clr_appdomains (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_clr_appdomains
- sys.dm_clr_appdomains
- dm_clr_appdomains_TSQL
- sys.dm_clr_appdomains_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_clr_appdomains dynamic management dynamic management view
ms.assetid: 9fe0d4fd-950a-4274-a493-85e776278045
caps.latest.revision: 24
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6f4eca61d0790e394e09ec73f73cb8f3b0062e3b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmclrappdomains-transact-sql"></a>sys.dm_clr_appdomains (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt eine Zeile für jede Anwendungsdomäne auf dem Server zurück. Die Anwendungsdomäne (**AppDomain**) ist ein Konstrukt in der [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] common Language Runtime (CLR, die die Einheit der Isolation für eine Anwendung ist). Verwenden Sie diese Ansicht, verstehen und Behandeln von CLR-integrationsobjekte, die in ausgeführten [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Es stehen mehrere Typen von CLR-Integrationsobjekten für verwaltete Datenbanken zur Verfügung. Allgemeine Informationen zu diesen Objekten finden Sie unter [Erstellen von Datenbankobjekten mit Common Language Runtime (CLR) Integration](../../relational-databases/clr-integration/database-objects/building-database-objects-with-common-language-runtime-clr-integration.md). Wenn diese Objekte ausgeführt werden, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erstellt eine **AppDomain** unter dem sich laden und führen Sie den erforderlichen Code. Die Isolationsstufe für eine **AppDomain** ist eine **AppDomain** pro Datenbank und Besitzer. Alle CLR-Objekte, die ein Benutzer im Besitz sind, also immer ausgeführt, in der gleichen **AppDomain** pro Datenbank (wenn ein Benutzer CLR-Datenbankobjekte in anderen Datenbanken, die CLR-Datenbank, die Objekte in anderen Anwendungsdomänen ausgeführt registriert). Ein **AppDomain** wird nicht zerstört, nachdem der Code die Ausführung beendet. Stattdessen wird sie für die zukünftige Ausführung im Arbeitsspeicher zwischengespeichert. Dies verbessert die Leistung.  
  
 Weitere Informationen finden Sie unter [Anwendungsdomänen](http://go.microsoft.com/fwlink/p/?LinkId=299658).  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**appdomain_address**|**varbinary(8)**|Der Adresse der **AppDomain**. Alle verwalteten Objekte, die im Besitz eines Benutzers immer, in der gleichen geladen werden Datenbank **AppDomain**. Verwenden Sie diese Spalte, um alle derzeit in diesem geladenen Assemblys suchen **AppDomain** in **dm_clr_loaded_assemblies**.|  
|**appdomain_id**|**int**|ID der **AppDomain**. Jede **AppDomain** hat eine eindeutige ID.|  
|**appdomain_name**|**varchar(386)**|Der Name der **AppDomain** , die von zugewiesen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**creation_time**|**datetime**|Uhrzeit der Erstellung der **AppDomain** erstellt wurde. Da **AppDomains** werden zwischengespeichert und wiederverwendet, die für eine bessere Leistung **Creation_time** ist nicht notwendigerweise dem Zeitpunkt, zu der Code ausgeführt wurde.|  
|**db_id**|**int**|ID der Datenbank, in der diese **AppDomain** erstellt wurde. Code, die in zwei verschiedenen Datenbanken gespeichert, kann keine gemeinsame **AppDomain**.|  
|**user_id**|**int**|ID des Benutzers, dessen Objekte können in diesem ausführen **AppDomain**.|  
|**state**|**nvarchar(128)**|Ein Deskriptor für den aktuellen Status von der **AppDomain**. Eine AppDomain kann sich in verschiedenen Zuständen befinden, von Erstellung bis Löschung. Weitere Informationen finden Sie im Abschnitt "Hinweise" in diesem Thema.|  
|**strong_refcount**|**int**|Anzahl der starken Verweise auf **AppDomain**. Dies gibt die Anzahl der derzeit ausgeführten Batches, die dieses wieder **AppDomain**. Beachten Sie, dass die Ausführung dieser Ansicht erstellen, wird eine **strong Refcount**; selbst wenn ist kein Code, der derzeit ausgeführten **Strong_refcount** wird der Wert 1 haben.|  
|**weak_refcount**|**int**|Anzahl der schwachen Verweise auf **AppDomain**. Dies gibt an, wie viele Objekte die **AppDomain** zwischengespeichert werden. Wenn Sie ein verwaltetes Datenbankobjekt ausführen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zwischengespeichert innerhalb der **AppDomain** für die zukünftige Wiederverwendung. Dies verbessert die Leistung.|  
|**cost**|**int**|Der Kosten der **AppDomain**. Je höher die Kosten, desto wahrscheinlicher dies **AppDomain** ist mit ungenügendem Arbeitsspeicher entladen wird. Kosten hängen normalerweise wie viel Arbeitsspeicher erforderlich ist, um das Neuerstellen **AppDomain**.|  
|**value**|**int**|Der Wert der **AppDomain**. Je niedriger der Wert, desto wahrscheinlicher dies **AppDomain** ist mit ungenügendem Arbeitsspeicher entladen wird. Wert in der Regel wie viele Verbindungen oder Batches diese verwenden hängt **AppDomain**.|  
|**total_processor_time_ms**|**bigint**|Gesamtprozessorzeit in Millisekunden, die von allen Threads beim Ausführen in der aktuellen Anwendungsdomäne ab dem Start des Prozesses verwendet wird. Dies entspricht dem **System.AppDomain.MonitoringTotalProcessorTime**.|  
|**total_allocated_memory_kb**|**bigint**|Gesamtgröße, in Kilobyte, aller Speicherbelegungen durch die Anwendungsdomäne seit der Erstellung, ohne Abzug des bei Sammlungsvorgängen freigegebenen Speichers. Dies entspricht dem **System.AppDomain.MonitoringTotalAllocatedMemorySize**.|  
|**survived_memory_kb**|**bigint**|Menge der Daten in KB, die die letzte vollständige Sammlung mit exklusivem Zugriff überdauert haben, und von denen bekannt ist, dass sie von der aktuellen Anwendungsdomäne referenziert werden. Dies entspricht dem **System.AppDomain.MonitoringSurvivedMemorySize**.|  
  
## <a name="remarks"></a>Hinweise  
 Es ist eine 1--Beziehung zwischen **dm_clr_appdomains** und **appdomain_address**.  
  
 Die folgenden Tabellen Liste möglich **Status** Werte, Beschreibungen, und wenn die Zeitpunkte in der **AppDomain** Lebenszyklus. Verwenden Sie diese Informationen zum Lebenszyklus führen eine **AppDomain** und zum Überwachen verdächtiger oder sich wiederholender **AppDomain** Instanzen entladen, ohne dass die Windows-Ereignisprotokoll analysieren.  
  
## <a name="appdomain-initialization"></a>AppDomain-Initialisierung  
  
|Status|Description|  
|-----------|-----------------|  
|E_APPDOMAIN_CREATING|Die **AppDomain** erstellt wird.|  
  
## <a name="appdomain-usage"></a>AppDomain-Verwendung  
  
|Status|Description|  
|-----------|-----------------|  
|E_APPDOMAIN_SHARED|Die Common Language Runtime **AppDomain** ist für die Verwendung durch mehrere Benutzer bereit.|  
|E_APPDOMAIN_SINGLEUSER|Die **AppDomain** ist für die Verwendung in DDL-Vorgänge bereit. Diese unterscheiden sich von E_APPDOMAIN_SHARED, indem im Gegensatz zu DDL-Vorgängen freigegebene AppDomains für die CLR-Integration verwendet werden, . Solche AppDomains werden von anderen gleichzeitigen Vorgängen isoliert.|  
|E_APPDOMAIN_DOOMED|Die **AppDomain** ist geplant, entladen werden, aber es gibt derzeit Threads darin ausgeführt.|  
  
## <a name="appdomain-cleanup"></a>AppDomain-Cleanup  
  
|Status|Description|  
|-----------|-----------------|  
|E_APPDOMAIN_UNLOADING|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] hat angefordert, dass die Common Language Runtime Entladen der **AppDomain**, in der Regel, da die Assembly, die verwalteten Datenbankobjekte enthält, geändert oder gelöscht wurde.|  
|E_APPDOMAIN_UNLOADED|Die CLR entladen hat die **AppDomain**. Dies ist normalerweise das Ergebnis einer ausweitungsprozedur aufgrund **ThreadAbort**, **OutOfMemory**, oder eine nicht behandelte Ausnahme im Benutzercode.|  
|E_APPDOMAIN_ENQUEUE_DESTROY|Die **AppDomain** wurde in CLR entladen, und Festlegen von zerstört werden [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|E_APPDOMAIN_DESTROY|Die **AppDomain** gerade zerstört wird durch [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|E_APPDOMAIN_ZOMBIE|Die **AppDomain** , zerstört wurde von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]jedoch nicht alle Verweise auf die **AppDomain** wurden bereinigt.|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die VIEW SERVER STATE-Berechtigung in der Datenbank.  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel zeigt, wie Sie die Details einer **AppDomain** für eine bestimmte Assembly:  
  
```  
select appdomain_id, creation_time, db_id, user_id, state  
from sys.dm_clr_appdomains a  
where appdomain_address =   
(select appdomain_address   
 from sys.dm_clr_loaded_assemblies  
   where assembly_id = 500);  
```  
  
 Das folgende Beispiel zeigt, wie Sie alle Assemblys in einer bestimmten **AppDomain**:  
  
```  
select a.name, a.assembly_id, a.permission_set_desc, a.is_visible, a.create_date, l.load_time   
from sys.dm_clr_loaded_assemblies as l   
inner join sys.assemblies as a  
on l.assembly_id = a.assembly_id  
where l.appdomain_address =   
(select appdomain_address   
from sys.dm_clr_appdomains  
where appdomain_id = 15);  
```  
  
## <a name="see-also"></a>Siehe auch  
 [sys.dm_clr_loaded_assemblies &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-clr-loaded-assemblies-transact-sql.md)   
 [Common Language Runtime verbundene dynamische Verwaltungssichten &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/common-language-runtime-related-dynamic-management-views-transact-sql.md)  
  
  
