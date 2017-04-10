---
title: "Azure HDInsight Pig-Task | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "02/28/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.afppigtask.f1"
  - "sql14.dts.designer.afppigtask.f1"
ms.assetid: 26f34f64-f344-486e-9190-acf71aef29a8
caps.latest.revision: 12
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 9
---
# Azure HDInsight Pig-Task
  Verwenden Sie den **Azure HDInsight Pig-Task** zum Ausführen eines Pig-Skripts auf einem Azure HDInsight-Cluster. 
    
Um einen **Azure HDInsight-Pig-Task** hinzuzufügen, legen Sie ihn mittels Drag & Drop auf dem SSIS-Designer ab, und doppelklicken Sie darauf, oder klicken Sie mit der rechten Maustaste, und klicken Sie anschließend auf **Bearbeiten**, um das folgende Dialogfeld **Azure HDInsight-Pig-Task-Editor** anzuzeigen.  
  
 Der **Azure HDInsight-Pig-Task** ist eine Komponente des SQL Server Integration Services (SSIS) Feature Packs für Azure für SQL Server 2016. Laden Sie das Feature Pack [hier](http://go.microsoft.com/fwlink/?LinkID=626967) herunter.  
  
1.  Wählen Sie für das Feld **AzureSubscriptionConnection** einen vorhandenen Azure-Abonnementverbindungs-Manager aus, oder erstellen Sie einen neuen, der auf ein Azure-Abonnement verweist, in dem der HDInsight-Cluster gehostet wird.  
  
2.  Geben Sie im Feld **HDInsightClusterName** den Namen des HDInsight-Clusters ein, auf dem Sie das Pig-Skript ausführen möchten.  
  
3.  Klicken Sie im Feld **LocalLogFolder** auf **... (Auslassungszeichen)**, und wählen Sie den Ordner aus, in den die Pig-Verarbeitungsprotokolle aus dem HDInsight-Cluster heruntergeladen werden soll.  
  
4.  Sie haben zwei Möglichkeiten, das Pig-Skript anzugeben:  
  
    1.  **Inlineskript**: Klicken Sie neben dem Feld **Skript** auf **... (Auslassungszeichen)**, und geben Sie im Dialogfeld **Skript eingeben** das Inlineskript ein.  
  
    2.  **Skriptdatei**: Laden Sie die Skriptdatei in einen Blobspeicherort hoch, und geben Sie **BlobName** an. Befindet sich das Blob nicht im Standardspeicher oder Container des HDInsight-Clusters, müssen **ExternalStorageAccountName** und **ExternalBlobContainer** angegeben werden. Stellen Sie bei einem externen Blob sicher, dass es als öffentlich zugänglich konfiguriert ist.  
  
     Wenn Skriptdatei und Inline-Skript angegeben sind, wird die Skriptdatei verwendet und das Inline-Skript ignoriert.  
  
  