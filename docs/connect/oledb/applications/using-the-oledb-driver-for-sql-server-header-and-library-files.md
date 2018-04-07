---
title: Mithilfe des OLE DB-Treibers für SQL Server-Header und Bibliotheksdateien | Microsoft Docs
description: Mithilfe der OLE DB-Treiber für SQL Server-Header- und-Bibliotheksdateien
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb|applications
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- header files [OLE DB Driver for SQL Server]
- MSOLEDBSQL, header files
- OLE DB, header files
- library files [OLE DB Driver for SQL Server]
- OLE DB Driver for SQL Server, header files
- data access [OLE DB Driver for SQL Server], header files
- data access [OLE DB Driver for SQL Server], library files
- OLE DB Driver for SQL Server, library files
- MSOLEDBSQL, library files
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 932a5c8d272bf975e4931326b96bea495e927a08
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2018
---
# <a name="using-the-ole-db-driver-for-sql-server-header-and-library-files"></a>Mithilfe des OLE DB-Treibers für SQL Server-Header und Bibliotheksdateien
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Der OLE DB-Treiber für SQL Server-Header und Bibliotheksdateien werden installiert, wenn während der Installation der OLE DB-Treiber für SQL Server-SDK-Option ausgewählt ist. Es ist wichtig, beim Entwickeln von Anwendungen alle für die Entwicklung erforderlichen Dateien in die Entwicklungsumgebung zu kopieren. Weitere Informationen zum Installieren und Verteilen von OLE DB-Treiber für SQL Server finden Sie unter [Installieren von OLE DB-Treiber für SQL Server](../../oledb/applications/installing-oledb-driver-for-sql-server.md).  
  
 Der OLE DB-Treiber für SQL Server-Header und Bibliotheksdateien werden an folgendem Speicherort installiert:  
  
 *%Programme%*\Microsoft SQL Server\Client SDK\OLEDB\180\SDK  
  
 Der OLE DB-Treiber für SQL Server-Headerdatei (msoledbsql.h) können OLE DB-Treiber für SQL Server Data Access-Funktionalität hinzufügen, um Ihren benutzerdefinierten Anwendungen verwendet werden. Der OLE DB-Treiber für SQL Server-Headerdatei enthält alle Definitionen, Attribute, Eigenschaften und Schnittstellen, die die neuen Funktionen nutzen, die in eingeführt [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  
  
 Zusätzlich zu den OLE DB-Treiber für SQL Server-Headerdatei ist auch eine msoledbsql.lib Bibliotheksdatei also die Exportbibliothek für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (Bulk Copy Program, BCP)-Funktionen.  
  
 Der OLE DB-Treiber für SQL Server-Headerdatei ist abwärtskompatibel mit der sqloledb.h-Header-Datei mit dem Microsoft Data Access Components (MDAC) verwendet, jedoch weder die CLSIDs für SQLOLEDB (den OLE DB-Anbieter für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in MDAC enthaltenen) oder für Symbole XML-Funktionen (die nicht vom OLE DB-Treiber für SQL Server unterstützt wird).    
  
 OLE DB-Anwendungen, die der OLE DB-Treiber für SQL Server verwenden und müssen nur msoledbsql.h verweisen. Wenn eine Anwendung MDAC (SQLOLEDB) und der OLE DB-Treiber für SQL Server verwendet, kann es sowohl auf sqloledb.h msoledbsql.h verweisen, jedoch muss der Verweis auf sqloledb.h zuerst.  
  
## <a name="using-the-ole-db-driver-for-sql-server-header-file"></a>Mithilfe des OLE DB-Treibers für SQL Server-Headerdatei  
 Um den OLE DB-Treiber für SQL Server-Headerdatei verwenden zu können, müssen Sie verwenden ein **enthalten** Anweisung in Ihrem C-/C++-Code programmieren. In den folgenden Abschnitten wird beschrieben, wie diese OLE DB-Anwendungen ausgeführt werden.  
  
> [!NOTE]  
>  Der OLE DB-Treiber für SQL Server-Header- und-Bibliotheksdateien kann nur kompiliert, die mithilfe von Visual Studio C++ 2012 oder höher sein.  
  
### <a name="ole-db"></a>OLE DB  
 So verwenden den OLE DB-Treiber für SQL Server-Headerdatei in einer OLE DB-Anwendung, die mit den folgenden Programmiercode:  
  
```    
include "msoledbsql.h";  
```  
  
> [!NOTE]  
>  Verfügt die Anwendung eine **enthalten** -Anweisung für sqloledb.h, die **enthalten** -Anweisung für msoledbsql.h muss nach dem sie stammen.  
  
 Verwenden Sie "MSOLEDBSQL" als Zeichenfolge des Anbieternamens, beim Erstellen einer Verbindungs mit einer Datenquelle über OLE DB-Treiber für SQL Server.  

  
## <a name="component-names-and-properties-by-version"></a>Komponentennamen und Eigenschaften nach Version  

|Eigenschaft|OLE DB-Treiber für SQLServer|MDAC|  
|--------|----------------------------|----|   
|OLE DB PROGID|MSOLEDBSQL|SQLOLEDB|  
|OLE DB-Headerdateiname|msoledbsql.h|Sqloledb.h|  
|OLE DB-Anbieter-DLL|msoledbsql.dll|Sqloledb.dll| 
  
  
## <a name="static-linking-and-bcp-functions"></a>Statische Verknüpfung und BCP-Funktionen  
 Wenn eine Anwendung BCP-Funktionen verwendet, muss in der Verbindungszeichenfolge der Treiber mit derselben Version angegeben werden, die mit der für die Anwendungskompilierung verwendeten Headerdatei und Bibliothek ausgeliefert wurde.  
  
 Weitere Informationen finden Sie unter Performing [Durchführen von Massenkopiervorgängen](../../oledb/features/performing-bulk-copy-operations.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen von Anwendungen mit dem OLE DB-Treiber für SQL Server](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
  
  
