---
title: Tabellenwertparameter (OLE DB) | Microsoft Docs
description: Tabellenwertparameter (OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-table-valued-parameters
ms.reviewer: ''
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB, table-valued parameters
- table-valued parameters (OLE DB)
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f8f219346a4ed5ed6e03d6cca707bbf14091df1a
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/30/2018
---
# <a name="table-valued-parameters-ole-db"></a>Tabellenwertparameter (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Dieser Abschnitt beschreibt die Unterstützung für Tabellenwertparameter in OLE DB-Treiber für SQL Server. Übersicht die zusätzliche Übersichtsinformationen finden Sie unter [Table-Valued Parameters &#40;OLE DB-Treiber für SQL Server&#41;](../../oledb/features/table-valued-parameters-oledb-driver-for-sql-server.md). Ein Beispiel finden Sie unter [Tabellenwertparametern &#40;OLE DB-&#41;](../../oledb/ole-db-how-to/use-table-valued-parameters-ole-db.md).  
  
## <a name="remarks"></a>Hinweise  
 Sie können derzeit mehrzeilige Daten an den Server senden, als Parameter an eine Prozedur mit Parametersätzen (der DBPARAMS-Parameter in **ICommand:: Execute**). Bei Parametersätzen muss jedes Element des Satzes in einer separaten Remoteprozeduranforderung (Remote Procedure Call, RPC) an den Server gesendet werden. Tabellenwertparameter stellen eine ähnliche Funktionalität bereit, bieten jedoch eine bessere Integration mit dem Server. Er reduziert die Anzahl der RPC-Anforderungen und setbasierte Vorgänge auf dem Server aktiviert.  
  
 Tabellenwertparameter werden in OLE DB-Treiber für SQL Server als OLE DB unterstützt **Rowset** Objekte. Alle **Rowset** Objekt konnte werden vom Consumer angegebene (d. h. die Clientanwendung mithilfe von OLE DB-Treiber für SQL Server) als Platzhalter für Tabellenwertparameter-Parameter. Tabellenwertparameter werden wie andere [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Parametertypen behandelt. Der OLE DB-Treiber für SQL Server stellt die Erstellung, Discovery-Spezifikation, Bindung und Schemaschnittstellen bereit.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
-   [Tabellenwertparameter-Rowseterstellung](../../oledb/ole-db-table-valued-parameters/table-valued-parameter-rowset-creation.md)  
  
-   [Tabellenwertparameter-Typermittlung](../../oledb/ole-db-table-valued-parameters/table-valued-parameter-type-discovery.md)  
  
-   [Ausführen von Befehlen, die Tabellenwertparameter enthalten](../../oledb/ole-db-table-valued-parameters/executing-commands-containing-table-valued-parameters.md)  
  
-   [Einfügen von Daten in Tabellenwertparameter](../../oledb/ole-db-table-valued-parameters/inserting-data-into-table-valued-parameters.md)  
  
-   [Schemarowsets für OLE DB-Tabellenwertparameter geändert](../../oledb/ole-db-table-valued-parameters/schema-rowsets-changed-for-ole-db-table-valued-parameters.md)  
  
-   [OLE DB-Typunterstützung für Tabellenwertparameter](../../oledb/ole-db-table-valued-parameters/ole-db-table-valued-parameter-type-support.md)  
  
-   [Unterstützung des OLE DB-Tabellenwertparameter-Typ &#40;Methoden&#41;](../../oledb/ole-db-table-valued-parameters/ole-db-table-valued-parameter-type-support-methods.md)  
  
-   [Unterstützung des OLE DB-Tabellenwertparameter-Typ &#40;Eigenschaften&#41;](../../oledb/ole-db-table-valued-parameters/ole-db-table-valued-parameter-type-support-properties.md)  
  
## <a name="see-also"></a>Siehe auch  
 [OLE DB-Treiber für SQLServer &#40;OLE DB&#41;](../../oledb/ole-db/oledb-driver-for-sql-server-ole-db.md)   
 [Verwenden des Table-Valued Parameters &#40; OLE DB &#41;](../../oledb/ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
