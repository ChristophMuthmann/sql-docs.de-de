---
title: Arbeiten mit Snapshot-Isolation | Microsoft Docs
description: Arbeiten mit Snapshot-Isolation in OLE DB-Treiber für SQL Server
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb|features
ms.reviewer: ''
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- data access [OLE DB Driver for SQL Server], snapshot isolation
- MSOLEDBSQL, snapshot isolation
- isolation levels [SQL Server], snapshot
- DBPROPSET_SESSION property set
- DBDROPSET_DATASOURCEINFO property set
- snapshot isolation [OLE DB Driver for SQL Server]
- OLE DB Driver for SQL Server, snapshot isolation
- SQLGetInfo function
- concurrency [OLE DB Driver for SQL Server]
- SQLSetConnectAttr function
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c33c9d2f6a12c5e43a5ee47000c4faf33b294002
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/30/2018
---
# <a name="working-with-snapshot-isolation"></a>Arbeiten mit Momentaufnahmeisolation
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  In [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] wurde eine neue Momentaufnahmenisolationsstufe eingeführt, die die Parallelität für OLTP-Anwendungen (Online Transaction Processing, Onlinetransaktionsverarbeitung) verbessern soll. In früheren Versionen von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] basierte die Parallelität ausschließlich auf dem Sperren, was zu Blockierungs- und Deadlockproblemen bei einigen Anwendungen führen konnte. Die Momentaufnahmenisolation hängt von Verbesserungen der Zeilenversionsverwaltung ab und soll die Leistung durch Vermeidung von Leser-/Schreiberblockierungsszenarien erhöhen.  
  
 Transaktionen, die mit der Momentaufnahmenisolation gestartet werden, lesen eine Datenbankmomentaufnahme zu dem Zeitpunkt, an dem die Transaktion gestartet wird. Keysetgesteuerte, dynamische und statische Servercursor innerhalb eines momentaufnahmentransaktionskontexts geöffnet Verhalten sich wie ähnlich wie statische Cursor, die innerhalb serialisierbarer Transaktionen geöffnet waren. Wenn der Cursor, unter geöffnet sind werden die Snapshot-Isolation Level Sperren jedoch nicht implementiert. Diese Tatsache reduzieren, auf dem Server blockiert.  
  
## <a name="ole-db-driver-for-sql-server"></a>OLE DB-Treiber für SQLServer  
 Der OLE DB-Treiber für SQL Server verfügt über Erweiterungen, die eingeführte Momentaufnahmenisolation nutzen [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. Diese Erweiterungen schließen Änderungen an den DBPROPSET_DATASOURCEINFO und DBPROPSET_SESSION-Eigenschaftsgruppen ein.  
  
### <a name="dbpropsetdatasourceinfo"></a>DBPROPSET_DATASOURCEINFO  
 Die DBPROPSET_DATASOURCEINFO-Eigenschaftsgruppe wurde geändert, um anzugeben, dass die Momentaufnahmenisolationsstufe vom hinzugefügten DBPROPVAL_TI_SNAPSHOT-Wert unterstützt wird, der in der DBPROP_SUPPORTEDTXNISOLEVELS-Eigenschaft verwendet wird. Dieser neue Wert gibt an, dass die Momentaufnahmenisolationsstufe unabhängig davon unterstützt wird, ob die Versionsverwaltung für die Datenbank aktiviert ist. In der folgenden Tabelle sind die DBPROP_SUPPORTEDTXNISOLEVELS-Werte aufgeführt:  
  
|Eigenschafts-ID|Description|  
|-----------------|-----------------|  
|DBPROP_SUPPORTEDTXNISOLEVELS|Typ: VT_I4<br /><br /> R/W: Schreibgeschützt<br /><br /> Beschreibung: Eine Bitmaske, die die unterstützten Transaktionsisolationsstufen angibt. Eine Kombination von null oder mehreren der folgenden Werte:<br /><br /> DBPROPVAL_TI_CHAOS<br /><br /> DBPROPVAL_TI_READUNCOMMITTED<br /><br /> DBPROPVAL_TI_BROWSE<br /><br /> DBPROPVAL_TI_CURSORSTABILITY<br /><br /> DBPROPVAL_TI_READCOMMITTED<br /><br /> DBPROPVAL_TI_REPEATABLEREAD<br /><br /> DBPROPVAL_TI_SERIALIZABLE<br /><br /> DBPROPVAL_TI_ISOLATED<br /><br /> DBPROPVAL_TI_SNAPSHOT|  
  
### <a name="dbpropsetsession"></a>DBPROPSET_SESSION  
 Die DBPROPSET_SESSION-Eigenschaftsgruppe wurde geändert, um anzugeben, dass die Momentaufnahmenisolationsstufe vom hinzugefügten DBPROPVAL_TI_SNAPSHOT-Wert unterstützt wird, der in der DBPROP_SESS_AUTOCOMMITISOLEVELS-Eigenschaft verwendet wird. Dieser neue Wert gibt an, dass die Momentaufnahmenisolationsstufe unabhängig davon unterstützt wird, ob die Versionsverwaltung für die Datenbank aktiviert ist. In der folgenden Tabelle sind die DBPROP_SESS_AUTOCOMMITISOLEVELS-Werte aufgeführt:
  
|Eigenschafts-ID|Description|  
|-----------------|-----------------|  
|DBPROP_SESS_AUTOCOMMITISOLEVELS|Typ: VT_I4<br /><br /> R/W: Schreibgeschützt<br /><br /> Beschreibung: Legt eine Bitmaske fest, die die Transaktionsisolationsstufe im Autocommit-Modus angibt. Die Werte, die in dieser Bitmaske festgelegt werden können, sind identisch mit den Werten, die für dbprop_supportedtxnisolevels möglichen Werten festgelegt werden können.|  
  
> [!NOTE]  
>  Der Fehler DB_S_ERRORSOCCURRED oder DB_E_ERRORSOCCURRED tritt auf, wenn DBPROPVAL_TI_SNAPSHOT in Versionen von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] vor [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] festgelegt wird.  
  
 Informationen, wie die Snapshot-Isolation in Transaktionen unterstützt wird, finden Sie unter [unterstützen lokale Transaktionen](../../oledb/ole-db-transactions/supporting-local-transactions.md).  

  
## <a name="see-also"></a>Siehe auch  
 [OLE DB-Treiber für SQL Server-Funktionen](../../oledb/features/oledb-driver-for-sql-server-features.md)    
 [Rowset-Eigenschaften und Verhaltensweisen](../../oledb/ole-db-rowsets/rowset-properties-and-behaviors.md)  
  
  
