---
title: Verwenden mehrerer Versionen und Instanzen von SQL Server | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- setup-install
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- concurrent installations [SQL Server]
- versions [SQL Server], multiple
- side-by-side installations [SQL Server]
- multiple SQL Server component versions
- installing SQL Server, side-by-side installations
- Setup [SQL Server], side-by-side installations
- 64-bit edition [SQL Server]
- 32-bit edition [SQL Server]
- editions [SQL Server], side-by-side installations
ms.assetid: 93acefa8-bb41-4ccc-b763-7801f51134e0
caps.latest.revision: 67
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: a5a66deec44b0d3d2b6b25c08f32cc34301ad0fc
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="work-with-multiple-versions-and-instances-of-sql-server"></a>Verwenden mehrerer Versionen und Instanzen von SQL Server
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] können auf ein und demselben Computer mehrere Instanzen von [!INCLUDE[ssDE](../../includes/ssde-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]und [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] verwaltet werden. Darüber hinaus können Sie frühere Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]aktualisieren oder [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf einem Computer installieren, auf dem bereits frühere [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Versionen installiert sind. Unterstützte Upgradeszenarien finden Sie unter [Unterstützte Versions- und Editionsupgrades](../../database-engine/install-windows/supported-version-and-edition-upgrades.md).  
  
## <a name="version-components-and-numbering"></a>Versionskomponenten und Nummerierung  
 Die folgenden Konzepte sind nützlich, um das Verhalten von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] für parallele Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]zu verstehen.  
  
 Das Standardformat der Produktversion für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ist MM.nn.bbbb.rr, wobei die einzelnen Segmente wie folgt definiert sind:  
  
 MM - Hauptversion  
  
 nn - Nebenversion  
  
 bbbb - Buildnummer  
  
 rr - Buildrevisionsnummer  
  
 Bei jeder Haupt- oder Nebenversion von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]wird die Versionsnummer erhöht, damit sie sich von früheren Versionen unterscheidet. Diese Änderung an der Version wird zu vielen Zwecken verwendet. Dazu gehören das Anzeigen von Versionsinformationen an der Benutzeroberfläche, die Steuerung der Ersetzung von Dateien während eines Upgrades, die Anwendung von Service Packs sowie die funktionale Differenzierung zwischen den aufeinanderfolgenden Versionen.  
  
### <a name="components-shared-by-all-versions-of-includessnoversionincludesssnoversion-mdmd"></a>Von allen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 Bestimmte Komponenten werden von allen Instanzen aller installierten Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]gemeinsam genutzt. Wenn Sie unterschiedliche Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf demselben Computer parallel installieren, werden diese Komponenten automatisch auf die neueste Version aktualisiert. Solche Komponenten werden im Allgemeinen automatisch deinstalliert, wenn die letzte Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deinstalliert wird.  
  
 Beispiele: der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Browser und Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] VSS Writer.  
  
### <a name="components-shared-across-all-instances-of-the-same-major-version-of-includessnoversionincludesssnoversion-mdmd"></a>Von allen Instanzen derselben [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Versionen, die die gleiche Hauptversion aufweisen, werden einige Komponenten von allen Instanzen gemeinsam genutzt. Wenn die freigegebenen Komponenten während des Upgrades ausgewählt werden, werden die vorhandenen Komponenten auf die neueste Version aktualisiert.  
  
 Beispiele: [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)], [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]und die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Onlinedokumentation.  
  
### <a name="components-shared-across-minor-versions"></a>Von Nebenversionen gemeinsam genutzte Komponenten  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Versionen, die die gleiche Haupt- und Nebenversion aufweisen, nutzen Komponenten gemeinsam.  
  
 Beispiel: Unterstützungsdateien für Setup.  
  
### <a name="components-specific-to-an-instance-of-includessnoversionincludesssnoversion-mdmd"></a>Für eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 Einige [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Komponenten oder -Dienste gehören speziell zu einer bestimmten Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Sie werden auch als instanzabhängig bezeichnet. Sie nutzen die gleiche Version wie ihre Hostinstanz und werden ausschließlich für diese Instanz verwendet.  
  
 Beispiele: [!INCLUDE[ssDE](../../includes/ssde-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]und [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
### <a name="components-that-are-independent-of-the-includessnoversionincludesssnoversion-mdmd-versions"></a>Von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Versionen unabhängige Komponenten  
 Bestimmte Komponenten werden während [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Setup installiert, aber sind von den Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]unabhängig. Sie werden möglicherweise von Hauptversionen oder von allen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Versionen gemeinsam genutzt.  
  
 Beispiele: Microsoft Sync Framework, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact.  
  
 Weitere Informationen über die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact-Installation finden Sie unter [Installieren von SQL Server 2016 vom Installations-Assistenten aus &#40;Setup&#41;](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md). Weitere Informationen zur Deinstallation von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact finden Sie unter [Deinstallieren einer vorhandenen SQL Server-Instanz &#40;Setup&#41;](../../sql-server/install/uninstall-an-existing-instance-of-sql-server-setup.md).  
  
## <a name="using-includessnoversionincludesssnoversion-mdmd-side-by-side-with-previous-versions-of-includessnoversionincludesssnoversion-mdmd"></a>Parallele Verwendung von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 Sie können [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf einem Computer installieren, auf dem bereits Instanzen einer früheren [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Version ausgeführt werden. Wenn auf dem Computer bereits eine Standardinstanz vorhanden ist, muss [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] als benannte Instanz installiert werden.  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SysPrep bietet keine Unterstützung für die parallele Installation von vorbereiteten [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] -Instanzen und früheren [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Versionen auf demselben Computer. Beispielsweise können Sie keine Instanz von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] parallel zu einer Instanz von vorbereiteten Instanz von [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]vorbereiten. Sie können jedoch mehrere vorbereitete Instanzen der gleichen Hauptversion von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] parallel auf dem gleichen Computer installieren. Weitere Informationen finden Sie unter [Considerations for Installing SQL Server Using SysPrep](../../database-engine/install-windows/considerations-for-installing-sql-server-using-sysprep.md).  
>   
>  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] kann nicht parallel mit früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf einem Computer installiert werden, auf dem Windows Server 2008 R2 Server Core SP1 ausgeführt wird. Weitere Informationen zu Server Core-Installationen finden Sie unter [Installieren von SQL Server 2016 unter Server Core](../../database-engine/install-windows/install-sql-server-on-server-core.md).  
  
 In der folgenden Tabelle wird die Unterstützung für eine parallele Installation von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]dargestellt:  
  
|Vorhandene Instanz von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]|Unterstützung paralleler Installationen|  
|--------------------------------------------------|----------------------------|  
|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] (64-Bit) [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)]|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] (32-Bit)<br /><br /> [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] (64-Bit) [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)]<br /><br /> [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (32-Bit)<br /><br /> [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (64-Bit) [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)]<br /><br /> [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] (32-Bit)<br /><br /> [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] (64-Bit) [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)]<br /><br /> [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] (32-Bit)<br /><br /> [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] (64-Bit) [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)]<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] (32-Bit)<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] (64-Bit) [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)]|  
  
## <a name="preventing-ip-address-conflicts"></a>Verhindern von Konflikten mit IP-Adressen  
 Wenn eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Failoverclusterinstanz und eine eigenständige [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]-Instanz parallel installiert sind, achten Sie darauf, dass Konflikte mit TCP-Portnummern für die IP-Adressen vermieden werden. Konflikte treten in der Regel auf, wenn in zwei [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Instanzen die Verwendung des TCP-Standartports (1433) konfiguriert wurde. Um Konflikte zu vermeiden, konfigurieren Sie in einer Instanz die Verwendung eines nicht standardmäßigen festen Ports. Die Konfiguration eines festen Ports kann in der Regel in der eigenständigen Instanz am einfachsten vorgenommen werden. Wenn [!INCLUDE[ssDE](../../includes/ssde-md.md)] für die Verwendung anderer Ports konfiguriert wird, wird verhindert, dass ein unerwarteter IP-Adressen-/TCP-Port-Konflikt auftritt, der den Start einer Instanz blockiert, wenn eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Failoverclusterinstanz einen Failover zu dem Standbyknoten ausführt.  
  
## <a name="see-also"></a>Siehe auch  
 [Hardware- und Softwareanforderungen für die Installation von SQL Server 2016](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)   
 [Installieren von SQL Server 2016 vom Installations-Assistenten aus &#40;Setup&#41;](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)   
 [Unterstützte Versions- und Editionsupgrades](../../database-engine/install-windows/supported-version-and-edition-upgrades.md)   
 [Aktualisieren auf SQL Server 2016](../../database-engine/install-windows/upgrade-sql-server.md)   
 [Von den SQL Server 2016-Editionen unterstützte Funktionen](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)   
 [Abwärtskompatibilität_gelöscht](http://msdn.microsoft.com/library/15d9117e-e2fa-4985-99ea-66a117c1e9fd)  
  
  

