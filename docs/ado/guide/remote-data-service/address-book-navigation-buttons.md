---
title: "Adresse Buch Navigationsschaltflächen | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- RDS scenarios [ADO], navigation buttons
- address book application scenario [ADO], navigation buttons
ms.assetid: f0dd84c6-5c33-4ab9-82b4-4c42dfdd2277
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 211e05c548d38ad364e8a7daa85f280e8ca62414
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="address-book-navigation-buttons"></a>Behandeln von Buch Navigationsschaltflächen
Die Adressbuch-Anwendung zeigt die Navigationsschaltflächen am unteren Rand der Webseite. Sie können die Navigationsschaltflächen verwenden, Navigieren durch die Daten in der Anzeige des HTML-Raster durch Auswählen von entweder die erste oder letzte Zeile der Daten oder Zeilen, die neben der aktuellen Auswahl.  
  
> [!IMPORTANT]
>  Ab Windows 8 und Windows Server 2012, sind nicht mehr RDS-Server-Komponenten in Windows-Betriebssystems enthalten (finden Sie unter Windows 8 und [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) detailliertere). RDS-Clientkomponenten werden in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Anwendungen, die RDS verwenden sollten migrieren [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="navigation-sub-procedures"></a>Navigation Sub-Prozeduren  
 Die Adressbuch-Anwendung enthält mehrere Verfahren, mit denen Benutzer auf die **erste**, **Weiter**, **zurück**, und **letzten** die Schaltflächen, um die Daten zu verschieben.  
  
 Klicken Sie z. B. die **erste** Schaltfläche aktiviert das VBScript First_OnClick Sub-Prozedur. Die Prozedur führt eine [MoveFirst](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md) -Methode, die der erste Zeile der Daten zur aktuellen Auswahl wird. Klicken auf die **letzten** Schaltfläche aktiviert die Unterprozedur Last_OnClick der [MoveLast](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md) -Methode, der letzten Zeile der Daten der aktuellen Auswahl getroffen. Die verbleibenden Navigationsschaltflächen funktionieren auf ähnliche Weise.  
  
```  
' Move to the first record in the bound Recordset.  
Sub First_OnClick  
   DC1.Recordset.MoveFirst  
End Sub  
  
' Move to the next record from the current position   
' in the bound Recordset.  
Sub Next_OnClick  
   If Not DC1.Recordset.EOF Then    ' Cannot move beyond bottom record.  
      DC1.Recordset.MoveNext  
      Exit Sub  
   End If     
End Sub  
  
' Move to the previous record from the current position in the bound   
' Recordset.  
Sub Prev_OnClick  
   If Not DC1.Recordset.BOF Then    ' Cannot move beyond top record.  
      DC1.Recordset.MovePrevious  
      Exit Sub  
   End If  
End Sub  
  
' Move to the last record in the bound Recordset.  
Sub Last_OnClick  
   DC1.Recordset.MoveLast  
End Sub  
```  
  
## <a name="see-also"></a>Siehe auch  
 [RDS (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)   
 [MoveFirst-, MoveLast-, MoveNext- und MovePrevious-Methode (RDS)](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)



