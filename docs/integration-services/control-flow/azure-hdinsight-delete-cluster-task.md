---
title: "Azure HDInsight-Delete Cluster-Task | Microsoft Docs"
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
  - "sql13.dts.designer.afpdelcltask.f1"
  - "sql14.dts.designer.afpdelcltask.f1"
ms.assetid: e298776e-d18a-4393-a8e6-65ee3d555749
caps.latest.revision: 12
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 9
---
# Azure HDInsight-Delete Cluster-Task
  Der **Azure HDInsight-Delete Cluster-Task** ermöglicht einem SSIS-Paket das Löschen eines Azure HDInsight-Clusters im angegebenen Azure-Abonnement.  
  
 Der **Azure HDInsight-Delete Cluster-Task** ist eine Komponente des SQL Server Integration Services (SSIS) Feature Packs für Azure für SQL Server 2016. Laden Sie das Feature Pack [hier](http://go.microsoft.com/fwlink/?LinkID=626967) herunter.  
  
> [!NOTE]  
>  Das Löschen eines HDInsight-Clusters nimmt normalerweise 10 Minuten in Anspruch.  
  
 Um einen **Azure HDInsight-Delete Cluster-Task** hinzuzufügen, legen Sie ihn mittels Drag & Drop auf dem SSIS-Designer ab, und doppelklicken Sie darauf, oder klicken Sie mit der rechten Maustaste, und klicken Sie dann auf **Bearbeiten**, um das folgende Dialogfeld A**zure HDInsight-Delete Cluster-Task-Editor** anzuzeigen.  
  
 Die folgende Tabelle enthält Beschreibungen der Felder in diesem Dialogfeld.  
  
|||  
|-|-|  
|**Feld**|**Description**|  
|AzureSubscriptionConnection|Wählen Sie einen vorhandenen Azure-Abonnementverbindungs-Manager aus, oder erstellen Sie einen neuen, der auf ein Azure-Abonnement verweist, in dem der HDInsight-Cluster gehostet ist.|  
|ClusterName|Geben Sie den Namen des zu löschenden Clusters an.|  
|FailIfNotExists|Geben Sie an, ob der Task einen Fehler ausgeben soll, wenn der Cluster nicht vorhanden ist.|  
  
  