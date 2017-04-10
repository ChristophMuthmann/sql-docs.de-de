---
title: "Erneutes Bereitstellen von Paketen | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Erneutes Bereitstellen von Paketen [Integration Services]"
  - "Bereitstellen von Paketen [Integration Services], erneute Bereitstellung"
ms.assetid: 86806efb-8cf4-4f9d-9824-1152cb4c495c
caps.latest.revision: 37
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 37
---
# Erneutes Bereitstellen von Paketen
  Nachdem ein Projekt bereitgestellt wurde, kann es erforderlich werden, die Paketfunktionalität zu aktualisieren oder zu erweitern und anschließend das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekt, das die aktualisierten Pakete enthält, erneut bereitzustellen. Im Zusammenhang mit dem erneuten Bereitstellen von Paketen sollten Sie die zum Bereitstellungshilfsprogramm gehörenden Konfigurationseigenschaften überprüfen. Beispielsweise können Sie festlegen, dass nach dem erneuten Bereitstellen des Pakets keine Konfigurationsänderungen zulässig sein sollen.  
  
## Prozess für die erneute Bereitstellung  
 Nachdem Sie die Pakete aktualisiert haben, erstellen Sie das Projekt neu. Kopieren Sie dann den Bereitstellungsordner zum Zielcomputer, und führen Sie dann den Paketinstallations-Assistenten erneut aus.  
  
 Wenn Sie nur wenige Pakete aus dem Projekt aktualisieren, muss eventuell nicht das gesamte Projekt erneut bereitgestellt werden. Um nur wenige Pakete bereitzustellen, können Sie ein neues [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekt erstellen, diesem neuen Projekt die aktualisierten Pakete hinzufügen und dann das Projekt erstellen und bereitstellen. Die Paketkonfigurationen werden automatisch zusammen mit dem Paket kopiert, wenn Sie das Paket einem anderen Projekt hinzufügen.  
  
## Verwandte Aufgaben  
 [Bereitstellen von Paketen mithilfe des Bereitstellungshilfsprogramms](../../integration-services/packages/deploy-packages-by-using-the-deployment-utility.md)  
  
  