---
title: 'Schritt 2: Aufrufen des Programms (RDS-Lernprogramm) | Microsoft Docs'
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: RDS tutorial [ADO], invoking server program
ms.assetid: 5e74c2da-65ee-4de4-8b41-6eac45c3632e
caps.latest.revision: "14"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b660e20a92bdebe80def1d487cfa47b8c79109a9
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="step-2-invoke-the-server-program-rds-tutorial"></a>Schritt 2: Aufrufen des Programms (RDS-Lernprogramm)
Beim Aufruf einer Methode auf dem Client *Proxy*, das tatsächliche Programm auf dem Server führt die Methode. In diesem Schritt führen Sie eine Abfrage auf dem Server.  
  
> [!IMPORTANT]
>  Ab Windows 8 und Windows Server 2012, sind nicht mehr RDS-Server-Komponenten in Windows-Betriebssystems enthalten (finden Sie unter Windows 8 und [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) detailliertere). RDS-Clientkomponenten werden in einer zukünftigen Version von Windows entfernt werden. Nutzen Sie diese Funktionen bei Neuentwicklungen nicht mehr, und planen Sie die Änderung von Anwendungen, die diese Funktion zurzeit verwenden. Anwendungen, die RDS verwenden sollten migrieren [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
 **Teil A** bei Verwendung von nicht waren [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) die einfachste Möglichkeit zum Ausführen dieses Schritts wäre in diesem Lernprogramm verwendet den [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) Objekt. Die **RDS. DataControl** verbindet den vorherigen Schritt erstellen Sie einen Proxy mit diesem Schritt wird die Ausgabe der Abfrage.  
  
 Legen Sie die **RDS. DataControl** Objekt [Server](../../../ado/reference/rds-api/server-property-rds.md) Eigenschaft identifizieren, in denen die Server-Anwendung instanziiert werden soll; die [verbinden](../../../ado/reference/rds-api/connect-property-rds.md) Eigenschaft die Verbindungszeichenfolge für den Zugriff auf die Datenquelle angeben und die [SQL](../../../ado/reference/rds-api/sql-property.md) -Eigenschaft Befehlstext der Abfrage an. Geben Sie dann die [aktualisieren](../../../ado/reference/rds-api/refresh-method-rds.md) Methode dazu führen, dass die Server-Anwendung eine Verbindung mit der Datenquelle und Abrufen von Zeilen, die von der Abfrage angegeben und Zurückgeben einer **Recordset** Objekt an den Client.  
  
 Dieses Lernprogramm verwendet nicht die **RDS. DataControl**, aber dies ist, wie es aussehen würde, wenn dem so wäre:  
  
```  
Sub RDSTutorial2A()  
   Dim DC as New RDS.DataControl  
   DC.Server = "http://yourServer"  
   DC.Connect = "DSN=Pubs"  
   DC.SQL = "SELECT * FROM Authors"  
   DC.Refresh  
...  
```  
  
 Noch Ruft das Lernprogramm RDS mit ADO-Objekten auf, aber dies ist wie es aussehen würde, wenn dem so wäre:  
  
```  
Dim rs as New ADODB.Recordset  
rs.Open "SELECT * FROM Authors","Provider=MS Remote;Data Source=Pubs;" & _  
        "Remote Server=http://yourServer;Remote Provider=SQLOLEDB;"  
```  
  
 **Teil B** die allgemeine Methode zur Durchführung dieses Schrittes ist das Aufrufen der **RDSServer.DataFactory** Objekt [Abfrage](../../../ado/reference/rds-api/query-method-rds.md) Methode. Diese Methode akzeptiert eine Verbindungszeichenfolge, die zum Herstellen einer Verbindung mit einer Datenquelle verwendet wird, und einen Befehlstext, dient zur Angabe der Zeilen aus der Datenquelle zurückgegeben werden.  
  
 Dieses Lernprogramm verwendet den **DataFactory** Objekt **Abfrage** Methode:  
  
```  
Sub RDSTutorial2B()  
   Dim DS as New RDS.DataSpace  
   Dim DF  
   Dim RS as ADODB.Recordset  
   Set DF = DS.CreateObject("RDSServer.DataFactory", "http://yourServer")  
   Set RS = DF.Query ("DSN=Pubs", "SELECT * FROM Authors")  
...  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Schritt 3: Server erhält ein Recordset (RDS-Lernprogramm)](../../../ado/guide/remote-data-service/step-3-server-obtains-a-recordset-rds-tutorial.md)   
 [RDS-Tutorial (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   
