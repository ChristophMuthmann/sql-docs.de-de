---
title: "Schritt 3: Ändern des Directory-Eigenschaftskonfigurationswertes | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: ba2a091f-361c-4331-afe2-53b465164c36
caps.latest.revision: 29
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 881aab31aab8cc4dc339b5f399f8cd207feb6ebb
ms.contentlocale: de-de
ms.lasthandoff: 09/26/2017

---
# <a name="lesson-5-3---modifying-the-directory-property-configuration-value"></a>Lektion 5-3: Ändern des Directory-Eigenschaftskonfigurationswertes
In dieser Aufgabe ändern Sie die in der Datei SSISTutorial.dtsConfig gespeicherte Konfigurationseinstellung für die Wert-Eigenschaft der Variablen `User::varFolderName`auf Paketebene. Die Variable aktualisiert die Verzeichnis-Eigenschaft des Foreach-Schleifencontainers. Der geänderte Wert zeigt nun auf den Ordner **New Sample Data** , den Sie in der vorherigen Aufgabe erstellt haben. Nachdem Sie die Konfigurationseinstellung geändert und das Paket ausgeführt haben, wird die Verzeichnis-Eigenschaft durch die Variable aktualisiert. Dabei wird der durch die Konfigurationsdatei aufgefüllte Wert anstelle des Verzeichniswerts verwendet, der ursprünglich im Paket konfiguriert war.  
  
### <a name="to-modify-the-configuration-setting-of-the-directory-property"></a>So ändern Sie die Konfigurationseinstellung der Directory-Eigenschaft  
  
1.  Suchen und öffnen Sie in Editor oder einem beliebigen anderen Texteditor die Konfigurationsdatei SSISTutorial.dtsConfig, die Sie mithilfe des Paketkonfigurations-Assistenten in der vorhergehenden Aufgabe erstellt haben.  
  
2.  Ändern Sie den Wert des **ConfiguredValue** -Elements so, dass er mit dem Pfad des Ordners **New Sample Data** übereinstimmt, den Sie in der vorherigen Aufgabe erstellt haben. Schließen Sie den Pfad nicht in Anführungszeichen ein. Wenn sich der Ordner **New Sample Data** auf der Stammebene des Laufwerks (z. B. C:\\) befindet, sollten die aktualisierten XML-Daten dem folgenden Beispiel ähneln:  
  
    `<?xml version="1.0"?><DTSConfiguration><DTSConfigurationHeading><DTSConfigurationFileInfo GeneratedBy="DOMAIN\UserName" GeneratedFromPackageName="Lesson 5" GeneratedFromPackageID="{F4475E73-59E3-478F-8EB2-B10AFA61D3FA}" GeneratedDate="6/10/2012 8:16:50 AM"/></DTSConfigurationHeading><Configuration ConfiguredType="Property" Path="\Package.Variables[User::varFolderName].Properties[Value]" ValueType="String"><ConfiguredValue></ConfiguredValue></Configuration></DTSConfiguration>`  
  
    Die Überschrifteninformationen **GeneratedBy**, **GeneratedFromPackageID**und **GeneratedDate** unterscheiden sich in Ihrer Datei natürlich. Achten Sie insbesondere auf das **Konfiguration** -Element. Die **Wert** -Eigenschaft der Variablen `User::varFolderName`enthält nun den Wert C:\New Sample Data.  
  
3.  Speichern Sie die Änderung, und schließen Sie dann den Texteditor.  
  
## <a name="next-task-in-lesson"></a>Nächste Aufgabe in der Lektion  
[Schritt 4: Testen des Lektion 5-Lernprogrammpakets](../integration-services/lesson-5-4-testing-the-lesson-5-tutorial-package.md)  
  
  
  

