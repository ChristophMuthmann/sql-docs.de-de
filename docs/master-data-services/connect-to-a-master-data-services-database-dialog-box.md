---
title: Verbindung mit einer Master Data Services-Datenbank herstellen (Dialogfeld) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: mds
ms.service: ''
ms.component: non-specific
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.mds.configmanager.srvconnect.f1
ms.assetid: b2f8c9b9-c31e-4f0d-9095-978709423190
caps.latest.revision: 10
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 124d70b1c0696bdc47834796e82a83b03f867f4c
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="connect-to-a-master-data-services-database-dialog-box"></a>Verbindung mit einer Master Data Services-Datenbank herstellen (Dialogfeld)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Verwenden Sie das Dialogfeld **Verbindung mit einer Master Data Services-Datenbank herstellen** , um eine [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] -Datenbank auszuwählen.  
  
 In [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]ist dieses Dialogfeld auf den folgenden Seiten verfügbar:  
  
-   Klicken Sie auf der Seite **Datenbankkonfiguration** auf **Datenbank auswählen.** Wählen Sie über dieses Dialogfeld eine Datenbank aus, für die Sie Systemeinstellungen konfigurieren möchten.  
  
-   Klicken Sie auf der Seite **Webkonfiguration** unter **///Anwendung einer Datenbank zuordnen**auf **Auswählen** , um die Datenbank auszuwählen, die der [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] -Website oder -Anwendung zugewiesen werden soll.  
  
## <a name="select-database"></a>Datenbank auswählen  
 Geben Sie Informationen für die Verbindung mit einer lokalen oder Remoteinstanz von [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] an, auf der die [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] -Datenbank gehostet werden soll. Um eine Verbindung mit einer Remoteinstanz herzustellen, müssen Sie diese für Remoteverbindungen einrichten.  
  
|Steuerelementname|Description|  
|------------------|-----------------|  
|**SQL Server-Instanz**|Geben Sie den Namen der [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] -Instanz an, auf der die [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] -Datenbank gehostet werden soll. Dies kann eine Standardinstanz oder eine benannte Instanz auf einem lokalen oder Remotecomputer sein. Geben Sie die Informationen wie folgt an:<br /><br /> Einen Punkt (.) für die Verbindung mit der Standardinstanz auf dem lokalen Computer.<br /><br /> Den Servernamen oder die IP-Adresse für die Verbindung mit der Standardinstanz auf dem angegebenen lokalen oder Remotecomputer.<br /><br /> Der Servername oder die IP-Adresse und der Instanzname für die Verbindung mit der benannten Instanz auf dem angegebenen lokalen oder Remotecomputer. Geben Sie diese Informationen im Format *Servername*\\*Instanzname*an.|  
|**Authentifizierungstyp**|Wählen Sie den Authentifizierungstyp aus, der für die Verbindung mit der angegebenen [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Instanz verwendet werden soll. Welche Datenbanken in der Dropdownliste **Master Data Services-Datenbank** angezeigt werden, hängt von den Anmeldeinformationen ab, mit denen Sie die Verbindung herstellen.<br /><br /> Mögliche Authentifizierungstypen:<br /><br /> **Aktueller Benutzer – Integrierte Sicherheit**: Verwendet die integrierte Windows-Authentifizierung, um eine Verbindung mit den Anmeldeinformationen des aktuellen Windows-Benutzerkontos herzustellen. [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] verwendet die Windows-Anmeldeinformationen des Benutzers, der am Computer angemeldet ist und die Anwendung geöffnet hat. Sie können keine anderen Windows-Anmeldeinformationen in der Anwendung angeben. Wenn Sie die Verbindung mit anderen Windows-Anmeldeinformationen herstellen möchten, müssen Sie sich als der betreffende Benutzer am Computer anmelden und [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]öffnen.<br /><br /> **SQL Server-Konto**: Verwendet ein SQL Server-Konto für die Verbindung. Wenn Sie diese Option auswählen, sind die Felder **Benutzername** und **Kennwort** aktiviert, und Sie müssen Anmeldeinformationen für ein [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Konto auf der betreffenden [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Instanz angeben.|  
|**User name**|Geben Sie den Namen des Benutzerkontos an, unter dem eine Verbindung mit der angegebenen SQL Server-Instanz hergestellt wird. Das Konto muss der Rolle **sysadmin** auf der angegebenen [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Instanz angehören:<br /><br /> Wenn der **Authentifizierungstyp** auf **Aktueller Benutzer – Integrierte Sicherheit**festgelegt wurde, ist das Feld **Benutzername** schreibgeschützt und zeigt den Namen des Windows-Benutzerkontos an, das auf dem Computer angemeldet ist.<br /><br /> Wenn der **Authentifizierungstyp** auf **SQL Server-Konto**festgelegt wurde, ist das Feld **Benutzername** aktiviert, und Sie müssen Anmeldeinformationen für ein [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Konto auf der betreffenden [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Instanz angeben.|  
|**Kennwort**|Geben Sie das Kennwort ein, das dem Benutzerkonto zugeordnet ist:<br /><br /> Wenn der **Authentifizierungstyp** auf **Aktueller Benutzer – Integrierte Sicherheit**festgelegt wurde, ist das Feld **Kennwort** schreibgeschützt, und die Verbindung wird mit Anmeldeinformationen des angegebenen Windows-Benutzerkontos hergestellt.<br /><br /> Wenn der **Authentifizierungstyp** auf **SQL Server-Konto**festgelegt wurde, ist das Feld **Kennwort** aktiviert, und Sie müssen das Kennwort angeben, das dem betreffenden Benutzerkonto zugeordnet ist.|  
|**Verbinden**|Stellen Sie mit den angegebenen Anmeldeinformationen eine Verbindung mit der [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Instanz her.|  
|**Master Data Services-Datenbank**|Zeigt die [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] -Datenbanken in der angegebenen [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Instanz auf Grundlage der folgenden Kriterien an:<br /><br /> Wenn der Benutzer Mitglied der Serverrolle **sysadmin** für diese Instanz ist, werden alle [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] -Datenbanken in dieser Instanz angezeigt.<br /><br /> Wenn der Benutzer ein Mitglied der Datenbankrolle **db_owner** für beliebige [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] -Datenbanken auf dieser Instanz ist, werden diese [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] -Datenbanken angezeigt.<br /><br/> Weitere Informationen zu SQL Server finden Sie unter [Rollen auf Serverebene](../relational-databases/security/authentication-access/server-level-roles.md) und [Rollen auf Datenbankebene](../relational-databases/security/authentication-access/database-level-roles.md).|  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Datenbankkonfiguration &#40;Seite im Konfigurations-Manager für Master Data Services&#41;](../master-data-services/database-configuration-page-master-data-services-configuration-manager.md)   

[Master Data Services – Installation und Konfiguration](../master-data-services/master-data-services-installation-and-configuration.md)
  
  
