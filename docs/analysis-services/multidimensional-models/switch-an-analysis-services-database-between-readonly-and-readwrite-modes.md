---
title: Umschalten in einer Analysis Services-Datenbank zwischen Schreib-und Lesemodus | Microsoft Docs
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
- ReadOnly property
- ReadWriteMode command
- operations [Analysis Services - multidimensional data]
ms.assetid: 4eff8181-08dd-4fad-b091-d400fc21a020
caps.latest.revision: 16
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 11eaa65564dcd59442bd8b111c0de009b00e8fd4
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="switch-an-analysis-services-database-between-readonly-and-readwrite-modes"></a>Umschalten einer Analysis Services-Datenbank zwischen schreibgeschütztem Modus und Lese-/Schreibmodus
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Datenbankadministratoren können den Lese-/Schreibmodus einer tabellarischen oder mehrdimensionalen Datenbank als Teil eines größeren Vorgangs ändern, bei dem eine Abfragearbeitsauslastung auf mehrere reine Abfrageserver verteilt wird.  
  
 Es stehen mehrere Möglichkeiten zum Umschalten des Datenbankmodus zur Verfügung. In diesem Dokument werden die folgenden gängigen Szenarien erläutert:  
  
-   Interaktiv mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
  
-   Programmgesteuert mithilfe von AMO  
  
-   Skript mithilfe von XMLA oder TMSL  
  
## <a name="switch-the-readwrite-mode-of-a-database-interactively-using-management-studio"></a>Umschalten des Lese-/Schreibmodus einer Datenbank interaktiv mithilfe von Management Studio  
  
1.  Klicken Sie im Objekt-Explorer mit der rechten Maustaste auf die Datenbank, und wählen Sie **Eigenschaften**aus.  
  
     Beachten Sie den Speicherort. Ein leerer Datenbankspeicherort weist darauf hin, dass sich der Datenbankordner im Datenordner des Servers befindet.  
  
2.  Klicken Sie mit der rechten Maustaste auf die Datenbank, und wählen Sie **Trennen…**aus.  
  
3.  Weisen Sie der Datenbank, die getrennt werden soll, ein Kennwort zu, und klicken Sie anschließend auf **OK** , um den Befehl zum Trennen auszuführen.  
  
4.  Klicken Sie im Objekt-Explorer mit der rechten Maustaste auf den Ordner **Datenbanken** , und wählen Sie **Anfügen...**aus.  
  
5.  Geben Sie im Textfeld **Ordner** den ursprünglichen Speicherort des Datenbankordners ein. Alternativ können Sie über die Schaltfläche zum Durchsuchen (**…**) nach dem Datenbankordner suchen.  
  
6.  Wählen Sie den Lese-/Schreibmodus für die Datenbank aus.  
  
7.  Geben Sie das Kennwort ein, und klicken Sie auf **OK** , um den Befehl zum Anfügen auszuführen.  
  
## <a name="switch-the-readwrite-mode-to-a-database-programmatically-using-amo"></a>Umschalten des Lese-/Schreibmodus einer Datenbank programmgesteuert mithilfe von AMO  
 Rufen Sie in der C#-Anwendung `SwitchReadWrite()` mit den erforderlichen Parametern auf. Kompilieren Sie den Code, und führen Sie ihn zum Verschieben der Datenbank aus.  
  
```  
private void SwitchReadWrite(Server server, string dbName, ReadWriteMode dbReadWriteMode)  
{  
    if (server.Databases.ContainsName(dbName))  
    {  
        Database db;  
        string databaseLocation;  
        db = server.Databases[dbName];  
        databaseLocation = db.DbStorageLocation;  
  
              if (databaseLocation == null)  
            {  
                 string dataDir = server.ServerProperties["DataDir"].Value;  
                 string dataDir = server.ServerProperties["DataDir"].Value;  
                 string dataDir = server.ServerProperties["DataDir"].Value;  
  
    String[] possibleFolders = Directory.GetDirectories(dataDir, string.Concat(dbName,"*"), SearchOption.TopDirectoryOnly);  
  
   if (possibleFolders.Length > 1)  
         {  
         List<String> sortedFolders = new List<string>(possibleFolders.Length);  
         sortedFolders.AddRange(possibleFolders);  
         sortedFolders.Sort();  
         databaseLocation = sortedFolders[sortedFolders.Count - 1];  
         }  
         else  
         {  
         databaseLocation = possibleFolders[0];  
          }  
        }  
    db.Detach();  
    server.Attach(databaseLocation, dbReadWriteMode);  
    }  
}  
  
```  
  
## <a name="switch-the-readwrite-mode-to-a-database-by-script-using-xmla"></a>Umschalten des Lese-/Schreibmodus einer Datenbank mit einem Skript mithilfe von XMLA  
 Die folgenden Anweisungen gelten für mehrdimensionale und tabellarische Datenbanken im Kompatibilitätsmodus 1050, 1100 oder 1103.  
  
1.  Klicken Sie im Objekt-Explorer mit der rechten Maustaste auf die Datenbank, und wählen Sie **Eigenschaften**aus.  
  
     Beachten Sie den Speicherort. Ein leerer Datenbankspeicherort weist darauf hin, dass sich der Datenbankordner im Datenordner des Servers befindet.  
  
2.  Klicken Sie mit der rechten Maustaste auf die Datenbank, und wählen Sie **Trennen…**aus.  
  
3.  Öffnen Sie in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]eine neue XMLA-Registerkarte.  
  
4.  Kopieren Sie die folgende Skriptvorlage für XMLA:  
  
    ```  
    <Detach xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
       <Object>  
          <DatabaseID>%dbName%</DatabaseID>  
          <Password>%password%</Password>  
       </Object>  
    </Detach>  
    ```  
  
5.  Ersetzen Sie `%dbName%` durch den Namen der Datenbank und `%password%` durch das Kennwort. Die %-Zeichen sind Teil der Vorlage und müssen entfernt werden.  
  
6.  Führen Sie den XMLA-Befehl aus.  
  
7.  Kopieren Sie die folgende Skriptvorlage für XMLA in eine neue XMLA-Registerkarte:  
  
    ```  
    <Attach xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
       <Folder>%dbFolder%</Folder>  
       <ReadWriteMode xmlns="http://schemas.microsoft.com/analysisservices/2008/engine/100">%ReadOnlyMode%</ReadWriteMode>  
    </Attach>  
    ```  
  
8.  Ersetzen Sie `%dbFolder%` durch den vollständigen UNC-Pfad des Datenbankordners, `%ReadOnlyMode%` durch den entsprechenden Wert **ReadOnly** oder **ReadWrite**und `%password%` durch das Kennwort. Die %-Zeichen sind Teil der Vorlage und müssen entfernt werden.  
  
9. Führen Sie den XMLA-Befehl aus.  
  
## <a name="see-also"></a>Siehe auch  
 <xref:Microsoft.AnalysisServices.Database.Detach%2A>   
 [Hohe Verfügbarkeit und Skalierbarkeit in Analysis Services](../../analysis-services/instances/high-availability-and-scalability-in-analysis-services.md)   
 [Anfügen und Trennen von Analysis Services-Datenbanken](../../analysis-services/multidimensional-models/attach-and-detach-analysis-services-databases.md)   
 [Datenbankspeicherort](../../analysis-services/multidimensional-models/database-storage-location.md)   
 [Datenbank-ReadWriteModes](../../analysis-services/multidimensional-models/database-readwritemodes.md)   
 [Attach-Element](../../analysis-services/xmla/xml-elements-commands/attach-element.md)   
 [Detach-Element](../../analysis-services/xmla/xml-elements-commands/detach-element.md)   
 [ReadWriteMode-Element](../../analysis-services/xmla/xml-elements-properties/readwritemode-element.md)   
 [DbStorageLocation-Element](../../analysis-services/xmla/xml-elements-properties/dbstoragelocation-element.md)  
  
  

