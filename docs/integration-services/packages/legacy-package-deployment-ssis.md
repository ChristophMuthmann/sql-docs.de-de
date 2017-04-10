---
title: "Legacy-Paketbereitstellung (SSIS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Integration Services-Pakete, Bereitstellen"
  - "Bereitstellen von Paketen [Integration Services]"
  - "SQL Server Integration Services-Pakete, Bereitstellen"
  - "Bereitstellen von Paketen [Integration Services], Informationen zum Bereitstellen von Paketen"
  - "Pakete [Integration Services], bereitstellen"
  - "SSIS-Pakete, bereitstellen"
ms.assetid: 0f5fc7be-e37e-4ecd-ba99-697c8ae3436f
caps.latest.revision: 46
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 46
---
# Legacy-Paketbereitstellung (SSIS)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] enthält Tools und Assistenten, mit denen Sie problemlos Pakete vom Entwicklungscomputer auf dem Produktionsserver oder anderen Computern bereitstellen können.  
  
 Das Paketbereitstellungsverfahren gliedert sich in vier Schritte:  
  
1.  Der erste Schritt ist optional und umfasst das Erstellen von Paketkonfigurationen, die Eigenschaften von Paketelementen zur Laufzeit aktualisieren. Diese Konfigurationen werden beim Bereitstellen der Pakete automatisch mit eingeschlossen.  
  
2.  Im zweiten Schritt wird das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekt erstellt, um damit ein Paketbereitstellungshilfsprogramm zu erstellen. Das Bereitstellungshilfsprogramm für das Projekt enthält die Pakete, die Sie bereitstellen möchten.  
  
3.  Im dritten Schritt wird der Bereitstellungsordner, den Sie beim Erstellen des [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekts erstellt haben, auf den Zielcomputer kopiert.  
  
4.  Im vierten Schritt wird auf dem Zielcomputer der Paketinstallations-Assistent ausgeführt, um damit die Pakete auf dem Dateisystem oder einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]zu installieren.  
  
## Verwandte Aufgaben  
 Informationen zum Erstellen eines Bereitstellungshilfsprogramms finden Sie unter [Erstellen eines Bereitstellungs-Hilfsprogramms](../../integration-services/packages/create-a-deployment-utility.md).  
  
 Informationen zum Bereitstellen von Paketen mit dem Bereitstellungshilfsprogramm finden Sie unter [Bereitstellen von Paketen mithilfe des Bereitstellungshilfsprogramms](../../integration-services/packages/deploy-packages-by-using-the-deployment-utility.md).  
  
 Informationen zum Erstellen von Paketkonfigurationen finden Sie unter [Erstellen von Paketkonfigurationen](../../integration-services/packages/create-package-configurations.md).  
  
  