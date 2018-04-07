---
title: Unterstützen lokaler Transaktionen | Microsoft Docs
description: Lokale Transaktionen in OLE DB-Treiber für SQL Server
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-transactions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB, transactions
- autocommit mode
- transactions [OLE DB]
- ITransactionLocal interface
- OLE DB Driver for SQL Server, transactions
- local transactions [OLE DB]
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5076c62a7c6553c0474585960da74af2f392b019
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2018
---
# <a name="supporting-local-transactions"></a>Unterstützen lokaler Transaktionen
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Eine Sitzung begrenzt den Transaktionsbereich für einen OLE DB-Treiber für lokale SQL Server-Transaktion. Wenn bei der Anweisung eines Consumers, der OLE DB-Treiber für SQL Server eine Anforderung an eine verbundene Instanz von übermittelt [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], die Anforderung stellt eine Arbeitseinheit für den OLE DB-Treiber für SQL Server. Lokale Transaktionen umschließen stets eine oder mehrere Arbeitseinheiten auf einen einzelnen OLE DB-Treiber für SQL Server-Sitzung.  
  
 Der Standard OLE DB-Treiber für SQL Server-Autocommit-Modus verwenden, wird eine einzelne Arbeitseinheit als Bereich einer lokalen Transaktion behandelt. Nur eine Einheit nimmt an der lokalen Transaktion teil. Wenn eine Sitzung erstellt wird, beginnt der OLE DB-Treiber für SQL Server eine Transaktion für die Sitzung an. Nach der erfolgreichen Verarbeitung einer Arbeitseinheit wird ein Commit für die Arbeit ausgeführt. Bei Auftreten eines Fehlers wird ein Rollback für den begonnenen Teil der Arbeit ausgeführt, und der Fehler wird dem Consumer gemeldet. In beiden Fällen startet der OLE DB-Treiber für SQL Server eine neue lokale Transaktion für die Sitzung, damit, dass alle Aufgaben innerhalb einer Transaktion durchgeführt wird.  
  
 Der OLE DB-Treiber für SQL Server-Consumer kann eine genauere Kontrolle über die lokalen Transaktionsbereich weiterleiten, mithilfe der **ITransactionLocal** Schnittstelle. Wenn eine consumersitzung eine Transaktion initiiert, alle Arbeitseinheiten der Sitzung zwischen der Transaktion starten, Punkt- und eventuellen **Commit** oder **Abort** Methodenaufrufe werden als unteilbare Einheit behandelt. Der OLE DB-Treiber für SQL Server startet implizit eine Transaktion, wenn Sie dazu aufgefordert werden, vom Consumer. Wenn der Consumer keine Beibehaltung anfordert, kehrt die Sitzung zum Verhalten der übergeordneten Transaktionsebene zurück, in der Regel ist das der Autocommitmodus.  
  
 Der OLE DB-Treiber für SQL Server unterstützt **ITransactionLocal:: StartTransaction** Parameter wie folgt.  
  
|Parameter|Description|  
|---------------|-----------------|  
|*IsoLevel*[in]|Die innerhalb dieser Transaktion zu verwendende Isolationsstufe. In lokalen Transaktionen unterstützt der OLE DB-Treiber für SQL Server Folgendes:<br /><br /> **ISOLATIONLEVEL_UNSPECIFIED**<br /><br /> **ISOLATIONLEVEL_CHAOS**<br /><br /> **ISOLATIONLEVEL_READUNCOMMITTED**<br /><br /> **ISOLATIONLEVEL_READCOMMITTED**<br /><br /> **ISOLATIONLEVEL_REPEATABLEREAD**<br /><br /> **ISOLATIONLEVEL_CURSORSTABILITY**<br /><br /> **ISOLATIONLEVEL_REPEATABLEREAD**<br /><br /> **ISOLATIONLEVEL_SERIALIZABLE**<br /><br /> **ISOLATIONLEVEL_ISOLATED**<br /><br /> **ISOLATIONLEVEL_SNAPSHOT**<br /><br /> <br /><br /> Hinweis: Ab [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], ISOLATIONLEVEL_SNAPSHOT gilt für die *IsoLevel* Argument fest, ob der versionsverwaltung für die Datenbank aktiviert ist. Jedoch tritt ein Fehler auf, wenn der Benutzer versucht, eine Anweisung auszuführen und die Versionsverwaltung nicht aktiviert und/oder die Datenbank nicht schreibgeschützt ist. Darüber hinaus wird der Fehler XACT_E_ISOLATIONLEVEL auftreten, wenn ISOLATIONLEVEL_SNAPSHOT als angegeben wird die *IsoLevel* beim Verbinden mit einer Version von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] vor [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].|  
|*IsoFlags*[in]|Der OLE DB-Treiber für SQL Server gibt einen Fehler für einen anderen Wert als 0 (null) zurück.|  
|*pOtherOptions*[in]|Wenn nicht NULL ist, der OLE DB-Treiber für SQL Server das Optionsobjekt von der Schnittstelle. Der OLE DB-Treiber für SQL Server gibt xact_e_notimeout zurück, wenn die Options-Objekt *UlTimeout* Element ist nicht 0 (null). Der OLE DB-Treiber für SQL Server ignoriert den Wert, der die *SzDescription* Member.|  
|*PulTransactionLevel*[Out]|Wenn nicht NULL ist, der OLE DB-Treiber für SQL Server gibt die Schachtelungsebene der Transaktion.|  
  
 Für lokale Transaktionen implementiert der OLE DB-Treiber für SQL Server **ITransaction:: Abort** Parameter wie folgt.  
  
|Parameter|Description|  
|---------------|-----------------|  
|*PboidReason*[in]|Wird bei Festlegung ignoriert. Kann daher auch NULL sein.|  
|*fRetaining*[in]|Wenn der Wert TRUE lautet, wird eine neue Transaktion implizit für die Sitzung begonnen. Für die Transaktion muss vom Consumer ein Commit ausgeführt werden oder sie muss beendet werden. Bei "false", wird der OLE DB-Treiber für SQL Server für die Sitzung den Autocommit-Modus zurückgesetzt.|  
|*fAsync*[in]|Asynchroner Abbruch wird vom OLE DB-Treiber für SQL Server nicht unterstützt. Der OLE DB-Treiber für SQL Server gibt xact_e_notsupported zurück, wenn der Wert nicht "false" ist.|  
  
 Für lokale Transaktionen implementiert der OLE DB-Treiber für SQL Server **ITransaction:: Commit** Parameter wie folgt.  
  
|Parameter|Description|  
|---------------|-----------------|  
|*fRetaining*[in]|Wenn der Wert TRUE lautet, wird eine neue Transaktion implizit für die Sitzung begonnen. Für die Transaktion muss vom Consumer ein Commit ausgeführt werden oder sie muss beendet werden. Bei "false", wird der OLE DB-Treiber für SQL Server für die Sitzung den Autocommit-Modus zurückgesetzt.|  
|*GrfTC*[in]|Asynchrone Rückkehr und die Phase, die einen zurückgibt, werden vom OLE DB-Treiber für SQL Server nicht unterstützt. Der OLE DB-Treiber für SQL Server gibt xacttc_sync für jeden Wert xact_e_notsupported zurück.|  
|*GrfRM*[in]|Muss den Wert 0 (null) haben.|  
  
 Der OLE DB-Treiber für SQL Server Rowsets in der Sitzung bleiben bei einem lokalen Commit- oder Abbruchvorgang basierend auf den Werten für die Rowseteigenschaften DBPROP_ABORTPRESERVE und dbprop_commitpreserve beibehalten. Standardmäßig sind diese Eigenschaften VARIANT_FALSE und alle OLE DB-Treiber für SQL Server Rowsets in der Sitzung verloren, nach einem Abbruch oder commit-Vorgang.  
  
 Der OLE DB-Treiber für SQL Server implementiert nicht die **ITransactionObject** Schnittstelle. Bei einem Versuch des Consumers, einen Verweis auf die Schnittstelle abzurufen, wird E_NOINTERFACE zurückgegeben.  
  
 Dieses Beispiel verwendet **ITransactionLocal**.  
  
```  
// Interfaces used in the example.  
IDBCreateSession*   pIDBCreateSession   = NULL;  
ITransaction*       pITransaction       = NULL;  
IDBCreateCommand*   pIDBCreateCommand   = NULL;  
IRowset*            pIRowset            = NULL;  
  
HRESULT             hr;  
  
// Get the command creation and local transaction interfaces for the  
// session.  
if (FAILED(hr = pIDBCreateSession->CreateSession(NULL,  
     IID_IDBCreateCommand, (IUnknown**) &pIDBCreateCommand)))  
    {  
    // Process error from session creation. Release any references and  
    // return.  
    }  
  
if (FAILED(hr = pIDBCreateCommand->QueryInterface(IID_ITransactionLocal,  
    (void**) &pITransaction)))  
    {  
    // Process error. Release any references and return.  
    }  
  
// Start the local transaction.  
if (FAILED(hr = ((ITransactionLocal*) pITransaction)->StartTransaction(  
    ISOLATIONLEVEL_REPEATABLEREAD, 0, NULL, NULL)))  
    {  
    // Process error from StartTransaction. Release any references and  
    // return.  
    }  
  
// Get data into a rowset, then update the data. Functions are not  
// illustrated in this example.  
if (FAILED(hr = ExecuteCommand(pIDBCreateCommand, &pIRowset)))  
    {  
    // Release any references and return.  
    }  
  
// If rowset data update fails, then terminate the transaction, else  
// commit. The example doesn't retain the rowset.  
if (FAILED(hr = UpdateDataInRowset(pIRowset, bDelayedUpdate)))  
    {  
    // Get error from update, then terminate.  
    pITransaction->Abort(NULL, FALSE, FALSE);  
    }  
else  
    {  
    if (FAILED(hr = pITransaction->Commit(FALSE, XACTTC_SYNC, 0)))  
        {  
        // Get error from failed commit.  
        }  
    }  
  
if (FAILED(hr))  
    {  
    // Update of data or commit failed. Release any references and  
    // return.  
    }  
  
// Release any references and continue.  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Transaktionen](../../oledb/ole-db-transactions/transactions.md)   
 [Arbeiten mit Momentaufnahmeisolation](../../oledb/features/working-with-snapshot-isolation.md)  
  
  
