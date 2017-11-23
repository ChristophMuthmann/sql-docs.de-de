---
title: 'Issabort:: Abort (OLE DB) | Microsoft Docs'
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-interfaces
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname: ISSAbort::Abort (OLE DB)
apitype: COM
helpviewer_keywords: Abort method
ms.assetid: a5bca169-694b-4895-84ac-e8fba491e479
caps.latest.revision: "17"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0ec5d868f317096ead72757d55bdfcfbf2bebecb
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="issabortabort-ole-db"></a>ISSAbort::Abort (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Bricht das aktuelle Rowset sowie eventuell mit dem aktuellen Befehl verknüpfte Batchbefehle ab.  
  
Die **ISSAbort** -Schnittstelle, die verfügbar gemacht werden die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter stellt die **issabort:: Abort** -Methode ab, das das aktuelle Rowset sowie Befehle abzubrechen mit dem Befehl, der das Rowset ursprünglich generierte, und, die Ausführung noch nicht abgeschlossen haben.  
  
 **ISSAbort** ist ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client-Anbieter spezifische Schnittstelle zur Verfügung, mit **QueryInterface** auf die **IMultipleResults** zurückgegebenes Objekt  **ICommand:: Execute** oder **IOpenRowset:: OPENROWSET**.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
HRESULT Abort(void);  
```  
  
## <a name="remarks"></a>Hinweise  
 Wenn der abgebrochene Befehl eine gespeicherte Prozedur ist, wird die Ausführung der gespeicherten Prozedur (und aller Prozeduren, die diese Prozedur aufgerufen haben) sowie des Befehlsbatch, der den gespeicherten Prozeduraufruf enthielt, ebenfalls beendet. Falls der Server gerade ein Resultset an den Client überträgt, wird dieses gestoppt. Wenn der Client ein Resultset nicht verarbeitet, wird durch Aufrufen von **ISSAbort::Abort** vor dem Freigeben des Rowsets die Rowsetfreigabe beschleunigt, aber wenn eine offene Transaktion vorhanden ist und XACT_ABORT auf ON gestellt ist, wird beim Aufrufen von **ISSAbort::Abort** ein Rollback für die Transaktion ausgeführt.  
  
 Sobald **ISSAbort::Abort** S_OK zurückgibt, kann die zugehörige **IMultipleResults** -Schnittstelle nicht mehr verwendet werden und gibt bei allen Methodenaufrufen DB_E_CANCELED zurück (außer bei Methoden, die durch die **IUnknown** -Schnittstelle definiert sind), bis sie wieder freigegeben wird. Falls vor dem **Abort** -Aufruf ein **IRowset** von **IMultipleResults**empfangen wurde, ist dieses ebenfalls nicht mehr verwendbar und gibt bei allen Methodenaufrufen DB_E_CANCELED zurück (außer bei Methoden, die durch die **IUnknown** -Schnittstelle und **IRowset::ReleaseRows**definiert sind), bis es nach einem erfolgreichen Aufruf von **ISSAbort::Abort**wieder freigegeben wird.  
  
> [!NOTE]  
>  Beginnend mit [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], wenn der Serverstatus XACT_ABORT ON ist, Ausführen von **issabort:: Abort** beendet und führt einen Rollback für alle aktuellen impliziten oder expliziten Transaktionen beim Verbinden mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Frühere Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] brechen die aktuelle Transaktion nicht ab.  
  
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
  
## <a name="see-also"></a>Siehe auch  
 [' Issabort ' &#40; OLE DB &#41;](http://msdn.microsoft.com/library/7c4df482-4a83-4da0-802b-3637b507693a)  
  
  
