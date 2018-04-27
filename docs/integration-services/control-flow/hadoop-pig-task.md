---
title: Hadoop Pig-Task | Microsoft-Dokumentation
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
- sql13.ssis.designer.hadooppigtask.f1
ms.assetid: 90646316-9822-48aa-9900-295a33750780
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 606fc01992c98bfedd64b19f962ebef3699be031
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="hadoop-pig-task"></a>Hadoop Pig-Task
  Mithilfe eines Hadoop Pig-Tasks können Sie ein Pig-Skript in einem Hadoop-Cluster ausführen.  
  
 Zum Hinzufügen eines Hadoop Pig-Tasks ziehen Sie diesen auf den Designer. Doppelklicken Sie anschließend auf den Task, oder klicken Sie mit der rechten Maustaste darauf, und klicken Sie auf **Bearbeiten**, um das Hadoop-Dialogfeld **Editor für den Pig-Task** zu öffnen.  
  
 ![Editor für den Pig-Task](../../integration-services/control-flow/media/hadoop-pig-task.png "Editor für den Pig-Task")  
  
## <a name="options"></a>Tastatur  
 Konfigurieren Sie die folgenden Optionen im Hadoop-Dialogfeld **Editor für den Pig-Task** .  
  
|Feld|Description|  
|-----------|-----------------|  
|**Hadoop-Verbindung**|Geben Sie einen vorhandenen Hadoop-Verbindungs-Manager an, oder erstellen Sie einen neuen. Dieser Verbindungs-Manager gibt an, wo der Dienst WebHCat gehostet wird.|  
|**SourceType**|Geben Sie den Quelltyp der Abfrage an. Mögliche Werte sind **ScriptFile** und **DirectInput**.|  
|**InlineScript**|Wenn der Wert von **SourceType** **DirectInput**ist, geben Sie das Pig-Skript an.|  
|**HadoopScriptFilePath**|Wenn der Wert von **SourceType** **ScriptFile**ist, geben Sie den Pfad der Skriptdatei auf Hadoop an.|  
|**TimeoutInMinutes**|Geben Sie einen Timeoutwert in Minuten an. Wenn der Hadoop-Job vor Ablauf des Timeouts nicht abgeschlossen wurde, wird er abgebrochen. Geben Sie 0 ein, wenn der Hadoop-Job asynchron ausgeführt werden soll.|  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Hadoop-Verbindungs-Manager](../../integration-services/connection-manager/hadoop-connection-manager.md)  
  
  
