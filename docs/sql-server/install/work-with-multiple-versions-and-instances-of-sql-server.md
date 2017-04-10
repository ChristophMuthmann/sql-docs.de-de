---
title: "Verwenden mehrerer Versionen und Instanzen von SQL Server | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "setup-install"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Gleichzeitige Installationen [SQL Server]"
  - "Versionen [SQL Server], mehrere"
  - "Parallele Installationen [SQL Server]"
  - "Mehrere Versionen von SQL Server-Komponenten"
  - "Installieren von SQL Server, parallele Installationen"
  - "Setup [SQL Server], parallele Installationen"
  - "64-Bit-Edition [SQL Server]"
  - "32-Bit-Edition [SQL Server]"
  - "Editionen [SQL Server], parallele Installationen"
ms.assetid: 93acefa8-bb41-4ccc-b763-7801f51134e0
caps.latest.revision: 67
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 67
---
# Verwenden mehrerer Versionen und Instanzen von SQL Server
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] können auf ein und demselben Computer mehrere Instanzen von [!INCLUDE[ssDE](../../includes/ssde-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]und [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] verwaltet werden. Darüber hinaus können Sie frühere Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aktualisieren oder [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf einem Computer installieren, auf dem bereits frühere [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Versionen installiert sind. Unterstützte Upgradeszenarien finden Sie unter [Unterstützte Versions- und Editionsupgrades](../../database-engine/install-windows/supported-version-and-edition-upgrades.md).  
  
## Versionskomponenten und Nummerierung  
 Die folgenden Konzepte sind nützlich, um das Verhalten von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] für parallele Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zu verstehen.  
  
 Das Standardformat der Produktversion für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ist MM.nn.bbbb.rr, wobei die einzelnen Segmente wie folgt definiert sind:  
  
 MM - Hauptversion  
  
 nn - Nebenversion  
  
 bbbb - Buildnummer  
  
 rr - Buildrevisionsnummer  
  
 Bei jeder Haupt- oder Nebenversion von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wird die Versionsnummer erhöht, damit sie sich von früheren Versionen unterscheidet. Diese Änderung an der Version wird zu vielen Zwecken verwendet. Dazu gehören das Anzeigen von Versionsinformationen an der Benutzeroberfläche, die Steuerung der Ersetzung von Dateien während eines Upgrades, die Anwendung von Service Packs sowie die funktionale Differenzierung zwischen den aufeinanderfolgenden Versionen.  
  
### Von allen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 Bestimmte Komponenten werden von allen Instanzen aller installierten Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gemeinsam genutzt. Wenn Sie unterschiedliche Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf demselben Computer parallel installieren, werden diese Komponenten automatisch auf die neueste Version aktualisiert. Solche Komponenten werden im Allgemeinen automatisch deinstalliert, wenn die letzte Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deinstalliert wird.  
  
 Beispiele: der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Browser und Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] VSS Writer.  
  
### Von allen Instanzen derselben [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Versionen, die die gleiche Hauptversion aufweisen, werden einige Komponenten von allen Instanzen gemeinsam genutzt. Wenn die freigegebenen Komponenten während des Upgrades ausgewählt werden, werden die vorhandenen Komponenten auf die neueste Version aktualisiert.  
  
 Beispiele: [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)], [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]und die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Onlinedokumentation.  
  
### Von Nebenversionen gemeinsam genutzte Komponenten  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Versionen, die die gleiche Haupt- und Nebenversion aufweisen, nutzen Komponenten gemeinsam.  
  
 Beispiel: Unterstützungsdateien für Setup.  
  
### Für eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 Einige [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Komponenten oder -Dienste gehören speziell zu einer bestimmten Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Sie werden auch als instanzabhängig bezeichnet. Sie nutzen die gleiche Version wie ihre Hostinstanz und werden ausschließlich für diese Instanz verwendet.  
  
 Beispiele: [!INCLUDE[ssDE](../../includes/ssde-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]und [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
### Von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Versionen unabhängige Komponenten  
 Bestimmte Komponenten werden während [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Setup installiert, aber sind von den Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]unabhängig. Sie werden möglicherweise von Hauptversionen oder von allen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Versionen gemeinsam genutzt.  
  
 Beispiele: Microsoft Sync Framework, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact.  
  
 Weitere Informationen über die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact-Installation finden Sie unter [Installieren von SQL Server 2016 vom Installations-Assistenten aus &#40;Setup&#41;](../../database-engine/install-windows/install-sql-server-2016-from-the-installation-wizard-setup.md). Weitere Informationen zur Deinstallation von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact finden Sie unter [Deinstallieren einer vorhandenen SQL Server-Instanz &#40;Setup&#41;](../../sql-server/install/uninstall-an-existing-instance-of-sql-server-setup.md).  
  
## Parallele Verwendung von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 Sie können [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf einem Computer installieren, auf dem bereits Instanzen einer früheren [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Version ausgeführt werden. Wenn auf dem Computer bereits eine Standardinstanz vorhanden ist, muss [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] als benannte Instanz installiert werden.  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SysPrep bietet keine Unterstützung für die parallele Installation von vorbereiteten [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] -Instanzen und früheren [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Versionen auf demselben Computer. Beispielsweise können Sie keine Instanz von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] parallel zu einer Instanz von vorbereiteten Instanz von [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]vorbereiten. Sie können jedoch mehrere vorbereitete Instanzen der gleichen Hauptversion von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] parallel auf dem gleichen Computer installieren. Weitere Informationen finden Sie unter [Considerations for Installing SQL Server Using SysPrep](../../database-engine/install-windows/considerations-for-installing-sql-server-using-sysprep.md).  
>   
>  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] kann nicht parallel mit früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf einem Computer installiert werden, auf dem Windows Server 2008 R2 Server Core SP1 ausgeführt wird. Weitere Informationen zu Server Core-Installationen finden Sie unter [Installieren von SQL Server 2016 unter Server Core](../../database-engine/install-windows/install-sql-server-2016-on-server-core.md).  
  
 In der folgenden Tabelle wird die Unterstützung für eine parallele Installation von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] dargestellt:  
  
|Vorhandene Instanz von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]|Unterstützung paralleler Installationen|  
|--------------------------------------------------|----------------------------|  
|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] (64-Bit) [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)]|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] (32-Bit)<br /><br /> [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] (64-Bit) [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)]<br /><br /> [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (32-Bit)<br /><br /> [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (64-Bit) [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)]<br /><br /> [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] (32-Bit)<br /><br /> [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] (64-Bit) [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)]<br /><br /> [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] (32-Bit)<br /><br /> [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] (64-Bit) [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)]<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] (32-Bit)<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] (64-Bit) [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)]|  
  
## Verhindern von Konflikten mit IP-Adressen  
 Wenn eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Failoverclusterinstanz und eine eigenständige [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]-Instanz parallel installiert sind, achten Sie darauf, dass Konflikte mit TCP-Portnummern für die IP-Adressen vermieden werden. Konflikte treten in der Regel auf, wenn in zwei [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanzen die Verwendung des TCP-Standartports (1433) konfiguriert wurde. Um Konflikte zu vermeiden, konfigurieren Sie in einer Instanz die Verwendung eines nicht standardmäßigen festen Ports. Die Konfiguration eines festen Ports kann in der Regel in der eigenständigen Instanz am einfachsten vorgenommen werden. Wenn [!INCLUDE[ssDE](../../includes/ssde-md.md)] für die Verwendung anderer Ports konfiguriert wird, wird verhindert, dass ein unerwarteter IP-Adressen-/TCP-Port-Konflikt auftritt, der den Start einer Instanz blockiert, wenn eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Failoverclusterinstanz einen Failover zu dem Standbyknoten ausführt.  
  
## Siehe auch  
 [Hardware- und Softwareanforderungen für die Installation von SQL Server 2016](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server-2016.md)   
 [Installieren von SQL Server 2016 vom Installations-Assistenten aus &#40;Setup&#41;](../../database-engine/install-windows/install-sql-server-2016-from-the-installation-wizard-setup.md)   
 [Unterstützte Versions- und Editionsupgrades](../../database-engine/install-windows/supported-version-and-edition-upgrades.md)   
 [Aktualisieren auf SQL Server 2016](../../database-engine/install-windows/upgrade-to-sql-server-2016.md)   
 [Von den SQL Server 2016-Editionen unterstützte Funktionen](../Topic/Features%20Supported%20by%20the%20Editions%20of%20SQL%20Server%202016.md)   
 [Abwärtskompatibilität_gelöscht](../Topic/Backward%20Compatibility_deleted.md)  
  
  