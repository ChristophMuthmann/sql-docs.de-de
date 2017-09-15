---
title: Parameters-Auflistung (ADO) | Microsoft Docs
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
- Command15::get_Parameters
- Command15::Parameters
- Command15::GetParameters
helpviewer_keywords:
- Parameters collection [ADO]
ms.assetid: 497cae10-3913-422a-9753-dcbb0a639b1b
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9dcfec51eb94eb1ca290ebb3323012e2aaa558b5
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="parameters-collection-ado"></a>Parameters-Auflistung (ADO)
Enthält alle der [Parameter](../../../ado/reference/ado-api/parameter-object.md) Objekte von einem [Befehl](../../../ado/reference/ado-api/command-object-ado.md) Objekt.  
  
## <a name="remarks"></a>Hinweise  
 Ein **Befehl** Objekt verfügt über eine **Parameter** Auflistung bestehend aus **Parameter** Objekte.  
  
 Mithilfe der [aktualisieren](../../../ado/reference/ado-api/refresh-method-ado.md) Methode auf eine **Befehl** des Objekts **Parameter** Auflistung Ruft Parameterinformationen für die gespeicherte Prozedur oder eine parametrisierte Abfrage Anbieter ab. im angegebenen der **Befehl** Objekt. Einige Anbieter unterstützen keine Aufrufe von gespeicherten Prozeduren oder parametrisierte Abfragen. Aufrufen der **aktualisieren** Methode für die **Parameter** Auflistung bei Verwendung eines solchen Anbieters ein Fehler zurückgegeben.  
  
 Wenn Sie nicht Ihre eigenen definiert haben **Parameter** Zugriff auf Objekte und Sie die **Parameter** Auflistung vor dem Aufruf der **aktualisieren** Methode, ADO wird automatisch aufgerufen haben die Methode, und füllen Sie die Auflistung für Sie.  
  
 Sie können Aufrufe an den Anbieter zum Verbessern der Leistung, wenn Sie die Eigenschaften der Parameter der gespeicherten Prozedur zugeordnet oder einer parametrisierten Abfrage wissen, dass Sie aufrufen möchten, minimieren. Verwenden Sie die [CreateParameter](../../../ado/reference/ado-api/createparameter-method-ado.md) Methode zum Erstellen der **Parameter** Objekte mit dem entsprechenden eigenschafteneinstellungen und Verwenden der [Anfügen](../../../ado/reference/ado-api/append-method-ado.md) Methode hinzugefügt der ** Parameter** Auflistung. Dadurch können Sie die festzulegen und Parameterwerte zurückzugeben, ohne den Anbieter für die Parameterinformationen aufrufen. Wenn Sie an einen Anbieter, der keine Parameterinformationen bereitstellt schreiben, müssen Sie manuell Auffüllen der **Parameter** Auflistung, die mit dieser Methode, um Parameter verwenden zu können. Verwenden der [löschen](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md) -Methode zum Entfernen **Parameter** Objekte aus der **Parameter** Auflistung bei Bedarf.  
  
 Die Objekte in der **Parameter** Auflistung von eine **Recordset** außerhalb des gültigen Bereichs (somit nicht verfügbar) wechseln Sie bei der **Recordset** geschlossen wird.  
  
 Beim Aufrufen einer gespeicherten Prozedur mit **Befehl**, die return-Wert/Output-Parameter einer gespeicherten Prozedur wird wie folgt abgerufen:  
  
1.  Beim Aufrufen einer gespeicherten Prozedur, die keine Parameter hat die **aktualisieren** Methode auf die **Parameter** Auflistung sollte aufgerufen werden, bevor die **Execute** Methode auf der **Befehl** Objekt.  
  
2.  Beim Aufrufen einer gespeicherten Prozedur mit Parametern und explizit anfügen Parameter an die **Parameter** Auflistung mit **Append**, return Wert/Output-Parameters angefügt werden soll, um die **Parameter** Auflistung. Der Rückgabewert muss zuerst angefügt werden, um die **Parameter** Auflistung. Verwendung **Anfügen** hinzuzufügende die anderen Parameter in der **Parameter** Auflistung in der Reihenfolge der Definition. Die gespeicherte Prozedur SPWithParam verfügt beispielsweise über zwei Parameter. Der erste Parameter *InParam*, ist ein Eingabeparameter, die als AdVarChar (20) definiert und der zweite Parameter *OutParam*, ist ein Ausgabeparameter, der als "AdVarChar (20)" definiert. Sie können die return-Wert/Output-Parameter durch den folgenden Code abrufen.  
  
    ```  
    ' Open Connection Conn  
    set ccmd = CreateObject("ADODB.Command")  
    ccmd.Activeconnection= Conn  
  
    ccmd.CommandText="SPWithParam"  
    ccmd.commandType = 4 'adCmdStoredProc  
  
    ccmd.parameters.Append ccmd.CreateParameter(, adInteger, adParamReturnValue, , NULL)   ' return value  
    ccmd.parameters.Append ccmd.CreateParameter("InParam", adVarChar, adParamInput, 20, "hello world")   ' input parameter  
    ccmd.parameters.Append ccmd.CreateParameter("OutParam", adVarChar, adParamOuput, 20, NULL)   ' output parameter  
  
    ccmd.execute()  
  
    ' Access ccmd.parameters(0) as return value of this stored procedure  
    ' Access ccmd.parameters("OutParam") as the output parameter of this stored procedure.  
  
    ```  
  
3.  Beim Aufrufen einer gespeicherten Prozedur mit Parametern und konfigurieren die Parameter durch Aufrufen der **Element** Methode für die **Parameter** Sammlung, die return-Wert/Output-Parameter der gespeicherten Prozedur kann abgerufen werden, aus der **Parameter** Auflistung. Die gespeicherte Prozedur SPWithParam verfügt beispielsweise über zwei Parameter. Der erste Parameter *InParam*, ist ein Eingabeparameter, die als AdVarChar (20) definiert und der zweite Parameter *OutParam*, ist ein Ausgabeparameter, der als "AdVarChar (20)" definiert. Sie können die return-Wert/Output-Parameter durch den folgenden Code abrufen.  
  
    ```  
    ' Open Connection Conn  
    set ccmd = CreateObject("ADODB.Command")  
    ccmd.Activeconnection= Conn  
  
    ccmd.CommandText="SPWithParam"  
    ccmd.commandType = 4 'adCmdStoredProc  
  
    ccmd.parameters.Item("InParam").value = "hello world" ' input parameter  
    ccmd.execute()  
  
    ' Access ccmd.parameters(0) as return value of stored procedure  
    ' Access ccmd.parameters(2) or ccmd.parameters("OutParam") as the output parameter.  
    ```  
  
 Dieser Abschnitt enthält das folgende Thema.  
  
-   [Parameter Auflistungseigenschaften, Methoden und Ereignisse](../../../ado/reference/ado-api/parameters-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Append-Methode (ADO)](../../../ado/reference/ado-api/append-method-ado.md)   
 [CreateParameter-Methode (ADO)](../../../ado/reference/ado-api/createparameter-method-ado.md)   
 [Parameter-Objekt](../../../ado/reference/ado-api/parameter-object.md)
