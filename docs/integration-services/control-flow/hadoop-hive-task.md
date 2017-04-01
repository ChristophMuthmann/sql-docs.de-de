---
title: "Hadoop Hive-Task | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.ssis.designer.hadoophivetask.f1"
ms.assetid: 10ff37c0-9f3f-442a-889b-c351afbdc74c
caps.latest.revision: 6
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 6
---
# Hadoop Hive-Task
  Mithilfe eines Hadoop Hive-Tasks können Sie ein Hive-Skript in einem Hadoop-Cluster ausführen.  
  
 Zum Hinzufügen eines Hadoop Hive-Tasks ziehen Sie diesen auf den Designer. Doppelklicken Sie anschließend auf den Task, oder klicken Sie mit der rechten Maustaste darauf, und klicken Sie auf **Bearbeiten**, um das Dialogfeld **Editor für Hadoop-Hive-Aufgaben** zu öffnen.  
  
 ![Hadoop Hive Task Editor](../../integration-services/control-flow/media/hadoop-hive-task.png "Hadoop Hive Task Editor")  
  
## enthalten  
 Konfigurieren Sie die folgenden Optionen im Dialogfeld **Editor für Hadoop-Hive-Aufgaben**.  
  
|Feld|Description|  
|-----------|-----------------|  
|**Hadoop-Verbindung**|Geben Sie einen vorhandenen Hadoop-Verbindungs-Manager an, oder erstellen Sie einen neuen. Dieser Verbindungs-Manager gibt an, wo der WebHCat-Dienst gehostet wird.|  
|**SourceType**|Geben Sie den Quelltyp der Abfrage an. Mögliche Werte sind **ScriptFile** und **DirectInput**.|  
|**InlineScript**|Wenn der Wert von **SourceType** **DirectInput** ist, geben Sie das Hive-Skript an.|  
|**HadoopScriptFilePath**|Wenn der Wert von **SourceType** **ScriptFile** ist, geben Sie den Pfad der Skriptdatei auf Hadoop an.|  
|**TimeoutInMinutes**|Geben Sie einen Timeoutwert in Minuten an. Wenn der Hadoop-Job vor Ablauf des Timeouts nicht abgeschlossen wurde, wird er abgebrochen. Geben Sie 0 ein, wenn der Hadoop-Job asynchron ausgeführt werden soll.|  
  
## Siehe auch  
 [Hadoop-Verbindungs-Manager](../../integration-services/connection-manager/hadoop-connection-manager.md)  
  
  