---
title: "Azure HDInsight Hive-Task | Microsoft Docs"
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
  - "sql13.dts.designer.afphivetask.f1"
  - "sql14.dts.designer.afphivetask.f1"
ms.assetid: e1896c73-128a-4128-9814-3e01f7dfe19b
caps.latest.revision: 13
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 10
---
# Azure HDInsight Hive-Task
  Verwenden Sie den **Azure HDInsight Hive-Task** zum Anwenden eines Hive-Skripts auf einen Azure HDInsight-Cluster.
     
Um einen **Azure HDInsight-Hive-Task** hinzuzufügen, legen Sie ihn mittels Drag & Drop auf dem SSIS-Designer ab, und doppelklicken Sie darauf, oder klicken Sie mit der rechten Maustaste, und klicken Sie dann auf **Bearbeiten**, um das folgende Dialogfeld **Azure HDInsight-Hive-Task-Editor** anzuzeigen.  
  
 Der **Azure HDInsight-Hive-Task** ist eine Komponente des SQL Server Integration Services (SSIS) Feature Packs für Azure für SQL Server 2016. Laden Sie das Feature Pack [hier](http://go.microsoft.com/fwlink/?LinkID=626967) herunter.  
  
 Die folgende Liste beschreibt Felder in diesem Dialogfeld.  
  
1.  Wählen Sie für das Feld **AzureSubscriptionConnection** einen vorhandenen Azure-Abonnementverbindungs-Manager aus, oder erstellen Sie einen neuen, der auf ein Azure-Abonnement verweist, in dem der HDInsight-Cluster gehostet ist.  
  
2.  Wählen Sie für das Feld **HDInsightClusterName** den Namen des HDInsight-Clusters, auf den Sie das Hive-Skript anwenden möchten.  
  
3.  Klicken Sie im Feld **LocalLogFolder** auf **... (Auslassungszeichen)**, und wählen Sie den Ordner, in den die Hive-Verarbeitungsprotokolle aus dem HDInsight-Cluster heruntergeladen werden soll.  
  
4.  Sie haben zwei Möglichkeiten, das Hive-Skript anzugeben:  
  
    1.  **Inline-Skript**: Klicken Sie neben dem Feld **Skript** auf **... (Auslassungszeichen)**, und geben Sie im Dialogfeld **Skriptnamen eingeben** den Namen des Inlineskripts ein.  
  
    2.  **Skriptdatei**: Laden Sie die Skriptdatei in einen Blobspeicherort hoch, und geben Sie den **BlobName** an. Befindet sich das Blob nicht im Standardspeicher oder Container des HDInsight-Clusters, müssen **ExternalStorageAccountName** und **ExternalBlobContainer** angegeben werden. Stellen Sie bei einem externen Blob sicher, dass es als öffentlich zugänglich konfiguriert ist.  
  
     Wenn Skriptdatei und Inline-Skript angegeben sind, wird die Skriptdatei verwendet und das Inline-Skript ignoriert.  
  
  