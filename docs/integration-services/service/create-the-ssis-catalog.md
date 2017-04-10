---
title: "Erstellen des SSIS-Katalogs | Microsoft Docs"
ms.custom: 
  - "ssisdev020617"
ms.date: "11/16/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6ed56d36-18d9-40c2-b51f-f2a4c71d1e73
caps.latest.revision: 17
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 17
---
# Erstellen des SSIS-Katalogs
  Nachdem Sie Pakete in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]entworfen und getestet haben, können Sie die Projekte, die die Pakete enthalten, auf einem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Server bereitstellen. Bevor Sie die Projekte auf dem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Server bereitstellen können, muss der **SSISDB**-Katalog auf dem Server vorhanden sein. Der Katalog wird vom Installationsprogramm für [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] nicht automatisch erstellt, Sie müssen den Katalog nach folgenden Anweisungen manuell erstellen.  
  
 Sie können den SSISDB-Katalog in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]erstellen. Sie können den Katalog auch programmgesteuert mit Windows PowerShell erstellen.  
  
### So erstellen Sie den SSISDB-Katalog in SQL Server Management Studio  
  
1.  Öffnen Sie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
2.  Stellen Sie eine Verbindung mit dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbankmodul her.  
  
3.  Erweitern Sie im Objekt-Explorer den Serverknoten, klicken Sie mit der rechten Maustaste auf **Integration Services-Kataloge**, und klicken Sie anschließend auf **Katalog erstellen**.  
  
4.  Klicken Sie auf **CLR-Integration aktivieren**.  
  
     Für den Katalog werden gespeicherte CLR-Prozeduren verwendet.  
  
5.  Klicken Sie auf **Automatische Ausführung gespeicherter Integration Services-Prozeduren beim Starten von SQL Server aktivieren**, um die gespeicherte Prozedur [catalog.startup](../../integration-services/system-stored-procedures/catalog-startup.md) jedes Mal ausführen zu lassen, wenn die [!INCLUDE[ssIS](../../includes/ssis-md.md)]-Serverinstanz neu gestartet wird.  
  
     Durch die gespeicherte Prozedur wird der Status von Vorgängen für den SSISDB-Katalog verwaltet. Dabei wird der Status aller Pakete korrigiert, die während des Ausfalls (falls zutreffend) der [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Serverinstanz ausgeführt wurden.  
  
6.  Geben Sie ein Kennwort ein, und klicken Sie dann auf **OK**.  
  
     Das Kennwort schützt den Datenbank-Hauptschlüssel, der zum Verschlüsseln der Katalogdaten verwendet wird. Bewahren Sie das Kennwort sicher auf. Es wird empfohlen, auch den Datenbank-Hauptschlüssel zu sichern. Weitere Informationen finden Sie unter [Back Up a Database Master Key](../../relational-databases/security/encryption/back-up-a-database-master-key.md).  
  
### So erstellen Sie den SSISDB-Katalog programmgesteuert  
  
1.  Führen Sie das folgende PowerShell-Skript aus:  
  
    ```  
    # Load the IntegrationServices Assembly  
    [Reflection.Assembly]::LoadWithPartialName("Microsoft.SqlServer.Management.IntegrationServices")  
  
    # Store the IntegrationServices Assembly namespace to avoid typing it every time  
    $ISNamespace = "Microsoft.SqlServer.Management.IntegrationServices"  
  
    Write-Host "Connecting to server ..."  
  
    # Create a connection to the server  
    $sqlConnectionString = "Data Source=localhost;Initial Catalog=master;Integrated Security=SSPI;"  
    $sqlConnection = New-Object System.Data.SqlClient.SqlConnection $sqlConnectionString  
  
    # Create the Integration Services object  
    $integrationServices = New-Object $ISNamespace".IntegrationServices" $sqlConnection  
  
    # Provision a new SSIS Catalog  
    $catalog = New-Object $ISNamespace".Catalog" ($integrationServices, "SSISDB", "P@assword1")  
    $catalog.Create()  
  
    ```  
  
     Weitere Beispiele zum Verwenden von Windows PowerShell und des <xref:Microsoft.SqlServer.Management.IntegrationServices>-Namespaces finden Sie im Blogeintrag [SSIS and PowerShell in SQL Server 2012](http://go.microsoft.com/fwlink/?LinkId=242539) (SSIS und PowerShell in SQL Server 2012) auf „blogs.msdn.com“. Eine Übersicht über den Namespace und Codebeispiele finden Sie im Blogeintrag [A Glimpse of the SSIS Catalog Managed Object Model](http://go.microsoft.com/fwlink/?LinkId=254267) (Übersicht über das SSIS-Katalogmodell verwalteter Objekte) auf „blogs.msdn.com“.  
  
## Siehe auch  
 [SSIS-Katalog](../../integration-services/service/ssis-catalog.md)   
 [Sichern, Wiederherstellen und Verschieben des SSIS-Katalogs](../../integration-services/service/backup-restore-and-move-the-ssis-catalog.md)  
  
  