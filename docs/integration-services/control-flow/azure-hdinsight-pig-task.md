---
title: Azure HDInsight Pig-Task | Microsoft Docs
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
- sql13.dts.designer.afppigtask.f1
- sql14.dts.designer.afppigtask.f1
ms.assetid: 26f34f64-f344-486e-9190-acf71aef29a8
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 9874b119b634966b146f8fa9d22c016bcd91617b
ms.contentlocale: de-de
ms.lasthandoff: 09/26/2017

---
# <a name="azure-hdinsight-pig-task"></a>Azure HDInsight Pig-Task
Verwenden Sie den **Azure HDInsight Pig-Task** zum Ausführen eines Pig-Skripts auf einem Azure HDInsight-Cluster.
     
Um einen **Azure HDInsight-Pig-Task**hinzuzufügen, legen Sie ihn mittels Drag &amp; Drop auf dem SSIS-Designer ab, und doppelklicken Sie darauf, oder klicken Sie mit der rechten Maustaste, und klicken Sie anschließend auf **Bearbeiten** , um das folgende Dialogfeld **Azure HDInsight-Pig-Task-Editor** anzuzeigen.  
  
Die **Azure HDInsight Pig-Task** ist eine Komponente von der [SQL Server Integration Services (SSIS) Feature Pack für Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).
  
 Die folgende Liste beschreibt Felder in diesem Dialogfeld.  
  
1.  Für die **HDInsightConnection** Feld, wählen Sie einen vorhandenen Azure HDInsight-Verbindungs-Manager aus, oder erstellen Sie ein neues eine, die auf den Azure HDInsight-Cluster verweist verwendet, um das Skript auszuführen.
  
2.  Für die **AzureStorageConnection** Feld, wählen Sie einen vorhandenen Azure Storage-Verbindungs-Manager aus, oder erstellen Sie ein neues Azure-Speicherkonto bezieht sich mit dem Cluster verbundenen. Dies ist nur erforderlich, wenn die Ausgabe und Fehler protokolliert das Skript-Ausführung heruntergeladen werden soll.
 
3.  Für die **BlobContainer** Feld, mit dem Cluster verbundenen speichercontainername angeben. Dies ist nur erforderlich, wenn die Ausgabe und Fehler protokolliert das Skript-Ausführung heruntergeladen werden soll.
  
4.  Für die **LocalLogFolder** -Feld verwendet wird, geben Sie den Ordner, auf die Ausgabe und Fehler protokolliert das Skript die Ausführung auf heruntergeladen werden. Dies ist nur erforderlich, wenn die Ausgabe und Fehler protokolliert das Skript-Ausführung heruntergeladen werden soll.   
  
5.  Es gibt zwei Möglichkeiten zum Angeben der Pig-Skript ausführen:
  
    1.  **Inline-Skript**: Geben Sie die **Skript** Feld durch Eingabe in-Line-das Skript in die **Skriptnamen eingeben** (Dialogfeld).
  
    2.  **Skriptdatei**: die Skriptdatei in Azure Blob-Speicher hochladen, und geben Sie die **"blobname"** Feld. Wenn das Blob nicht im standardmäßigen Speicherkonto oder Container gehört, mit dem HDInsight-Cluster ist die **ExternalStorageAccountName** und **ExternalBlobContainer** Felder müssen angegeben werden. Stellen Sie für ein externes Blob sicher, dass es konfiguriert ist als öffentlich zugegriffen werden kann.  
  
     Wenn beide angegeben sind, Skriptdatei verwendet werden, und das Inline-Skript ignoriert werden.

