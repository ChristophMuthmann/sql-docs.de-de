---
title: CommandTypeEnum | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: CommandTypeEnum
helpviewer_keywords: CommandTypeEnum enumeration [ADO]
ms.assetid: 4b1feb9c-a855-40fe-a906-efe688687e9f
caps.latest.revision: "13"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: b4a2e9e05e48913e2aecc3ef5a6f0651cd36e2d8
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="commandtypeenum"></a>CommandTypeEnum
Gibt an, wie ein Befehlsargument interpretiert werden sollen.  
  
 Es ist wichtig, überprüfen Sie die benutzerdefinierte *CommandString* Werte, um zu vermeiden, mit dem Benutzer der Anwendung die Möglichkeit zum Einfügen von potenziell gefährlichen Befehle für ADO zum Ausführen.  
  
|Konstante|Wert|Description|  
|--------------|-----------|-----------------|  
|**adCmdUnspecified**|-1|Gibt das Typargument für den Befehl keine.|  
|**adCmdText**|1|Wertet [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) als Textdefinition ein Befehl oder gespeicherte Prozedur aufrufen.|  
|**adCmdTable**|2|Wertet **CommandText** als Namen einer Tabelle, deren Spalten sind von einem intern generierten SQL-Abfrage zurückgegeben.|  
|**adCmdStoredProc**|4|Wertet **CommandText** als Name einer gespeicherten Prozedur.|  
|**adCmdUnknown**|8|Standard. Gibt an, dass der Typ des Befehls in die **CommandText** Eigenschaft ist nicht bekannt.<br /><br /> Wenn der Typ des Befehls nicht bekannt ist, stellen ADO mehrere Versuche zum Interpretieren der **CommandText**.<br /><br /> -   **CommandText** als Textdefinition von einem Befehl oder gespeicherte Prozeduraufruf interpretiert wird. Dies ist das gleiche Verhalten wie **AdCmdText**.<br />-   **CommandText** ist der Name einer gespeicherten Prozedur. Dies ist das gleiche Verhalten wie **AdCmdStoredProc**.<br />-   **CommandText** als den Namen einer Tabelle interpretiert. Von einem intern generierten SQL-Abfrage werden alle Spalten zurückgegeben. Dies ist das gleiche Verhalten wie **AdCmdTable**.|  
|**adCmdFile**|256|Wertet **CommandText** als den Dateinamen der dauerhaft gespeicherten [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md). Mit verwendet **Recordset.** [Öffnen](../../../ado/reference/ado-api/open-method-ado-recordset.md) oder [Requery](../../../ado/reference/ado-api/requery-method.md) nur.|  
|**adCmdTableDirect**|512|Wertet **CommandText** als Namen einer Tabelle, deren Spalten alle zurückgegeben. Mit verwendet **Recordset.Open** oder **Requery** nur. Verwenden der [Seek](../../../ado/reference/ado-api/seek-method.md) -Methode, die **Recordset** muss geöffnet sein, mit **AdCmdTableDirect**.<br /><br /> Dieser Wert kann nicht kombiniert werden, mit der [ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md) Wert **AdAsyncExecute**.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC-Entsprechung  
 Paket: **com.ms.wfc.data**  
  
|Konstante|  
|--------------|  
|AdoEnums.CommandType.UNSPECIFIED|  
|AdoEnums.CommandType.TEXT|  
|AdoEnums.CommandType.TABLE|  
|AdoEnums.CommandType.STOREDPROC|  
|AdoEnums.CommandType.UNKNOWN|  
|AdoEnums.CommandType.FILE|  
|AdoEnums.CommandType.TABLEDIRECT|  
  
## <a name="applies-to"></a>Gilt für  
  
|||  
|-|-|  
|[CommandType-Eigenschaft (ADO)](../../../ado/reference/ado-api/commandtype-property-ado.md)|[Execute-Methode (ADO Command)](../../../ado/reference/ado-api/execute-method-ado-command.md)|  
|[Execute-Methode (ADO Connection)](../../../ado/reference/ado-api/execute-method-ado-connection.md)|[Open-Methode (ADO Recordset)](../../../ado/reference/ado-api/open-method-ado-recordset.md)|  
|[Requery-Methode](../../../ado/reference/ado-api/requery-method.md)||
