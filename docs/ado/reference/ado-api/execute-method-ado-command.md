---
title: Execute-Methode (ADO-Befehl) | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Command15::Execute
- Command15::raw_Execute
helpviewer_keywords:
- Execute method [ADO]
ms.assetid: f84a5ff3-0528-4ad7-9bea-9a15103378dd
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 651123d3112ca58c028412bd025325f303f0d637
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="execute-method-ado-command"></a>Execute-Methode (ADO-Befehl)
Führt die Abfrage, die SQL-Anweisung oder die gespeicherte Prozedur, die im angegebenen der [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) oder [CommandStream](../../../ado/reference/ado-api/commandstream-property-ado.md) Eigenschaft von der [Befehlsobjekt](../../../ado/reference/ado-api/command-object-ado.md).  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Set recordset = command.Execute( RecordsAffected, Parameters, Options )  
```  
  
## <a name="return-value"></a>Rückgabewert  
 Gibt eine [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) Objektverweis, einen Stream oder **nichts**.  
  
#### <a name="parameters"></a>Parameter  
 *RecordsAffected*  
 Optional. Ein **lange** Variablen, zu dem der Anbieter gibt die Anzahl der Datensätze, die der Vorgang betroffen. Die *RecordsAffected* Parameter gilt nur für die Aktionsabfragen oder gespeicherte Prozeduren. *RecordsAffected* gibt die Anzahl der Datensätze, die von einer Abfrage Ergebnis zurückgibt oder der gespeicherten Prozedur zurückgegebenen keinen zurück. Verwenden Sie zum Abrufen dieser Informationen die [RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md) Eigenschaft. Die **Execute** Methodenrückgabewert wird nicht die richtige Informationen bei Verwendung mit **AdAsyncExecute**, einfach, da bei ein Befehl asynchron ausgeführt wird, die Anzahl der betroffenen Datensätze möglicherweise nicht noch bekannt zum Zeitpunkt erfolgt die Methodenrückgabe.  
  
 *Parameter*  
 Optional. Ein **Variant** Array von Parameterwerten, die zusammen mit der Eingabezeichenfolge oder im angegebenen Stream **CommandText** oder **CommandStream**. (Output-Parameter werden keine richtige Werte, wenn dieses Argument übergeben zurück.)  
  
 *Optionen*  
 Optional. Ein **lange** Wert, der angibt, wie der Anbieter auswerten soll die [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) oder die [CommandStream](../../../ado/reference/ado-api/commandstream-property-ado.md) Eigenschaft von der [Befehl](../../../ado/reference/ado-api/command-object-ado.md) -Objekt. Kann ein Bitmaskenwert mit [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) und/oder [ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md) Werte. Beispielsweise können Sie **AdCmdText** und **AdExecuteNoRecords** in Kombination, wenn Sie den Wert des ADO haben möchten die **CommandText** Eigenschaft als Text und Geben Sie an, dass der Befehl sollte verwerfen und keine Datensätze, die generiert werden können zurück, wenn der Befehlstext ausgeführt wird.  
  
> [!NOTE]
>  Verwenden der **ExecuteOptionEnum** Wert **AdExecuteNoRecords** zum Verbessern der Leistung durch Minimierung der internen Verarbeitung. Wenn **AdExecuteStream** angegeben wurde, die Optionen **AdAsyncFetch** und **AdAsynchFetchNonBlocking** werden ignoriert. Verwenden Sie nicht die **CommandTypeEnum** Werte **AdCmdFile** oder **AdCmdTableDirect** mit **Execute**. Diese Werte können nur verwendet werden, als Optionen für die [öffnen](../../../ado/reference/ado-api/open-method-ado-recordset.md) und [Requery](../../../ado/reference/ado-api/requery-method.md) Methoden eine **Recordset**.  
  
## <a name="remarks"></a>Hinweise  
 Mithilfe der **Execute** Methode auf eine **Befehl** Objekt führt die Abfrage, die im angegebenen der **CommandText** Eigenschaft oder **CommandStream** die Eigenschaft des Objekts.  
  
 Ergebnisse werden zurückgegeben, einem **Recordset** (standardmäßig) oder als Datenstrom von binären Informationen. Geben Sie zum Abrufen eines binären Streams **AdExecuteStream** in *Optionen*, geben Sie einen Stream durch Festlegen von **Command.Properties ("Ausgabestream")**. Ein ADO **Stream** Objekt angegeben werden, um die Ergebnisse zu erhalten, oder einem anderen Streamobjekt, z. B. der IIS-Response-Objekt angegeben werden. Wenn kein Stream vor dem Aufruf angegeben wurde **Execute** mit **AdExecuteStream**, ein Fehler auftritt. Die Position des Streams bei der Rückgabe aus **Execute** ist Anbieter spezifisch.  
  
 Der Anbieter gibt zurück, wenn der Befehl nicht beabsichtigt ist, Zurückgeben von Ergebnissen (z. B. eine SQL-UPDATE-Abfrage) **nichts** solange die Option **AdExecuteNoRecords** angegeben ist; gibt andernfalls führen eine geschlossen **Recordset**. Einige Anwendungssprachen können Sie diesen Rückgabewert ignorieren, wenn kein **Recordset** erwünscht ist.  
  
 **Führen Sie** löst einen Fehler aus, wenn der Benutzer einen Wert für angibt **CommandStream** bei der **CommandType** ist **AdCmdStoredProc**,  **AdCmdTable**, oder **AdCmdTableDirect**.  
  
 Wenn die Abfrage Parameter enthält, Werte der aktuellen für die **Befehl** objektspezifischen Parameter werden verwendet, es sei denn, Sie überschreiben Sie diese mit Parameterwerten, die nur mit der **Execute** aufrufen. Sie können eine Teilmenge der Parameter überschreiben, indem Sie neue Werte für einige der Parameter auslassen, beim Aufrufen der **Execute** Methode. Die Reihenfolge, in der Sie die Parameter angeben, ist die gleiche Reihenfolge, in der Sie die Methode übergibt. Angenommen, es wurden vier (oder mehr) Parameter und neue Werte für nur der erste und vierte Parameter übergeben möchten, übergeben Sie `Array(var1,,,var4)` als die *Parameter* Argument.  
  
> [!NOTE]
>  Output-Parametern nicht richtig geben Werte zurück, wenn übergeben der *Parameter* Argument.  
  
 Ein [ExecuteComplete](../../../ado/reference/ado-api/executecomplete-event-ado.md) Ereignis wird ausgegeben, wenn dieser Vorgang abgeschlossen ist.  
  
> [!NOTE]
>  Beim Ausgeben von Befehlen, die mit den URLs Aufrufen der http-Authentifizierungsschema verwendeten automatisch die [Microsoft OLE DB-Anbieter für Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Weitere Informationen finden Sie unter [absoluten und relativen URLs](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
## <a name="applies-to"></a>Gilt für  
 [Command-Objekt (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Führen Sie abzufragen und Clear-Methoden-Beispiel (VB)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vb.md)   
 [Führen Sie abzufragen und Clear-Methoden-Beispiel (VBScript)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vbscript.md)   
 [Führen Sie Requery und deaktivieren Sie die Methoden (VC++-Beispiel)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vc.md)   
 [CommandStream-Eigenschaft (ADO)](../../../ado/reference/ado-api/commandstream-property-ado.md)   
 [CommandText-Eigenschaft (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md)   
 [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)   
 [Execute-Methode (ADO-Verbindung)](../../../ado/reference/ado-api/execute-method-ado-connection.md)   
 [ExecuteComplete-Ereignis (ADO)](../../../ado/reference/ado-api/executecomplete-event-ado.md)

