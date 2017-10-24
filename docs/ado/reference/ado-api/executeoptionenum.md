---
title: ExecuteOptionEnum | Microsoft Docs
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
- ExecuteOptionEnum
helpviewer_keywords:
- ExecuteOptionEnum enumeration [ADO]
ms.assetid: 68bfa83a-5df4-4bef-8736-0f88ae8c29ea
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 74248756628e892ff8a00e0e6e206b5eb7639e05
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="executeoptionenum"></a>ExecuteOptionEnum
Gibt an, wie ein Anbieter einen Befehl ausgeführt werden soll.  
  
|Konstante|Wert|Description|  
|--------------|-----------|-----------------|  
|**adAsyncExecute**|0x10|Gibt an, dass der Befehl asynchron ausgeführt werden soll.<br /><br /> Dieser Wert kann nicht kombiniert werden, mit der [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) Wert **AdCmdTableDirect**.|  
|**adAsyncFetch**|0x20|Gibt an, dass die verbleibenden Zeilen nach die ersten Menge in angegeben die [CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md) Eigenschaft asynchron abgerufen werden sollen.|  
|**adAsyncFetchNonBlocking**|0x40|Gibt an, dass der Hauptthread beim Abrufen nie blockiert wird. Wenn nicht die angeforderte Zeile abgerufen wurde, wird die aktuelle Zeile automatisch an das Ende der Datei verschoben.<br /><br /> Wenn Sie öffnen ein [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) aus eine [Stream](../../../ado/reference/ado-api/stream-object-ado.md) mit einem dauerhaft gespeicherten **Recordset**, **AdAsyncFetchNonBlocking** keine angewendet wird. der Vorgang wird synchron und blockiert werden.<br /><br /> **AdAsynchFetchNonBlocking** hat keine Wirkung, wenn die [AdCmdTableDirect](../../../ado/reference/ado-api/commandtypeenum.md) Option dient zum Öffnen der **Recordset**.|  
|**adExecuteNoRecords**|0x80|Gibt an, dass der Befehlstext ist, einen Befehl oder gespeicherte Prozedur, der keinen Zeilen (z. B. einen Befehl, der nur Daten einfügt) zurückgibt. Wenn keine Zeilen abgerufen werden, werden sie verworfen und nicht zurückgegeben.<br /><br /> **AdExecuteNoRecords** können nur als einen optionalen Parameter übergeben werden die **Befehl** oder **Verbindung ausführen** Methode.|  
|**adExecuteStream**|0x400|Gibt an, dass die Ergebnisse der befehlsausführung eines als Stream zurückgegeben werden sollen.<br /><br /> **AdExecuteStream** können nur als einen optionalen Parameter übergeben werden die **Befehlsausführung** Methode.|  
|**adExecuteRecord**||Gibt an, dass die **CommandText** ist ein Befehl oder gespeicherte Prozedur, die eine einzelne Zeile zurückgibt, die als zurückgegeben werden sollen eine **Datensatz** Objekt.|  
|**adOptionUnspecified**|-1|Gibt an, dass der Befehl nicht angegeben wird.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC-Entsprechung  
 Paket: **com.ms.wfc.data**  
  
|Konstante|  
|--------------|  
|AdoEnums.ExecuteOption.ASYNCEXECUTE|  
|AdoEnums.ExecuteOption.ASYNCFETCH|  
|AdoEnums.ExecuteOption.ASYNCFETCHNONBLOCKING|  
|AdoEnums.ExecuteOption.NORECORDS|  
|AdoEnums.ExecuteOption.UNSPECIFIED|  
  
## <a name="applies-to"></a>Gilt für  
  
|||  
|-|-|  
|[Execute-Methode (ADO-Befehl)](../../../ado/reference/ado-api/execute-method-ado-command.md)|[Execute-Methode (ADO-Verbindung)](../../../ado/reference/ado-api/execute-method-ado-connection.md)|  
|[Open-Methode (ADO-Recordset)](../../../ado/reference/ado-api/open-method-ado-recordset.md)|[Requery-Methode](../../../ado/reference/ado-api/requery-method.md)|

