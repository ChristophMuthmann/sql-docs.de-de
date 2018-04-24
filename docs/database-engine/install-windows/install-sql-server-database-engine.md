---
title: Installation des Datenbankmoduls von SQL Server Datenbankmodul | Microsoft-Dokumentation
ms.custom: ''
ms.date: 09/05/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: install-windows
ms.reviewer: ''
ms.suite: sql
ms.technology:
- setup-install
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Database Engine [SQL Server], installing
ms.assetid: d0876e7f-aa52-4dd7-bd5c-029e2ffded5f
caps.latest.revision: 45
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 88b8ac95ab76abdd7fa7772fa422293d421c8884
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="install-sql-server-database-engine"></a>Installieren des SQL Server-Datenbankmoduls

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Bei der Komponente [!INCLUDE[ssDE](../../includes/ssde-md.md)] von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] handelt es sich um den zentralen Dienst zum Speichern, Verarbeiten und Sichern von Daten. Das [!INCLUDE[ssDE](../../includes/ssde-md.md)] bietet gesteuerten Zugriff und eine zügige Transaktionsverarbeitung und erfüllt damit die Anforderungen selbst der anspruchsvollsten datenlastigen Anwendungen des Unternehmens.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt bis zu 50 Instanzen von [!INCLUDE[ssDE](../../includes/ssde-md.md)] auf einem einzelnen Computer. Um eine typische [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Installation durchzuführen, gehen Sie auf die Seite [Install SQL Server from the Installation Wizard &#40;Setup&#41; (Installieren von SQL Server mit dem Installations-Assistenten &#40;Setup&#41;)](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md).  
  
>[!IMPORTANT]
>Bei lokalen Installationen müssen Sie das Setup als Administrator ausführen. Wenn Sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] von einer Remotefreigabe installieren, müssen Sie ein Domänenkonto verwenden, das Lese- und Ausführungsberechtigungen auf der Remotefreigabe hat.  
  
## <a name="related-features"></a>Verwandte Funktionen

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
>  Standardmäßig werden Beispieldatenbanken und Beispielcode nicht als Teil des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Setups installiert. Informationen zur Installation von Beispieldatenbanken und Beispielcode finden Sie unter [Microsoft SQL Server Samples (Beispiele für Microsoft SQL Server)](../../sample/microsoft-sql-server-samples.md). Ältere Beispiele finden Sie auf der [CodePlex](http://go.microsoft.com/fwlink/?LinkId=87843)-Seite.  
  
## <a name="see-also"></a>Siehe auch  
 [Editionen und unterstützten Funktionen von SQL Server 2017](~/sql-server/editions-and-components-of-sql-server-2017.md)   
 [Planen einer SQL Server-Installation](../../sql-server/install/planning-a-sql-server-installation.md)   
 [Lösungen mit hoher Verfügbarkeit &#40;SQL Server&#41;](../../sql-server/failover-clusters/high-availability-solutions-sql-server.md)   
 [Upgrade SQL Server Using the Installation Wizard (Setup) (Upgrade von SQL Server mithilfe des Installations-Assistenten (Setup))](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)  
  
  
