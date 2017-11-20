---
title: "Schritt 3: Hinzufügen von Paketen und weiteren Dateien | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
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
ms.assetid: a7e6ec9c-d31d-4613-9525-8947a7b358f7
caps.latest.revision: 24
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f8cf4eedc8930492e28f41cee67f0c25a382bacd
ms.contentlocale: de-de
ms.lasthandoff: 09/26/2017

---
# <a name="lesson-1-3---adding-packages-and-other-files"></a>Lektion 1 – 3 – Hinzufügen von Paketen und weiteren Dateien
In diesem Schritt fügen Sie dem im vorherigen Schritt erstellten Deployment Tutorial-Projekt vorhandene Pakete, Hilfsdateien zur Unterstützung einzelner Pakete und eine Infodatei hinzu. Sie fügen z. B. eine XML-Datendatei hinzu, die die Daten für ein Paket und eine Textdatei enthält, von der Infodateiinformationen zu allen Paketen im Projekt bereitgestellt werden.  
  
Wenn Sie Pakete in einer Test- oder Produktionsumgebung bereitstellen, fügen Sie normalerweise die Datendateien nicht in die Bereitstellung ein. Stattdessen verwenden Sie Konfigurationen zum Aktualisieren der Pfade der Datenquellen, um auf Test- oder Produktionsversionen der Datendateien oder Datenbanken zuzugreifen. Zu Unterrichtszwecken sind in diesem Lernprogramm Datendateien in der Paketbereitstellung enthalten.  
  
Die Pakete und die darin verwendeten Beispieldaten werden zusammen mit den [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Beispielen installiert. Sie fügen dem Deployment Tutorial-Projekt die folgenden Pakete hinzu:  
  
-   **DataTransfer.** Einfaches Paket, von dem Daten aus einer Flatfile extrahiert werden, Spaltenwerte ausgewertet werden, um Zeilen bedingt im Dataset beizubehalten, und Daten in eine Tabelle in der AdventureWorks-Datenbank geladen werden.  
  
-   **LoadXMLData.** Datenübertragungspaket, von dem Daten aus einer XML-Datendatei extrahiert, Spaltenwerte ausgewertet und aggregiert sowie Daten in eine Tabelle in der AdventureWorks-Datenbank geladen werden.  
  
Zur Unterstützung der Bereitstellung dieser Pakete fügen Sie dem Deployment Tutorial-Projekt die folgenden Hilfsdateien hinzu.  
  
|Paket|File|  
|-----------|--------|  
|DataTransfer|NewCustomers.txt|  
|LoadXMLData|orders.xml und orders.xsd|  
  
Sie fügen auch eine Infodatei hinzu. Dabei handelt es sich um eine Textdatei, die Informationen zum Deployment Tutorial-Projekt enthält.  
  
Die in den folgenden Verfahren verwendeten Pfade setzen voraus, dass die [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Beispiele am Standardspeicherort, [!INCLUDE[ssSampPathIS](../includes/sssamppathis-md.md)], installiert wurden. Wenn Sie die Beispiele an einem anderen Speicherort installiert haben, müssen Sie stattdessen diesen Speicherort in den Verfahren verwenden.  
  
In der folgenden Aufgabe fügen Sie den DataTransfer- und LoadXMLData-Paketen Konfigurationen hinzu. Alle Konfigurationen werden in XML-Dateien gespeichert. Sie verwenden eine Systemumgebungsvariable, um den Speicherort dieser Dateien anzugeben. Nachdem Sie die Konfigurationsdateien erstellt haben, fügen Sie sie dem Projekt hinzu.  
  
### <a name="to-add-packages-to-the-deployment-tutorial-project"></a>So fügen Sie dem Deployment Tutorial-Projekt Pakete hinzu  
  
1.  Wenn [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] noch nicht geöffnet ist, klicken Sie auf **Start**, zeigen Sie auf **Alle Programme**, zeigen Sie auf **Microsoft SQL Server**, und klicken Sie dann auf **SQL Server Data Tools**.  
  
2.  Klicken Sie im Menü **Datei** auf **Öffnen**&gt; **Projekt/Projektmappe**. Wählen Sie den Ordner **Deployment Tutorial** aus, klicken Sie auf **Öffnen**und anschließend doppelt auf **Deployment Tutorial.sln**.  
  
3.  Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf Deployment Tutorial, dann auf **Hinzufügen**und anschließend auf **Vorhandenes Paket**.  
  
4.  Wählen Sie im Dialogfeld **Kopie des vorhandenen Pakets hinzufügen** unter **Paketspeicherort**die Option **Dateisystem**aus.  
  
5.  Klicken Sie auf die Schaltfläche mit den drei Punkten **(...)** , navigieren Sie zu C:\Program Files\Microsoft SQL Server\100\Samples\Integration ServicesTutorial\Deploying Packages\Completed Packages, wählen Sie **DataTransfer.dtsx**aus, und klicken Sie anschließend auf **Öffnen**.  
  
6.  Klicken Sie auf **OK**.  
  
7.  Wiederholen Sie die Schritte 3 - 6. Fügen Sie diesmal jedoch die Datei LoadXMLData.dtsx hinzu, die sich in C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services\Tutorial\Deploying Packages\Completed Packages befindet.  
  
### <a name="to-add-ancillary-files-to-the-deployment-tutorial-project"></a>So fügen Sie dem Deployment Tutorial-Projekt Hilfsdateien hinzu  
  
1.  Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf Deployment Tutorial, klicken Sie auf **Hinzufügen**und anschließend auf **Vorhandenes Element**.  
  
2.  Navigieren Sie im Dialogfeld **Vorhandenes Element hinzufügen - Deployment Tutorial** zu C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services\Tutorial\Deployment Packages\Sample Data, wählen Sie orders.xml, orders.xsd und NewCustomers.txt aus, und klicken Sie anschließend auf **Hinzufügen**.  
  
3.  Navigieren Sie im Dialogfeld **Vorhandenes Element hinzufügen - Deployment Tutorial** zu C:\Programme\Microsoft SQL Server\100\Samples\Integration Services\Tutorial\Deployment Packages\\, wählen Sie Readme.txt aus und klicken Sie auf **Hinzufügen**.  
  
4.  Klicken Sie im Menü Datei auf **Alle speichern**.  
  
## <a name="next-task-in-lesson"></a>Nächste Aufgabe in der Lektion  
[Schritt 4: Hinzufügen von Paketkonfigurationen](../integration-services/lesson-1-4-adding-package-configurations.md)  
  
  
  

