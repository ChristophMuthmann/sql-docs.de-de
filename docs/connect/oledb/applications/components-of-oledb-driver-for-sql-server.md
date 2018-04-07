---
title: Komponenten des OLE DB-Treiber für SQLServer | Microsoft Docs
description: Komponenten des OLE DB-Treiber für SQLServer
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
- data access [OLE DB Driver for SQL Server], components
- components [OLE DB Driver for SQL Server]
- MSOLEDBSQL, about OLE DB Driver for SQL Server
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 82a3a0999b2d04b699a7b8b9b0299fefc04628de
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2018
---
# <a name="components-of-ole-db-driver-for-sql-server"></a>Komponenten des OLE DB-Treiber für SQLServer
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  OLE DB-Treiber für SQL Server enthält die folgenden Komponenten:  

|Komponente|Description|  
|---------------|-----------------|  
|msoledbsql.dll|Die Dynamic Link Library (DLL)-Datei, die alle von der OLE DB-Treiber für SQL Server-Funktionen enthält.|  
|msoledbsqlr.rll|Die begleitende Ressourcendatei für den OLE DB-Treiber für SQL Server-Bibliothek.|   
|msoledbsql.h|Der OLE DB-Treiber für SQL Server-Headerdatei, die alle erforderlichen neuen Definitionen enthält erforderlich, um OLE DB-Treiber für SQL Server verwenden. Diese Headerdatei ersetzt die sqloledb.h-Headerdatei.<br /><br /> Hinweis: Sie können msoledbsql.h und sqloledb.h im selben Programm verweisen solange sqloledb.h zuerst definiert wird.|  
|msoledbsql.lib|Die Bibliotheksdatei benötigt für den direkten Aufruf der **Bcp** Hilfsfunktionen, die Teil der OLE DB-Treiber für SQL Server sind.<br /><br /> Hinweis: Wenn Sie die Datei msoledbsql.lib in Ihrem Programmcode verweisen, müssen Sie sicherstellen, dass die Datei msoledbsql.dll ist in Ihrem Systempfad sowie im Systempfad der Benutzer, die Stellen der Anwendung verwenden.|  

## <a name="see-also"></a>Siehe auch  
 [Erstellen von Anwendungen mit dem OLE DB-Treiber für SQL Server](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
