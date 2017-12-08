---
title: Erstellen eines Analysis Services-Projekts (SSDT) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- templates [Analysis Services]
- templates [Analysis Services], projects
- projects [Analysis Services], creating
- projects [Analysis Services], Business Intelligence Development Studio
- Business Intelligence Development Studio, defining projects [Analysis Services]
- items [Analysis Services]
ms.assetid: d00913b0-cd6d-4de0-a1e7-4ce86fcc078d
caps.latest.revision: "37"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: a5b26af390b901d6f23eacd409d919a6d1c656ee
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="create-an-analysis-services-project-ssdt"></a>Erstellen eines Analysis Services-Projekts (SSDT)
  Sie können ein [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] entweder mithilfe der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projektvorlage oder mithilfe des Assistenten zum Importieren einer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank definieren, um die Inhalte einer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank zu lesen. Wenn gerade keine Projektmappe in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]geladen ist, wird beim Erstellen eines neuen [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekts automatisch eine neue Projektmappe erstellt. Andernfalls wird der vorhandenen Projektmappe das neue [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt hinzugefügt. Eine bewährte Methode für die Projektmappenentwicklung besteht darin, getrennte Projekte für die verschiedenen Typen von Anwendungsdaten unter Verwendung einer einzelnen Projektmappe zu erstellen, sofern sich die Projekte aufeinander beziehen. Sie können z. B. über eine einzelne Projektmappe verfügen, die getrennte Projekte für Integration Services-Pakete, Analysis Services-Datenbanken und Reporting Services-Berichte enthält, die alle von der gleichen Geschäftsanwendung verwendet werden.  
  
 Ein Analysis Services-Projekt enthält in einer einzelnen Analysis Services-Datenbank verwendete Objekte. Der Name des Servers und der Datenbank, unter denen die Projektmetadaten als instanziierte Objekte bereitgestellt werden, sind in den Bereitstellungseigenschaften des Projekts angegeben.  
  
 Dieses Thema enthält folgende Abschnitte:  
  
 [Erstellen eines neuen Projekts unter Verwendung der Vorlage "Analysis Services-Projekt"](#bkmk_NewUsingTemplate)  
  
 [Erstellen eines neuen Projekts mithilfe einer vorhandenen Analysis Services-Datenbank](#bkmk_NewUsingWizard)  
  
 [Hinzufügen eines Analysis Services-Projekts zu einer vorhandenen Projektmappe](#bkmk_AddtoExistingSolution)  
  
 [Erstellen und Bereitstellen der Projektmappe](#bkmk_buildDeploy)  
  
 [Analysis Services-Projektordner](#bkmk_ProjectFolders)  
  
 [Analysis Services-Dateitypen](#bkmk_FileTypes)  
  
 [Analysis Services-Elementvorlagen](#bkmk_ItemTemplates)  
  
##  <a name="bkmk_NewUsingTemplate"></a> Erstellen eines neuen Projekts unter Verwendung der Vorlage "Analysis Services-Projekt"  
 Verwenden Sie diese Anweisungen zum Erstellen eines leeren Projekts, in dem Sie [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Objekte definieren, die Sie anschließend als neue [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank bereitstellen können.  
  
1.  Klicken Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]auf **Datei**, zeigen Sie auf **Neu**, und klicken Sie auf **Projekt**. Wählen Sie im Dialogfeld **Neues Projekt** im Bereich **Projekttypen** die Option **Business Intelligence-Projekte**aus.  
  
2.  Wählen Sie im Dialogfeld **Neues Projekt** in der Kategorie **Von Visual Studio installierte Vorlagen** die Option **Analysis Services-Projekt**aus.  
  
3.  Geben Sie im Textfeld **Name** den Namen des Projekts ein. Der eingegebene Name wird als Standardname für die Datenbank verwendet.  
  
4.  Geben Sie in der Dropdownliste **Speicherort** den Ordner ein, oder wählen Sie den Ordner aus, in dem Sie die Dateien für das Projekt speichern möchten, oder klicken Sie auf **Durchsuchen** , um einen Ordner auszuwählen.  
  
5.  Wählen Sie in der Dropdownliste **Projektmappe** die Option **Zur Projektmappe hinzufügen**aus, um das neue Projekt der vorhandenen Projektmappe hinzuzufügen.  
  
     – oder –  
  
     Wählen Sie in der Dropdownliste **Projektmappe** die Option **Neue Projektmappe erstellen**aus, um eine neue Projektmappe zu erstellen. Aktivieren Sie das Kontrollkästchen **Projektmappenverzeichnis erstellen**, um einen neuen Ordner für die neue Projektmappe zu erstellen. Geben Sie im Feld **Projektmappenname**den Namen der neuen Projektmappe ein.  
  
6.  Klicken Sie auf **OK**.  
  
##  <a name="bkmk_NewUsingWizard"></a> Erstellen eines neuen Projekts mithilfe einer vorhandenen Analysis Services-Datenbank  
 Erstellen Sie mithilfe des Assistenten zum Importieren einer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank ein Projekt, das auf den Objekten in der vorhandenen [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank basiert. Wenn Sie ein [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt auf Grundlage einer vorhandenen [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank definieren, werden die Metadaten für diese Datenbank in einem [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]geöffnet. Diese Objekte können dann innerhalb des Projekts geändert werden, ohne dass sich dies auf die ursprünglichen Objekte auswirkt, und anschließend in derselben [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank, sofern diese Datenbank in den Bereitstellungseigenschaften angegeben ist, oder zu Vergleichszwecken in einer neu erstellten [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank bereitgestellt werden. Die vorgenommenen Änderungen haben so lange keine Auswirkungen auf die vorhandene [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank, bis die Änderungen bereitgestellt werden.  
  
 Sie können auch die Vorlage [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank importieren verwenden, um ein Projekt auf Basis einer Produktionsdatenbank zu erstellen, an der seit der Bereitstellung des ursprünglichen [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekts Änderungen direkt vorgenommen wurden.  
  
 Bevor Sie das Projekt verarbeiten oder bereitstellen, müssen Sie u. U. den Datenanbieter ändern, der in den Datenquellen angegeben ist. Wenn die verwendete SQL Server-Software neuer als die Software ist, die zum Erstellen der Datenbank verwendet wurde, ist der im Projekt angegebene Datenanbieter u. U. nicht auf dem Computer installiert. Während der Verarbeitung wird das Dienstkonto zum Abrufen der Daten in der Analysis Services-Datenbank verwendet. Wenn sich die Datenbank auf einem Remoteserver befindet, überprüfen Sie, ob der lokale Dienst über Verarbeitungs- und Leseberechtigungen auf diesem Server verfügt.  
  
1.  Klicken Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]auf **Datei**, zeigen Sie auf **Neu**, und klicken Sie auf **Projekt**. Wählen Sie im Dialogfeld **Neues Projekt** im Bereich **Projekttypen** die Option **Business Intelligence-Projekte**aus.  
  
2.  Wählen Sie im Dialogfeld **Neues Projekt** in der Kategorie **Von Visual Studio installierte Vorlagen** die Option **Analysis Services-Datenbank importieren**aus.  
  
3.  Geben Sie Eigenschaftsinformationen für das Projekt und die Projektmappe ein, einschließlich den Namen und Speicherort für die Dateien. Klicken Sie auf **OK**.  
  
4.  Klicken Sie auf der Seite **Assistent zum Importieren einer Analysis Services-Datenbank** auf **Weiter**.  
  
5.  Geben Sie auf der Seite **Quelldatenbank** den Server und die Datenbank an, aus der der Assistent den Inhalt extrahieren wird und auf deren Basis das [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt erstellt wird, und klicken Sie dann auf **Weiter**.  
  
     Die in den folgenden Versionen von Analysis Services erstellten Datenbanken werden unterstützt: [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]und [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].  
  
     Sie können den Datenbanknamen entweder eingeben oder den Server abfragen, um die vorhandenen Datenbanken auf dem Server anzuzeigen. Wenn sich die Datenbank auf einem Remoteserver oder einem Produktionsserver befindet, müssen Sie u. U. eine Leseberechtigung für die Datenbank anfordern. Darüber hinaus kann der Zugriff auf eine Datenbank durch Konfigurationseinstellungen für die Firewall eingeschränkt werden. Wenn beim Versuch, eine Verbindung mit der Datenbank herzustellen, ein Fehler auftritt, überprüfen Sie zunächst die Berechtigungen und Firewalleinstellungen.  
  
6.  Wenn der Assistent das Extrahieren des Inhalts der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank abgeschlossen hat, klicken Sie auf der Seite **Assistenten abschließen** auf **Fertig stellen** .  
  
7.  Öffnen Sie das Fenster Projektmappen-Explorer, um den Inhalt des Projekts anzuzeigen.  
  
##  <a name="bkmk_AddtoExistingSolution"></a> Hinzufügen eines Analysis Services-Projekts zu einer vorhandenen Projektmappe  
 Wenn Sie bereits über eine Projektmappe verfügen, die alle Quelldateien einer Geschäftsanwendung enthält, können Sie dieser Projektmappe ein neues Analysis Services-Projekt hinzufügen.  
  
 Beim Hinzufügen eines vorhandenen Projekts zu einer Projektmappe wird das Projekt der Projektmappe zugeordnet, jedoch nicht kopiert. Wenn das Analysis Services-Projekt in einer anderen Projektmappe erstellt wurde, verbleiben die Projektdateien in der ursprünglichen Projektmappe, für die es erstellt wurde. Dies bedeutet, dass alle Änderungen, die Sie über eine der beiden Projektmappen am Projekt vornehmen, auf den gleichen Satz von Quelldateien angewendet werden. Wenn dieses Verhalten nicht gewünscht ist, sollten Sie die Projektdateien zuerst in den neuen Projektmappenordner kopieren oder verschieben und das Projekt erst dann der Projektmappe hinzufügen.  
  
1.  Öffnen Sie die Projektmappe in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf die Projektmappe, zeigen Sie auf **Hinzufügen**, und klicken Sie dann auf **Vorhandenes Projekt** , um das hinzuzufügende Projekt auszuwählen.  
  
2.  Wählen Sie eine DWPROJ-Datei aus, die der Projektmappe hinzugefügt werden soll.  
  
##  <a name="bkmk_buildDeploy"></a> Erstellen und Bereitstellen der Projektmappe  
 Standardmäßig stellt [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] ein Projekt auf der Standardinstanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] auf dem lokalen Computer bereit. Sie können dieses Bereitstellungsziel ändern, indem Sie im Dialogfeld **Eigenschaftenseiten** des [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekts eine Änderung der **Server** -Konfigurationseigenschaft vornehmen.  
  
> [!NOTE]  
>  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] verarbeitet beim Bereitstellen einer Projektmappe standardmäßig nur Objekte, die vom Bereitstellungsskript geändert wurden, sowie von ihnen abhängige Objekte. Sie können diese Funktionalität ändern, indem Sie im Dialogfeld **Eigenschaftenseiten** für das [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt eine Änderung der Verarbeitungsoption-Konfigurationseigenschaft vornehmen.  
  
 Erstellen Sie zu Testzwecken die Projektmappe in einer Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] und stellen diese bereit. Beim Erstellen einer Projektmappe werden die Objektdefinitionen und Abhängigkeiten im Projekt überprüft und ein Bereitstellungsskript generiert. Beim Bereitstellen einer Projektmappe wird das Bereitstellungsmodul von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] verwendet, um das Bereitstellungsskript an die angegebene Instanz zu senden.  
  
 Nachdem Sie das Projekt bereitgestellt haben, muss die bereitgestellte Datenbank überprüft und getestet werden. Anschließend können Sie Objektdefinitionen ändern und das Projekt erneut erstellen und bereitstellen, bis es abgeschlossen ist.  
  
 Nachdem das Projekt abgeschlossen ist, können Sie das beim Erstellen der Projektmappe generierte Bereitstellungsskript mithilfe des Bereitstellungs-Assistenten auf den Zielinstanzen bereitstellen, um dort die letzten Test-, Staging- und Bereitstellungsarbeiten auszuführen.  
  
##  <a name="bkmk_ProjectFolders"></a> Analysis Services-Projektordner  
 Ein [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt enthält die folgenden Ordner, in denen die im Projekt enthaltenen Elemente organisiert werden.  
  
|Ordner|Description|  
|------------|-----------------|  
|Datenquellen|Enthält Datenquellen für ein [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt. Erstellen Sie diese Objekte mit dem Datenquellen-Assistenten und bearbeiten Sie sie im Datenquellen-Designer.|  
|Datenquellensichten|Enthält Datenquellensichten für ein [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt. Erstellen Sie diese Objekte mit dem Datenquellensicht-Assistenten und bearbeiten Sie sie im Datenquellensicht-Designer.|  
|Cubes|Enthält Cubes für ein [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt. Erstellen Sie diese Objekte mit dem Cube-Assistenten und bearbeiten sie im Cube-Designer.|  
|Dimensionen|Enthält Dimensionen für ein [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt. Erstellen Sie diese Objekte mit dem Dimensions-Assistenten oder dem Cube-Assistenten und bearbeiten Sie sie im Dimensions-Designer.|  
|Miningstrukturen|Enthält Miningstrukturen für ein [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt. Erstellen Sie diese Objekte mit dem Miningmodell-Assistenten und bearbeiten sie im Miningmodell-Designer.|  
|Rollen|Enthält Datenbankrollen für ein [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt. Erstellen und verwalten Sie Rollen mit dem Rollen-Designer.|  
|Assemblys|Enthält Verweise auf COM-Bibliotheken und [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework-Assemblys für ein [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt. Erstellen Sie Verweise im Dialogfeld **Verweis hinzufügen** .|  
|Sonstiges|Enthält alle Dateitypen außer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Dateitypen. Fügen Sie diesem Ordner sonstige Dateien hinzu, z. B. Textdateien mit Projektnotizen.|  
  
##  <a name="bkmk_FileTypes"></a> Analysis Services-Dateitypen  
 Je nachdem, welche Projekte in die Projektmappe und welche Elemente in die einzelnen Projekte für die betreffende Projektmappe eingefügt wurden, kann eine [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] -Projektmappe mehrere Dateitypen enthalten. Normalerweise werden die Dateien aller Projekte in einer [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] -Projektmappe im Projektmappenordner gespeichert, wobei für jedes Projekt ein eigener Ordner angelegt wird.  
  
> [!NOTE]  
>  Wenn Sie eine Datei für ein Objekt in einen Projektordner kopieren, wird dadurch das Objekt nicht dem Projekt hinzugefügt. Verwenden Sie in **den Befehl** Hinzufügen [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] aus dem Kontextmenü für das Projekt, um eine vorhandene Objektdefinition einem Projekt hinzuzufügen.  
  
 Der Projektordner für ein [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt kann die in der folgenden Tabelle aufgelisteten Dateitypen enthalten.  
  
|Dateityp|Description|  
|---------------|-----------------|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Projektdefinitionsdatei (DWPROJ)|Enthält Metadaten zu den Elementen, Konfigurationen und Assemblyverweisen, die im [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt definiert und enthalten sind.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Benutzereinstellungen für das Projekt (DWPROJ.USER)|Enthält Konfigurationsinformationen für das [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt für einen bestimmten Benutzer.|  
|Datenquelldatei (DS)|Enthält die [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -ASSL-Elemente (Analysis Services Scripting Language), die die Metadaten für eine Datenquelle definieren.|  
|Datenquellen-Sichtdatei (DSV)|Enthält die ASSL-Elemente, die die Metadaten für eine Datenquellensicht definieren.|  
|Cubedatei (CUBE)|Enthält die ASSL-Elemente, die die Metadaten für einen Cube definieren, einschließlich Measuregruppen, Measures und Cubedimensionen.|  
|Partitionsdatei (PARTITIONS)|Enthält die ASSL-Elemente, die die Metadaten für die Partitionen eines bestimmten Cubes definieren.|  
|Dimensionsdatei (DIM)|Enthält die ASSL-Elemente, die die Metadaten für eine Datenbankdimension definieren.|  
|Miningstrukturdatei (DMM)|Enthält die ASSL-Elemente, die die Metadaten für eine Miningstruktur und verbundene Miningmodelle definieren.|  
|Datenbankdatei (DATABASE)|Enthält die ASSL-Elemente, die die Metadaten für eine Datenbank definieren, einschließlich Kontotypen, Übersetzungen und Datenbankberechtigungen.|  
|Datenbank-Rollendatei (ROLE)|Enthält die ASSL-Elemente, die die Metadaten für eine Datenbankrolle definieren, einschließlich Rollenmitglieder.|  
  
##  <a name="bkmk_ItemTemplates"></a> Analysis Services-Elementvorlagen  
 Wenn Sie über das Dialogfeld **Neues Element hinzufügen** einem [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt neue Elemente hinzufügen, können Sie wahlweise eine Elementvorlage, ein vordefiniertes Skript oder eine vordefinierte Anweisung verwenden, die die Ausführung einer bestimmten Aktion veranschaulicht.  
  
 Die in der folgenden Tabelle aufgelisteten Elementvorlagen sind in der Kategorie [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projektelemente im Dialogfeld **Neues Element hinzufügen** verfügbar.  
  
|Kategorie|Elementvorlage|Description|  
|--------------|-------------------|-----------------|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projektelemente|Cube|Startet den Cube-Assistenten, um dem [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt einen neuen Cube hinzuzufügen.|  
||Datenquelle|Startet den Datenquellen-Assistenten, um dem [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt eine neue Datenquelle hinzuzufügen.|  
||Datenquellensicht|Startet den Datenquellensicht-Assistenten, um dem [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt eine neue Datenquellensicht hinzuzufügen.|  
||Datenbankrolle|Fügt dem [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt eine neue Datenbankrolle hinzu. Anschließend wird der Rollen-Designer für die neue Datenbankrolle angezeigt.|  
||Dimension|Startet den Dimensions-Assistenten, um dem [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt eine neue Datenbankdimension hinzuzufügen.|  
||Miningstruktur|Startet den Data Mining-Assistenten, um dem [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt eine neue Miningstruktur und das zugehörige Miningmodell hinzuzufügen.|  
  
## <a name="see-also"></a>Siehe auch  
 [Konfigurieren von Analysis Services-Projekteigenschaften &#40;SSDT&#41;](../../analysis-services/multidimensional-models/configure-analysis-services-project-properties-ssdt.md)   
 [Erstellen von Analysis Services-Projekten &#40;SSDT&#41;](../../analysis-services/multidimensional-models/build-analysis-services-projects-ssdt.md)   
 [Bereitstellen von Analysis Services-Projekten &#40;SSDT&#41;](../../analysis-services/multidimensional-models/deploy-analysis-services-projects-ssdt.md)  
  
  
