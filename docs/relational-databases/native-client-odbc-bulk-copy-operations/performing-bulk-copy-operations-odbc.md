---
title: "Durchführen von Massenkopiervorgängen (ODBC) | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-bulk-copy-operations
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, bulk copy
- bulk copy [ODBC]
- ODBC, bulk copy operations
- minimally logged operations [SQL Server Native Client]
- bulk copy [ODBC], about bulk copy
ms.assetid: 5c793405-487c-4f52-88b8-0091d529afb3
caps.latest.revision: "38"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d2756cf41ac8b33fb542b37faa75b603b0783228
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="performing-bulk-copy-operations-odbc"></a>Durchführen von Massenkopiervorgängen (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Der ODBC-Standard unterstützt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Massenkopiervorgänge nicht direkt. Wenn der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Version 7.0 oder höher verbunden ist, unterstützt er die DB-Library-Funktionen, die die Massenkopiervorgänge in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] durchführen. Diese treiberspezifische Erweiterung stellt eine einfache Möglichkeit dar, bestehende DB-Library-Anwendungen zu aktualisieren, die Funktionen zum Massenkopieren verwenden. Die spezialisierte Unterstützung für Massenkopiervorgänge befindet sich in den folgenden Dateien:  
  
-   sqlncli.h  
  
     Enthält Funktionsprototypen und Konstantendefinitionen für Funktionen zum Massenkopieren. sqlncli.h muss in der ODBC-Anwendung, die Massenkopiervorgänge ausführt, enthalten sein und im Includepfad der Anwendung angegeben werden, wenn die Anwendung kompiliert wird.  
  
-   sqlncli11.lib  
  
     Muss im Bibliothekspfad des Linkers enthalten sein und als zu verknüpfende Datei angegeben werden. sqlncli11.lib wird zusammen mit dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client-ODBC-Treiber bereitgestellt.  
  
-   sqlncli11.dll  
  
     Muss zur Ausführungszeit verfügbar sein. sqlncli11.dll wird zusammen mit den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber.  
  
> [!NOTE]  
>  Die ODBC **SQLBulkOperations** Funktion hat keine Beziehung zu den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Massenkopierfunktionen. Anwendungen müssen die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-spezifischen Massenkopierfunktionen verwenden, um Massenkopiervorgänge durchzuführen.  
  
## <a name="minimally-logging-bulk-copies"></a>Minimales Protokollieren von Massenkopiervorgängen  
 Beim vollständigen Wiederherstellungsmodell werden alle beim Massenladen ausgeführten Vorgänge für das Einfügen von Zeilen vollständig im Transaktionsprotokoll protokolliert. Bei umfangreichen Datenladevorgängen kann dies dazu führen, dass das Transaktionsprotokoll schnell aufgefüllt wird. Unter bestimmten Umständen ist die minimale Protokollierung möglich. Bei der minimalen Protokollierung wird das Risiko verkleinert, dass ein Massenladevorgang das Protokoll auffüllt. Außerdem ist sie effizienter als die vollständige Protokollierung.  
  
 Informationen zur Verwendung der minimalen Protokollierung finden Sie unter [Prerequisites for Minimal Logging in Bulk Import](../../relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import.md).  
  
## <a name="remarks"></a>Hinweise  
 Bei der Verwendung von bcp.exe in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] oder höher erhalten Sie unter Umständen Fehler in Situationen, die in Versionen vor [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] keine Fehler hervorriefen. Das liegt daran, dass bcp.exe in höheren Versionen keine implizite Datentypkonvertierung mehr vornimmt. Vor [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] wurden numerische Daten von bcp.exe in den money-Datentyp konvertiert, wenn die Zieltabelle einen money-Datentyp aufwies. Allerdings wurden in dieser Situation zusätzliche Felder von bcp.exe einfach abgeschnitten. Ab [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] gibt bcp.exe einen Fehler aus, wenn die Datentypen von Datei und Zieltabelle nicht übereinstimmen, und dadurch Daten abgeschnitten werden müssten, um in die Zieltabelle zu passen. Um diesen Fehler zu beheben, korrigieren Sie die Daten so, dass sie zum Zieldatentyp passen. Optional können Sie die Datei bcp.exe aus einer Version vor [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] verwenden.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
-   [Verwenden von Datendateien und Formatdateien](../../relational-databases/native-client-odbc-bulk-copy-operations/using-data-files-and-format-files.md)  
  
-   [Massenkopieren aus Programmvariablen](../../relational-databases/native-client-odbc-bulk-copy-operations/bulk-copying-from-program-variables.md)  
  
-   [Verwalten von Batchgrößen für das Massenkopieren](../../relational-databases/native-client-odbc-bulk-copy-operations/managing-bulk-copy-batch-sizes.md)  
  
-   [Massenkopieren von Text- und Bilddaten](../../relational-databases/native-client-odbc-bulk-copy-operations/bulk-copying-text-and-image-data.md)  
  
-   [Konvertieren von DB-Library-Programmen zum Massenkopieren in ODBC-Programme](../../relational-databases/native-client-odbc-bulk-copy-operations/converting-from-db-library-to-odbc-bulk-copy.md)  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server Native Client &#40; ODBC &#41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)   
 [Massenimport und -export von Daten &#40;SQL Server&#41;](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)  
  
  
