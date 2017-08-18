---
title: Installation des Datenbankmoduls von SQL Server Datenbankmodul | Microsoft-Dokumentation
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
- Database Engine [SQL Server], installing
ms.assetid: d0876e7f-aa52-4dd7-bd5c-029e2ffded5f
caps.latest.revision: 45
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 192549457850c9c24fd72ce3f205e0ddedfe1d12
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="install-sql-server-database-engine"></a>Installieren des SQL Server-Datenbankmoduls
  Bei der Komponente [!INCLUDE[ssDE](../../includes/ssde-md.md)] von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] handelt es sich um den zentralen Dienst zum Speichern, Verarbeiten und Sichern von Daten. Das [!INCLUDE[ssDE](../../includes/ssde-md.md)] bietet gesteuerten Zugriff und eine zügige Transaktionsverarbeitung und erfüllt damit die Anforderungen selbst der anspruchsvollsten datenlastigen Anwendungen des Unternehmens.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt bis zu 50 Instanzen von [!INCLUDE[ssDE](../../includes/ssde-md.md)] auf einem einzelnen Computer. Informationen zum Erstellen einer typischen Installation von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] finden Sie unter [Installieren von SQL Server 2016 vom Installations-Assistenten aus &#40;Setup&#41;](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md).  
  
 **Wichtig** Bei einer lokalen Installation müssen Sie Setup als Administrator ausführen. Wenn Sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] von einer Remotefreigabe installieren, müssen Sie ein Domänenkonto verwenden, das Lese- und Ausführungsberechtigungen auf der Remotefreigabe hat.  
  
 Wenn Sie im Installations-Assistenten von **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf der Seite Zu installierende Komponenten die Option** -Datenbankmodul [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auswählen, werden folgenden Funktionen installiert:  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
-   Replikation – optionale Komponente  
  
-   Volltextsuche – optionale Komponente  
  
-   Data Quality Services – optionale Komponente  
  
    > [!NOTE]  
    >  In dieser Version wird durch Aktivieren des Kontrollkästchens **Data Quality Services** während des Setups DQS (Data Quality Services)-Server nicht installiert. Sie müssen nach der Installation weitere Schritte ausführen, um DQS-Server zu installieren. Weitere Informationen finden Sie unter [Install Data Quality Services](../../data-quality-services/install-windows/install-data-quality-services.md).  
  
 In vielen typischen Benutzerszenarien sind die folgenden zusätzlichen Funktionen als Optionen verfügbar:  
  
-   Data Quality Client  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
  
-   Konnektivitätskomponenten  
  
-   Programmiermodelle  
  
-   Verwaltungstools  
  
-   [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]  
  
-   Dokumentationskomponenten  
  
> [!NOTE]  
>  Standardmäßig werden Beispieldatenbanken und Beispielcode nicht als Teil des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Setups installiert. Informationen zur Installation von Beispieldatenbanken und Beispielcode finden Sie auf der [CodePlex-Website](http://go.microsoft.com/fwlink/?LinkId=87843).  
  
## <a name="see-also"></a>Siehe auch  
 [Von den SQL Server 2016-Editionen unterstützte Funktionen](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)   
 [Editionen und Komponenten von SQL Server 2016](../../sql-server/editions-and-components-of-sql-server-2016.md)   
 [Planen einer SQL Server-Installation](../../sql-server/install/planning-a-sql-server-installation.md)   
 [Lösungen mit hoher Verfügbarkeit &#40;SQL Server&#41;](../../sql-server/failover-clusters/high-availability-solutions-sql-server.md)   
 [Aktualisieren auf SQL Server 2016 mithilfe des Installations-Assistenten &#40;Setup&#41;](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)  
  
  

