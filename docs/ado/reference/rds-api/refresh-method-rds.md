---
title: Refresh-Methode (RDS) | Microsoft Docs
ms.technology: drivers
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
f1_keywords:
- Refresh
- RDS.DataControl::Refresh
- DataControl::Refresh
helpviewer_keywords: Refresh method [RDS]
ms.assetid: c90a8050-0ff4-4c83-9925-261f2f2ccfe9
caps.latest.revision: "17"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5730f11f027cf6fb4492f8133f88ce80ac35aee3
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/20/2017
---
# <a name="refresh-method-rds"></a>Refresh-Methode (RDS)
Fragt die Datenquelle angegeben, der [verbinden](../../../ado/reference/rds-api/connect-property-rds.md) Eigenschaft und aktualisiert die Ergebnisse der Abfrage.  
  
> [!IMPORTANT]
>  Ab Windows 8 und Windows Server 2012, sind nicht mehr RDS-Server-Komponenten in Windows-Betriebssystems enthalten (finden Sie unter Windows 8 und [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) detailliertere). RDS-Clientkomponenten werden in einer zukünftigen Version von Windows entfernt werden. Nutzen Sie diese Funktionen bei Neuentwicklungen nicht mehr, und planen Sie die Änderung von Anwendungen, die diese Funktion zurzeit verwenden. Anwendungen, die RDS verwenden sollten migrieren [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Syntax  
  
```  
  
DataControl.Refresh  
```  
  
#### <a name="parameters"></a>Parameter  
 *DataControl*  
 Objektvariable stellt eine [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) Objekt.  
  
## <a name="remarks"></a>Hinweise  
 Sie müssen festlegen, die [verbinden](../../../ado/reference/rds-api/connect-property-rds.md), [Server](../../../ado/reference/rds-api/server-property-rds.md), und [SQL](../../../ado/reference/rds-api/sql-property.md) Eigenschaften vor der Verwendung der **aktualisieren** Methode. Alle datengebundenen Steuerelemente im Formular zugeordnet ein **RDS. DataControl** Objekt wird die neue Gruppe von Datensätzen widerzuspiegeln. Bereits vorhandene [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) Objekt freigegeben wird und alle nicht gespeicherten Änderungen werden verworfen. Die **aktualisieren** Methode wird automatisch der erste Datensatz zum aktuellen Datensatz.  
  
 Es ist eine gute Idee, rufen Sie die **aktualisieren** Methode in regelmäßigen Abständen beim Arbeiten mit Daten. Wenn Sie Daten abrufen, und lassen Sie es auf einem Clientcomputer, für eine Weile, ist es wahrscheinlich nicht mehr aktuell sind. Es ist möglich, dass Änderungen, die Sie fehl, da eine andere Person möglicherweise den Datensatz geändert haben, und übermittelt die Änderungen vor.  
  
## <a name="applies-to"></a>Gilt für  
 [DataControl-Objekt (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Aktualisieren von Methodenbeispiel (VB)](../../../ado/reference/ado-api/refresh-method-example-vb.md)   
 [Aktualisieren Sie die Methodenbeispiel (VBScript)](../../../ado/reference/rds-api/refresh-method-example-vbscript.md)   
 [Behandeln von Buch Befehlsschaltflächen](../../../ado/guide/remote-data-service/address-book-command-buttons.md)   
 [CancelUpdate-Methode (RDS)](../../../ado/reference/rds-api/cancelupdate-method-rds.md)   
 [Refresh-Methode (ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)   
 [SubmitChanges-Methode (RDS)](../../../ado/reference/rds-api/submitchanges-method-rds.md)


