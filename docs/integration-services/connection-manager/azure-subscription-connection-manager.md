---
title: "Azure-Abonnementverbindungs-Manager | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/02/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.afpsubscrconn.f1"
  - "sql14.dts.designer.afpsubscrconn.f1"
ms.assetid: e1225327-c308-4c50-8f44-c411f52ef378
caps.latest.revision: 11
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 10
---
# Azure-Abonnementverbindungs-Manager
  Der **Azure HDInsight-Verbindungs-Manager** ermöglicht die Verbindung eines SSIS-Pakets mit einem Azure-Abonnement, indem die Werte verwendet werden, die Sie für die folgenden Eigenschaften angeben: Azure-Abonnement-ID und das Verwaltungszertifikat.  
  
 Der **Azure Abonnement-Verbindungs-Manager** ist eine Komponente des SQL Server Integration Services (SSIS) Feature Pack für Azure für SQL Server 2016. Laden Sie das Feature Pack [hier](http://go.microsoft.com/fwlink/?LinkID=626967) herunter.  
  
1.  Wählen Sie im oben angezeigten Dialogfeld **SSIS-Verbindungs-Manager hinzufügen** die Option **Azure-Abonnement** aus, und klicken Sie auf **Hinzufügen**.  Das Dialogfeld **Azure-Abonnementverbindungs-Manager-Editor** wird geöffnet.  
  
    ![SSIS-AzureSubscriptionConnectionManager](../../integration-services/connection-manager/media/ssis-azuresubscriptionconnectionmanager.png)
  
2.  Geben Sie Ihre Azure-Abonnement-ID, die ein Azure-Abonnement eindeutig identifiziert, in **Azure-Abonnement-ID** ein.  Der Wert befindet sich im [Azure-Verwaltungsportal](https://manage.windowsazure.com) auf der Seite **Einstellungen**:  
  
    ![SSIS-AzureSettings-SubscriptionID](../../integration-services/connection-manager/media/ssis-azuresettings-subscriptionid.png "SSIS-AzureSettings-SubscriptionID")  
  
3.  Wählen Sie **Verwaltungszertifikatspeicherort** und **Verwaltungszertifikatspeichername** aus den Dropdownlisten aus.  
  
4.  Geben Sie den **Fingerabdruck des Verwaltungszertifikats** ein, oder klicken Sie auf **Durchsuchen...**, um im ausgewählten Store ein Zertifikat auszuwählen. Das Zertifikat muss als Verwaltungszertifikat für das Abonnement hochgeladen werden. Klicken Sie hierzu auf der folgenden Seite des Azure-Portals auf **Hochladen** (in diesem [MSDN-Beitrag](https://msdn.microsoft.com/library/azure/gg551722.aspx) finden Sie weitere Informationen).  
  
     ![SSIS-AzureSettings-ManagementCertificate](../../integration-services/connection-manager/media/ssis-azuresettings-managementcertificate.png "SSIS-AzureSettings-ManagementCertificate")  
  
5.  Klicken Sie auf **Verbindung testen**, um die Verbindung zu testen.  
  
6.  Klicken Sie auf **OK** , um das Dialogfeld zu schließen.  
  
  