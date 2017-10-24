---
title: CommandText-Eigenschaft (ADO) | Microsoft Docs
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
- Command15::CommandText
helpviewer_keywords:
- CommandText property [ADO]
ms.assetid: 4dd7e82a-8da5-4a4e-b439-11a29286fa0e
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 60ee83c7d1f667feb0b1fcb4985dcd50edfda27b
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="commandtext-property-ado"></a>CommandText-Eigenschaft (ADO)
Gibt den Text eines Befehls für einen Anbieter ausgestellt werden.  
  
## <a name="settings-and-return-values"></a>Einstellungen und Rückgabewerte  
 Ruft ab oder legt einen **Zeichenfolge** Wert, der einen Anbieterbefehl, z. B. eine SQL-Anweisung, einen Tabellennamen, eine relative URL oder Aufruf einer gespeicherten Prozedur enthält. Der Standardwert ist eine leere Zeichenfolge ("").  
  
## <a name="remarks"></a>Hinweise  
 Verwenden der **CommandText** Eigenschaft festlegen oder Zurückgeben des Texts eines Befehls, dargestellt durch eine [Befehl](../../../ado/reference/ado-api/command-object-ado.md) Objekt. In der Regel Dadurch wird eine SQL-Anweisung sein, aber kann auch andere Typen von Command-Anweisung, die vom Anbieter, z. B. Aufruf einer gespeicherten Prozedur erkannt werden. Eine SQL-Anweisung muss die bestimmten Dialekt oder vom Abfrageprozessor für den Anbieter unterstützte Version aufweisen.  
  
 Wenn die [Prepared](../../../ado/reference/ado-api/prepared-property-ado.md) Eigenschaft von der **Befehl** -Objekts festgelegt wird, um **"true"** und die **Befehl** Objekt an eine offene Verbindung gebunden ist, wenn Sie festlegen die **CommandText** Eigenschaft ADO bereitet die Abfrage (d. h. eine kompilierte Form der Abfrage, die vom Anbieter gespeichert ist) beim Aufrufen der [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md) oder [öffnen](../../../ado/reference/ado-api/open-method-ado-connection.md)Methoden.  
  
 Je nach der [CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md) Eigenschaft festlegen, ADO kann alter der **CommandText** Eigenschaft. Informieren Sie sich die **CommandText** Eigenschaft jederzeit aufrufen, um den eigentlichen Befehlstext sehen, ADO wird während der Ausführung verwenden.  
  
 Verwenden der **CommandText** Eigenschaft so festlegen oder zurückgeben eine relative URL, der eine Ressource, z. B. eine Datei oder ein Verzeichnis angibt. Die Ressource ist relativ zu einem Speicherort explizit angegeben werden, indem Sie eine absolute URL oder implizit eine offene [Verbindung](../../../ado/reference/ado-api/connection-object-ado.md) Objekt.  
  
> [!NOTE]
>  URLs, die mit dem HTTP-Schema werden automatisch aufgerufen. der [Microsoft OLE DB-Anbieter für Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Weitere Informationen finden Sie unter [absoluten und relativen URLs](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
## <a name="applies-to"></a>Gilt für  
 [Command-Objekt (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>Siehe auch  
 [ActiveConnection, CommandText CommandTimeout, Befehlstyp (CommandType), Größe und Eigenschaften Beispiel für die Richtung (VB)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [ActiveConnection, CommandText CommandTimeout, Befehlstyp (CommandType), Größe und Richtung Eigenschaften (VC++-Beispiel)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [Requery-Methode](../../../ado/reference/ado-api/requery-method.md)   
 [ActiveConnection, CommandText CommandTimeout, Befehlstyp (CommandType), Größe und Eigenschaften Beispiel für die Richtung (JScript)](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)

