---
title: Ausführen von asynchronen Vorgängen | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client|features
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- initialization [SQL Server Native Client]
- database connections [SQL Server Native Client]
- data access [SQL Server Native Client], asynchronous operations
- connections [SQL Server Native Client]
- asynchronous operations [SQL Server Native Client]
- rowsets [SQL Server], initializing
- SQLNCLI, asynchronous operations
- SQL Server Native Client, asynchronous operations
ms.assetid: 8fbd84b4-69cb-4708-9f0f-bbdf69029bcc
caps.latest.revision: 45
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 1b433851601bb3bbe1a9bd339b4af2b0835c1673
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="performing-asynchronous-operations"></a>Ausführen asynchroner Vorgänge
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ermöglicht es Anwendungen, asynchrone Datenbankvorgänge auszuführen. Die asynchrone Verarbeitung ermöglicht es Methoden, Rückgaben unverzüglich zu übermitteln, ohne den aufrufenden Thread zu blockieren. Dadurch kann ein Großteil der Leistungsfähigkeit und Flexibilität des Multithreadings genutzt werden, ohne dass Entwickler Threads explizit erstellen oder die Synchronisation durchführen müssen. Anwendungen fordern die asynchrone Verarbeitung an, wenn sie eine Datenbankverbindung oder das Ergebnis einer Befehlsausführung initialisieren.  
  
## <a name="opening-and-closing-a-database-connection"></a>Öffnen und Schließen einer Datenbankverbindung  
 Bei Verwendung der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter entwickelt, um die asynchrone Initialisierung ein Datenquellenobjekts Anwendungen können das DBPROPVAL_ASYNCH_INITIALIZE-bit in der DBPROP_INIT_ASYNCH-Eigenschaft vor dem Aufruf festlegen  **IDBInitialize:: Initialize**. Wenn diese Eigenschaft festgelegt ist, gibt der Anbieter sofort aus dem Aufruf von **initialisieren** mit S_OK, wenn die Operation sofort abgeschlossen ist, oder DB_S_ASYNCHRONOUS, wenn die Initialisierung asynchron fortgesetzt wird. Anwendungen können eine Abfrage für die **IDBAsynchStatus** oder [ISSAsynchStatus](../../../relational-databases/native-client-ole-db-interfaces/issasynchstatus-ole-db.md)-Schnittstelle für das Datenquellenobjekt, und rufen dann **idbasynchstatus:: GetStatus** oder[ Issasynchstatus:: Waitforasynchcompletion](../../../relational-databases/native-client-ole-db-interfaces/issasynchstatus-waitforasynchcompletion-ole-db.md) zum Abrufen des Status der Initialisierung.  
  
 Außerdem wurde dem DBPROPSET_SQLSERVERROWSET-Eigenschaftensatz die SSPROP_ISSAsynchStatus-Eigenschaft hinzugefügt. Anbieter, die die **ISSAsynchStatus** -Schnittstelle unterstützen, müssen diese Eigenschaft mit dem Wert VARIANT_TRUE implementieren.  
  
 **Idbasynchstatus:: Abort** oder [issasynchstatus:: Abort](../../../relational-databases/native-client-ole-db-interfaces/issasynchstatus-abort-ole-db.md) aufgerufen werden, um den asynchronen "Abbrechen" **initialisieren** aufrufen. Der Consumer muss die asynchrone Datenquellinitialisierung explizit anfordern. Andernfalls **IDBInitialize:: Initialize** wird nicht zurückgegeben, bis das Datenquellenobjekt vollständig initialisiert ist.  
  
> [!NOTE]  
>  Datenquellenobjekte, die für das Verbindungspooling verwendet nicht Aufrufen der **ISSAsynchStatus** -Schnittstelle in der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter. Die **ISSAsynchStatus** Schnittstelle wird nicht für in einem Pool zusammengefasste Datenquellenobjekte verfügbar gemacht.  
>   
>  Wenn eine Anwendung Verwendung des Cursormoduls explizit erzwingt **IOpenRowset:: OPENROWSET** und **IMultipleResults:: GetResult** asynchrone Verarbeitung wird nicht unterstützt.  
>   
>  Das Remoting Proxy/Stub-Dll (in MDAC 2.8) kann nicht aufgerufen werden darüber hinaus die **ISSAsynchStatus** -Schnittstelle in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. Die **ISSAsynchStatus** Schnittstelle wird durch Remoting nicht verfügbar gemacht.  
>   
>  Dienstkomponenten unterstützen keine **ISSAsynchStatus**.  
  
## <a name="execution-and-rowset-initialization"></a>Ausführung und Rowsetinitialisierung  
 Anwendungen, die dafür ausgelegt sind, das Ergebnis einer Befehlsausführung asynchron zu öffnen, können das DBPROPVAL_ASYNCH_INITIALIZE-Bit in der DBPROP_ROWSET_ASYNCH-Eigenschaft festlegen. Wenn dieses Bit vor dem Aufrufen **IDBInitialize:: Initialize**, **ICommand:: Execute**, **IOpenRowset:: OPENROWSET** oder **IMultipleResults:: GetResult**, *Riid* Argument muss auf IID_IDBAsynchStatus, IID_ISSAsynchStatus oder IID_IUnknown festgelegt werden.  
  
 Die Methode gibt unverzüglich S_OK zurück, wenn die rowsetinitialisierung abgeschlossen wird sofort oder mit DB_S_ASYNCHRONOUS, wenn die rowsetinitialisierung asynchron fortgesetzt wird, mit *PpRowset* auf die angeforderte Schnittstelle festgelegt ist, auf die Rowset. Für die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter diese Schnittstelle ist nur möglich **IDBAsynchStatus** oder **ISSAsynchStatus**. Bis das Rowset vollständig initialisiert wurde, wird diese Schnittstelle verhält, als wäre er in einen Zustand "angehalten", und der Aufruf **QueryInterface** für andere Schnittstellen als **IID_IDBAsynchStatus** oder **IID_ ISSAsynchStatus** möglicherweise zur Rückgabe von E_NOINTERFACE. Sofern der Consumer die asynchrone Verarbeitung nicht explizit anfordert, wird das Rowset synchron initialisiert. Alle angeforderten Schnittstellen sind verfügbar, wenn **Idbasynchstaus** oder **issasynchstatus:: Waitforasynchcompletion** gibt, die mit der Angabe, dass der asynchrone Vorgang abgeschlossen ist zurück. Das bedeutet nicht notwendigerweise, dass das Rowset vollständig aufgefüllt ist, jedoch ist es komplett und voll funktionstüchtig.  
  
 Wenn der ausgeführte Befehl kein Rowset zurückgibt, ist es weiterhin sofort zurückgegeben ein Objekt, das unterstützt **IDBAsynchStatus**.  
  
 Wenn Sie mehrere Ergebnisse von der asynchronen Befehlsausführung benötigen, sollten Sie Folgendes tun:  
  
-   Legen Sie das DBPROPVAL_ASYNCH_INITIALIZE-Bit der DBPROP_ROWSET_ASYNCH-Eigenschaft vor dem Ausführen des Befehls fest.  
  
-   Rufen Sie **ICommand:: Execute**, und fordern **IMultipleResults**.  
  
 Die **IDBAsynchStatus** und **ISSAsynchStatus** Schnittstellen können dann abgerufen werden, durch Abfragen, die mehrere Ergebnisse Schnittstelle mit **QueryInterface**.  
  
 Wenn der Befehl ausgeführt hat, **IMultipleResults** genutzt werden wie gewohnt mit einer Ausnahme, die den synchronen Fall: möglicherweise wird DB_S_ASYNCHRONOUS zurückgegeben, in diesem Fall **IDBAsynchStatus** oder **ISSAsynchStatus** können verwendet werden, um zu bestimmen, wann der Vorgang abgeschlossen ist.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel ruft die Anwendung eine nicht blockierende Methode auf, führt andere Verarbeitungsvorgänge aus und kehrt dann zur Verarbeitung der Ergebnisse zurück. **Issasynchstatus:: Waitforasynchcompletion** wartet auf das interne Ereignisobjekt, bis der asynchrone Vorgang abgeschlossen ist und die Menge des angegebenen Zeitintervalls *DwMilisecTimeOut* übergeben wird.  
  
```  
// Set the DBPROPVAL_ASYNCH_INITIALIZE bit in the   
// DBPROP_ROWSET_ASYNCH property before calling Execute().  
  
DBPROPSET CmdPropset[1];  
DBPROP CmdProperties[1];  
  
CmdPropset[0].rgProperties = CmdProperties;  
CmdPropset[0].cProperties = 1;  
CmdPropset[0].guidPropertySet = DBPROPSET_ROWSET;  
  
// Set asynch mode for command.  
CmdProperties[0].dwPropertyID = DBPROP_ROWSET_ASYNCH;  
CmdProperties[0].vValue.vt = VT_I4;  
CmdProperties[0].vValue.lVal = DBPROPVAL_ASYNCH_INITIALIZE;  
CmdProperties[0].dwOptions = DBPROPOPTIONS_REQUIRED;  
  
hr = pICommandProps->SetProperties(1, CmdPropset);  
  
hr = pICommand->Execute(  
   pUnkOuter,  
   IID_ISSAsynchStatus,  
   pParams,  
   pcRowsAffected,  
   (IUnknown**)&pISSAsynchStatus);  
  
if (hr == DB_S_ASYNCHRONOUS)  
{  
   // Do some work here...  
  
   hr = pISSAsynchStatus->WaitForAsynchCompletion(dwMilisecTimeOut);  
   if ( hr == S_OK)  
   {  
      hr = pISSAsynchStatus->QueryInterface(IID_IRowset, (void**)&pRowset);  
      pISSAsynchStatus->Release();  
   }  
}  
```  
  
 **Issasynchstatus:: Waitforasynchcompletion** wartet auf das interne Ereignisobjekt, bis der asynchrone Vorgang abgeschlossen ist oder die *DwMilisecTimeOut* Wert übergeben wird.  
  
 Im folgenden Beispiel wird die asynchrone Verarbeitung mit mehreren Resultsets veranschaulicht:  
  
```  
DBPROP CmdProperties[1];  
  
// Set asynch mode for command.  
CmdProperties[0].dwPropertyID = DBPROP_ROWSET_ASYNCH;  
CmdProperties[0].vValue.vt = VT_I4;  
CmdProperties[0].vValue.lVal = DBPROPVAL_ASYNCH_INITIALIZE;  
  
hr = pICommand->Execute(  
   pUnkOuter,  
   IID_IMultipleResults,  
   pParams,  
   pcRowsAffected,  
   (IUnknown**)&pIMultipleResults);  
  
// Use GetResults for ISSAsynchStatus.  
hr = pIMultipleResults->GetResult(IID_ISSAsynchStatus, (void **) &pISSAsynchStatus);  
  
if (hr == DB_S_ASYNCHRONOUS)  
{  
   // Do some work here...  
  
   hr = pISSAsynchStatus->WaitForAsynchCompletion(dwMilisecTimeOut);  
   if (hr == S_OK)  
   {  
      hr = pISSAsynchStatus->QueryInterface(IID_IRowset, (void**)&pRowset);  
      pISSAsynchStatus->Release();  
   }  
}  
```  
  
 Der Client kann den Status eines asynchron ausgeführten Vorgangs überprüfen, um das Blockieren zu verhindern, wie im folgenden Codebeispiel gezeigt:  
  
```  
// Set the DBPROPVAL_ASYNCH_INITIALIZE bit in the   
// DBPROP_ROWSET_ASYNCH property before calling Execute().  
hr = pICommand->Execute(  
   pUnkOuter,  
   IID_ISSAsynchStatus,  
   pParams,  
   pcRowsAffected,  
   (IUnknown**)&pISSAsynchStatus);   
  
if (hr == DB_S_ASYNCHRONOUS)  
{  
   do{  
      // Do some work...  
      hr = pISSAsynchStatus->GetStatus(DB_NULL_HCHAPTER, DBASYNCHOP_OPEN, NULL, NULL, &ulAsynchPhase, NULL);  
   }while (DBASYNCHPHASE_COMPLETE != ulAsynchPhase)  
   if SUCCEEDED(hr)  
   {  
      hr = pISSAsynchStatus->QueryInterface(IID_IRowset, (void**)&pRowset);  
   }  
   pIDBAsynchStatus->Release();  
}  
```  
  
 Im folgenden Beispiel wird veranschaulicht, wie Sie die gerade ausgeführte asynchrone Operation abbrechen können:  
  
```  
// Set the DBPROPVAL_ASYNCH_INITIALIZE bit in the   
// DBPROP_ROWSET_ASYNCH property before calling Execute().  
hr = pICommand->Execute(  
   pUnkOuter,  
   IID_ISSAsynchStatus,  
   pParams,  
   pcRowsAffected,  
   (IUnknown**)&pISSAsynchStatus);  
  
if (hr == DB_S_ASYNCHRONOUS)  
{  
   // Do some work...  
   hr = pISSAsynchStatus->Abort(DB_NULL_HCHAPTER, DBASYNCHOP_OPEN);  
}  
```  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server Native Client-Funktionen](../../../relational-databases/native-client/features/sql-server-native-client-features.md)   
 [Eigenschaften und Verhaltensweisen von Rowsets](../../../relational-databases/native-client-ole-db-rowsets/rowset-properties-and-behaviors.md)   
 [ISSAsynchStatus & #40; OLE DB & #41;](../../../relational-databases/native-client-ole-db-interfaces/issasynchstatus-ole-db.md)  
  
  
