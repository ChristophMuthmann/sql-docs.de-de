---
title: Hadoop-Dateisystemtask | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
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
- sql13.ssis.designer.hadoopfiletask.f1
ms.assetid: 594aaf5d-7703-4788-897d-fb95aca798c5
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b963428b347e86b10f8110b21c95b32f1c10eea0
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="hadoop-file-system-task"></a>Hadoop-Dateisystemtask
  Der Hadoop-Dateisystemtask ermöglicht einem SSIS-Paket das Kopieren von Dateien aus einem, in ein oder innerhalb eines Hadoop-Clusters.  
  
 Zum Hinzufügen eines Hadoop-Dateisystemtasks ziehen Sie diesen auf den Designer. Doppelklicken Sie anschließend auf den Task, oder klicken Sie mit der rechten Maustaste darauf, und klicken Sie auf **Bearbeiten**, um das Hadoop-Dialogfeld **Editor für den Task „Dateisystem“** zu öffnen.  
  
 ![Editor für den Task „Dateisystem“](../../integration-services/control-flow/media/hadoop-filesystem-task.png "Editor für den Task „Dateisystem“")  
  
## <a name="options"></a>Tastatur  
 Konfigurieren Sie die folgenden Optionen im Hadoop-Dialogfeld **Editor für den Task „Dateisystem“** .  
  
|Feld|Description|  
|-----------|-----------------|  
|**Hadoop-Verbindung**|Geben Sie einen vorhandenen Hadoop-Verbindungs-Manager an, oder erstellen Sie einen neuen. Dieser Verbindungs-Manager gibt an, wo die Zieldateien gehostet werden.|  
|**Hadoop-Dateipfad**|Geben Sie den Datei- oder Verzeichnispfad auf HDFS an.|  
|**Hadoop-Dateityp**|Geben Sie an, ob es sich beim HDFS-Dateisystemobjekt um eine Datei oder um ein Verzeichnis handelt.|  
|**Ziel überschreiben**|Geben Sie an, ob die Zieldatei überschrieben werden soll, wenn sie bereits vorhanden ist.|  
|**Vorgang**|Geben Sie den Vorgang an. Verfügbare Vorgänge sind **CopyToHDFS**, **CopyFromHDFS**und **CopyWithinHDFS**.|  
|**Lokale Dateiverbindung**|Geben Sie einen vorhandenen Dateiverbindungs-Manager an, oder erstellen Sie einen neuen. Dieser Verbindungs-Manager gibt an, wo die Quelldateien gehostet werden.|  
|**Ist rekursiv**|Geben Sie an, ob alle Unterordner rekursiv kopiert werden sollen.|  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Hadoop-Verbindungs-Manager](../../integration-services/connection-manager/hadoop-connection-manager.md)   
 [Dateiverbindungs-Manager](../../integration-services/connection-manager/file-connection-manager.md)  
  
  
