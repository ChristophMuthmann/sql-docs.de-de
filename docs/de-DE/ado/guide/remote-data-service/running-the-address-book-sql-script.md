---
title: Ausführen des Skripts Adressbuch SQL | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- address book application scenario [ADO]
- RDS scenarios [ADO]
ms.assetid: 409b3f8b-0ced-4867-acbe-b245dcdf6702
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: eadbc99a62e4ba15856ced9aa0b85a80e7be2be7
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="running-the-address-book-sql-script"></a>Die Adressbuch SQL-Skript ausführen
> [!IMPORTANT]
>  Ab Windows 8 und Windows Server 2012, sind nicht mehr RDS-Server-Komponenten in Windows-Betriebssystems enthalten (finden Sie unter Windows 8 und [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) detailliertere). RDS-Clientkomponenten werden in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Anwendungen, die RDS verwenden sollten migrieren [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Verwenden Sie das Befehlszeilendienstprogramm ISQL/Query Analyzer oder SQL Server Enterprise Manager, führen Sie in SQL-Skript (Sampleemp.sql), die:  
  
-   Erstellt eine neue Datenbank, AddrBookDB, auf dem Standardgerät.  
  
-   Eine Verbindung mit der Datenbank AddrBookDB.  
  
-   Erstellt eine Employee-Tabelle.  
  
-   Füllt die Tabelle mit Beispieldaten.  
  
-   Führt eine einfache SELECT-Anweisung, um zu überprüfen, ob die Auffüllung der Datenbanktabelle.  
  
-   Richtet ein Benutzerkonto namens "Adcdemo" mit dem Kennwort "Adcdemo."  
  
#### <a name="to-run-the-sampleempsql-script-in-microsoft-sql-server-65"></a>Zum Ausführen des Sampleemp.sql-Skripts in Microsoft SQL Server 6.5  
  
1.  Klicken Sie auf **starten**, zeigen Sie auf **Programme**, und zeigen Sie dann auf **Microsoft SQL Server 6.5**. Klicken Sie auf **SQL Enterprise Manager**.  
  
2.  Aus der **Tools** Menü klicken Sie auf **SQL-Abfragetool**.  
  
3.  Klicken Sie auf **SQL-Skript laden** und navigieren Sie zu c:\Platform SDK\Samples\DataAccess\RDS\AddressBook.  
  
4.  Wählen Sie die Datei Sampleemp.sql. Klicken Sie auf **Öffnen**.  
  
5.  Klicken Sie auf die **Abfrage ausführen** Schaltfläche (der grüne Pfeil auf der Symbolleiste).  
  
6.  Nachdem er ausgeführt wird, schließen Sie die **Abfrage** und **Enterprise Manager** Windows.  
  
#### <a name="to-run-the-sampleempsql-script-in-microsoft-sql-server-70"></a>Zum Ausführen des Sampleemp.sql-Skripts in Microsoft SQL Server 7.0  
  
1.  Klicken Sie auf **starten**, zeigen Sie auf **Programme**, und zeigen Sie dann auf **Microsoft SQL Server 7.0**. Klicken Sie auf **Enterprise Manager**.  
  
2.  Achten Sie darauf, dass die SQL-Server, die Sie verwenden möchten, aus der Liste der registrierten Server in Enterprise Manager ausgewählt ist.  
  
3.  Aus der **Tools** Menü klicken Sie auf **SQL Server Query Analyzer**.  
  
4.  Klicken Sie auf die **SQL-Skript laden** Schaltfläche (den geöffneten Ordner auf der Symbolleiste), und navigieren Sie zu c:\Platform SDK\Samples\DataAccess\RDS\AddressBook.  
  
5.  Wählen Sie die Datei Sampleemp.sql. Klicken Sie auf **Öffnen**.  
  
6.  Klicken Sie auf die **Abfrage ausführen** Schaltfläche (der grüne Pfeil auf der Symbolleiste) oder **F5**.  
  
7.  Nachdem er ausgeführt wird, schließen Sie die **Abfrage**, **Query Analyzer**, und **Enterprise Manager** Windows.  
  
## <a name="see-also"></a>Siehe auch  
 [Ausführen der Adress Book-Beispielanwendung](../../../ado/guide/remote-data-service/running-the-address-book-sample-application.md)


