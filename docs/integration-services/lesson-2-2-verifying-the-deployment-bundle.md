---
title: "Schritt 2: Überprüfen des Bereitstellungspakets | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: integration-services
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: 6c13f5c9-c75e-4e52-94dc-2d2db2c578fe
caps.latest.revision: 18
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 20d8b11e28f7e26e5b61662d8340ab6dbfcc0b95
ms.contentlocale: de-de
ms.lasthandoff: 09/26/2017

---
# <a name="lesson-2-2---verifying-the-deployment-bundle"></a>Lektion 2 x 2-Überprüfen des Bereitstellungspakets
In Lektion 1 haben Sie das Deployment Tutorial-Projekt erstellt und dem Projekt Pakete und Hilfsdateien hinzugefügt; in der vorherigen Aufgabe haben Sie ein Bereitstellungsprogramm für das Projekt erstellt.  
  
In dieser Aufgabe überprüfen Sie den Inhalt des Bereitstellungspakets. Das Bereitstellungspaket ist der Ordner, den Sie auf den Zielcomputer kopieren und zum Installieren der Pakete verwenden. Wenn Sie den Standardwert – bin\Deployment – als Speicherort des Bereitstellungshilfsprogramms verwendet haben, entspricht das Bereitstellungspaket dem Ordner Bin\Deployment im Ordner Deployment Tutorial des [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Projekts.  
  
### <a name="to-verify-the-content-of-deployment-bundle"></a>So überprüfen Sie den Inhalt des Bereitstellungspakets  
  
1.  Suchen Sie den Ordner bin\Deployment auf dem Computer.  
  
2.  Überprüfen Sie, ob die folgenden Dateien vorhanden sind:  
  
    -   DataTransfer.dtsx  
  
    -   datatransferconfig.dtsconfig  
  
    -   Deployment Tutorial.SSISDeploymentManifest  
  
    -   LoadXMLData.dtsx  
  
    -   loadxmldataconfig.dtsconfig  
  
    -   NewCustomers.txt  
  
    -   orders.xml  
  
    -   orders.xsd  
  
    -   Readme.txt  
  
3.  Klicken Sie mit der rechten Maustaste auf Deployment Tutorial.SSISDeploymentManifest, zeigen Sie auf **Öffnen mit**, und klicken Sie anschließend auf **Internet Explorer**. Sie können die Datei auch in einem Texteditor, wie z. B. dem Editor, öffnen. Der XML-Code für die Datei sollte folgendermaßen lauten:  
  
    `<?xml version="1.0"?><DTSDeploymentManifest GeneratedBy="Domain\UserName" GeneratedFromProjectName="Deployment Tutorial" GeneratedDate="2006-02-24T13:29:02.6537669-08:00" AllowConfigurationChanges="true"><Package>DataTransfer.dtsx</Package><Package>LoadXMLData.dtsx</Package><ConfigurationFile>datatransferconfig.dtsconfig</ConfigurationFile><ConfigurationFile>loadxmldataconfig.dtsconfig</ConfigurationFile><MiscellaneousFile>Readme.txt</MiscellaneousFile><MiscellaneousFile>orders.xml</MiscellaneousFile><MiscellaneousFile>NewCustomers.txt</MiscellaneousFile><MiscellaneousFile>orders.xsd</MiscellaneousFile></DTSDeploymentManifest>`  
  
4.  Überprüfen Sie, ob der Wert des Attributs **AllowConfigurationChanges** **TRUE** lautet und ob der XML-Code je ein **Paket** -Element für die beiden Pakete, je ein **MiscellaneousFile** -Element für die vier Nichtpaketdateien und je ein **ConfigurationFile** -Element für die beiden XML-Konfigurationsdateien enthält.  
  
5.  Beenden Sie Internet Explorer oder den Texteditor.  
  
## <a name="next-lesson"></a>Nächste Lektion  
[Lektion 3: Installieren von SSIS-Paketen](../integration-services/lesson-3-install-ssis-packages.md)  
  
  
  

