---
title: Massenkopierfunktionen | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-extensions-bulk-copy-functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, bulk copy
- bulk copy [ODBC], functions
- ODBC, bulk copy operations
- functions [ODBC]
ms.assetid: 6526b892-1d58-4f55-8335-f09887f6ea02
caps.latest.revision: "41"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5338872437725e4a6b95d78c55cf6995dc10c835
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sql-server-driver-extensions---bulk-copy-functions"></a>SQL Server-Treibererweiterungen - Funktionen zum Massenkopieren
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  ODBC (Open Database Connectivity) ist eine Win32-Anwendungsprogrammierschnittstelle von Microsoft, mit deren Hilfe Anwendungen auf Daten in ODBC-Datenquellen zugreifen. In der Referenz zum ODBC-Treiber von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client sind nicht sämtliche ODBC-Funktionsaufrufe dokumentiert. Es werden nur diejenigen Funktionen besprochen, die über treiberspezifische Parameter verfügen oder ein treiberspezifisches Verhalten zeigen, wenn sie mit dem ODBC-Treiber von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client verwendet werden.  
  
 Der ODBC-Treiber von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Native Client entspricht der Spezifikation für ODBC 3.51. Für eine umfassende Referenz zu ODBC 3.51 Herunterladen der Microsoft Data Access Components SDK aus der [Data Access and Storage Developer Center](http://go.microsoft.com/fwlink?linkid=4173), oder zeigen Sie an der [ODBC Programmer's Reference](http://go.microsoft.com/fwlink/?LinkId=45250) online.  
 
 Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-spezifische API-Erweiterung für Massenkopierfunktionen des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC-Treibers ermöglicht es Clientanwendungen, einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Tabelle auf schnelle Weise Datenzeilen hinzuzufügen bzw. Datenzeilen aus einer Tabelle zu extrahieren.  Bei der Verwendung von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client können Sie die Massenkopierfunktionen (BCP) in SQLNCLI11.LIB und SQLNCLI.H nutzen.  
  
 Eine Anwendung, die BCP-API-Funktionsaufrufe verwendet, sollte mit der Bibliothek (LIB-Datei) verknüpft werden, die mit dem von der Anwendung verwendeten Treiber (DLL-Datei) geliefert wurde. Eine BCP-Anwendung sollte nicht mit mehr als einer Treiberbibliothek verknüpft werden.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
-   [bcp_batch](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-batch.md)  
  
-   [bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md)  
  
-   [bcp_colfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-colfmt.md)  
  
-   [bcp_collen](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-collen.md)  
  
-   [bcp_colptr](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-colptr.md)  
  
-   [bcp_columns](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-columns.md)  
  
-   [bcp_control](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-control.md)  
  
-   [bcp_done](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-done.md)  
  
-   [bcp_exec](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-exec.md)  
  
-   [bcp_getcolfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-getcolfmt.md)  
  
-   [bcp_gettypename](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-gettypename.md)  
  
-   [bcp_init](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-init.md)  
  
-   [bcp_moretext](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md)  
  
-   [bcp_readfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-readfmt.md)  
  
-   [bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md)  
  
-   [bcp_setbulkmode](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-setbulkmode.md)  
  
-   [bcp_setcolfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-setcolfmt.md)  
  
-   [bcp_writefmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-writefmt.md)  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server-Treibererweiterungen](http://msdn.microsoft.com/library/1043bc93-965d-4939-bd1c-21e9d8d3e9ac)   
 [Ausführen von Massenkopiervorgängen &#40; ODBC &#41;](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)  
  
  
