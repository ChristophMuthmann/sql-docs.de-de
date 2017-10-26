---
title: Azure HDInsight-Delete Cluster-Task | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 02/28/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.afpdelcltask.f1
- sql14.dts.designer.afpdelcltask.f1
ms.assetid: e298776e-d18a-4393-a8e6-65ee3d555749
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f98b69e8bd3b2e78f6dd20a19ca17a83a834c3b3
ms.contentlocale: de-de
ms.lasthandoff: 09/26/2017

---
# <a name="azure-hdinsight-delete-cluster-task"></a>Azure HDInsight-Delete Cluster-Task
Die **Azure HDInsight Delete Cluster-Task** ermöglicht einem SSIS-Paket So löschen Sie einen Azure HDInsight-Cluster in der angegebenen Gruppe für Azure Abonnement- und Ressourcenstatus.
  
Die **Azure HDInsight Delete Cluster-Task** ist eine Komponente von der [SQL Server Integration Services (SSIS) Feature Pack für Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).
  
> [!NOTE]
> Das Löschen eines HDInsight-Clusters dauert 10 ~ 20 Minuten.  
  
Um einen **Azure HDInsight-Delete Cluster-Task**hinzuzufügen, legen Sie ihn mittels Drag &amp; Drop auf dem SSIS-Designer ab, und doppelklicken Sie darauf, oder klicken Sie mit der rechten Maustaste, und klicken Sie dann auf **Bearbeiten** , um das folgende Dialogfeld A **zure HDInsight-Delete Cluster-Task-Editor** anzuzeigen.  
  
Die folgende Tabelle enthält eine Beschreibung für die Felder im Dialogfeld.  
  
|||  
|-|-|  
|**Feld**|**Description**|  
|AzureResourceManagerConnection|Wählen Sie einen vorhandenen Azure Resource Manager Verbindungs-Manager, oder erstellen Sie eine neue, mit der HDInsight-Cluster löschen.|
|"SubscriptionId"|Geben Sie die ID des Abonnements, in dem der HDInsight-Cluster befindet.|
|"ResourceGroup"|Geben Sie den Azure-Ressourcengruppe, in dem der HDInsight-Cluster befindet.|
|ClusterName|Geben Sie den Namen des zu löschenden Clusters an.|  
|FailIfNotExists|Geben Sie an, ob der Task einen Fehler ausgeben soll, wenn der Cluster nicht vorhanden ist.|

