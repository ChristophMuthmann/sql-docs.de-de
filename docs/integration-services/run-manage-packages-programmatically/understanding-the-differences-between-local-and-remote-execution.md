---
title: "Grundlegendes zu den Unterschieden zwischen lokalen und Remote-Ausführung | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Integration Services packages, running
- packages [Integration Services], running
- packages [Integration Services], troubleshooting
ms.assetid: 610ee7d9-4fea-4aba-9395-57add826923b
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 1921a7760e42f101ebf5d9b898972c2b2ab8173b
ms.contentlocale: de-de
ms.lasthandoff: 09/26/2017

---
# <a name="understanding-the-differences-between-local-and-remote-execution"></a>Grundlegendes zu den Unterschieden zwischen der lokalen und der Remoteausführung
  Paketentwickler und Administratoren sollten die Beschränkungen hinsichtlich des Ausführungsorts eines [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Pakets beachten.  
  
-   **Ein Paket ausgeführt wird, auf dem gleichen Computer wie das Programm, das es startet**. Auch wenn ein Progamm ein Paket lädt, das auf einem anderen Server remote gespeichert ist, wird das Paket auf dem lokalen Computer ausgeführt.  
  
-   **Sie können nur ein Paket außerhalb der Entwicklungsumgebung ausführen, auf dem Integration Services installiert ist**. Sie können Pakete außerhalb von [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] nur auf Clientcomputern ausführen, auf denen [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] installiert ist, wobei die Bedingungen Ihrer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Lizenz möglicherweise die Installation von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] auf weiteren Computern nicht zulassen. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ist eine Serverkomponente und ist nicht auf Clientcomputer verteilt. Um Pakete von einem Clientcomputer aus auszuführen, müssen Sie diese so starten, dass die Ausführung auf dem Server sichergestellt ist.  
  
 Weitere Informationen zum Laden und Ausführen eines gespeicherten Pakets finden Sie unter:  
  
-   [Programmgesteuertes Laden und Ausführen eines lokalen Pakets](../../integration-services/run-manage-packages-programmatically/loading-and-running-a-local-package-programmatically.md)  
  
-   [Programmgesteuertes Laden und Ausführen eines Remotepakets](../../integration-services/run-manage-packages-programmatically/loading-and-running-a-remote-package-programmatically.md)  
  
 Weitere Informationen zum Ausführen eines Pakets und Laden von dessen Ausgabe in ein benutzerdefiniertes Programm finden Sie unter:  
  
-   [Laden der Ausgabe eines lokalen Pakets](../../integration-services/run-manage-packages-programmatically/loading-the-output-of-a-local-package.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Programmgesteuerten laden und Ausführen eines lokalen Pakets](../../integration-services/run-manage-packages-programmatically/loading-and-running-a-local-package-programmatically.md)   
 [Programmgesteuerten laden und Ausführen eines Remotepakets](../../integration-services/run-manage-packages-programmatically/loading-and-running-a-remote-package-programmatically.md)   
 [Laden der Ausgabe eines lokalen Pakets](../../integration-services/run-manage-packages-programmatically/loading-the-output-of-a-local-package.md)  
  
  
