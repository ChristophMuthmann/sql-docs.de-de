---
title: Verwendung von OLE DB-Treiber für SQLServer | Microsoft Docs
description: Verwendung von OLE DB-Treiber für SQL Server
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb
ms.reviewer: ''
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server
- MSOLEDBSQL, about OLE DB Driver for SQL Server
- data access [OLE DB Driver for SQL Server], about OLE DB Driver for SQL Server
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: cf64d680b0d45bf7b46ba5d07df8a291723bb0cb
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/30/2018
---
# <a name="when-to-use-ole-db-driver-for-sql-server"></a>Verwendung von OLE DB-Treiber für SQLServer
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  OLE DB-Treiber für SQL Server ist eine Technologie, die Sie verwenden können, Zugriff auf Daten in einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Datenbank.  Eine Erläuterung der verschiedenen datenzugriffstechnologien, finden Sie unter [Data Access Technologies Road Map](http://go.microsoft.com/fwlink/?LinkID=179186)  
  
 Bei der Entscheidung, ob OLE DB-Treiber für SQL Server als datenzugriffstechnologie in Ihrer Anwendung verwendet, sollten Sie die verschiedenen Faktoren ab.  
  
 Wenn Sie neue Anwendungen in einer verwalteten Programmiersprache wie Microsoft Visual C# oder Visual Basic schreiben und auf die neuen Funktionen, die in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eingeführt wurden, zugreifen müssen, sollten Sie den .NET Framework-Datenanbieter für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwenden, der Teil von .NET Framework ist.  
  
 Wenn Sie eine COM-basierte Anwendung entwickeln und auf die neuen Funktionen zugreifen müssen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], sollten Sie OLE DB-Treiber für SQL Server verwenden. Wenn Sie nicht auf die neuen Funktionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zugreifen müssen, können Sie weiterhin Windows Data Access Components (WDAC) verwenden.  
  
 Bei vorhandenen OLE DB-Anwendungen ist ausschlaggebend, ob Sie Zugriff auf die neuen Funktionen müssen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Wenn Sie eine ausgereifte Anwendung haben, die nicht auf die neuen Funktionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zugreifen muss, können Sie weiterhin WDAC verwenden. Aber wenn Sie benötigen diese neuen Features wie z. B. den Zugriff auf die [Xml-Datentyp](../../t-sql/xml/xml-transact-sql.md), sollten Sie OLE DB-Treiber für SQL Server verwenden.  
  
 Beide OLE DB-Treiber für SQL Server auch MDAC unterstützen lesen committed-Transaktionsisolation mit zeilenversionsverwaltung, aber nur OLE DB-Treiber für SQL Server unterstützt die Momentaufnahmen-Transaktionsisolation. (Programmiertechnisch ausgedrückt ist read committed-Transaktionsisolation mit zeilenversionsverwaltung Read Committed-Transaktion identisch.)  
  
 Informationen zu den Unterschieden zwischen OLE DB-Treiber für SQL Server und MDAC finden Sie unter [Aktualisieren von einer Anwendung auf OLE DB-Treiber für SQL Server von MDAC](../oledb/applications/updating-an-application-to-oledb-driver-for-sql-server-from-mdac.md).  
  
## <a name="see-also"></a>Siehe auch  
 [OLE DB-Treiber für SQL Server-Programmierung](../oledb/oledb-driver-for-sql-server-programming.md)     
 [OLE DB-Themen zur Vorgehensweise](../oledb/ole-db-how-to/ole-db-how-to-topics.md)  
  
  
