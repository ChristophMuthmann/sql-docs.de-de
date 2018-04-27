---
title: Azure HDInsight Hive-Task | Microsoft-Dokumentation
ms.custom: ''
ms.date: 02/28/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: control-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.dts.designer.afphivetask.f1
- sql14.dts.designer.afphivetask.f1
ms.assetid: e1896c73-128a-4128-9814-3e01f7dfe19b
caps.latest.revision: 13
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: af68d13b1391d1e6890f42e8bbba0e0da70ddfed
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="azure-hdinsight-hive-task"></a>Azure HDInsight Hive-Task
Verwenden Sie den **Azure HDInsight Hive-Task** zum Anwenden eines Hive-Skripts auf einen Azure HDInsight-Cluster.
     
Um einen **Azure HDInsight-Hive-Task**hinzuzufügen, legen Sie ihn mittels Drag &amp; Drop auf dem SSIS-Designer ab, und doppelklicken Sie darauf, oder klicken Sie mit der rechten Maustaste, und klicken Sie dann auf **Bearbeiten** , um das folgende Dialogfeld **Azure HDInsight-Hive-Task-Editor** anzuzeigen.  
  
Der **Azure HDInsight-Hive-Task** ist eine Komponente des [SQL Server Integration Services-Feature Packs (SSIS) für Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).
  
 Die folgende Liste beschreibt Felder in diesem Dialogfeld.  
  
1.  Wählen Sie für das Feld **HDInsightConnection** einen vorhandenen HDInsight-Verbindungs-Manager aus, oder erstellen Sie einen neuen, der auf einen Azure HDInsight-Cluster verweist, in dem das Skript ausgeführt wird.
  
2.  Wählen Sie für das Feld **AzureStorageConnection** einen vorhandenen Azure Storage-Verbindungs-Manager aus, oder erstellen Sie einen neuen, der auf das Azure Storage-Konto verweist, das mit dem Cluster verbunden ist. Dies ist nur erforderlich, wenn Sie die Skriptausführungsausgabe- und Fehlerprotokolle herunterladen möchten.
 
3.  Geben Sie für das Feld **BlobContainer** den Speichercontainernamen an, der mit dem Cluster verbunden ist. Dies ist nur erforderlich, wenn Sie die Skriptausführungsausgabe- und Fehlerprotokolle herunterladen möchten.
  
4.  Geben Sie für das Feld **LocalLogFolder** den Ordner an, in den die Skriptausführungsausgabe- und Fehlerprotokolle heruntergeladen werden sollen. Dies ist nur erforderlich, wenn Sie die Skriptausführungsausgabe- und Fehlerprotokolle herunterladen möchten.   
  
5.  Sie haben zwei Möglichkeiten, das auszuführende Hive-Skript anzugeben:
  
    1.  **Inlineskript**: Legen Sie das Feld **Skript** fest, indem Sie im Dialogfeld **Skript eingeben** inline das auszuführende Skript eingeben.
  
    2.  **Skriptdatei**: Laden Sie die Skriptdatei in Azure Blob Storage hoch, und legen Sie das Feld **BlobName** fest. Befindet sich das Blob nicht im Standardspeicherkonto oder -container des HDInsight-Clusters, müssen die Felder **ExternalStorageAccountName** und **ExternalBlobContainer** festgelegt werden. Stellen Sie bei einem externen Blob sicher, dass es als öffentlich zugänglich konfiguriert ist.  
  
     Wenn Skriptdatei und Inlineskript angegeben sind, wird die Skriptdatei verwendet und das Inlineskript ignoriert.
