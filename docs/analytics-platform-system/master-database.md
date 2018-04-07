---
title: Master-Datenbank (SQL Server PDW)
author: barbkess
ms.author: barbkess
manager: craigg
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: ''
ms.component: ''
ms.technology: mpp-data-warehouse
ms.custom: ''
ms.date: 01/13/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c71617c0-6689-4f52-81c6-58f4cf7c7377
caps.latest.revision: 8
ms.workload: not set
ms.openlocfilehash: 0031e4720c7fbcf7e60b7e35a59d16ad31a24103
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2018
---
# <a name="master-database"></a>master-Datenbank
Der SQL Server PDW-master-Datenbank speichert Informationen Appliance-Anmeldung sowie der Datenbankkatalog. Es ist eine SQL Server-master-Datenbank, die auf den Knoten "Zugriffssteuerung" befindet. Daher verfügt über sie ähnliche Funktionen in SQL Server PDW als Master für SQL Server bereitstellt.  
  
Weitere Informationen zu den Systemdatenbanken, finden Sie unter [Systemdatenbanken](system-databases.md).  
  
## <a name="limitations-and-restrictions"></a>Einschränkungen  
Die folgende Liste beschreibt die Vorgänge, die für die SQL Server PDW-Masterdatenbank ausgeführt werden können.  
  
Sie *kann nicht:*  
  
-   Führen Sie eine differenzielle Sicherung der Master-Datenbank.  
  
-   Erstellen von Benutzerobjekten in der Masterdatenbank.  
  
-   Ändern Sie die Sortierung der Master-Datenbank.  
  
-   Ändern Sie den Besitzer der Master-Datenbank.  
  
-   Löschen oder Umbenennen von Master.  
  
-   Ändern Sie die Berechtigungen zum Master.  
  
-   Führen Sie **DBCC SHRINKLOG**.  
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
  
|Task|Description|  
|--------|---------------|  
|Erstellen Sie eine vollständige Sicherung der Master-Datenbank.|Beispiel:<br /><br />`BACKUP DATABASE master TO backup_directory;`<br /><br />Weitere Informationen finden Sie unter [BACKUP DATABASE](../t-sql/statements/backup-database-parallel-data-warehouse.md).|  
|Wiederherstellen der master-Datenbank|Verwenden Sie zum Wiederherstellen des master-Datenbank die [Wiederherstellen der Master-Datenbank](restore-the-master-database.md) Seite im Konfigurations-Manager.|  
|Zeigen Sie die Kataloginformationen für die Datenbank an.|`SELECT * FROM master.sys.databases;`|  
|Systemweite Anmelde- und Informationen anzeigen.|`SELECT * FROM master.sys.server_permissions;`<br /><br />`SELECT * FROM master.sys.server_principals;`<br /><br />`SELECT * FROM master.sys.sql_logins;`|  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
