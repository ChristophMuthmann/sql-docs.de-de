---
title: Recordset SourceRecordset-Eigenschaft (RDS) | Microsoft Docs
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
helpviewer_keywords:
- Recordset property [ADO]
ms.assetid: a29e3fb9-306d-497a-9a59-1856a914e5e9
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2c5ce9fc2ef297c44f4bcfb3868168d0cb1dda15
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="recordset-sourcerecordset-properties-rds"></a>Recordset SourceRecordset-Eigenschaft (RDS)
Gibt an, die **Recordset** vom ein benutzerdefiniertes Geschäftsobjekt zurückgegebenen Objekts.  
  
 **Gilt für:** [RDS (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
> [!IMPORTANT]
>  Ab Windows 8 und Windows Server 2012, sind nicht mehr RDS-Server-Komponenten in Windows-Betriebssystems enthalten (finden Sie unter Windows 8 und [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) detailliertere). RDS-Clientkomponenten werden in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Anwendungen, die RDS verwenden sollten migrieren [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Syntax  
  
```  
  
DataControl.SourceRecordset = Recordset  
Recordset = DataControl.Recordset   
```  
  
#### <a name="parameters"></a>Parameter  
 *DataControl*  
 Objektvariable stellt eine [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) Objekt.  
  
 *Recordset*  
 Objektvariable stellt eine **Recordset** Objekt.  
  
## <a name="remarks"></a>Hinweise  
 Sie können festlegen, die **SourceRecordset** Eigenschaft, um eine [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) aus einem benutzerdefinierten Geschäftsobjekt zurückgegeben.  
  
 Diese Eigenschaften ermöglichen es eine Anwendung zur Handhabung der Bindungsprozess durch einen benutzerdefinierten Prozess. Erhalt ein Rowsets, die eingebunden in eine **Recordset** , damit Sie direkt interagieren können die **Recordset**, Ausführen von Aktionen wie das Festlegen von Eigenschaften oder durchlaufen die **Recordset **.  
  
 Sie können festlegen, die **SourceRecordset** -Eigenschaft, oder erfahren Sie die **Recordset** Eigenschaft zur Laufzeit in Skriptcode.  
  
 **SourceRecordset** ist eine Nur-Schreiben Eigenschaft, im Gegensatz zu den **Recordset** -Eigenschaft, die eine Eigenschaft schreibgeschützt ist.  
  
## <a name="applies-to"></a>Gilt für  
 [RDS (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Recordset und SourceRecordset Eigenschaften Beispiel (VBScript)](../../../ado/reference/rds-api/recordset-and-sourcerecordset-properties-example-vbscript.md)   
 [CreateRecordset-Methode (RDS)](../../../ado/reference/rds-api/createrecordset-method-rds.md)   
 [Query-Methode (RDS)](../../../ado/reference/rds-api/query-method-rds.md)



