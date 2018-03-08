---
title: "Ausführen eines Befehls | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-provider
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- commands [SQL Server Native Client]
- OLE DB, executing commands
- sessions [SQL Server Native Client]
- OLE DB extensions for XML
- SQL Server Native Client OLE DB provider, command execution
ms.assetid: bb0b3cbf-fe45-46ba-b2ec-c5a39e3c7081
caps.latest.revision: "40"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 495f632181ec7697c08002684e2f6e77f272d39a
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="executing-a-command"></a>Ausführen eines Befehls
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Nachdem die Verbindung mit einer Datenquelle hergestellt wurde, ruft der Consumer die **IDBCreateSession:: CreateSession** Methode, um eine Sitzung zu erstellen. Die Sitzung fungiert als Befehl, Rowset oder Transaktionsfactory.  
  
 Um direkt mit einzelnen Tabellen oder Indizes arbeiten fordert der Consumer die **IOpenRowset** Schnittstelle. Die **IOpenRowset:: OPENROWSET** -Methode öffnet und gibt ein Rowset, das alle Zeilen aus einer einzelnen Basistabelle oder einem Index enthält.  
  
 Zum Ausführen eines Befehls (z. B. SELECT \* FROM Authors), fordert der Consumer die **IDBCreateCommand** Schnittstelle. Der Consumer kann führen Sie die **IDBCreateCommand:: CreateCommand** Methode, um ein Befehlsobjekt zu erstellen und eine Anforderung für die **ICommandText** Schnittstelle. Die **ICommandText:: SetCommandText** Methode wird verwendet, um den Befehl anzugeben, die ausgeführt werden soll.  
  
 Die **Execute** -Befehl wird verwendet, um den Befehl auszuführen. Bei dem Befehl kann es sich um jede SQL-Anweisung oder jeden Prozedurnamen handeln. Nicht alle Befehle erzeugen ein Resultsetobjekt (Rowset). Befehle, wie z. B. SELECT * FROM Authors, erzeugen ein Resultset.  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen eine SQL Server Native Client OLE DB-Anbieteranwendung](../../relational-databases/native-client-ole-db-provider/creating-a-sql-server-native-client-ole-db-provider-application.md)  
  
  
