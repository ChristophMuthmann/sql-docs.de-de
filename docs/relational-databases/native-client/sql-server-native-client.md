---
title: SQL Server Native Client | Microsoft Docs
ms.date: 04/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client
ms.reviewer: 
ms.suite: sql
ms.custom: 
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e4d4fe39-0090-42a7-8405-6378370d11cb
caps.latest.revision: "43"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 2efcd738e4f5e1047f5d265ea063e90a7cdb8de8
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sql-server-native-client"></a>SQL Server Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

SNAC oder SQL Server Native Client ist ein Begriff, der Synonym zum Verweisen auf ODBC und OLE DB-Treiber für SQL Server verwendet wurde. 

**Weitere Informationen und die SNAC oder ODBC-Treiber herunterzuladen, besuchen Sie [SNAC-Lebenszyklus erklärt](https://blogs.msdn.microsoft.com/sqlreleaseservices/snac-lifecycle-explained/).**

Weitere Informationen zu ODBC-Treiber für SQL Server, finden Sie unter [Microsoft ODBC Driver for SQL Server on Windows](https://msdn.microsoft.com/library/jj730314(v=sql.110).aspx).  Siehe auch [Einführung in die neue Microsoft ODBC-Treiber für SQL Server](https://blogs.msdn.microsoft.com/sqlnativeclient/2013/01/23/introducing-the-new-microsoft-odbc-drivers-for-sql-server/), und [ODBC Driver 13.1 for SQL Server freigegeben](https://blogs.technet.microsoft.com/dataplatforminsider/2016/08/03/odbc-driver-13-1-for-sql-server-released/).  
  
 Informationen zu den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client-Funktionen mit veröffentlicht [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], die letzte verfügbare Version von SQL Server native Client: 
  
-   [SQL Server Native Client-Unterstützung für LocalDB](../../relational-databases/native-client/features/sql-server-native-client-support-for-localdb.md)  
  
-   [Metadatenermittlung](../../relational-databases/native-client/features/metadata-discovery.md)  
  
-   [Unterstützung für UTF-16 in SQL Server Native Client 11.0](../../relational-databases/native-client/features/utf-16-support-in-sql-server-native-client-11-0.md)  
  
-   [SQL Server Native Client-Unterstützung für hohe Verfügbarkeit, Notfallwiederherstellung](../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)  
  
-   [Zugreifen auf Diagnoseinformationen im Protokoll der erweiterten Ereignisse](../../relational-databases/native-client/features/accessing-diagnostic-information-in-the-extended-events-log.md)  
  
ODBC im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client unterstützt drei Funktionen, die im SDK für Windows 7 ODBC-Standardfunktionalität hinzugefügt wurden:  
  
-   Asynchrone Ausführung von Vorgängen mit Verbindungen. Weitere Informationen finden Sie unter [asynchrone Ausführung](http://go.microsoft.com/fwlink/?LinkID=191493).  
  
-   Erweiterbarkeit von C-Datentypen. Weitere Informationen finden Sie unter [C-Datentypen in ODBC](http://go.microsoft.com/fwlink/?LinkID=191495).  
  
     Zur Unterstützung dieser Funktion in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client SQLGetDescField kann zurückgeben **SQL_C_SS_TIME2** (für **Zeit** Typen) oder **SQL_C_SS_TIMESTAMPOFFSET** (für **"DateTimeOffset"**) anstelle von **SQL_C_BINARY**, wenn die Anwendung ODBC 3.8 verwendet. Weitere Informationen finden Sie unter [Datentypunterstützung für ODBC-Datum und Uhrzeit-Verbesserungen](../../relational-databases/native-client-odbc-date-time/data-type-support-for-odbc-date-and-time-improvements.md).  
  
-   Aufrufen von **SQLGetData** mit einem kleinen Puffer mehrere Male auf, um einen großen Parameterwert abzurufen. Weitere Informationen finden Sie unter [Abrufen von Ausgabeparametern mit SQLGetData](http://go.microsoft.com/fwlink/?LinkID=191494).  
  
 In den folgenden Themen werden Änderungen des Verhaltens von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client in [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] beschrieben.  
  
-   Beim Aufrufen von **ICommandWithParameters:: SetParameterInfo**, der an übergebene Wert den *PwszName* Parameter muss ein gültiger Bezeichner sein. Weitere Informationen finden Sie unter [ICommandWithParameters](../../relational-databases/native-client-ole-db-interfaces/icommandwithparameters.md).  
  
-   **SQLDescribeParam** gibt stets einen ODBC-Spezifikation übereinstimmenden Wert zurück. Weitere Informationen finden Sie unter [SQLDescribeParam](../../relational-databases/native-client-odbc-api/sqldescribeparam.md).  
  
-   [Verhaltensänderungen des ODBC-Treibers bei der Behandlung von Zeichenkonvertierungen](../../relational-databases/native-client/features/odbc-driver-behavior-change-when-handling-character-conversions.md)  
  
## <a name="see-also"></a>Siehe auch  
[Installieren Sie SQL Server Native Client](../../relational-databases/native-client/applications/installing-sql-server-native-client.md)  
 [SQL Server Native Client-Features](../../relational-databases/native-client/features/sql-server-native-client-features.md)  
  
  
