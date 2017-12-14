---
title: "Lektion 5: Hinzufügen von SSIS-Paketkonfigurationen für das Paketbereitstellungsmodell | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
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
ms.assetid: 1c10dd54-67cb-4b63-9e4d-aa6ff0452ecb
caps.latest.revision: "28"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: ca7f828ee5ade6114887f261b51b9086f17c40d9
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="lesson-5-add-ssis-package-configurations-for-the-package-deployment-model"></a>Lesson 5: Add SSIS Package Configurations for the Package Deployment Model
Mithilfe von Paketkonfigurationen können Sie Laufzeiteigenschaften und -variablen von außerhalb der Entwicklungsumgebung festlegen. Mithilfe von Konfigurationen können Sie Pakete entwickeln, die flexibel und einfach bereitzustellen sowie zu verteilen sind. [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] stellt die folgenden Konfigurationstypen bereit:  
  
-   XML-Konfigurationsdatei  
  
-   Umgebungsvariable  
  
-   Registrierungseintrag  
  
-   Variable für das übergeordnete Paket  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] table  
  
In dieser Lektion ändern Sie das einfache [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Paket, das Sie in [Lesson 4: Adding Error Flow Redirection with SSIS](../integration-services/lesson-4-add-error-flow-redirection-with-ssis.md) (Lektion 4: Hinzufügen der Fehlerflussumleitung mit SSIS) erstellt haben, um das Paketbereitstellungsmodell und die Paketkonfigurationen nutzen zu können. Sie können auch das abgeschlossene Paket aus Lektion 4 kopieren, das im Lieferumfang der Lernprogramme enthalten ist. Mithilfe des Paketkonfigurations-Assistenten erstellen Sie eine XML-Konfiguration, die die **Directory** -Eigenschaft des Foreach-Schleifencontainers mithilfe einer Variablen auf Paketebene aktualisiert, die der Directory-Eigenschaft zugeordnet ist. Nach dem Erstellen der Konfigurationsdatei ändern Sie den Wert der Variablen von außerhalb der Entwicklungsumgebung und legen die geänderte Eigenschaft als Zeiger auf einen neuen Beispieldatenordner fest. Wenn Sie das Paket erneut ausführen, wird der Wert der Variablen von der Konfigurationsdatei aufgefüllt, und die Variable aktualisiert im Gegenzug die **Directory**-Eigenschaft. Im Ergebnis iteriert das Paket durch die Dateien im neuen Datenordner, und nicht durch die Dateien im Originalordner, der im Paket hartcodiert war.  
  
> [!IMPORTANT]  
> Dieses Lernprogramm erfordert die **AdventureWorksDW2012** -Beispieldatenbank. Weitere Informationen zum Installieren und Bereitstellen von **AdventureWorksDW2012**finden Sie unter [Reporting Services Produktbeispiel-Projekt auf CodePlex](http://go.microsoft.com/fwlink/p/?LinkID=526910).  
  
## <a name="lesson-tasks"></a>Lektionsaufgaben  
Diese Lektion enthält die folgenden Aufgaben:  
  
-   [Schritt 1: Kopieren des Pakets aus Lektion 4](../integration-services/lesson-5-1-copying-the-lesson-4-package.md)  
  
-   [Schritt 2: Aktivieren und Konfigurieren von Paketkonfigurationen](../integration-services/lesson-5-2-enabling-and-configuring-package-configurations.md)  
  
-   [Schritt 3: Ändern des Directory-Eigenschaftskonfigurationswertes](../integration-services/lesson-5-3-modifying-the-directory-property-configuration-value.md)  
  
-   [Schritt 4: Testen des Lektion 5-Lernprogrammpakets](../integration-services/lesson-5-4-testing-the-lesson-5-tutorial-package.md)  
  
## <a name="start-the-lesson"></a>Lektion beginnen  
  
-   [Schritt 1: Kopieren des Pakets aus Lektion 4](../integration-services/lesson-5-1-copying-the-lesson-4-package.md)  
  
  
  
