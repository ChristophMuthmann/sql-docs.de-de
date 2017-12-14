---
title: HDFS-Dateiziel | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.ssis.designer.hdfsfiledest.f1
ms.assetid: 4338ce9f-c077-4301-aca5-47ed070ec94d
caps.latest.revision: "8"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d07d4efaa0b26a19f60ca27e465177d0ea7b797c
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="hdfs-file-destination"></a>HDFS-Dateiziel
  Die HDFS-Dateizielkomponente ermöglicht einem SSIS-Paket das Schreiben von Daten in eine HDFS-Datei. Die unterstützten Dateiformate sind Text, Avro und ORC.  
  
 Um das HDFS-Dateiziel zu konfigurieren, ziehen Sie die HDFS-Dateiquelle in den Datenfluss-Designer, und doppelklicken Sie auf die Komponente, um den Editor zu öffnen.  
  
 ![HDFS-Dateiziel-Editor](../../integration-services/data-flow/media/hdfs-file-dest.png "HDFS-Dateiziel-Editor")  
  
## <a name="options"></a>enthalten  
 Konfigurieren Sie die folgenden Optionen auf der Registerkarte **Allgemein** im Dialogfeld **Dateiziel-Editor für Hadoop** .  
  
|Feld|Beschreibung|  
|-----------|-----------------|  
|**Hadoop-Verbindung**|Geben Sie einen vorhandenen Hadoop-Verbindungs-Manager an, oder erstellen Sie einen neuen. Dieser Verbindungs-Manager gibt an, wo die HDFS-Dateien gehostet werden.|  
|**Dateipfad**|Geben Sie den Namen der HDFS-Datei an.|  
|**Dateiformat**|Geben Sie das Format für die HDFS-Datei an. Die verfügbaren Optionen sind Text, Avro und ORC.|  
|**Spaltentrennzeichen**|Wenn Sie das Textformat auswählen, geben Sie das Spaltentrennzeichen an.|  
|**Spaltennamen in der ersten Datenzeile**|Wenn Sie das Textformat auswählen, geben Sie an, ob die erste Zeile in der Datei Spaltennamen enthält.|  
  
 Nachdem Sie diese Optionen konfiguriert haben, wählen Sie die Registerkarte **Spalten** aus, um Quellspalten zu Zielspalten im Datenfluss zuzuordnen.  
  
## <a name="see-also"></a>Siehe auch  
 [Hadoop-Verbindungs-Manager](../../integration-services/connection-manager/hadoop-connection-manager.md)   
 [HDFS-Dateiquelle](../../integration-services/data-flow/hdfs-file-source.md)  
  
  
