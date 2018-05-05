---
title: Umbenennen einer Analysis Services-Instanz | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ''
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 48729d35a5c5c5e0e0808862f1317877b1ee3be6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="rename-an-analysis-services-instance"></a>Umbenennen einer Analysis Services-Instanz
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Sie können eine vorhandene Instanz von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] mithilfe des Tools **Instanz umbenennen** umbenennen, das mit Management Studio (Webinstallation) installiert wird.  
  
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
  
  
