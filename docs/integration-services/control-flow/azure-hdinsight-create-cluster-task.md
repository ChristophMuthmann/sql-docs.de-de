---
title: Azure HDInsight Create Cluster-Task | Microsoft Docs
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
- sql13.dts.designer.afpcreatecltask.f1
- sql14.dts.designer.afpcreatecltask.f1
ms.assetid: a8ec413a-38d3-45df-887e-6f5f4d9f8465
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 71a24dc15253916c32b07e6024e2ab32514c9d39
ms.contentlocale: de-de
ms.lasthandoff: 09/26/2017

---
# <a name="azure-hdinsight-create-cluster-task"></a>Azure HDInsight Create Cluster-Task
Die **Azure HDInsight Create Cluster-Task** ermöglicht einem SSIS-Paket zum Erstellen eines Azure HDInsight-Clusters in der angegebenen Gruppe für Azure Abonnement- und Ressourcenstatus.
  
Die **Azure HDInsight Create Cluster-Task** ist eine Komponente von der [SQL Server Integration Services (SSIS) Feature Pack für Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).
  
> [!NOTE]  
> - Erstellen eines neuen HDInsight-Clusters dauert 10 ~ 20 Minuten.  
> - Es ist ein gewisser Aufwand verbunden mit erstellen und Ausführen eines Azure HDInsight-Clusters. Finden Sie unter [HDInsight Preise](http://azure.microsoft.com/en-us/pricing/details/hdinsight/) Details.  
  
Um einen **Azure HDInsight Create Cluster-Task**hinzuzufügen, legen Sie ihn mittels Drag &amp; Drop auf dem SSIS-Designer ab, und doppelklicken Sie darauf, oder klicken Sie mit der rechten Maustaste darauf. Klicken Sie dann auf **Bearbeiten** , um das folgende Dialogfeld **Azure HDInsight Create Cluster-Task-Editor** anzuzeigen.  
  
Die folgende Tabelle enthält eine Beschreibung für die Felder in diesem Dialogfeld.  
  
|||  
|-|-|  
|**Feld**|**Description**|  
|AzureResourceManagerConnection|Wählen Sie einen vorhandenen Azure Resource Manager Verbindungs-Manager, oder erstellen Sie eine neue, die zum Erstellen des HDInsight-Clusters verwendet werden.|  
|AzureStorageConnection|Wählen Sie einen vorhandenen Azure Storage-Verbindungs-Manager aus, oder erstellen Sie einen neuen, der auf ein Azure Storage-Konto verweist, um ihn mit dem HDInsight-Cluster zu verknüpfen.|
|"SubscriptionId"|Geben Sie die ID des Abonnements, die in der HDInsight-Cluster erstellt wird.|
|"ResourceGroup"|Geben Sie an die Azure-Ressource Gruppieren der HDInsight-Cluster in erstellt werden soll.|
|Speicherort|Geben Sie den Speicherort des HDInsight-Clusters an. Der Cluster muss am gleichen Speicherort wie das Azure-Speicherkonto angegeben erstellt werden.|  
|ClusterName|Geben Sie einen Namen für den zu erstellenden HDInsight-Cluster an.|  
|ClusterSize|Geben Sie die Anzahl der Knoten im Cluster zu erstellen.|  
|BlobContainer|Geben Sie den Namen des standardmäßigen Speichercontainers an den HDInsight-Cluster zugeordnet werden soll.|  
|UserName|Geben Sie den Benutzernamen zum Herstellen einer Verbindung mit dem HDInsight-Cluster verwendet werden soll.|  
|Kennwort|Geben Sie das Kennwort zum Herstellen einer Verbindung mit dem HDInsight-Cluster verwendet werden soll.|
|SshUserName|Geben Sie den Benutzernamen für den Remotezugriff auf den HDInsight-Cluster mithilfe von SSH auf verwendet.|
|SshPassword|Geben Sie das Kennwort für den Remotezugriff auf den HDInsight-Cluster mithilfe von SSH auf verwendet.|
|FailIfExists|Geben Sie an, ob der Task einen Fehler ausgeben soll, wenn der Cluster bereits vorhanden ist.|  
  
> [!NOTE]  
> Die Speicherorte der HDInsight-Clusters und der Azure-Speicherkonto müssen identisch sein.

