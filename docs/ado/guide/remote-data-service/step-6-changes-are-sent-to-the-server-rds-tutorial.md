---
title: "Schritt 6: Änderungen werden an den Server gesendet (RDS-Lernprogramm) | Microsoft Docs"
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
- RDS tutorial [ADO], changes sent to server
ms.assetid: b1e927d6-7d50-4978-9eef-045043cdce7a
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b811d4b5fb1809c0e528f644f28d81559d5df6b6
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="step-6-changes-are-sent-to-the-server-rds-tutorial"></a>Schritt 6: Änderungen werden an den Server (RDS-Lernprogramm) gesendet.
Wenn die **Recordset** Objekt bearbeitet wird, können alle Änderungen (d. h. Zeilen, die hinzugefügt, geändert oder gelöscht werden) an den Server gesendet werden.  
  
> [!NOTE]
>  Das Standardverhalten von RDS kann implizit mit ADO-Objekten und der Microsoft OLE DB-Anbieter für Remoting aufgerufen werden. Abfragen können zurückgeben **Recordset**s, und bearbeitete **Recordset**s die Datenquelle aktualisieren kann. In diesem Lernprogramm keine RDS mit ADO-Objekten aufgerufen, aber dies ist, wie es aussehen würde, wenn dem so wäre:  
  
```  
Dim rs as New ADODB.Recordset  
rs. "SELECT * FROM Authors","=MS Remote;=Pubs;" & _  
=http://yourServer;=SQLOLEDB;"  
...              ' Edit the Recordset.  
rs.   ' The equivalent of   
...  
```  
  
 **Teil A** annehmen, dass für diesen Fall, die Sie, nur verwendet haben die [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) und eine **Recordset** Objekt jetzt zugeordnet ist die **RDS. DataControl**. Die [SubmitChanges](../../../ado/reference/rds-api/submitchanges-method-rds.md) Methode aktualisiert die Datenquelle mit allen Änderungen der **Recordset** Objekt, wenn die [Server](../../../ado/reference/rds-api/server-property-rds.md) und [verbinden](../../../ado/reference/rds-api/connect-property-rds.md) Eigenschaften werden immer noch festgelegt.  
  
```  
Sub RDSTutorial6A()  
Dim DC as New RDS.DataControl  
Dim RS as ADODB.Recordset  
DC. = "http://yourServer"  
DC. = "DSN=Pubs"  
DC. = "SELECT * FROM Authors"  
DC.  
...  
Set RS = DC.  
   ' Edit the Recordset.  
...  
DC.  
...  
```  
  
 **Teil B** Alternativ könnte Sie aktualisieren Sie den Server mit der [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) Objekt, das Angeben einer Verbindung und eine **Recordset** Objekt.  
  
```  
Sub RDSTutorial6B()  
Dim DS As New RDS.DataSpace  
Dim RS As ADODB.Recordset  
Dim DC As New RDS.DataControl  
Dim DF As Object  
Dim blnStatus As Boolean  
Set DF = DS.("RDSServer.DataFactory", "http://yourServer")  
Set RS = DF. ("DSN=Pubs", "SELECT * FROM Authors")  
DC. = RS    ' Visual controls can now bind to DC.  
    ' Edit the Recordset.  
blnStatus = DF."DSN=Pubs", RS  
End Sub  
```  
  
 **Dies ist das Ende des Lernprogramms.**  
  
> [!IMPORTANT]
>  Ab Windows 8 und Windows Server 2012, sind nicht mehr RDS-Server-Komponenten in Windows-Betriebssystems enthalten (finden Sie unter Windows 8 und [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) detailliertere). RDS-Clientkomponenten werden in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Anwendungen, die RDS verwenden sollten migrieren [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="see-also"></a>Siehe auch  
 [Microsoft OLE DB-Anbieter für Remoting (ADO-Dienstanbieter)](../../../ado/guide/appendixes/microsoft-ole-db-remoting-provider-ado-service-provider.md)   
 [RDS-Lernprogramm](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [RDS-Tutorial (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   

