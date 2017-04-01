---
title: "Ausf&#252;hren eines Pakets auf dem SSIS-Server mit SQL Server Management Studio | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 56dc1bf8-99d4-41dc-bdc4-f64f1ccfd688
caps.latest.revision: 9
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 9
---
# Ausf&#252;hren eines Pakets auf dem SSIS-Server mit SQL Server Management Studio
  Nachdem Sie das Projekt auf dem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Server bereitgestellt haben, können Sie das Paket auf dem Server ausführen.  
  
 Sie können Vorgangsberichte verwenden, um Informationen über Pakete anzuzeigen, deren Ausführung abgeschlossen ist bzw. die derzeit auf dem Server ausgeführt werden. Weitere Informationen finden Sie unter [Berichte für den Integration Services-Server](../../integration-services/performance/reports-for-the-integration-services-server.md).  
  
### So führen Sie mit SQL Server Management Studio ein Paket auf dem Server aus  
  
1.  Öffnen Sie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , und stellen Sie eine Verbindung mit der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] her, die den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Katalog enthält.  
  
2.  Erweitern Sie im Objekt-Explorer den Knoten **Integration Services-Kataloge** und den Knoten **SSISDB** , und navigieren Sie zu dem Paket, das im bereitgestellten Projekt enthalten ist.  
  
3.  Klicken Sie mit der rechten Maustaste auf den Paketnamen, und wählen Sie **Ausführen** aus.  
  
4.  Konfigurieren Sie die Paketausführung mit den Einstellungen im Dialogfeld **Paket ausführen**auf den Registerkarten **Parameter**, **Verbindungs-Managern** und **Erweitert** .  
  
5.  Klicken Sie auf **OK** , um das Paket auszuführen.  
  
     -oder-  
  
     Verwenden Sie gespeicherte Prozeduren zum Ausführen des Pakets. Klicken Sie auf **Skript**, um die Transact-SQL-Anweisung zu generieren, die eine Instanz der Ausführung erstellt und startet. Die Anweisung enthält einen Aufruf der gespeicherten Prozeduren catalog.create_execution, catalog.set_execution_parameter_value und catalog.start_execution. Weitere Informationen zu diesen gespeicherten Prozeduren finden Sie unter [catalog.create_execution &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database.md), [catalog.set_execution_parameter_value &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md) und [catalog.start_execution &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md).  
  
  