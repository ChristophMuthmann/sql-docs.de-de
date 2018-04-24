---
title: Master-Datenbank - Parallel Data Warehouse | Microsoft Docs
description: Erfahren Sie, bis der master-Datenbank in Parallel Data Warehouse.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: bf07b9c27e08a49cb0866b177a0ec37fed4528a0
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/19/2018
---
# <a name="master-database---parallel-data-warehouse"></a>Master-Datenbank - Parallel Data Warehouse
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
  
