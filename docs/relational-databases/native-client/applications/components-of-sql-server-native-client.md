---
title: Komponenten von SQL Server Native Client | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client|applications
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, about SQL Server Native Client ODBC driver
- data access [SQL Server Native Client], components
- components [SQL Server Native Client]
- SQLNCLI, about SQL Server Native Client
ms.assetid: 65f932d5-daa1-4eff-b6df-ee633fcf2a7c
caps.latest.revision: "25"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3148b8910db157a6cc6befe2b742e6d0c0cd1016
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="components-of-sql-server-native-client"></a>Komponenten von SQL Server Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client enthält die folgenden Komponenten:  
  
|Komponente|Description|  
|---------------|-----------------|  
|sqlncli11.dll|Die DLL-Datei (Dynamic-Link Library, DLL), die die gesamte Funktionalität von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client enthält. Dies umfasst auch den [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter und den [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber.|  
|sqlnclir11.rll|Die begleitende Ressourcendatei für die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client-Bibliothek.|   
|sqlncli.h|Die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client-Headerdatei, die alle neuen, zur Verwendung von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client erforderlichen Definitionen enthält. Diese Headerdatei ersetzt die Headerdateien odbcss.h und sqloledb.h.<br /><br /> Hinweis: Sie können nicht auf sqlncli.h und odbcss.h im selben Programm verweisen, aber Sie können sqlncli.h und sqloledb.h im selben Programm verweisen, solange sqloledb.h zuerst definiert wird.|  
|sqlncli11.lib|Die Bibliotheksdatei benötigt für den direkten Aufruf der **Bcp** Hilfsfunktionen, die Teil der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber.<br /><br /> Hinweis: Wenn Sie in Ihrem Programmcode die Datei sqlncli11.lib verweisen, müssen Sie sicherstellen, dass die Datei sqlncli11.dll in Ihrem Systempfad sowie im Systempfad der Benutzer, die Stellen der Anwendung verwenden.|  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen von Anwendungen mit SQL Server Native Client](../../../relational-databases/native-client/applications/building-applications-with-sql-server-native-client.md)  
  
  
