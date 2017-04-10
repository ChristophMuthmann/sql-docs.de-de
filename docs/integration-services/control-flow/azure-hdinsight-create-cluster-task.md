---
title: "Azure HDInsight Create Cluster-Task | Microsoft Docs"
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
  - "sql13.dts.designer.afpcreatecltask.f1"
  - "sql14.dts.designer.afpcreatecltask.f1"
ms.assetid: a8ec413a-38d3-45df-887e-6f5f4d9f8465
caps.latest.revision: 11
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 8
---
# Azure HDInsight Create Cluster-Task
  Der **Azure HDInsight Create Cluster-Task** ermöglicht einem SSIS-Paket das Erstellen eines Azure HDInsight-Clusters im angegebenen Azure-Abonnement.  
  
 Der **Azure HDInsight Create Cluster-Task** ist eine Komponente des SQL Server Integration Services (SSIS) Feature Packs für Azure für SQL Server 2016. Laden Sie das Feature Pack [hier](http://go.microsoft.com/fwlink/?LinkID=626967) herunter.  
  
> [!NOTE]  
>  -   Das Erstellen eines neuen HDInsight-Clusters dauert normalerweise 10 Minuten.  
> -   Beim Erstellen und Ausführen eines Azure HDInsight-Clusters fallen Kosten an. Details finden Sie auf der Webseite mit den [Preisinformationen für HDInsight](http://azure.microsoft.com/en-us/pricing/details/hdinsight/).  
  
 Um einen **Azure HDInsight Create Cluster-Task** hinzuzufügen, legen Sie ihn mittels Drag & Drop auf dem SSIS-Designer ab, und doppelklicken Sie darauf, oder klicken Sie mit der rechten Maustaste darauf. Klicken Sie dann auf **Bearbeiten**, um das folgende Dialogfeld **Azure HDInsight Create Cluster-Task-Editor** anzuzeigen.  
  
 Die folgende Tabelle enthält Beschreibungen der Felder in diesem Dialogfeld.  
  
|||  
|-|-|  
|**Feld**|**Description**|  
|AzureSubscriptionConnection|Wählen Sie einen vorhandenen Azure-Abonnementverbindungs-Manager aus, oder erstellen Sie einen neuen, der auf ein Azure-Abonnement verweist, in dem der HDInsight-Cluster gehostet ist.|  
|AzureStorageConnection|Wählen Sie einen vorhandenen Azure Storage-Verbindungs-Manager aus, oder erstellen Sie einen neuen, der auf ein Azure Storage-Konto verweist, um ihn mit dem HDInsight-Cluster zu verknüpfen.|  
|Speicherort|Geben Sie den Speicherort des HDInsight-Clusters an. Der Cluster muss am selben Speicherort wie der Azure-Speicher erstellt werden.|  
|ClusterName|Geben Sie einen Namen für den zu erstellenden HDInsight-Cluster an.|  
|ClusterSize|Geben Sie die Anzahl der Knoten an, die im Cluster enthalten sein sollen.|  
|BlobContainer|Geben Sie den Namen des standardmäßigen Speichercontainers an, der mit dem HDInsight-Cluster verknüpft ist.|  
|UserName|Geben Sie den Namen des Benutzers an, der Zugriff auf den Cluster hat.|  
|Kennwort|Geben Sie das Kennwort für den Benutzer an.|  
|FailIfExists|Geben Sie an, ob der Task einen Fehler ausgeben soll, wenn der Cluster bereits vorhanden ist.|  
  
> [!NOTE]  
>  Der Speicherort des HDInsight-Clusters und des Azure-Speichers muss identisch sein.  
  
  