---
title: 'Lektion 6: Verwenden von Parametern mit dem Projektbereitstellungsmodell in SSIS | Microsoft-Dokumentation'
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: integration-services
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to: SQL Server 2016
ms.assetid: 9216f18c-1762-4f2d-8c22-bd0ab7107555
caps.latest.revision: "5"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 9e6cc56ec5fe995f27833fad48ec75c317598587
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="lesson-6-using-parameters-with-the-project-deployment-model-in-ssis"></a>Lesson 6: Using Parameters with the Project Deployment Model in SSIS
In SQL Server 2012 wird ein neues Bereitstellungsmodell eingeführt, mit dem Sie Projekte auf dem Integration Services-Server bereitstellen können. Der Integration Services-Server ermöglicht es Ihnen, Pakete zu verwalten und auszuführen sowie Laufzeitwerte für Pakete zu konfigurieren.  
  
In dieser Lektion ändern Sie das Paket, das Sie in [Lektion 5: Hinzufügen von SSIS-Paketkonfigurationen für das Paketbereitstellungsmodell](../integration-services/lesson-5-add-ssis-package-configurations-for-the-package-deployment-model.md) erstellt haben, um das Projektbereitstellungsmodell verwenden. Sie ersetzen den Konfigurationswert durch einen Parameter, um den Speicherort der Beispieldaten anzugeben. Sie können auch das abgeschlossene Paket aus Lektion 5 kopieren, das im Lieferumfang der Lernprogramme enthalten ist.  
  
Mithilfe des Assistenten zum Konvertieren von Integration Services-Projekten konvertieren Sie das Projekt in das Projektbereitstellungsmodell und verwenden einen Parameter anstelle eines Konfigurationswerts, um die Directory-Eigenschaft festzulegen. Diese Lektion enthält einen Teil der Schritte, die Sie ausführen müssen, um vorhandene SSIS-Pakete in das neue Projektbereitstellungsmodell zu konvertieren.  
  
Wenn Sie das Paket erneut ausführen, verwendet der Integration Services-Dienst den Parameter, um den Wert der Variablen aufzufüllen, und die Variable aktualisiert wiederum die Directory-Eigenschaft. Deshalb durchläuft das Paket die Dateien im neuen, durch den Parameterwert angegebenen Datenordner anstatt in dem Ordner, der in der Paketkonfigurationsdatei festgelegt wurde.  
  
> [!IMPORTANT]  
> Dieses Lernprogramm erfordert die **AdventureWorksDW2012** -Beispieldatenbank. Weitere Informationen zur Installation und Bereitstellung von **AdventureWorksDW2012**finden Sie unter [Überlegungen zum Installieren der SQL Server-Beispiele und -Beispieldatenbanken](http://technet.microsoft.com/en-us/library/ms161556%28v=sql.105%29).  
  
## <a name="lesson-tasks"></a>Lektionsaufgaben  
Diese Lektion enthält die folgenden Aufgaben:  
  
1.  [Schritt 1: Kopieren des Pakets aus Lektion 5](../integration-services/lesson-6-1-copying-the-lesson-5-package.md)  
  
2.  [Schritt 2: Converting the Project to the Project Deployment Model (Konvertieren des Projekts in das Projektbereitstellungsmodell)](../integration-services/lesson-6-2-converting-the-project-to-the-project-deployment-model.md)  
  
3.  [Schritt 3: Testen des Pakets aus Lektion 6](../integration-services/lesson-6-3-testing-the-lesson-6-package.md)  
  
4.  [Schritt 4: Bereitstellen des Pakets aus Lektion 6](../integration-services/lesson-6-4-deploying-the-lesson-6-package.md)  
  
## <a name="start-the-lesson"></a>Lektion beginnen  
[Schritt 1: Kopieren des Pakets aus Lektion 5](../integration-services/lesson-6-1-copying-the-lesson-5-package.md)  
  
