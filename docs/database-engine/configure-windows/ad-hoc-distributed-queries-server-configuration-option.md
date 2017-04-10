---
title: "Ad Hoc Distributed Queries (Serverkonfigurationsoption) | Microsoft Docs"
ms.custom: ""
ms.date: "03/02/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "OPENROWSET-Funktion, Option "Ad Hoc Distributed Queries""
  - "Ad Hoc Distributed Queries (Option)"
  - "Ad Hoc Distributed Queries"
  - "7415 (Datenbankmodulfehler)"
  - "OPENDATASOURCE-Funktion, Option "Ad Hoc Distributed Queries""
  - "Ad-hoc-Zugriff"
ms.assetid: 5b982015-e196-44c3-83b8-275fb9d769b2
caps.latest.revision: 29
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 29
---
# Ad Hoc Distributed Queries (Serverkonfigurationsoption)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Standardmäßig ist es in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nicht zulässig, dass für verteilte Ad-hoc-Abfragen OPENROWSET und OPENDATASOURCE verwendet werden. Wird diese Option auf 1 festgelegt, ist in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] der Ad-hoc-Zugriff zulässig. Wenn diese Option nicht festgelegt oder auf 0 festgelegt wird, ist in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] kein Ad-hoc-Zugriff zulässig.  
  
 Verteilte Ad-hoc-Abfragen verwenden die OPENROWSET- und OPENDATASOURCE-Funktionen, um eine Verbindung mit Remotedatenquellen herzustellen, die OLE DB verwenden. OPENROWSET und OPENDATASOURCE sollten nur für Verweise auf OLE DB-Datenquellen verwendet werden, auf die selten zugegriffen wird. Definieren Sie einen Verbindungsserver für Datenquellen, auf die mehr als nur wenige Male zugegriffen wird.  
  
> [!IMPORTANT]  
>  Das Aktivieren der Verwendung von Ad-hoc-Namen bedeutet, dass jede authentifizierte Anmeldung an [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf den Anbieter zugreifen kann. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Administratoren sollten diese Funktion für Anbieter aktivieren, auf die von jeder lokalen Anmeldung sicher zugegriffen werden kann.  
  
## Hinweise  
 Der Versuch, eine Ad-hoc-Verbindung ohne die Option **Ad Hoc Distributed Queries** herzustellen, verursacht den folgenden Fehler: Meldung 7415, Ebene 16, Status 1, Zeile 1  
  
 Der Ad-hoc-Zugriff auf den OLE DB-Anbieter 'Microsoft.ACE.OLEDB.12.0' wurde verweigert. Sie müssen auf diesen Anbieter über einen Verbindungsserver zugreifen.  
  
## Beispiele  
 Im folgenden Beispiel werden 'Ad Hoc Distributed Queries' aktiviert und anschließend ein Server mit dem Namen `Seattle1` mithilfe der `OPENROWSET`-Funktion abgefragt.  
  
```  
sp_configure 'show advanced options', 1;  
RECONFIGURE;
GO 
sp_configure 'Ad Hoc Distributed Queries', 1;  
RECONFIGURE;  
GO  
  
SELECT a.*  
FROM OPENROWSET('SQLNCLI', 'Server=Seattle1;Trusted_Connection=yes;',  
     'SELECT GroupName, Name, DepartmentID  
      FROM AdventureWorks2012.HumanResources.Department  
      ORDER BY GroupName, Name') AS a;  
GO  
```  
  
## Siehe auch  
 [Serverkonfigurationsoptionen &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [Verbindungsserver &#40;Datenbankmodul&#41;](../../relational-databases/linked-servers/linked-servers-database-engine.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [OPENDATASOURCE &#40;Transact-SQL&#41;](../../t-sql/functions/opendatasource-transact-sql.md)   
 [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)  
  
  