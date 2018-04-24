---
title: PowerShell-Cmdlet für die Migrationsauswertung | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: in-memory-oltp
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 117250d3-9982-47fe-94fd-6f29f6159940
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 7e6f051e918e96e2d7e5c4db951b1b4ea9ed23c7
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="powershell-cmdlet-for-migration-evaluation"></a>PowerShell-Cmdlet für die Migrationsauswertung
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Das Cmdlet Save-SqlMigrationReport ist ein Tool zur Auswertung der Eignung mehrerer Objekte einer SQL Server-Datenbank für die Migration. Derzeit beschränkt es sich noch auf die Auswertung der Migrationseignung von In-Memory-OLTP. Das Cmdlet kann in einer erweiterten Windows PowerShell-Umgebung und in Sqlps ausgeführt werden.  
  
## <a name="syntax"></a>Syntax  
  
```powershell  
Save-SqlMigrationReport [ -MigrationType OLTP ] [ -Server server -Database database [ -Object object_name ] ]  |  [ -InputObject smo_object ] -FolderPath path  
```  
  
#### <a name="parameters"></a>Parameter  
 Die Parameter werden in der folgenden Tabelle erläutert.  
  
|Parameter|Description|  
|----------------|-----------------|  
|MigrationType|Der Typ des Migrationsszenarios, den das Cmdlet überprüft. Derzeit ist der einzige Wert die Standard-OLTP. Optional.|  
|Server|Der Name der SQL Server-Zielinstanz. In der Windows PowerShell-Umgebung obligatorisch, wenn der Parameter -InputObject fehlt. Optional in SQLPS.|  
|Datenbank|Der Name der SQL Server-Zieldatenbank. In der Windows PowerShell-Umgebung obligatorisch, wenn der Parameter -InputObject fehlt. Optional in SQLPS.|  
|Objekt|Der Name des Zieldatenbankobjekts. Kann eine Tabelle oder eine gespeicherte Prozedur sein.|  
|InputObject|Das SMO-Zielobjekt des Cmdlets. In der Windows PowerShell-Umgebung obligatorisch, wenn die Parameter -Server und -Database fehlen. Optional in SQLPS.|  
|FolderPath|Der Ordner, in dem das Cmdlet die generierten Berichte ablegen soll. Erforderlich.|  
  
## <a name="results"></a>Ergebnisse  
 Unter dem durch -FolderPath angegebenen Ordner werden zwei Ordner erstellt: "Tables" und "Stored Procedures". Wenn das Zielobjekt eine Tabelle ist, wird der Bericht zu diesem Objekt im Ordner "Tables" abgelegt. Andernfalls wird es im Ordner "Stored Procedures" abgelegt.  
  
  
