---
title: ODBC-Cursorbibliothek | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client-odbc-cursors
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- cursors [ODBC], library
- SQL_CUR_USE_DRIVER option
- ODBC applications, cursors
- ODBC cursors, library
- SQL_CUR_USE_IF_NEEDED option
- SQLSetConnectAttr function
- SQL_CUR_USE_ODBC option
ms.assetid: 3c610d3d-6e06-49cf-9a40-05b6a1c83a32
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: e6db6db58a56c9cedb440a362d3e3f58ad0059ba
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="odbc-cursor-library"></a>ODBC-Cursorbibliothek
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  Einige ODBC-Treiber unterstützen nur die Standardeinstellungen für den Cursor. Diese Treiber unterstützen auch keine Vorgänge für positionierte Cursor, wie z. B. **SQLSetPos**. Die ODBC-Cursorbibliothek ist eine Komponente von Microsoft Data Access Components (MDAC), mit der Block- oder statische Cursor in einem Treiber implementiert werden, der sie normalerweise nicht unterstützt. Die Cursorbibliothek implementiert auch positionierte Update- und DELETE-Anweisungen und **SQLSetPos** für die Cursor, die es erstellt.  
  
 Die ODBC-Cursorbibliothek wird als Ebene zwischen dem ODBC-Treiber-Manager und einem ODBC-Treiber implementiert. Wenn die ODBC-Cursorbibliothek geladen ist, leitet der ODBC-Treiber-Manager alle cursorspezifischen Befehle an die Cursorbibliothek statt an den Treiber weiter. Die Cursorbibliothek implementiert einen Cursor durch Abrufen des gesamten Resultsets aus dem zugrunde liegenden Treiber und durch Zwischenspeichern des Resultsets auf dem Client. Bei Verwendung der ODBC-Cursorbibliothek ist die Anwendung auf die Cursorfunktionen der Cursorbibliothek beschränkt. Zusätzliche Cursorfunktionen im zugrunde liegenden Treiber sind für die Anwendung nicht verfügbar.  
  
 Es besteht kaum Bedarf, die ODBC-Cursorbibliothek mit dem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber zu verwenden, da der Treiber selbst mehr Cursorfunktionen unterstützt als die ODBC-Cursorbibliothek. Der einzige Grund für die ODBC-Cursorbibliothek mit verwenden die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber ist, da der Treiber seine cursorunterstützung durch Servercursor implementiert und Servercursor nicht alle SQL-Anweisungen unterstützen. Erwägen Sie die Verwendung der ODBC-Cursorbibliothek, wenn ein statischer Cursor mit gespeicherten Prozeduren, Batches oder SLQ-Anweisungen, die COMPUTE, COMPUTE BY, FOR BROWSE oder INTO enthalten, erforderlich ist. Gehen Sie mit der Cursorbibliothek jedoch sorgfältig um, da sie das gesamte Resultset auf dem Client zwischenspeichert und dadurch viel Speicherplatz belegt und die Leistung beeinträchtigt werden kann.  
  
 Eine Anwendung ruft die Cursorbibliothek Verbindung von Verbindungen mit [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) das SQL_ATTR_ODBC_CURSORS-Verbindungsattribut vor dem Herstellen einer Verbindung mit einer Datenquelle festlegen. SQL_ATTR_ODBC_CURSORS wird auf einen von drei Werten festgelegt:  
  
 SQL_CUR_USE_ODBC  
 Wenn diese Option festgelegt ist, mit der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber die ODBC-Cursorbibliothek überschreibt die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] systemeigene cursorunterstützung Native Client ODBC-Treiber. Für die Verbindung können nur von der Cursorbibliothek unterstützte Cursortypen verwendet werden. Servercursor können nicht verwendet werden.  
  
 SQL_CUR_USE_DRIVER  
 Wenn diese Option festgelegt ist, unterstützt alle des Cursors vom einheitlichen Modus zum die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber für die Verbindung verwendet werden kann. Die ODBC-Cursorbibliothek kann nicht verwendet werden. Alle Cursor werden als Servercursor implementiert.  
  
 SQL_CUR_USE_IF_NEEDED  
 Wenn diese Option festgelegt ist, der Effekt ist derselbe wie SQL_CUR_USE_DRIVER bei Verwendung mit der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber. Zum Zeitpunkt des Verbindungsaufbaus testet der ODBC-Treiber-Manager um festzustellen, ob der ODBC-Treiber eine Verbindung hergestellt wird, die SQL_FETCH_PRIOR-Option von unterstützt [SQLFetchScroll](../../../relational-databases/native-client-odbc-api/sqlfetchscroll.md). Wenn der Treiber die Option nicht unterstützt, lädt der ODBC-Treiber-Manager die ODBC-Cursorbibliothek. Unterstützt der Treiber die Option, so lädt der ODBC-Treiber-Manager die ODBC-Cursorbibliothek nicht und die Anwendung verwendet die systemeigene Unterstützung des Treibers. Da die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber SQL_FETCH_PRIOR unterstützt, die ODBC-Treiber-Manager wird nicht die ODBC-Cursorbibliothek geladen.  
  
 Die Cursorbibliothek ermöglicht Anwendungen, mehrere aktive Anwendungen für eine Verbindung sowie bildlauffähige und aktualisierbare Cursor zu verwenden. Die Cursorbibliothek muss geladen sein, damit diese Funktion unterstützt wird. Verwendung [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) angeben, wie die Cursorbibliothek verwendet werden soll und [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) die Cursor-Typ, Parallelitäts- und Rowset Größe fest.  
  
## <a name="see-also"></a>Siehe auch  
 [Implementieren von Cursorn](../../../relational-databases/native-client-odbc-cursors/implementation/how-cursors-are-implemented.md)  
  
  
