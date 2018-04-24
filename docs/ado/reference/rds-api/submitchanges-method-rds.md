---
title: SubmitChanges-Methode (RDS) | Microsoft Docs
ms.technology:
- drivers
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
- SubmitChanges method [ADO]
ms.assetid: 250062a4-13c4-4bed-807d-8b9ad81536d4
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a297a6f41fe3a191742ef6e92f84ecbc2e971eae
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="submitchanges-method-rds"></a>SubmitChanges-Methode (RDS)
Ausstehende Änderungen von der lokal zwischengespeicherten und aktualisierbare übermittelt [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) mit der Datenquelle angegeben, der [verbinden](../../../ado/reference/rds-api/connect-property-rds.md) Eigenschaft oder die [URL](../../../ado/reference/rds-api/url-property-rds.md) Eigenschaft.  
  
> [!IMPORTANT]
>  Ab Windows 8 und Windows Server 2012, sind nicht mehr RDS-Server-Komponenten in Windows-Betriebssystems enthalten (finden Sie unter Windows 8 und [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) detailliertere). RDS-Clientkomponenten werden in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Anwendungen, die RDS verwenden sollten migrieren [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Syntax  
  
```  
  
DataControl.SubmitChanges DataFactory.SubmitChanges Connection, Recordset  
```  
  
#### <a name="parameters"></a>Parameter  
 *DataControl*  
 Objektvariable stellt eine [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) Objekt.  
  
 *DataFactory*  
 Objektvariable stellt eine [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) Objekt.  
  
 *Verbindung*  
 Ein **Zeichenfolge** -Wert, der die Verbindung erstellt, mit der **RDS. DataControl** des Objekts [verbinden](../../../ado/reference/rds-api/connect-property-rds.md) Eigenschaft.  
  
 *Recordset*  
 Objektvariable stellt eine **Recordset** Objekt.  
  
## <a name="remarks"></a>Hinweise  
 Die [verbinden](../../../ado/reference/rds-api/connect-property-rds.md), [Server](../../../ado/reference/rds-api/server-property-rds.md), und [SQL](../../../ado/reference/rds-api/sql-property.md) Eigenschaften müssen festgelegt werden, bevor Sie verwenden können, die **SubmitChanges** Methode mit der  **RDS. DataControl** Objekt.  
  
 Beim Aufrufen der [CancelUpdate](../../../ado/reference/rds-api/cancelupdate-method-rds.md) -Methode auf, nachdem Sie aufgerufen haben **SubmitChanges** für dieselbe **Recordset** -Objekt, das **CancelUpdate** -Abruf fehlschlägt, da die Änderungen bereits ein Commit ausgeführt wurde.  
  
 Nur die geänderten Datensätze werden für die Änderung und entweder alle Änderungen gesendet, entweder erfolgreich sind oder alle Änderungen für die zusammen ein.  
  
 Sie können **SubmitChanges** nur mit der standardmäßigen **RDSServer.DataFactory** Objekt. Diese Methode können keine benutzerdefinierten Geschäftsobjekte.  
  
 Wenn die **URL** Eigenschaft festgelegt wurde, **SubmitChanges** wird Änderungen an den Speicherort, der die URL senden.  
  
## <a name="applies-to"></a>Gilt für  
  
|||  
|-|-|  
|[DataControl-Objekt (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)|[DataFactory-Objekt (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [SubmitChanges-Methode (Beispiel (VBScript)](../../../ado/reference/rds-api/submitchanges-method-example-vbscript.md)   
 [Behandeln von Buch Befehlsschaltflächen](../../../ado/guide/remote-data-service/address-book-command-buttons.md)   
 [CancelUpdate-Methode (RDS)](../../../ado/reference/rds-api/cancelupdate-method-rds.md)   
 [Refresh-Methode (RDS)](../../../ado/reference/rds-api/refresh-method-rds.md)



