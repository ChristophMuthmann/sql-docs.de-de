---
title: Installieren von SQL Server-Wartungsupdates | Microsoft-Dokumentation
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
ms.assetid: 7d6c962b-c8d0-49f7-a2ac-00ad8dca930a
caps.latest.revision: 13
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a8f82cc7e1afa88af9a3eeb30dc2970baaa10f7b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="install-sql-server-servicing-updates"></a>Installieren von SQL Server-Wartungsupdates

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Dieser Artikel bietet Informationen zum Installieren von Updates für [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)]. In diesem Abschnitt finden Sie Informationen zu den folgenden Themen:
  
- Installieren von Updates für [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)] während einer neuen Installation  
  
- Installieren von Updates für [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)] , nachdem es bereits installiert wurde.  
  
Installieren Sie die neuesten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Updates zeitnah, um sicherzustellen, dass Systeme mit den letzten Sicherheitsupdates aktualisiert wurden.  
  
## <a name="installing-updates-for-includenoversionincludesssnoversion-mdmd-during-a-new-installation"></a>Installieren von Updates für [!INCLUDE[noVersion](../../includes/ssNoVersion-md.md)] während einer neuen Installation  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Setup integriert die neuesten Produktupdates in die Installation des Hauptprodukts, sodass das Hauptprodukt und geeignete Updates gleichzeitig installiert werden. Das Produktupdate kann an folgenden Orten nach anwendbaren Updates suchen:  
  
- [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update  
  
- Windows Server Update Services (WSUS)  
  
- Ein lokaler Ordner  
  
- Eine Netzwerkfreigabe  
  
Nachdem Setup die neuesten Versionen der anwendbaren Updates gefunden hat, lädt es diese herunter und integriert sie in den aktuellen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Installationsvorgang. Produktupdate kann ein kumulatives Update, Service Pack oder Service Pack plus kumulatives Update enthalten.  
  
## <a name="installing-updates-for-includessnoversionincludesssnoversion-mdmd-after-it-has-already-been-installed"></a>Installieren von Updates für [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)] , nachdem es bereits installiert wurde  
Auf einer installierten Instanz von [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)]empfiehlt es sich, dass Sie die letzten Sicherheitsupdates und wichtige Updates einschließlich allgemeiner Verteilungsversionen (GDRs), Service Packs (SPS) und kumulativer Updates anwenden. Weitere Informationen finden Sie in der [Ankündigung zum inkrementellen Servicemodell für SQL Server (ISM) vom März 2016](http://blogs.msdn.microsoft.com/sqlreleaseservices/announcing-updates-to-the-sql-server-incremental-servicing-model-ism/).

> [!NOTE]
> Ab [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] wurde ein vereinfachtes vorhersehbares, allgemeingültiges Servicemodell implementiert. Service Packs (SPs) sind nicht mehr verfügbar, sondern bei Bedarf nur noch kumulative Updates (Cumulative Updates, CUs) und allgemeine Vertriebsversionen (General Distribution Releases, GDRs).
> Weitere Informationen finden Sie in der [Ankündigung zum modernen Servicemodell für SQL Server (MSM) vom September 2017](http://blogs.msdn.microsoft.com/sqlreleaseservices/announcing-the-modern-servicing-model-for-sql-server/).
  
Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Updates sind über [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update (MU), Windows Server Update Services (WSUS) und das Microsoft Download Center verfügbar. Sicherheits- und wichtige Updates für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sind über [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update verfügbar. Um diese Updates sehen zu können, müssen Sie sich in MU durch das Windows Update-Applet in der Systemsteuerung anmelden.  
  
Wenn Sie über [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update ein Update empfangen, aktualisiert es alle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Funktionen im unbeaufsichtigten Modus auf die neueste Version. Wenn Sie mehr Flexibilität benötigen oder keinen Internet- oder WSUS-Zugriff haben, müssen Sie die Updates aus dem [!INCLUDE[msCoName](../../includes/msconame-md.md)] Download Center abrufen.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[Installieren von SQL Server über den Installations-Assistenten &#40;Setup&#41;](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)
[Hinzufügen von Funktionen zu einer Instanz von SQL Server &#40;Setup&#41;](../../database-engine/install-windows/add-features-to-an-instance-of-sql-server-2016-setup.md)
[Reparieren von Fehlern bei einer SQL Server-Installation](../../database-engine/install-windows/repair-a-failed-sql-server-installation.md)  

