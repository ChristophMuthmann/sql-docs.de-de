---
title: URL-Eigenschaft (RDS) | Microsoft Docs
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.component: reference
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords:
- URL property [ADO]
ms.assetid: 8c56b233-1be8-442c-8d0e-a4c96465bc99
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0f050d414dce5afcdfff8457e93505068cb7d8d9
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="url-property-rds"></a>URL-Eigenschaft (RDS)
Gibt eine Zeichenfolge, die eine relative oder absolute URL enthält, an.  
  
 Sie können festlegen, die **URL** Eigenschaft zur Entwurfszeit in der [DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) OBJEKTS kennzeichnen oder zur Laufzeit in Skriptcode.  
  
> [!IMPORTANT]
>  Ab Windows 8 und Windows Server 2012, sind nicht mehr RDS-Server-Komponenten in Windows-Betriebssystems enthalten (finden Sie unter Windows 8 und [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) detailliertere). RDS-Clientkomponenten werden in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Anwendungen, die RDS verwenden sollten migrieren [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Design time: <PARAM NAME="URL" VALUE="Server">  
Run time: DataControl.URL="Server"  
```  
  
#### <a name="parameters"></a>Parameter  
 *Server*  
 Ein **Zeichenfolge** Wert, der eine gültige URL enthält.  
  
 *DataControl*  
 Objektvariable stellt eine **DataControl** Objekt.  
  
## <a name="remarks"></a>Hinweise  
 In der Regel identifiziert die URL für eine Active Server Page (ASP)-Datei, die erstellen und zurückgeben kann eine [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md). Aus diesem Grund erhalten Benutzer eine **Recordset** ohne Aufrufen der serverseitigen [DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) -Objekts oder ein benutzerdefiniertes Geschäftsobjekt programmieren.  
  
 Wenn die **URL** Eigenschaft festgelegt wurde, [SubmitChanges](../../../ado/reference/rds-api/submitchanges-method-rds.md) wird Änderungen an den Speicherort, der die URL senden.  
  
## <a name="applies-to"></a>Gilt für  
 [DataControl-Objekt (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Siehe auch  
 [URL-Eigenschaft – Beispiel (VBScript)](../../../ado/reference/rds-api/url-property-example-vbscript.md)


