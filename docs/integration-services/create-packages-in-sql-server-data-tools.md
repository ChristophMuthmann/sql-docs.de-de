---
title: Erstellen von Paketen in SQL Server Data Tools | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: non-specific
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SSIS packages, creating
- Integration Services packages, creating
- packages [Integration Services], creating
- SQL Server Integration Services packages, creating
ms.assetid: bb3c085b-1458-49fa-8348-6a76b6e97ea6
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 4ce6e014e80c33181a6ac41c4d249adb5e5df5a0
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="create-packages-in-sql-server-data-tools"></a>Erstellen von Paketen in SQL Server-Datentools
  In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]können Sie mit einer der folgenden Methoden ein neues Paket erstellen:  
  
-   Verwenden der Paketvorlage in [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
-   Verwenden Sie eine benutzerdefinierte Vorlage.  
  
     Sie müssen nur die als Vorlage zu verwendenden benutzerdefinierten Pakete zum Erstellen neuer Pakete in den DataTransformationItems-Ordner kopieren. Dieser Ordner befindet sich standardmäßig unter C:\Programme\Microsoft Visual Studio 10.0\Common7\IDE\PrivateAssemblies\ProjectItems\DataTransformationProject.  
  
-   Kopieren Sei ein vorhandenes Paket.  
  
     Wenn vorhandene Pakete Funktionen enthalten, die Sie wiederverwenden möchten, können Sie die Ablaufsteuerung und die Datenflüsse des neuen Pakets schneller erstellen, indem Sie aus den anderen Paketen Objekte kopieren und diese im neuen Paket einfügen. Weitere Informationen zu Kopier- und Einfügevorgängen in [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] finden Sie unter [Wiederverwenden von Paketobjekten](../integration-services/reuse-of-package-objects.md).  
  
     Beim Erstellen eines neuen Pakets durch Kopieren eines vorhandenen Pakets oder mithilfe eines benutzerdefinierten Pakets, welches als Vorlage dient, werden Name und GUID des vorhandenen Pakets ebenfalls kopiert. Sie sollten den Namen und GUID des neuen Pakets aktualisieren, um das neue Paket vom Paket, von dem es kopiert wurde, zu unterscheiden. Beispielsweise können bei Paketen mit demselben GUID die Pakete, zu denen die Protokolldaten gehören, schwieriger identifiziert werden. Sie können die GUID in der **ID** -Eigenschaft neu generieren und den Wert der **Name** -Eigenschaft mithilfe des Eigenschaftenfensters in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]aktualisieren. Weitere Informationen finden Sie unter [Festlegen von Paketeigenschaften](../integration-services/set-package-properties.md) und [dtutil (Hilfsprogramm)](../integration-services/dtutil-utility.md).  
  
-   Verwenden Sie ein benutzerdefiniertes Paket, das Sie als Vorlage festgelegt haben.  
  
-   Ausführen des [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Import/Export-Assistenten  
  
     Der [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Import/Export-Assistent erstellt ein vollständiges Paket für einen einfachen Import oder Export. Dieser Assistent konfiguriert die Verbindungen, die Quelle und das Ziel und fügt alle Datentransformationen hinzu, die Sie zum sofortigen Ausführen des Imports oder Exports benötigen. Optional können Sie das Paket speichern, um es zu einem späteren Zeitpunkt auszuführen oder in [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]zu verfeinern und zu erweitern. Wenn Sie das Paket speichern, müssen Sie es jedoch zunächst einem vorhandenen [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Projekt hinzufügen, bevor Sie das Paket ändern oder in [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]ausführen können.  
  
 Die Pakete, die Sie in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] mit dem [!INCLUDE[ssIS](../includes/ssis-md.md)] -Designer erstellen, werden im Dateisystem gespeichert. Zum Speichern eines Pakets in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] oder im Paketspeicher müssen Sie eine Kopie des Pakets speichern. Weitere Informationen finden Sie unter [Erstellen einer Kopie eines Miningmodells](http://msdn.microsoft.com/library/21482a20-e420-4452-b7eb-8f9fa1929f31).  

 Unter [Erstellen eines Basispakets (SQL Server-Video)](http://go.microsoft.com/fwlink/?LinkId=131023)können Sie ein Video abspielen, in dem das Erstellen eines Basispakets mithilfe der Standardpaketvorlage veranschaulicht wird.  

## <a name="get-sql-server-data-tools"></a>Herunterladen von SQL Server Data Tools
Informationen zum Installieren von SQL Server Data Tools (SSDT) finden Sie unter [Herunterladen von SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md).

## <a name="create-a-package-in-sql-server-data-tools-using-the-package-template"></a>Erstellen eines Pakets in SQL Server Data Tools mithilfe der Paketvorlage  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Projekt, in dem Sie ein Paket erstellen möchten.  
  
2.  Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf den Ordner **SSIS-Pakete** , und klicken Sie dann auf **Neues SSIS-Paket**.  
  
3.  Fügen Sie dem Paket optional Ablaufsteuerungen, Datenflusstasks und Ereignishandler hinzu. Weitere Informationen finden Sie unter [Ablaufsteuerung](../integration-services/control-flow/control-flow.md), [Datenfluss](../integration-services/data-flow/data-flow.md) und [Integration Services-Ereignishandler &#40;SSIS&#41;](../integration-services/integration-services-ssis-event-handlers.md).  
  
4.  Klicken Sie im Menü **Datei** auf **Ausgewählte Elemente speichern** , um das neue Paket zu speichern.  
  
    > [!NOTE]  
    >  Es ist möglich, ein leeres Paket zu speichern.  
  
## <a name="choose-the-target-version-of-a-project-and-its-packages"></a>Wählen der Zielversion eines Projekt und der zugehörigen Pakete  
  
1.  Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf ein Integration Services-Projekt, und wählen Sie **Eigenschaften** aus, um die Eigenschaftsseiten für das Projekt zu öffnen.  
  
2.  Klicken Sie in der Registerkarte **Allgemein** in den **Konfigurationseigenschaften**auf die Eigenschaft **TargetServerVersion** , und wählen Sie dann SQL Server 2016, 2014 oder 2012 aus.  
  
     ![TargetServerVersion-Eigenschaft im Dialogfeld „Projekteigenschaften“](../integration-services/media/targetserverversion2.png "TargetServerVersion property in project properties dialog box")  
  
 Sie können Pakete für SQL Server 2016, SQL Server 2014 oder SQL Server 2012 erstellen, verwalten und ausführen.  
  
  
