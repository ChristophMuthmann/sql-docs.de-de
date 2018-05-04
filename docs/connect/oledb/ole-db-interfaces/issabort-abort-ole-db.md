---
title: 'Issabort:: Abort (OLE DB) | Microsoft Docs'
description: ISSAbort::Abort (OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-interfaces
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ISSAbort::Abort (OLE DB)
apitype: COM
helpviewer_keywords:
- Abort method
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: c6103c07bcab8db090d393a5b7560fdaf79c7a73
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="issabortabort-ole-db"></a>ISSAbort::Abort (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Bricht das aktuelle Rowset sowie eventuell mit dem aktuellen Befehl verknüpfte Batchbefehle ab.  
  
Die **ISSAbort** -Schnittstelle, die in der OLE DB-Treiber für SQL Server verfügbar ist, stellt die **issabort:: Abort** Methode ab, das das aktuelle Rowset sowie Befehle abzubrechen, die als Batch erstellt mit dem Befehl der das Rowset ursprünglich generierte, und, die Ausführung noch nicht abgeschlossen haben.  
  
 **ISSAbort** steht ein OLE DB-Treiber für SQL Server-spezifische Schnittstelle mithilfe **QueryInterface** auf die **IMultipleResults** zurückgegebenes Objekt **ICommand:: Execute**  oder **IOpenRowset:: OPENROWSET**.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
HRESULT Abort(void);  
```  
  
## <a name="remarks"></a>Hinweise  
 Wenn der abgebrochene Befehl in einer gespeicherten Prozedur ist, wird Ausführung der gespeicherten Prozedur (und aller Prozeduren, die diese Prozedur aufgerufen wurde) sowie des Befehlsbatch beendet, die den Aufruf der gespeicherten Prozedur enthält. Falls der Server gerade ein Resultset an den Client überträgt, wird die Übertragung beendet werden. Wenn der Client ein Resultset nicht verarbeitet, wird durch Aufrufen von **ISSAbort::Abort** vor dem Freigeben des Rowsets die Rowsetfreigabe beschleunigt, aber wenn eine offene Transaktion vorhanden ist und XACT_ABORT auf ON gestellt ist, wird beim Aufrufen von **ISSAbort::Abort** ein Rollback für die Transaktion ausgeführt.  
  
 Nach dem **issabort:: Abort** S_OK zurückgibt, das zugeordnete **IMultipleResults** Schnittstelle geht in einem nicht verwendbaren Status, und gibt Sie allen Methodenaufrufen DB_E_CANCELED zurück (außer bei Methoden, die durch die definierten**IUnknown** Schnittstelle), bis es veröffentlicht wird. Falls vor dem **Abort** -Aufruf ein **IRowset** von **IMultipleResults**empfangen wurde, ist dieses ebenfalls nicht mehr verwendbar und gibt bei allen Methodenaufrufen DB_E_CANCELED zurück (außer bei Methoden, die durch die **IUnknown** -Schnittstelle und **IRowset::ReleaseRows**definiert sind), bis es nach einem erfolgreichen Aufruf von **ISSAbort::Abort**wieder freigegeben wird.  
  
> [!NOTE]  
>  Ab [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]gilt: Wenn der Serverstatus XACT_ABORT ON ist, werden bei Ausführung von **ISSAbort::Abort** alle aktuellen impliziten oder expliziten Transaktionen beendet und ein Rollback ausgeführt, wenn eine Verbindung zu [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]besteht. Frühere Versionen von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] brechen die aktuelle Transaktion nicht ab.  
  
## <a name="arguments"></a>Argumente  
 Keine.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 S_OK  
 Die **ISSAbort::Abort** -Methode gibt S_OK zurück, wenn der Batch abgebrochen wurde, andernfalls DB_E_CANTCANCEL. Wenn der Batch bereits abgebrochen wurde, wird DB_E_CANCELED zurückgegeben.  
  
 DB_E_CANCELED  
 Der Batch wurde bereits abgebrochen.  
  
 DB_E_CANTCANCEL  
 Der Batch wurde nicht abgebrochen.  
  
 E_FAIL  
 Ein anbieterspezifischer Fehler aufgetreten. Ausführliche Informationen erhalten Sie die [ISQLServerErrorInfo](http://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1) Schnittstelle.  
  
 E_UNEXPECTED  
 Die Methode wurde unerwartet aufgerufen. Zum Beispiel ist das Objekt in einem Zombiezustand, da **ISSAbort::Abort** bereits aufgerufen wurde.  
  
 E_OUTOFMEMORY  
 Fehler aufgrund von nicht genügend Arbeitsspeicher.  
  
  
