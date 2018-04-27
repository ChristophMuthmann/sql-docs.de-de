---
title: Bereitstellen von Paketen mit SSIS | Microsoft-Dokumentation
ms.custom: ''
ms.date: 11/16/2016
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: non-specific
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: get-started-article
helpviewer_keywords:
- deployment tutorial [Integration Services]
- deploying packages [Integration Services]
- SSIS, tutorials
- Integration Services, tutorials
- deploying packages [Integration Services], installing
- SQL Server Integration Services, tutorials
- walkthroughs [Integration Services]
- deployment utility [Integration Services]
- deploying packages [Integration Services], configurations
ms.assetid: de18468c-cff3-48f4-99ec-6863610e5886
caps.latest.revision: 27
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 5c6d9d81bf1924c05e4c6d735d5ac1d6de74593b
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="deploy-packages-with-ssis"></a>Bereitstellen von Paketen mit SSIS
[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] bietet Tools zum einfachen Bereitstellen von Paketen auf anderen Computern. Von den Bereitstellungstools werden auch mögliche Abhängigkeiten wie vom Paket benötigte Konfigurationen und Dateien verwaltet. In diesem Lernprogramm lernen Sie, wie Sie diese Tools verwenden, um Pakete und ihre Abhängigkeiten auf einem Zielrechner zu installieren.    
    
Zuerst führen Sie Aufgaben aus, um die Bereitstellung vorzubereiten. Sie erstellen zunächst ein neues [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Projekt in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] und fügen diesem vorhandene Pakete und Datendateien hinzu. Sie erstellen keine neuen Pakete. Stattdessen arbeiten Sie nur mit fertigen Paketen, die speziell für dieses Lernprogramm erstellt wurden. Sie nehmen in diesem Lernprogramm keine Änderung der Funktionalität der Pakete vor. Nachdem Sie die Pakete dem Projekt hinzugefügt haben, sollten Sie sie jedoch im [!INCLUDE[ssIS](../includes/ssis-md.md)] -Designer öffnen und ihren Inhalt überprüfen. Durch Untersuchen der Pakete erhalten Sie Informationen zu Paketabhängigkeiten wie Protokolldateien und weiteren interessanten Funktionen der Pakete.    
    
Bei der Vorbereitung der Bereitstellung aktualisieren Sie die Pakete auch, um Konfigurationen zu verwenden. Durch die Konfigurationen können die Eigenschaften von Paketen und Paketobjekten zur Laufzeit aktualisiert werden. In diesem Lernprogramm verwenden Sie Konfigurationen, um die Verbindungszeichenfolgen der Protokoll- und Textdateien und die Speicherorte der XML- und XSD-Dateien, die vom Paket verwendet werden, zu aktualisieren. Weitere Informationen zu Konfigurationen finden Sie unter [Paketkonfigurationen](../integration-services/packages/package-configurations.md) und [Erstellen von Paketkonfigurationen](../integration-services/packages/create-package-configurations.md).    
    
Nachdem Sie überprüft haben, ob die Pakete erfolgreich in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]ausgeführt werden, erstellen Sie die Bereitstellungsgruppe, um die Pakete zu installieren. Die Bereitstellungsgruppe besteht aus den Paketdateien und weiteren Elementen, die Sie dem [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Projekt hinzugefügt haben, den Paketabhängigkeiten, die [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] automatisch enthält, und dem von Ihnen erstellten Bereitstellungshilfsprogramm. Weitere Informationen finden Sie unter [Create a Deployment Utility](../integration-services/packages/create-a-deployment-utility.md).    
    
Sie kopieren dann die Bereitstellungsgruppe zum Zielrechner und führen den Paketinstallations-Assistenten aus, um die Pakete und Paketabhängigkeiten zu installieren. Die Pakete werden in der SQL Server-Datenbank msdb installiert, und die Unterstützungs- und Hilfsdateien werden im Dateisystem installiert. Da die bereitgestellten Pakete Konfigurationen verwenden, aktualisieren Sie die Konfiguration zur Verwendung neuer Werte, damit die Pakete erfolgreich in der neuen Umgebung ausgeführt werden können.    
    
Schließlich führen Sie die Pakete in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] mithilfe des Paketausführungshilfsprogramms aus.    
    
Es ist Ziel dieses Lernprogramms, die Komplexität von Bereitstellungsproblemen zu simulieren, die in der Praxis auftreten können. Wenn Sie die Pakete nicht auf einem anderen Computer bereitstellen können, können Sie dieses Lernprogramm dennoch ausführen. Dazu müssen Sie die Pakete in der msdb-Datenbank einer lokalen Instanz von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]installieren und dann von [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] auf derselben Instanz ausführen.    
    
## <a name="what-you-will-learn"></a>Lernziele    
Die beste Möglichkeit, den Umgang mit den neuen Tools, Steuerelementen und Funktionen von [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] zu üben, besteht in ihrer Verwendung. Dieses Lernprogramm führt Sie schrittweise durch die Erstellung eines [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Projekts und das anschließende Hinzufügen der Pakete und weiterer erforderlicher Dateien zum Projekt. Wenn das Projekt vollständig ist, erstellen Sie ein Bereitstellungspaket, kopieren es zum Zielcomputer und installieren dann die Pakete auf dem Zielcomputer.    
    
## <a name="requirements"></a>Anforderungen    
Dieses Tutorial wendet sich an Benutzer, die bereits mit grundlegenden Dateisystemvorgängen vertraut sind, aber nur über begrenzte Kenntnisse in Bezug auf die neuen Funktionen von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]verfügen. Um die grundlegenden [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Konzepte besser zu verstehen, deren Sie sich in diesem Tutorial bedienen, sollten Sie zuerst die folgenden [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Tutorials ausführen: [SSIS-Tutorials: Erstellen eines einfachen ETL-Pakets](../integration-services/ssis-how-to-create-an-etl-package.md).    
    
**Quellcomputer.** Auf dem Computer, auf dem Sie das Bereitstellungspaket erstellen, **müssen die folgenden Komponenten installiert sein:**
- SQL Server  
- Beispieldaten, fertige Pakete, Konfigurationen und eine Infodatei. Diese Dateien werden zusammen installiert, wenn Sie die [Adventure Works 2014 Sample Databases](https://msftdbprodsamples.codeplex.com/releases/view/125550)herunterladen.     
> **Hinweis!** Sie müssen die Berechtigung haben, Tabellen in AdventureWorks oder andere Daten, die Sie verwenden, erstellen und löschen zu können.         
    
-   [SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md)    
    
**Zielcomputer.** Auf dem Computer, auf dem Sie die Pakete bereitstellen, **müssen die folgenden Komponenten installiert sein:**    
    
- SQL Server
- Beispieldaten, fertige Pakete, Konfigurationen und eine Infodatei. Diese Dateien werden zusammen installiert, wenn Sie die [Adventure Works 2014 Sample Databases](https://msftdbprodsamples.codeplex.com/releases/view/125550)herunterladen. 
    
- [SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md).    
    
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].    
    
-   Sie müssen über die Berechtigungen zum Erstellen und Löschen von Tabellen in AdventureWorks und zum Ausführen von Paketen in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]verfügen.    
    
-   Sie müssen über Lese- und Schreibberechtigung für die sysssispackages-Tabelle in der [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Systemdatenbank msdb verfügen.    
    
Wenn Sie die Pakete auf demselben Computer bereitstellen möchten wie dem, auf dem Sie das Bereitstellungspaket erstellen, muss dieser Computer die Anforderungen sowohl des Quell- als auch des Zielcomputers erfüllen.    
    
**Geschätzte Zeit zum Bearbeiten dieses Tutorials:** 2 Stunden    
    
## <a name="lessons-in-this-tutorial"></a>Lektionen in diesem Lernprogramm    
[Lektion 1: Vorbereiten der Erstellung des Bereitstellungspakets](../integration-services/lesson-1-preparing-to-create-the-deployment-bundle.md)    
In dieser Lektion beginnen Sie mit der Bereitstellung einer ETL-Lösung, indem Sie ein neues [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Projekt erstellen und diesem die Pakete und weitere erforderliche Dateien hinzufügen.    
    
[Lektion 2: Erstellen des Bereitstellungspakets in SSIS](../integration-services/lesson-2-create-the-deployment-bundle-in-ssis.md)    
In dieser Lektion erstellen Sie ein Bereitstellungshilfsprogramm und überprüfen, ob das Bereitstellungspaket die notwendigen Dateien enthält.    
    
[Lektion 3: Installieren von SSIS-Paketen](../integration-services/lesson-3-install-ssis-packages.md)    
In dieser Lektion kopieren Sie das Bereitstellungspaket auf den Zielcomputer, installieren die Pakete und führen diese dann aus.    
    

