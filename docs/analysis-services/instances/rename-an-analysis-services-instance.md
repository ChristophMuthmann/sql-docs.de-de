---
title: Umbenennen einer Analysis Services-Instanz | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- instances of Analysis Services, renaming
- renaming instances of Analysis Services
- names [Analysis Services], renaming instances
- names [Analysis Services]
ms.assetid: 87494741-4a2e-4fed-8061-418fd1e111c3
caps.latest.revision: "53"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: c08828062b6434b29e91c217af652f6445b75b19
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="rename-an-analysis-services-instance"></a>Umbenennen einer Analysis Services-Instanz
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Sie können eine vorhandene Instanz von umbenennen [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] mithilfe der **Instanz umbenennen** Tool, mit Management Studio (Webinstallation) installiert.  
  
> [!IMPORTANT]  
>  Das Tool zum Umbenennen von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Instanzen wird beim Umbenennen der Instanz mit erhöhten Rechten ausgeführt und aktualisiert den Windows-Dienstnamen, Sicherheitskonten und Registrierungseinträge, die dieser Instanz zugeordnet sind. Um sicherzustellen, dass diese Aktionen stattfinden, muss das Tool als lokaler Systemadministrator ausgeführt werden.  
  
 Das Tool zum Umbenennen von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Instanzen ändert nicht den Programmordner, der für die ursprüngliche Instanz erstellt wurde. Ändern Sie den Namen des Programmordners nicht entsprechend der umbenannten Instanz. Wenn Sie den Namen eines Programmordners ändern, kann dies dazu führen, dass Setup die Installation nicht reparieren oder deinstallieren kann.  
  
> [!NOTE]  
>  Das [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Tool zur Instanzumbenennung wird in einer Clusterumgebung nicht unterstützt.  
  
### <a name="to-rename-an-instance-of-analysis-services"></a>So benennen Sie eine Instanz von Analysis Services um  
  
1.  Starten Sie das **Tool zum Umbenennen von Instanzen** , asinstancerename.exe, im Verzeichnis **C:\Program Files (x86)\Microsoft SQL Server\130\Tools\Binn\ManagementStudio**.  
  
2.  Wählen Sie im Dialogfeld **Instanz umbenennen** aus der Liste **Umzubenennende Instanz** die Instanz aus, die Sie umbenennen möchten.  
  
3.  Geben Sie in das Feld **Neuer Instanzname** den neuen Namen für die Instanz ein.  
  
4.  Überprüfen Sie den Benutzernamen und das Kennwort, und klicken Sie auf **Umbenennen**.  
  
     Die Analysis Services-Instanz wird im Rahmen der Namensänderung beendet und neu gestartet.  
  
### <a name="post-rename-checklist"></a>Prüfliste nach dem Umbenennen  
  
1.  Um wieder auf die Datenbanken auf der umbenannten Instanz zugreifen zu können, müssen Sie die Datenverbindungen in Excel oder anderen Clientanwendungen manuell aktualisieren. Überprüfen Sie auch alle vordefinierten Verbindungen, z. B. freigegebene Reporting Services-Datenquellen, Excel-ODC-Dateien oder BI Semantikmodell-Verbindungsdateien, die möglicherweise auf die umbenannte Instanz verweisen. Weitere Informationen finden Sie unter [Verbinden mit Analysis Services](../../analysis-services/instances/connect-to-analysis-services.md).  
  
2.  Aktualisieren Sie PowerShell-Skripts oder AMO-Skripts, mit denen Sie routinemäßig Datenbanken sichern, synchronisieren oder verarbeiten.  
  
3.  Aktualisieren Sie die Projekteigenschaften für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekte, mit denen Sie in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]arbeiten. Für Serverinstanzen im tabellarischen Modus müssen die Eigenschaft Arbeitsbereichsserver für die Datei model.bim und die Eigenschaft Server für das Projekt aktualisiert werden.  
  
4.  Je nachdem, wie Sie das Dienstkonto angegeben haben, müssen Sie ggf. Datenbank-Anmeldenamen oder Dateiberechtigungen aktualisieren, die dem Dienst Datenzugriffsrechte gewähren (z. B., wenn Sie das Dienstkonto verwenden, um Daten zu verarbeiten oder auf verknüpfte Objekte auf einem anderen Server zuzugreifen).  
  
     Das Aktualisieren eines Datenbank-Anmeldenamens oder von Dateiberechtigungen ist erforderlich, wenn Sie ein virtuelles Konto zum Bereitstellen des Diensts verwendet haben. Virtuelle Konten basieren auf dem Instanznamen. Wenn Sie die Instanz umbenennen, wird daher gleichzeitig auch das virtuelle Konto aktualisiert. Dies bedeutet, dass alle vorherigen Anmeldenamen oder Berechtigungen, die Sie für die vorherige Instanz erstellt haben, nicht mehr gültig sind.  
  
     Dies wird im folgenden Beispiel veranschaulicht. Angenommen, Sie haben einen Server im tabellarischen Modus als Instanz mit dem Namen "Tabular" unter Verwendung des virtuellen Standardkontos installiert. Die resultierende Konfiguration sieht wie folgt aus:  
  
    1.  Instanzname = \<Server > \TABULAR  
  
    2.  Dienstname = MSOLAP$TABULAR  
  
    3.  Virtuelles Konto = NT-Dienst\ MSOLAP$TABULAR  
  
     Angenommen, Sie benennen die Instanz jetzt in "TAB2" um. Nach der Namensänderung würde die Konfiguration wie folgt aussehen:  
  
    1.  Instanzname = \<Server > \TAB2  
  
    2.  Dienstname = MSOLAP$TAB2  
  
    3.  Virtuelles Konto = NT-Dienst\ MSOLAP$TAB2  
  
     Wie Sie sehen können, sind Datenbank- und Dateiberechtigungen, die "NT-Dienst\ MSOLAP$TABULAR" zuvor gewährt wurden, nicht mehr gültig. Um sicherzustellen, dass Tasks und Vorgänge wie zuvor vom Dienst ausgeführt werden, müssen Sie "für NT-Dienst\ MSOLAP$TAB2" neue Datenbank- und Dateiberechtigungen gewähren.  
  
  
