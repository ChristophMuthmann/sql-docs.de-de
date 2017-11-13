---
title: Open-Methode (ADO-Recordset) | Microsoft Docs
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
- Recordset15::raw_Open
- Recordset15::Open
helpviewer_keywords:
- Open method [ADO]
ms.assetid: 3236749c-4b71-4235-89e2-ccdfaaa9319d
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1977d0381311ac2d7f43bd161099d1f0eb0f6665
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="open-method-ado-recordset"></a>Open-Methode (ADO-Recordset)
Öffnet einen Cursor auf einem [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) Objekt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
recordset.Open Source, ActiveConnection, CursorType, LockType, Options  
```  
  
#### <a name="parameters"></a>Parameter  
 *Quelle*  
 Optional. Ein **Variant** , ausgewertet wird, um eine gültige [Befehl](../../../ado/reference/ado-api/command-object-ado.md) -Objekt, eine SQL-Anweisung, einen Tabellennamen, Aufruf einer gespeicherten Prozedur, eine URL oder den Namen einer Datei oder [Stream](../../../ado/reference/ado-api/stream-object-ado.md) mit einer persistent gespeichert [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
 *ActiveConnection*  
 Optional. Entweder eine **Variant** , ausgewertet wird, um eine gültige [Verbindung](../../../ado/reference/ado-api/connection-object-ado.md) Objekt Variablennamen ein, oder ein **Zeichenfolge** enthält ["ConnectionString"](../../../ado/reference/ado-api/connectionstring-property-ado.md) Parameter.  
  
 *CursorType*  
 Optional. Ein [CursorTypeEnum](../../../ado/reference/ado-api/cursortypeenum.md) Wert, der den Typ des Cursors bestimmt, die der Anbieter sollte beim Öffnen der **Recordset**. Der Standardwert ist **AdOpenForwardOnly**.  
  
 *LockType*  
 Optional. Ein [LockTypeEnum](../../../ado/reference/ado-api/locktypeenum.md) Wert, der bestimmt, welche Art von Sperren (Concurrency) des Anbieters verwenden soll, beim Öffnen der **Recordset**. Der Standardwert ist **AdLockReadOnly**.  
  
 *Optionen*  
 Optional. Ein **lange** Wert, der angibt, wie der Anbieter auswerten soll die *Quelle* -Argument an, wenn es etwas anders als darstellt eine **Befehl** -Objekt, oder dass die **Recordset** wiederhergestellt werden sollen, aus einer Datei, in denen es bereits gespeichert wurde. Kann eine oder mehrere [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) oder [ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md) Werte, die mit einem bitweisen OR-Operator kombiniert werden können.  
  
> [!NOTE]
>  Öffnen einer **Recordset** aus eine **Stream** , enthält eine permanent **Recordset**unter Verwendung einer [ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md) Wert **AdAsyncFetchNonBlocking** hat keine Auswirkungen; das Abrufen von Daten werden synchron und blockiert.  
  
> [!NOTE]
>  Die **ExecuteOpenEnum** Werte **AdExecuteNoRecords** oder **AdExecuteStream** sollte nicht verwendet werden, mit **öffnen**.  
  
## <a name="remarks"></a>Hinweise  
 Den Standardcursor für ADO **Recordset** ein Vorwärtscursor, schreibgeschützte Cursor, die auf dem Server gespeichert ist.  
  
 Mithilfe der **öffnen** Methode auf eine **Recordset** Objekt öffnet einen Cursor, der Datensätze, aus einer Basistabelle, die Ergebnisse einer Abfrage oder eine zuvor gespeicherte darstellt **Recordset**.  
  
 Verwenden Sie das optionale *Quelle* Argument, um eine Datenquelle mithilfe eines der folgenden anzugeben: ein **Befehl** Object-Variablen, eine SQL-Anweisung, eine gespeicherte Prozedur, einen Tabellennamen, eine URL oder einen vollständigen Dateinamen Pfad an. Wenn *Quelle* den Pfadnamen einer Datei, ist es möglich, einen vollständigen Pfad ("c:\dir\file.rst"), einen relativen Pfad (".. \file.rst) oder eine URL ("http://files/file.rst").  
  
 Es ist nicht ratsam, verwenden Sie die *Quelle* Argument der **öffnen** Methode, um eine Abfrage auszuführen, die keinen Datensätze zurückgibt, weil es keine einfache Methode zum bestimmen ist, ob der Aufruf erfolgreich war. Die **Recordset** zurückgegebenes z. B. eine Abfrage wird geschlossen. Aufrufen, um eine Abfrage auszuführen, die keinen Datensätze, z. B. eine SQL INSERT-Anweisung zurückgibt der [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md) Methode eine **Befehl** Objekt oder die [Execute](../../../ado/reference/ado-api/execute-method-ado-connection.md) Methode von einer [Verbindung](../../../ado/reference/ado-api/connection-object-ado.md) stattdessen-Objekt.  
  
 Die *ActiveConnection* Argument entspricht dem [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) Eigenschaft und gibt an, in welcher Verbindung öffnen die **Recordset** Objekt. Wenn Sie eine Verbindungsdefinition für dieses Argument übergeben, wird von ADO mit den angegebenen Parametern eine neue Verbindung geöffnet. Nach dem Öffnen der **Recordset** mit einem clientseitigen Cursor durch Festlegen der [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) Eigenschaft **AdUseClient**, können Sie den Wert dieser Eigenschaft zum Senden ändern Updates auf einen anderen Anbieter. Oder Sie können diese Eigenschaft festlegen, um **nichts** (in Microsoft Visual Basic) oder NULL, trennen Sie die **Recordset** von beliebigen Anbietern. Ändern von *ActiveConnection* für ein serverseitigen Cursor jedoch einen Fehler generiert.  
  
 Für die anderen Argumente, die Eigenschaften des entsprechen einem **Recordset** Objekt (*Quelle*, *CursorType*, und *LockType*), die Beziehung der Argumente, um die Eigenschaften lautet wie folgt:  
  
-   Die Eigenschaft ist Lese-/Schreibzugriff, bevor die **Recordset** -Objekt geöffnet ist.  
  
-   Die eigenschafteneinstellungen werden verwendet, es sei denn, Sie die entsprechenden Argumente, beim Ausführen übergeben der **öffnen** Methode. Wenn Sie ein Argument übergeben, wird die entsprechende Einstellung der Eigenschaft überschrieben und die Einstellung der Eigenschaft mit dem Argumentwert aktualisiert wird.  
  
-   Nach dem Öffnen der **Recordset** -Objekt, diese Eigenschaften sind schreibgeschützt.  
  
> [!NOTE]
>  Die **ActiveConnection** Eigenschaft ist schreibgeschützt und für **Recordset** -Objekte, deren [Quelle](../../../ado/reference/ado-api/source-property-ado-recordset.md) Eigenschaftensatz wird eine gültige **Befehl** Objekt auch wenn die **Recordset** Objekt ist nicht geöffnet.  
  
 Wenn Sie übergeben ein **Befehl** -Objekt in der *Quelle* Argument und auch übergeben ein *ActiveConnection* Argument, ein Fehler auftritt. Der **ActiveConnection** Eigenschaft von der **Befehl** -Objekts muss bereits festgelegt werden, um eine gültige **Verbindung** Objekt oder die Verbindungszeichenfolge.  
  
 Wenn Sie etwas anders als übergeben einer **Befehl** Objekt in der *Quelle* Argument können Sie die *Optionen* Argument zur Auswertung der Optimierung der *Quelle*  Argument. Wenn die *Optionen* Argument ist nicht definiert ist, treten möglicherweise Leistungseinbußen hinnehmbar, da ADO Aufrufe an den Anbieter, um festzustellen, ob das Argument eine SQL-Anweisung, eine gespeicherte Prozedur, eine URL oder ein Tabellenname ist vornehmen muss. Wenn Sie, was wissen *Quelle* Typ, die Sie verwenden, Festlegen der *Optionen* Argument weist ADO direkt auf den gewünschten Code zu springen. Wenn die *Optionen* Argument entspricht nicht der *Quelle* eingeben, ein Fehler auftritt.  
  
 Wenn Sie übergeben ein **Stream** Objekt in der *Quelle* Argument nicht übergeben Sie Informationen in die anderen Argumente. Auf diese Weise wird ein Fehler generiert. Die **ActiveConnection** sind keine Informationen beibehalten, wenn eine **Recordset** geöffnet wird eine **Stream**.  
  
 Die Standardeinstellung für die *Optionen* Argument ist **AdCmdFile** , wenn keine Verbindung zugeordnet ist die **Recordset**. Dies ist in der Regel wird die Groß-/Kleinschreibung für persistent gespeichert **Recordset** Objekte.  
  
 Wenn die Datenquelle keine Datensätze zurückgibt, legt der Anbieter die [BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) und [EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) Eigenschaften **"true"**, und die Position des aktuellen Datensatzes ist nicht definiert. Weiterhin können Sie neue Daten hinzufügen, um diesem leeren **Recordset** -Objekt Cursortyp zulässt.  
  
 Wenn Sie Ihre Vorgänge über ein offenes geschlossen haben **Recordset** -Objekts die [schließen](../../../ado/reference/ado-api/close-method-ado.md) -Methode freizugeben zugeordnete Systemressourcen verfügbar sind. Schließen ein Objekt entfernt diesen nicht aus dem Arbeitsspeicher; Sie können die eigenschafteneinstellungen ändern und die **öffnen** Methode, um sie später erneut öffnen. Um ein Objekt aus dem Arbeitsspeicher vollständig zu vermeiden, legen Sie die Objektvariable auf *nichts*.  
  
 Vor der **ActiveConnection** Eigenschaft festgelegt ist, rufen Sie **öffnen** ohne Operanden zum Erstellen einer Instanz von einer **Recordset** erstellt, indem Sie Felder mit Anfügen der  **Recordset** [Felder](../../../ado/reference/ado-api/fields-collection-ado.md) Auflistung.  
  
 Wenn Sie festgelegt haben die [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) Eigenschaft **AdUseClient**, Sie können Zeilen asynchron in zwei Arten abrufen. Die empfohlene Methode ist festzulegende *Optionen* auf **AdAsyncFetch**. Alternativ können Sie die "Asynchrone Rowset Verarbeitung" dynamische Eigenschaft in der [Eigenschaften](../../../ado/reference/ado-api/properties-collection-ado.md) Auflistung, aber verwandte abgerufenen Ereignisse können verloren, wenn Sie nicht festlegen, die *Optionen* Parameter **AdAsyncFetch**.  
  
> [!NOTE]
>  Wird nur durch Hintergrund Abrufen von Zeilen in der MS-Remote-Anbieter unterstützt die **öffnen** Methode *Optionen* Parameter.  
  
> [!NOTE]
>  URLs, die mit dem HTTP-Schema werden automatisch aufgerufen. der [Microsoft OLE DB-Anbieter für Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Weitere Informationen finden Sie unter [absoluten und relativen URLs](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
 Bestimmte Kombinationen von [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) und [ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md) Werte sind nicht gültig. Informationen darüber, welche Optionen können nicht kombiniert werden, finden Sie unter den Themen für die [ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md), und [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md).  
  
## <a name="applies-to"></a>Gilt für  
 [Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Beispiel für Eröffnungs- und Methoden (VB)](../../../ado/reference/ado-api/open-and-close-methods-example-vb.md)   
 [Öffnen Sie und schließen Sie die Methoden-Beispiel (VBScript)](../../../ado/reference/ado-api/open-and-close-methods-example-vbscript.md)   
 [Öffnen Sie und schließen Sie die Methoden (VC++-Beispiel)](../../../ado/reference/ado-api/open-and-close-methods-example-vc.md)   
 [Speichern Sie und öffnen Sie die Methoden-Beispiel (VB)](../../../ado/reference/ado-api/save-and-open-methods-example-vb.md)   
 [Open-Methode (ADO-Verbindung)](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Open-Methode (ADO-Datensatz)](../../../ado/reference/ado-api/open-method-ado-record.md)   
 [Open-Methode (ADO-Datenstrom)](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [OpenSchema-Methode](../../../ado/reference/ado-api/openschema-method.md)   
 [Save-Methode](../../../ado/reference/ado-api/save-method.md)

