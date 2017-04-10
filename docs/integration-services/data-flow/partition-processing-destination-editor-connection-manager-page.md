---
title: "Ziel-Editor f&#252;r Partitionsverarbeitung (Seite Verbindungs-Manager) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.partprocessingtransformation.connection.f1"
helpviewer_keywords: 
  - "Ziel-Editor für Partitionsverarbeitung"
ms.assetid: 7add6f82-eed1-47fc-a5d7-7b91f3f24d34
caps.latest.revision: 27
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 27
---
# Ziel-Editor f&#252;r Partitionsverarbeitung (Seite Verbindungs-Manager)
  Geben Sie auf der Seite **Verbindungs-Manager** des Dialogfelds **Ziel-Editor für Partitionsverarbeitung** eine Verbindung mit einem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt oder einer Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]an.  
  
 Weitere Informationen zum Ziel für Partitionsverarbeitung finden Sie unter [Partition Processing Destination](../../integration-services/data-flow/partition-processing-destination.md).  
  
> [!NOTE]  
>  Hier beschriebene Tasks gelten nicht für tabellarische Analysis Services-Modelle.  Sie können Partitionsspalten für tabellarische Modelle keine Eingabespalten zuordnen. Sie können stattdessen den Analysis Services-Task "DDL ausführen" [Analysis Services Execute DDL Task](../../integration-services/control-flow/analysis-services-execute-ddl-task.md) verwenden, um die Partition zu verarbeiten.  
  
## enthalten  
 **Verbindungs-Manager**  
 Wählen Sie in der Liste einen vorhandenen Verbindungs-Manager aus, oder erstellen Sie eine neue Verbindung, indem Sie auf **Neu** klicken.  
  
 **Neu**  
 Erstellen Sie mithilfe des Dialogfelds **Analysis Services-Verbindungs-Manager hinzufügen** eine neue Verbindung.  
  
 **Liste der verfügbaren Partitionen**  
 Wählen Sie die zu verarbeitende Partition aus.  
  
 **Verarbeitungsmethode**  
 Wählen Sie die Verarbeitungsmethode aus. Der Standardwert für diese Option ist **Vollständig**.  
  
|Wert|Description|  
|-----------|-----------------|  
|Hinzufügen (inkrementell)|Führt eine inkrementelle Verarbeitung der Partition aus.|  
|Full|Führt eine vollständige Verarbeitung der Partition aus.|  
|Nur Daten|Führt eine Verarbeitung der Updates für die Partition aus.|  
  
## Siehe auch  
 [Fehler- und Meldungsreferenz von Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Ziel-Editor für Partitionsverarbeitung &#40;Seite „Zuordnungen“&#41;](../../integration-services/data-flow/partition-processing-destination-editor-mappings-page.md)   
 [Ziel-Editor für Partitionsverarbeitung &#40;Seite „Erweitert“&#41;](../../integration-services/data-flow/partition-processing-destination-editor-advanced-page.md)  
  
  