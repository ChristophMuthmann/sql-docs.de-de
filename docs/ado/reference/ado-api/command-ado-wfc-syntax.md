---
title: Befehl (ADO - WFC-Syntax) | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Command collection [ADO], ADO/WFC syntax
ms.assetid: 39d0aa06-03ac-4c9a-8400-83947756ef99
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 15b045d8f45e9c6c7bcc7ff10430c4b715084c33
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="command-ado---wfc-syntax"></a>Befehl (ADO - WFC-Syntax)
## <a name="package-commswfcdata"></a>Paket com.ms.wfc.data  
  
### <a name="constructor"></a>Konstruktor  
  
```  
public Command()  
public Command(String commandtext)  
```  
  
### <a name="methods"></a>Methoden  
  
```  
public void cancel()  
public com.ms.wfc.data.Parameter createParameter(String  
    Name, int Type, int Direction, int Size, Object Value)  
public Recordset execute()  
public Recordset execute(Object[] parameters)  
public Recordset execute(Object[] parameters, int options)  
public int executeUpdate(Object[] parameters)  
public int executeUpdate(Object[] parameters, int options)  
public int executeUpdate()  
```  
  
 Die **ExecuteUpdate** Methode ist eine spezielle Groß-/Kleinschreibung, die das zugrunde liegende ADO aufruft **ausführen** Methode mit bestimmten Parametern. Der **ExecuteUpdate** Methode unterstützt nicht die Rückgabe von einer **Recordset** -Objekt, damit die **ausführen** Methode *Optionen* Parameter ist mit geändert **AdoEnums.ExecuteOptions.NORECORDS**. Nach der **ausführen** Methode ausgeführt wird, die aktualisierte *RecordsAffected* Parameter übergeben wird, zurück an die **ExecuteUpdate** -Methode, die als eine schließlichzurückgegebenwird**Int**.  
  
### <a name="properties"></a>Eigenschaften  
  
```  
public com.ms.wfc.data.Connection getActiveConnection()  
public void setActiveConnection(com.ms.wfc.data.Connection con)  
public void setActiveConnection(String conString)  
public String getCommandText()  
public void setCommandText(String command)  
public int getCommandTimeout()  
public void setCommandTimeout(int timeout)  
public int getCommandType()  
public void setCommandType(int type)  
public String getName()  
public void setName(String name)  
public boolean getPrepared()  
public void setPrepared(boolean prepared)  
public int getState()  
public com.ms.wfc.data.Parameter getParameter(int n)  
public com.ms.wfc.data.Parameter getParameter(String n)  
public com.ms.wfc.data.Parameters getParameters()  
public AdoProperties getProperties()  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Command-Objekt (ADO)](../../../ado/reference/ado-api/command-object-ado.md)
