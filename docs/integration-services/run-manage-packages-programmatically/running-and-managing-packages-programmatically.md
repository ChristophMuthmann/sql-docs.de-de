---
title: "Ausführen und verwalten Pakete programmgesteuert | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: run-manage-packages-programmatically
ms.reviewer: 
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: 1a08c75e-ce8c-45ee-81bd-32248bbdb2b2
caps.latest.revision: 26
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 206411bed262d99b043cf667b9699a6fbeb85981
ms.contentlocale: de-de
ms.lasthandoff: 09/26/2017

---
# <a name="running-and-managing-packages-programmatically"></a>Programmgesteuerte Ausführung und Verwaltung von Paketen
  Wenn Sie [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Pakete außerhalb der Entwicklungsumgebung verwalten und ausführen müssen, können Sie Pakete programmgesteuert ändern. Dieser Ansatz bietet Ihnen eine Reihe von Optionen:  
  
-   Laden und Ausführen eines vorhandenen Pakets ohne Änderung  
  
-   Laden, Neukonfigurieren (z. B. für eine andere Datenquelle) und Ausführen eines vorhandenen Pakets  
  
-   Erstellen eines neuen Pakets, Hinzufügen und Konfigurieren von Komponenten Objekt um Objekt und Eigenschaft um Eigenschaft, Speichern und Ausführen des Pakets  
  
 Sie können auch ein vorhandenes Paket von einer Clientanwendung aus laden und ausführen, indem Sie nur einige Zeilen Code schreiben.  
  
 In diesem Abschnitt wird beschrieben und veranschaulicht, wie ein vorhandenes Paket programmgesteuert ausgeführt wird und wie auf die Ausgabe des Datenflusses anderer Anwendungen zugegriffen werden kann. Mit einer erweiterten programmieroption können Sie programmgesteuert erstellen eine [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Paket zeilenweise, wie im Thema beschrieben [Programmgesteuertes Erstellen von Paketen](../../integration-services/building-packages-programmatically/building-packages-programmatically.md).  
  
 In diesem Abschnitt werden auch weitere administrative Tasks behandelt, die Sie programmgesteuert ausführen können, um gespeicherte und ausgeführte Pakete sowie Paketrollen zu verwalten.  
  
## <a name="running-packages-on-the-integration-services-server"></a>Ausführen von Paketen auf dem Integration Services-Server  
 Wenn Sie Pakete auf dem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Server bereitstellen, können Sie die Pakete programmgesteuert unter Verwendung des <xref:Microsoft.SqlServer.Management.IntegrationServices>-Namespaces ausführen. Die Microsoft.SqlServer.Management.IntegrationServices-Assembly wird mit .NET Framework 3.5 kompiliert. Wenn Sie eine .NET Framework 4.0-Anwendung erstellen, müssen Sie der Projektdatei den Assemblyverweis möglicherweise direkt hinzufügen.  
  
 Sie können auch den Namespace verwenden, um [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Projekte auf dem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Server bereitzustellen und zu verwalten. Einen Überblick über den Namespace und die Codeausschnitte finden Sie im Blogeintrag [Überblick über das SSIS-Katalogmodell verwalteter Objekte](http://go.microsoft.com/fwlink/?LinkId=253122), auf blogs.msdn.com.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 [Grundlegendes zu den Unterschieden zwischen der lokalen und der Remoteausführung](../../integration-services/run-manage-packages-programmatically/understanding-the-differences-between-local-and-remote-execution.md)  
 Erläutert wichtige Unterschiede zwischen der Ausführung eines Pakets in der lokalen Umgebung oder auf dem Server.  
  
 [Programmgesteuertes Laden und Ausführen eines lokalen Pakets](../../integration-services/run-manage-packages-programmatically/loading-and-running-a-local-package-programmatically.md)  
 Beschreibt, wie ein vorhandenes Paket von einer Clientanwendung auf dem lokalen Computer ausgeführt wird.  
  
 [Programmgesteuertes Laden und Ausführen eines Remotepakets](../../integration-services/run-manage-packages-programmatically/loading-and-running-a-remote-package-programmatically.md)  
 Beschreibt die Ausführung eines vorhandenes Pakets von einer Clientanwendung und wie sichergestellt wird, dass das Paket auf dem Server ausgeführt wird.  
  
 [Laden der Ausgabe eines lokalen Pakets](../../integration-services/run-manage-packages-programmatically/loading-the-output-of-a-local-package.md)  
 Beschreibt, wie ein Paket auf dem lokalen Computer ausgeführt und die Ausgabe des Datenflusses unter Verwendung des DataReader-Ziels und des DtsClient-Namespaces in eine Clientanwendung geladen wird.  
  
 [Programmgesteuertes Auflisten verfügbarer Pakete](../../integration-services/run-manage-packages-programmatically/enumerating-available-packages-programmatically.md)  
 Beschreibt die verfügbaren Pakete zu ermitteln, die von verwaltet werden die [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Dienst.  
  
 [Programmgesteuerte Verwaltung von Paketen und Ordnern](../../integration-services/run-manage-packages-programmatically/managing-packages-and-folders-programmatically.md)  
 Beschreibt das Erstellen, Umbenennen und Löschen von Paketen und Ordnern.  
  
 [Programmgesteuerte Verwaltung von ausgeführten Paketen](../../integration-services/run-manage-packages-programmatically/managing-running-packages-programmatically.md)  
 Beschreibt, wie Pakete, die gerade ausgeführt werden, aufgelistet werden, wie ihre Eigenschaften untersucht werden und wie ein ausgeführtes Paket beendet werden kann.  
  
 [Programmgesteuertes Verwalten von Paketrollen &#40; SSIS-Dienst &#41;](../../integration-services/run-manage-packages-programmatically/managing-package-roles-programmatically-ssis-service.md)  
 Beschreibt, wie Informationen über die einem Paket oder einem Ordner zugewiesenen Rollen abgerufen oder festgelegt werden können.  
  
## <a name="reference"></a>Verweis  
 [Fehler- und Meldungsreferenz von Integration Services](../../integration-services/integration-services-error-and-message-reference.md)  
 Listet die vordefinierten [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Fehlercodes mit ihren symbolischen Namen und Beschreibungen auf.  
  
## <a name="related-sections"></a>Verwandte Abschnitte  
 [Erweitern von Paketen mit Skripts](../../integration-services/extending-packages-scripting/extending-packages-with-scripting.md)  
 Erläutert, wie die Ablaufsteuerung mithilfe des Skripttasks und der Datenfluss mithilfe der Skriptkomponente erweitert werden können.  
  
 [Erweitern von Paketen mit benutzerdefinierten Objekten](../../integration-services/extending-packages-custom-objects/extending-packages-with-custom-objects.md)  
 Beschreibt, wie benutzerdefinierte Tasks, Datenflusskomponenten und andere Paketobjekte für die Verwendung in mehreren Paketen erstellt und programmiert werden.  
  
 [Programmgesteuertes Erstellen von Paketen](../../integration-services/building-packages-programmatically/building-packages-programmatically.md)  
 Erläutert das Erstellen, konfigurieren und speichern Sie [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Pakete programmgesteuert.  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server Integration Services](../../integration-services/sql-server-integration-services.md)  
  
  

