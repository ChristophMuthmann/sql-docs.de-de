---
title: Refresh-Methode (ADO) | Microsoft Docs
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
- _Collection::Refresh
- Parameters::Refresh
- Properties::Refresh
helpviewer_keywords:
- Refresh method [ADO]
ms.assetid: 089b7ca7-684f-4259-8032-5bd1ecc54426
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 00a739b4bf90651f1e38402a8309482bf8217680
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="refresh-method-ado"></a>Refresh-Methode (ADO)
Aktualisiert die Objekte in einer Auflistung von verfügbaren Objekte entsprechend, und spezifische an den Anbieter an.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
collection.Refresh  
```  
  
## <a name="remarks"></a>Hinweise  
 Die **aktualisieren** Methode umfasst verschiedene Aufgaben abhängig von der Auflistung aus der Sie aufrufen.  
  
### <a name="parameters"></a>Parameter  
 Mithilfe der **aktualisieren** Methode für die [Parameter](../../../ado/reference/ado-api/parameters-collection-ado.md) Auflistung von einer [Befehl](../../../ado/reference/ado-api/command-object-ado.md) Objekt ruft Anbieterseite Parameterinformationen für die gespeicherte Prozedur oder parametrisierte Abfrage angegeben, der **Befehl** Objekt. Die Auflistung ist leer für Anbieter, die Aufrufe von gespeicherten Prozeduren oder parametrisierte Abfragen nicht unterstützt werden.  
  
 Sollten Sie festlegen der [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) Eigenschaft der **Befehl** Objekt auf eine gültige [Verbindung](../../../ado/reference/ado-api/connection-object-ado.md) -Objekt, das [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) Eigenschaft Um einen gültigen Befehl und die [Befehlstyp (CommandType)](../../../ado/reference/ado-api/commandtype-property-ado.md) Eigenschaft **AdCmdStoredProc** vor dem Aufruf der **aktualisieren** Methode.  
  
 Wenn Sie Zugriff auf die **Parameter** Auflistung vor dem Aufruf der **aktualisieren** ADO-Methode automatisch rufen Sie die Methode und die Auflistung für Sie aufzufüllen.  
  
> [!NOTE]
>  Bei Verwendung der **aktualisieren** Methode zum Abrufen von Parameterinformationen von dem Anbieter, und es gibt eine oder mehrere Daten variabler Länge-Typ [Parameter](../../../ado/reference/ado-api/parameter-object.md) Objekte ADO möglicherweise Arbeitsspeicher für die Parameter basierend Klicken Sie auf ihre maximale potenzielle Größe, wodurch einen Fehler während der Ausführung gehindert wird. Sollten Sie explizit festlegen der [Größe](../../../ado/reference/ado-api/size-property-ado-parameter.md) -Eigenschaft für diese Parameter vor dem Aufrufen der [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md) Methode, um Fehler zu vermeiden.  
  
### <a name="fields"></a>Felder  
 Mithilfe der **aktualisieren** Methode für die [Felder](../../../ado/reference/ado-api/fields-collection-ado.md) Auflistung wirkt sich nicht sichtbar. Um Änderungen aus der Datenbankstruktur der zugrunde liegenden abzurufen, müssen Sie entweder verwenden die [Requery](../../../ado/reference/ado-api/requery-method.md) Methode oder, wenn die [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) Objekt unterstützt keine Lesezeichen, die [MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)Methode.  
  
### <a name="properties"></a>Eigenschaften  
 Mithilfe der **aktualisieren** Methode auf eine **Eigenschaften** Auflistung einiger Objekte füllt die Auflistung mit den dynamischen Eigenschaften, die der Anbieter verfügbar macht. Diese Eigenschaften stellen Informationen zu spezifischen Funktionen bereit, an den Anbieter, über die integrierten Eigenschaften ADO unterstützt.  
  
## <a name="applies-to"></a>Gilt für  
  
||||  
|-|-|-|  
|[Axes-Auflistung](../../../ado/reference/ado-md-api/axes-collection-ado-md.md)|[Columns-Auflistung](../../../ado/reference/adox-api/columns-collection-adox.md)|[CubeDefs-Auflistung](../../../ado/reference/ado-md-api/cubedefs-collection-ado-md.md)|  
|[Auflistung von Dimensionen](../../../ado/reference/ado-md-api/dimensions-collection-ado-md.md)|[Fehlerauflistung](../../../ado/reference/ado-api/errors-collection-ado.md)|[Fields-Auflistung](../../../ado/reference/ado-api/fields-collection-ado.md)|  
|[Auflistung von Gruppen](../../../ado/reference/adox-api/groups-collection-adox.md)|[Hierarchies-Auflistung](../../../ado/reference/ado-md-api/hierarchies-collection-ado-md.md)|[Auflistung von Indizes](../../../ado/reference/adox-api/indexes-collection-adox.md)|  
|[Auflistung von Schlüsseln](../../../ado/reference/adox-api/keys-collection-adox.md)|[Levels-Auflistung](../../../ado/reference/ado-md-api/levels-collection-ado-md.md)|[Members-Auflistung](../../../ado/reference/ado-md-api/members-collection-ado-md.md)|  
|[Parameters-Auflistung](../../../ado/reference/ado-api/parameters-collection-ado.md)|[Auflistung der Positionen](../../../ado/reference/ado-md-api/positions-collection-ado-md.md)|[Auflistung von Prozeduren](../../../ado/reference/adox-api/procedures-collection-adox.md)|  
|[Properties-Auflistung](../../../ado/reference/ado-api/properties-collection-ado.md)|[Tables-Auflistung](../../../ado/reference/adox-api/tables-collection-adox.md)|[Users-Auflistung](../../../ado/reference/adox-api/users-collection-adox.md)|  
|[Sammlung von Ansichten](../../../ado/reference/adox-api/views-collection-adox.md)|||  
  
## <a name="see-also"></a>Siehe auch  
 [Aktualisieren von Methodenbeispiel (VB)](../../../ado/reference/ado-api/refresh-method-example-vb.md)   
 [Aktualisieren Sie die (VC++-Methodenbeispiel)](../../../ado/reference/ado-api/refresh-method-example-vc.md)   
 [Count-Eigenschaft (ADO)](../../../ado/reference/ado-api/count-property-ado.md)   
 [Refresh-Methode (RDS)](../../../ado/reference/rds-api/refresh-method-rds.md)

