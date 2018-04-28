---
title: Aktualisieren von Daten in SQL Server-Cursor | Microsoft Docs
description: Aktualisieren von Daten in SQL Server-Cursor
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-rowsets
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- updating data [SQL Server]
- isolation levels [SQL Server]
- delayed update mode [OLE DB]
- immediate update mode [OLE DB]
- cursors [OLE DB]
- data updates [SQL Server], OLE DB
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 97c03835408ef89cb3940f951f117640e5b432fe
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="updating-data-in-sql-server-cursors"></a>Aktualisieren von Daten in SQL Server-Cursorn
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Beim Abrufen und Aktualisieren von Daten über [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Cursor, eine OLE DB-Treiber für SQL Server-Consumer-Anwendung gebunden ist, durch die gleichen Überlegungen und Einschränkungen, die für jede andere Clientanwendung gelten.  
  
 Nur Zeilen in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Cursorn nehmen an der gleichzeitigen Datenzugriffssteuerung teil. Wenn der Consumer ein änderbares Rowset anfordert, wird die Parallelitätssteuerung von DBPROP_LOCKMODE kontrolliert. Um die Steuerungsebene für den gleichzeitigen Zugriff zu ändern, legt der Consumer die DBPROP_LOCKMODE-Eigenschaft vor dem Öffnen des Rowsets fest.  
  
 Transaktionsisolationsstufen können zu beträchtlichen Verzögerungen bei der Zeilenpositionierung führen, wenn Transaktionen aufgrund des Designs der Clientanwendung über längere Zeit geöffnet bleiben. Standardmäßig verwendet der OLE DB-Treiber für SQL Server die von DBPROPVAL_TI_READCOMMITTED angegebene Read committed-Isolationsstufe. Der OLE DB-Treiber für SQL Server unterstützt die dirty read-Isolation, wenn die rowsetparallelität schreibgeschützt ist. Daher kann der Consumer in einem änderbaren Rowset eine höhere Isolationsstufe jedoch keine niedrigere Stufe erfolgreich anfordern.  
  
## <a name="immediate-and-delayed-update-modes"></a>Unmittelbarer und verzögerter Updatemodus  
 Im sofortupdatemodus, hat jeder Aufruf von **IRowsetChange:: SetData** bewirkt, dass einen Roundtrip zum der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Wenn der Consumer mehrere Änderungen an einer einzelnen Zeile vornimmt, es ist jedoch effizienter, um alle Änderungen mit einem einzelnen übergeben **SetData** aufrufen.  
  
 Im verzögerten Updatemodus ein Roundtrip zu den [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] für jede Zeile im angegebenen der *cRows* und *RghRows* Parameter des **IRowsetUpdate:: Update**.  
  
 In beiden Modi stellt ein Roundtrip eine separate Transaktion dar, wenn kein Transaktionsobjekt für das Rowset geöffnet ist.  
  
 Wenn Sie verwenden **IRowsetUpdate:: Update**, OLE DB-Treiber für SQL Server versucht, jede angegebene Zeile zu verarbeiten. Ein Fehler aufgrund ungültiger Daten, Längen- oder Statuswerte Werte für jede Zeile wird OLE DB-Treiber für SQL Server-Verarbeitung nicht beendet werden. Es können nur alle oder keine der anderen am Update beteiligten Zeilen geändert werden. Der Consumer muss das zurückgegebene untersuchen *PrgRowStatus* Array Fehler für eine bestimmte Zeile bestimmt, wenn der OLE DB-Treiber für SQL Server DB_S_ERRORSOCCURRED zurückgibt.  
  
 Ein Consumer darf nicht davon ausgehen, dass Zeilen in einer bestimmten Reihenfolge verarbeitet werden. Wenn ein Consumer es erfordert, dass die Verarbeitung von Datenänderungen in mehr als einer Zeile in einer bestimmten Reihenfolge durchgeführt wird, muss der Consumer diese Reihenfolge in der Anwendungslogik festlegen und eine Transaktion öffnen, um den Prozess darin einzuschließen.  
  
## <a name="see-also"></a>Siehe auch  
 [Aktualisieren von Daten in Rowsets](../../oledb/ole-db-rowsets/updating-data-in-rowsets.md)  
  
  
