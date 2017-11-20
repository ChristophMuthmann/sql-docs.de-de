---
title: "Remote Blob Store (RBS) und Always On-Verfügbarkeitsgruppen (SQL Server) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 05/17/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: availability-groups
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 01a70258-d4fd-40bc-bc44-c490b5d6c420
caps.latest.revision: 15
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: e6b39d1e5bda9e7426b92611df9f0ac0dfa3a495
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="remote-blob-store-rbs-and-always-on-availability-groups-sql-server"></a>Remote Blob Store (RBS) und Always On-Verfügbarkeitsgruppen (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] kann eine Lösung für hohe Verfügbarkeit und Notfallwiederherstellung für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)][Remote Blob Store (RBS)](../../../relational-databases/blob/remote-blob-store-rbs-sql-server.md) -BLOB-Objekte (BLOBs) bereitstellen. [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] schützt alle in einer Verfügbarkeitsdatenbank gespeicherten RBS-Metadaten und -Schemas, indem sie an die sekundären Replikate repliziert werden. Dabei handelt es sich um die SharePoint-Inhaltsdatenbank. Im Allgemeinen speichert [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] diese RBS-Metadaten unabhängig vom BLOB.  
  
 Der Schutz der RBS-BLOB-Daten hängt vom Speicherort des BLOB-Speichers ab:  
  
|Speicherort des BLOB-Speichers|Können diese BLOB-Daten von Verfügbarkeitsgruppen geschützt werden?|  
|-------------------------|-----------------------------------------------------|  
|Dieselbe Datenbank, in der die (mithilfe eines RBS-FILESTREAM-Anbieters gespeicherten) RBS-Metadaten enthalten sind.|Ja|  
|Eine andere Datenbank in derselben Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (die mithilfe eines RBS-FILESTREAM-Anbieters gespeichert wurde)|Ja<br /><br /> Es empfiehlt sich, diese Datenbank in derselben Verfügbarkeitsgruppe anzulegen wie die Datenbank, in der die RBS-Metadaten enthalten sind.|  
|Eine andere Datenbank in einer anderen Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (die mithilfe eines RBS-FILESTREAM-Anbieters gespeichert wurde)|Ja<br /><br /> Diese Datenbank muss in einer separaten Verfügbarkeitsgruppe enthalten sein.|  
|Ein BLOB-Speicher eines Drittanbieters|Nein<br /><br /> Um diese BLOB-Daten zu schützen, verwenden Sie die Hochverfügbarkeitsmechanismen des BLOB-Speicheranbieters.|  
  
##  <a name="Limitations"></a> Einschränkungen  
  
-   Für RBS-Maintainer muss das primäre Replikat als Ziel angegeben werden.  
  
##  <a name="Recommendations"></a> Empfehlungen  
  
-   Verwenden Sie einen Verfügbarkeitsgruppenlistener. Weitere Informationen finden Sie unter [Verfügbarkeitsgruppenlistener, Clientkonnektivität und Anwendungsfailover &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md)wichtig sind.  
  
##  <a name="RelatedContent"></a> Verwandte Inhalte  
  
-   [Wartung von Remote BLOB-Speicher](http://msdn.microsoft.com/library/gg316773\(SQL.105\).aspx) (in der [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] -Onlinedokumentation)  
  
-   [Ausführen des RBS-Maintainers](http://blogs.msdn.com/b/sqlrbs/archive/2010/03/19/running-rbs-maintainer.aspx) (Blog)  
  
-   [Konfigurieren von Remote BLOB Storage (RBS) mit dem FILESTREAM-Anbieter (SharePoint 2010)](http://blogs.msdn.com/b/mvpawardprogram/archive/2012/04/02/configure-remote-blob-storage-rbs-with-the-filestream-provider-sharepoint-2010.aspx) (Blog)  
  
## <a name="see-also"></a>Siehe auch  
 [Always On-Clientkonnektivität &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-client-connectivity-sql-server.md)   
 [Remoteblobspeicher &#40;RBS&#41; &#40;SQL Server&#41;](../../../relational-databases/blob/remote-blob-store-rbs-sql-server.md)  
  
  

