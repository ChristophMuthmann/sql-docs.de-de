---
title: Execute-Methode (ADO-Verbindung) | Microsoft Docs
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
- Connection15::Execute
- Connection15::raw_Execute
helpviewer_keywords:
- Execute method [ADO]
ms.assetid: 03c69320-96b2-4d85-8d49-a13b13e31578
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6c2606221388b56f672b0b44cf4a0f0656b3861c
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="execute-method-ado-connection"></a>Execute-Methode (ADO-Verbindung)
Führt die angegebene Abfrage, SQL-Anweisung, gespeicherte Prozedur oder anbieterspezifischen Text.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Set recordset = connection.Execute (CommandText, RecordsAffected, Options)  
Set recordset = connection.Execute (CommandText, RecordsAffected, Options)  
```  
  
## <a name="return-value"></a>Rückgabewert  
 Gibt eine [Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md) -Objektverweis.  
  
#### <a name="parameters"></a>Parameter  
 *' CommandText '*  
 Ein **Zeichenfolge** Wert, der die SQL-Anweisung, gespeicherte Prozedur, eine URL oder Anbieter-spezifischen Text auszuführende enthält. **Optional**, Tabellennamen können jedoch nur verwendet werden, wenn der Anbieter SQL bekannt ist. Wenn z. B. ein Tabellenname "Kunden" verwendet wird, voranstellen ADO die standardmäßige SQL Select-Syntax um bilden, und übergeben "SELECT * FROM Customers" als eine [!INCLUDE[tsql](../../../includes/tsql_md.md)] Anweisung an den Anbieter.  
  
 *RecordsAffected*  
 Optional. Ein **lange** Variablen, zu dem der Anbieter gibt die Anzahl der Datensätze, die der Vorgang betroffen.  
  
 *Optionen*  
 Optional. Ein **lange** Wert, der angibt, wie der Anbieter das Argument ' CommandText ' ausgewertet werden soll. Kann eine Bitmaske aus einem oder mehreren [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) oder [ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md) Werte.  
  
 **Hinweis** verwenden die **ExecuteOptionEnum** Wert **AdExecuteNoRecords** zur Verbesserung der Leistung durch Minimierung der internen Verarbeitung und für Anwendungen, die Sie aus Visual Basic Portieren 6.0.  
  
 Verwenden Sie keine **AdExecuteStream** mit der **Execute** Methode von einer **Verbindung** Objekt.  
  
 Verwenden Sie nicht die Werte CommandTypeEnum AdCmdFile oder AdCmdTableDirect mit Execute. Diese Werte können nur verwendet werden, als Optionen für die [Open-Methode (ADO-Recordset)](../../../ado/reference/ado-api/open-method-ado-recordset.md) und [Requery-Methode](../../../ado/reference/ado-api/requery-method.md) Methoden eine **Recordset**.  
  
## <a name="remarks"></a>Hinweise  
 Mithilfe der **Execute** Methode auf eine [Verbindung Object (ADO)](../../../ado/reference/ado-api/connection-object-ado.md) -Objekt ausgeführt wird, eine Abfrage, die Sie für die angegebene Verbindung an die Methode in der ' CommandText '-Argument übergeben. Wenn das Argument ' CommandText ' eine Zeile zurückgeben Abfrage angibt, werden alle Ergebnisse, die die Ausführung generiert gespeichert, in einem neuen **Recordset** Objekt. Der Anbieter gibt zurück, wenn der Befehl nicht beabsichtigt ist, Zurückgeben von Ergebnissen (z. B. eine SQL-UPDATE-Abfrage) **nichts** solange die Option **AdExecuteNoRecords** angegeben ist; gibt andernfalls führen eine geschlossen **Recordset**.  
  
 Das zurückgegebene **Recordset** Objekt ist immer einen schreibgeschützten, nur vorwärts-Cursor. Wenn Sie müssen eine **Recordset** Objekt mit zusätzlichen Funktionen, erstellen Sie zunächst eine **Recordset** Objekt mit den gewünschten eigenschafteneinstellungen, verwenden Sie die **Recordset** Objekt [ Open-Methode (ADO-Recordset)](../../../ado/reference/ado-api/open-method-ado-recordset.md) Methode, um die Abfrage auszuführen und den gewünschten Cursor-Datentyp zurückgeben.  
  
 Der Inhalt der *CommandText* Argument an den Anbieter spezifisch sind und SQL-Standardsyntax oder spezielle Befehlsformat, die der Anbieter unterstützt werden können.  
  
 Ein ExecuteComplete-Ereignis wird ausgegeben, wenn dieser Vorgang abgeschlossen ist.  
  
> [!NOTE]
>  URLs, die mit dem HTTP-Schema werden automatisch aufgerufen. der [Microsoft OLE DB-Anbieter für Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Weitere Informationen finden Sie unter [absoluten und relativen URLs](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
## <a name="applies-to"></a>Gilt für  
 [Verbindungsobjekt (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
