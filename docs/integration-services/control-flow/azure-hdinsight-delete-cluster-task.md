---
title: Azure HDInsight-Delete Cluster-Task | Microsoft-Dokumentation
ms.custom: 
ms.date: 02/28/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: control-flow
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.afpdelcltask.f1
- sql14.dts.designer.afpdelcltask.f1
ms.assetid: e298776e-d18a-4393-a8e6-65ee3d555749
caps.latest.revision: "12"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e93cfaf8afd3bda1242635a27a9fd38d3cb8859d
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="azure-hdinsight-delete-cluster-task"></a>Azure HDInsight-Delete Cluster-Task
Der **Azure HDInsight-Delete Cluster-Task** ermöglicht einem SSIS-Paket das Löschen eines Azure HDInsight-Clusters im angegebenen Azure-Abonnement und der Ressourcengruppe.
  
Der **Azure HDInsight-Delete Cluster-Task** ist eine Komponente des [SQL Server Integration Services-Feature Packs (SSIS) für Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).
  
> [!NOTE]
> Das Löschen eines HDInsight-Clusters kann 10-20 Minuten in Anspruch nehmen.  
  
Um einen **Azure HDInsight-Delete Cluster-Task**hinzuzufügen, legen Sie ihn mittels Drag &amp; Drop auf dem SSIS-Designer ab, und doppelklicken Sie darauf, oder klicken Sie mit der rechten Maustaste, und klicken Sie dann auf **Bearbeiten** , um das folgende Dialogfeld A **zure HDInsight-Delete Cluster-Task-Editor** anzuzeigen.  
  
Die folgende Tabelle enthält Beschreibungen für die Felder in diesem Dialogfeld.  
  
|||  
|-|-|  
|**Feld**|**Description**|  
|AzureResourceManagerConnection|Wählen Sie einen vorhandenen Azure Resource Manager-Verbindungs-Manager aus, oder erstellen Sie einen neuen, mit dem der HDInsight-Cluster gelöscht wird.|
|SubscriptionId|Geben Sie die ID des Abonnements an, in dem sich der HDInsight-Cluster befindet.|
|ResourceGroup|Geben Sie die Azure-Ressourcengruppe an, in der sich der HDInsight-Cluster befindet.|
|ClusterName|Geben Sie den Namen des zu löschenden Clusters an.|  
|FailIfNotExists|Geben Sie an, ob der Task einen Fehler ausgeben soll, wenn der Cluster nicht vorhanden ist.|
