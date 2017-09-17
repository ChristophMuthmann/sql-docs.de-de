---
title: "Schritt 3: Server erhält ein Recordset (RDS-Lernprogramm) | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- RDS tutorial [ADO], server obtains Recordset
ms.assetid: 9c6779c9-1208-4696-ac51-c39f3a6d9240
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 62210ae4cbf206faebed32b87bdbf64edd3265d9
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="step-3-server-obtains-a-recordset-rds-tutorial"></a>Schritt 3: Server erhält ein Recordset (RDS-Lernprogramm)
Server verwendet den Connect-Zeichenfolge und Befehl Text zum Abfragen der Datenquelle für die gewünschten Zeilen. ADO wird normalerweise verwendet, um diesen abzurufen **Recordset**, obwohl andere Microsoft-Daten Schnittstellen zuzugreifen, z. B. OLE DB verwendet werden konnte.  
  
> [!IMPORTANT]
>  Ab Windows 8 und Windows Server 2012, sind nicht mehr RDS-Server-Komponenten in Windows-Betriebssystems enthalten (finden Sie unter Windows 8 und [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) detailliertere). RDS-Clientkomponenten werden in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Anwendungen, die RDS verwenden sollten migrieren [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Ein benutzerdefiniertes Serverprogramm kann wie folgt aussehen:  
  
```  
Public Function ServerProgram(cn as String, qry as String) as Object  
Dim rs as New ADODB.Recordset  
   rs.CursorLocation = adUseClient  
   rs.Open qry, cn   
   rs.ActiveConnection = Nothing  
   Set ServerProgram = rs  
End Function  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Schritt 4: Server gibt das Recordset (RDS-Lernprogramm)](../../../ado/guide/remote-data-service/step-4-server-returns-the-recordset-rds-tutorial.md)   
 [RDS-Tutorial (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   

