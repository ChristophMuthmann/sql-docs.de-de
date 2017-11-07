---
title: Verschieben eine Analysis Services-Datenbank | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- moving databases [Anlysis Services]
- moving databases
- operations [Analysis Services - multidimensional data]
ms.assetid: fa644e5d-e276-445e-98d9-673afcfb83fe
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 73d410fdb16765b5ae1022362f11be8e918140fa
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="move-an-analysis-services-database"></a>Verschieben einer Analysis Services Datenbank
  Es gibt oftmals Situationen, in denen ein [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbankadministrator (DBA) eine mehrdimensionale oder tabellarische Modelldatenbank an einen anderen Speicherort verschieben möchte. Diese Situationen hängen in der Regel von Geschäftsforderungen ab, z. B. wenn die Datenbank zur Leistungssteigerung auf einen anderen Datenträger verschoben werden soll, wenn bei Datenbankzuwachs Platz geschaffen werden muss oder wenn ein Produkt aktualisiert werden soll.  
  
 Es stehen zahlreiche Möglichkeiten zum Verschieben einer Datenbank zur Verfügung. In diesem Dokument werden die folgenden gängigen Szenarien erläutert:  
  
-   Interaktiv mithilfe von SSMS  
  
-   Programmgesteuert mithilfe von AMO  
  
-   Mit einem Skript mithilfe von XMLA  
  
 In allen Szenarien muss der Benutzer auf den Datenbankordner zugreifen und eine Methode zum Verschieben der Dateien an das gewünschte endgültige Ziel verwenden.  
  
> [!NOTE]  
>  Wenn Sie eine Datenbank trennen, ohne ihr ein Kennwort zuzuweisen, befindet sich die Datenbank in einem ungesicherten Zustand. Es wird daher empfohlen, dass Sie der Datenbank ein Kennwort zuweisen, um vertrauliche Informationen zu schützen. Zudem sollten Sie die entsprechende Zugriffssicherheit auf den Datenbankordner, die Unterordner und die Dateien anwenden, um den nicht autorisierten Zugriff darauf zu verhindern.  
  
## <a name="procedures"></a>Vorgehensweisen  
  
#### <a name="moving-a-database-interactively-using-ssms"></a>Interaktives Verschieben einer Datenbank mithilfe von SSMS  
  
1.  Suchen Sie im linken oder rechten Bereich von SSMS nach der zu verschiebenden Datenbank.  
  
2.  Klicken Sie mit der rechten Maustaste auf die Datenbank, und wählen Sie **Trennen**aus.  
  
3.  Weisen Sie der Datenbank, die getrennt werden soll, ein Kennwort zu, und klicken Sie dann auf **OK** , um den Befehl zum Trennen auszuführen.  
  
4.  Verwenden Sie einen Mechanismus des Betriebssystems oder eine Standardmethode zum Verschieben des Datenbankordners an einen neuen Speicherort.  
  
5.  Suchen Sie im linken oder rechten Bereich von SSMS nach dem Ordner **Datenbanken** .  
  
6.  Klicken Sie mit der rechten Maustaste auf den Ordner **Datenbanken** , und wählen Sie **Anfügen**aus.  
  
7.  Geben Sie im Textfeld **Ordner** den neuen Speicherort des Datenbankordners ein. Sie können auch über die Schaltfläche zum Durchsuchen (**…**) nach dem Datenbankordner suchen.  
  
8.  Wählen Sie den **Lese-/Schreibmodus** für die Datenbank aus.  
  
9. Geben Sie das in Schritt 3 verwendete Kennwort ein, und klicken Sie auf **OK** , um den Befehl zum Anfügen auszuführen.  
  
#### <a name="moving-a-database-programmatically-using-amo"></a>Programmgesteuertes Verschieben einer Datenbank mithilfe von AMO  
  
1.  Passen Sie in der C#-Anwendung den folgenden Beispielcode an, und führen Sie die angegebenen Aufgaben aus.  
  
 `private void MoveDb(Server server, string dbName,`  
  
 `string dbInitialLocation, string dbFinalLocation,`  
  
 `string dbPassword, ReadWriteMode dbReadWriteMode)`  
  
 `{`  
  
 `//Verify dbInitialLocation exists before continuing`  
  
 `if (server.Databases.ContainsName(dbName))`  
  
 `{`  
  
 `Database db;`  
  
 `//Save current cursor and change cursor to Cursors.WaitCursor`  
  
 `db = server.Databases[dbName];`  
  
 `db.Detach(dbPassword);`  
  
 `//Add your own code to copy the database files to the destination where you intend to attach the database`  
  
 `//Verify dbFinalLocation exists before continuing`  
  
 `server.Attach(dbFinalLocation, dbReadWriteMode, dbPassword);`  
  
 `//Restore cursor to its original`  
  
 `}`  
  
 `}`  
  
1.  Rufen Sie in der C#-Anwendung `MoveDb()` mit den erforderlichen Parametern auf.  
  
2.  Kompilieren Sie den Code, und führen Sie ihn zum Verschieben der Datenbank aus.  
  
#### <a name="moving-a-database-by-script-using-xmla"></a>Verschieben einer Datenbank mit einem Skript mithilfe von XMLA  
  
1.  Öffnen Sie in SSMS eine neue XMLA-Registerkarte.  
  
2.  Kopieren Sie die folgende Skriptvorlage für XMLA:  
  
 `<Detach xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">`  
  
 `<Object>`  
  
 `<DatabaseID>%dbName%</DatabaseID>`  
  
 `<Password>%password%</Password>`  
  
 `</Object>`  
  
 `</Detach>`  
  
1.  Ersetzen Sie `%dbName%` durch den Namen der Datenbank und `%password%` durch das Kennwort. Die %-Zeichen sind Teil der Vorlage und müssen entfernt werden.  
  
2.  Führen Sie den XMLA-Befehl aus.  
  
3.  Verwenden Sie einen Mechanismus des Betriebssystems oder eine Standardmethode zum Verschieben des Datenbankordners an einen neuen Speicherort.  
  
4.  Kopieren Sie die folgende Skriptvorlage für XMLA in eine neue XMLA-Registerkarte:  
  
 `<Attach xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">`  
  
 `<Folder>%dbFolder%</Folder>`  
  
 `<ReadWriteMode xmlns="http://schemas.microsoft.com/analysisservices/2008/engine/100">%ReadOnlyMode%</ReadWriteMode>`  
  
 `</Attach>`  
  
1.  Ersetzen Sie `%dbFolder%` durch den vollständigen UNC-Pfad des Datenbankordners, `%ReadOnlyMode%` durch den entsprechenden Wert **ReadOnly** oder **ReadWrite**und `%password%` durch das Kennwort. Die %-Zeichen sind Teil der Vorlage und müssen entfernt werden.  
  
2.  Führen Sie den XMLA-Befehl aus.  
  
## <a name="see-also"></a>Siehe auch  
 <xref:Microsoft.AnalysisServices.Core.Server.Attach%2A>   
 <xref:Microsoft.AnalysisServices.Database.Detach%2A>   
 [Anfügen und Trennen von Analysis Services-Datenbanken](../../analysis-services/multidimensional-models/attach-and-detach-analysis-services-databases.md)   
 [Datenbankspeicherort](../../analysis-services/multidimensional-models/database-storage-location.md)   
 [Datenbank-ReadWriteModes](../../analysis-services/multidimensional-models/database-readwritemodes.md)   
 [Attach-Element](../../analysis-services/xmla/xml-elements-commands/attach-element.md)   
 [Detach-Element](../../analysis-services/xmla/xml-elements-commands/detach-element.md)   
 [ReadWriteMode-Element](../../analysis-services/xmla/xml-elements-properties/readwritemode-element.md)   
 [DbStorageLocation-Element](../../analysis-services/xmla/xml-elements-properties/dbstoragelocation-element.md)  
  
  

