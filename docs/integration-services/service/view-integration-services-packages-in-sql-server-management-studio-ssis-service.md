---
title: "Anzeigen von Integration Services-Paketen in SQL Server Management Studio (SSIS-Dienst) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Anzeigen von Paketen"
  - "Verbindungen [Integration Services], Pakete"
ms.assetid: 783e653c-0f1f-45ed-b3ef-5ba07b019f27
caps.latest.revision: 24
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 24
---
# Anzeigen von Integration Services-Paketen in SQL Server Management Studio (SSIS-Dienst)
    
> [!IMPORTANT]  
>  In diesem Thema wird der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst beschrieben, ein Windows-Dienst zur Verwaltung von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Paketen. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] unterstützt den Dienst für die Abwärtskompatibilität mit früheren Versionen von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Ab [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]können Sie Objekte, z. B. Pakete, auf dem Integration Services-Server verwalten.  
  
 In diesem Verfahren wird beschrieben, wie eine Verbindung mit [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] hergestellt und eine Liste der vom [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst verwalteten Pakete angezeigt wird.  
  
### So stellen Sie eine Verbindung mit Integration Services her  
  
1.  Klicken Sie auf **Start**, zeigen Sie auf **Alle Programme**, zeigen Sie auf **Microsoft SQL Server**, und klicken Sie dann auf **SQL Server Management Studio**.  
  
2.  Wählen Sie im Dialogfeld **Verbindung mit Server herstellen** in der Liste **Servertyp** die Option **Integration Services** aus, geben Sie im Feld **Servername** einen Servernamen an, und klicken Sie dann auf **Verbinden**.  
  
    > [!IMPORTANT]  
    >  Wenn Sie keine Verbindung mit [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]herstellen können, wird der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst wahrscheinlich nicht ausgeführt. Wenn Sie weitere Informationen zum Status des Diensts erhalten möchten, klicken Sie auf **Start**, zeigen Sie auf **Alle Programme**, zeigen Sie auf **Microsoft SQL Server**, zeigen Sie auf **Konfigurationstools**, und klicken Sie dann auf **SQL Server-Konfigurations-Manager**. Klicken Sie im linken Bereich auf **SQL Server-Dienste**. Suchen Sie im rechten Bereich den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst. Starten Sie den Dienst, wenn er nicht bereits ausgeführt wird.  
  
     [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] wird geöffnet. Standardmäßig ist das Fenster des Objekt-Explorers geöffnet und in der unteren linken Ecke des Studios positioniert. Ist der Objekt-Explorer nicht geöffnet, klicken Sie im Menü **Ansicht** auf **Objekt-Explorer** .  
  
### So zeigen Sie die vom Integration Services-Dienst verwalteten Pakete an  
  
1.  Erweitern Sie im Objekt-Explorer den Ordner Gespeicherte Pakete.  
  
2.  Erweitern Sie die Unterordner Gespeicherte Pakete, um die Pakete anzuzeigen.  
  
## Siehe auch  
 [Paketverwaltung &#40;SSIS-Dienst&#41;](../../integration-services/service/package-management-ssis-service.md)   
 [Verwenden von SQL Server Management Studio](../../ssms/use-sql-server-management-studio.md)  
  
  