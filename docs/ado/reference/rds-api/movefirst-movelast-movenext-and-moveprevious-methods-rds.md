---
title: MoveFirst, MoveLast, MoveNext und MovePrevious-Methoden (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- MoveLast method [RDS]
- MovePrevious method [RDS]
- MoveFirst method [RDS]
- MoveNext method [RDS]
ms.assetid: 45c80bb5-136f-4204-9df2-78740fa55574
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 315ebd2a4de1a98634a5077096c0909550d979e6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="movefirst-movelast-movenext-and-moveprevious-methods-rds"></a>MoveFirst, MoveLast, MoveNext und MovePrevious-Methoden (RDS)
Wechselt zum ersten, letzten, nächsten oder vorherigen Datensatz in einem angegebenen [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) Objekt.  
  
> [!IMPORTANT]
>  Ab Windows 8 und Windows Server 2012, sind nicht mehr RDS-Server-Komponenten in Windows-Betriebssystems enthalten (finden Sie unter Windows 8 und [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) detailliertere). RDS-Clientkomponenten werden in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Anwendungen, die RDS verwenden sollten migrieren [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Syntax  
  
```  
  
DataControl.Recordset.{MoveFirst | MoveLast | MoveNext | MovePrevious}  
```  
  
#### <a name="parameters"></a>Parameter  
 *DataControl*  
 Objektvariable stellt eine [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) Objekt.  
  
## <a name="remarks"></a>Hinweise  
 Sie können der **verschieben** Methoden mit der **RDS. DataControl** -Objekt zum Navigieren durch die Datensätze in die datengebundene Steuerelemente auf einer Webseite. Nehmen wir beispielsweise an, die Sie anzeigen, eine **Recordset** in einem Raster von der Bindung an eine **RDS. DataControl** Objekt. Dann können Sie First, Last, weiter und zurück Schaltflächen, die Benutzer, um verschieben auf den ersten, letzten, nächsten klicken können, einfügen oder vorherigen Datensatz in der angezeigten **Recordset**. Dazu rufen die **MoveFirst**, **MoveLast**, **MoveNext**, und **MovePrevious** Methoden die **RDS. DataControl** bzw. Objekt in den OnClick Verfahren für die Schaltflächen First, Last, weiter und zurück. Die [Adressbuch Beispiel](../../../ado/guide/remote-data-service/address-book-navigation-buttons.md) veranschaulicht dies.  
  
## <a name="applies-to"></a>Gilt für  
 [DataControl-Objekt (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Move-Methode (ADO)](../../../ado/reference/ado-api/move-method-ado.md)   
 [MoveFirst, MoveLast, MoveNext und MovePrevious-Methoden (ADO)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)   
 [MoveRecord-Methode (ADO)](../../../ado/reference/ado-api/moverecord-method-ado.md)


