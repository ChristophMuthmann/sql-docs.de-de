---
title: "Konfigurieren der Serverkonfigurationsoption &quot;Remote Data Archive&quot; | Microsoft Docs"
ms.custom: ""
ms.date: "03/02/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b5817b5a-f39a-4faf-b11e-a47b54fd9f32
caps.latest.revision: 8
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 8
---
# Konfigurieren der Serverkonfigurationsoption &quot;Remote Data Archive&quot;
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Geben Sie mit der Option **Remotedatenarchiv** an, ob Datenbanken und Tabellen auf dem Server für Stretch aktiviert werden können. Weitere Informationen finden Sie unter [Enable Stretch Database for a database](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md).  
  
 Die Option **Remotedatenarchiv** kann die folgenden Werte enthalten.  
  
|Wert|Beschreibung|  
|-----------|-----------------|  
|0|Datenbanken und Tabellen auf dem Server können nicht für Stretch aktiviert werden.|  
|1|Datenbanken und Tabellen auf dem Server können für Stretch aktiviert werden.|  
  
 Um **sp_configure** auszuführen und den Wert der Option **Remotedatenarchiv** festzulegen, sind sysadmin- oder serveradmin-Berechtigungen erforderlich.  
  
## Beispiel  
 Das folgende Beispiel zeigt zunächst die aktuelle Einstellung der Option **Remotedatenarchiv**. Danach aktiviert das Beispiel die Option **Remotedatenarchiv**, indem ihr Wert auf 1 festgelegt wird.  
  
```  
EXEC sp_configure 'remote data archive';  
GO  
EXEC sp_configure 'remote data archive' , '1';  
GO  
RECONFIGURE;  
GO  
```  
  
 Wenn Sie die Option deaktivieren möchten, legen Sie den Wert auf 0 fest.  
  
## Siehe auch  
 [Aktivieren von Stretch-Datenbank für eine Datenbank](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md)   
 [Stretch-Datenbank](../../sql-server/stretch-database/stretch-database.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  