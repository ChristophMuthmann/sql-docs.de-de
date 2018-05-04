---
title: SQL-Eigenschaft | Microsoft Docs
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.prod: sql
ms.prod_service: drivers
ms.component: reference
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- SQL property [RDS]
ms.assetid: e0dabf23-a159-4fe5-a962-3df544a21f5c
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a5ddbfa6b69f4859f61130e8ec1c9b758c40cf64
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sql-property"></a>SQL-Eigenschaft
Gibt die Abfragezeichenfolge zum Abrufen der [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
 Sie können festlegen, die **SQL** Eigenschaft zur Entwurfszeit in den [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) Objekttags des Objekts, oder zur Laufzeit im Skriptcode.  
  
> [!IMPORTANT]
>  Ab Windows 8 und Windows Server 2012, sind nicht mehr RDS-Server-Komponenten in Windows-Betriebssystems enthalten (finden Sie unter Windows 8 und [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) detailliertere). RDS-Clientkomponenten werden in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Anwendungen, die RDS verwenden sollten migrieren [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Design time: <PARAM NAME="SQL" VALUE="QueryString">  
Run time: DataControl.SQL = "QueryString"  
```  
  
#### <a name="parameters"></a>Parameter  
 *QueryString*  
 Ein **Zeichenfolge** Wert, der eine gültige SQL-Daten-Anforderung enthält.  
  
 *DataControl*  
 Objektvariable stellt eine **RDS. DataControl** Objekt.  
  
## <a name="remarks"></a>Hinweise  
 Im Allgemeinen ist dies eine SQL-Anweisung (mit dem Dialekt des Datenbankservers), wie z. B. `"Select * from NewTitles"`. Um sicherzustellen, dass Datensätze übereinstimmen und richtig aktualisiert werden, muss eine aktualisierbare Abfrage ein Feld als ein lang binäres Feld oder ein berechnetes Feld enthalten.  
  
 Die **SQL** Eigenschaft ist optional, wenn ein benutzerdefiniertes Geschäftsobjekt serverseitige für den Client die Daten abruft.  
  
## <a name="applies-to"></a>Gilt für  
 [DataControl-Objekt (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Siehe auch  
 [SQL-Eigenschaft-Beispiel (VBScript)](../../../ado/reference/rds-api/sql-property-example-vbscript.md)   
 [Connect-Eigenschaft (RDS)](../../../ado/reference/rds-api/connect-property-rds.md)   
 [Query-Methode (RDS)](../../../ado/reference/rds-api/query-method-rds.md)   
 [Refresh-Methode (RDS)](../../../ado/reference/rds-api/refresh-method-rds.md)   
 [SubmitChanges-Methode (RDS)](../../../ado/reference/rds-api/submitchanges-method-rds.md)


