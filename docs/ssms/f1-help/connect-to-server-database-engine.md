---
title: Verbindung mit Server herstellen (Datenbankmodul) (Datenbankmodul) | Microsoft-Dokumentation
ms.custom:
- SQL2016_New_Updated
ms.date: 01/30/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.connectoserverunknownservertype.f1
- sql13.swb.connection.login.sqlce.f1
- sql13.swb.connecttoce.f1
- SQL13.SWB.CONNECTION.LOGIN.SQLSERVER.F1
- sql13.swb.connection.login.sqlserver.f1
- sql13.swb.manageSS2k.f1
ms.assetid: ee9017b4-8a19-4360-9003-9e6484082d41
caps.latest.revision: 6
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: d421bcb09ec7ebde28b5d1cce6eca2263cfb1c48
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="connect-to-server-database-engine"></a>Verbindung mit Server herstellen (Datenbankmodul)
Verwenden Sie dieses Dialogfeld, um Optionen für Verbindungen mit Computern mit [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)] anzuzeigen oder anzugeben. In den meisten Fällen können Sie eine Verbindung herstellen, indem Sie im Feld **Servername** den Computernamen des Datenbankservers eingeben und dann auf **Verbinden**klicken. Geben Sie beim Herstellen der Verbindung mit [!INCLUDE[ssExpress](../../includes/ssexpress_md.md)]den Computernamen gefolgt von **\sqlexpress**an.  
  
Viele Faktoren können Auswirkungen auf die Fähigkeit zum Herstellen der Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]haben.  
  
## <a name="options"></a>enthalten  
**Servertyp**  
Wenn Sie einen Server über den Objekt-Explorer registrieren, wählen Sie den Typ des Servers aus, mit dem die Verbindung hergestellt werden soll: [!INCLUDE[ssDE](../../includes/ssde_md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion_md.md)], [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion_md.md)]oder [!INCLUDE[ssISnoversion](../../includes/ssisnoversion_md.md)]. Im verbleibenden Bereich des Dialogfelds werden nur die Optionen angezeigt, die auf den ausgewählten Servertyp zutreffen. Wenn Sie einen Server über „Registrierte Server“ registrieren, ist das Feld **Servertyp** schreibgeschützt, wobei der Feldeintrag mit dem in der Komponente „Registrierte Server“ angezeigten Servertyp übereinstimmt. Zum Registrieren eines anderen Servertyps wählen Sie auf der Symbolleiste Registrierte Server [!INCLUDE[ssDE](../../includes/ssde_md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion_md.md)], [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion_md.md)], [!INCLUDE[ssEW](../../includes/ssew_md.md)]oder [!INCLUDE[ssISnoversion](../../includes/ssisnoversion_md.md)] aus, bevor Sie mit der Registrierung eines neuen Servers beginnen.  
  
**Servername**  
Wählen Sie die Serverinstanz aus, mit der eine Verbindung hergestellt werden soll. Standardmäßig wird die Serverinstanz angezeigt, mit der zuletzt eine Verbindung bestanden hat.  
  
> [!NOTE]  
> Um eine Verbindung mit einer aktiven Instanz von [!INCLUDE[ssExpress](../../includes/ssexpress_md.md)] herzustellen, verwenden Sie das Named Pipes-Protokoll unter Angabe des Pipenamens, z. B. „np:\\\\.\pipe\3C3DF6B1-2262-47\tsql\query“. Weitere Informationen finden Sie in der Dokumentation von [!INCLUDE[ssExpress](../../includes/ssexpress_md.md)] .  
  
**Authentifizierung**  
Beim Herstellen einer Verbindung mit einer Instanz von [!INCLUDE[ssDE](../../includes/ssde_md.md)]sind drei Authentifizierungsmodi verfügbar.  
  
**Windows-Authentifizierung**  
[!INCLUDE[msCoName](../../includes/msconame_md.md)] Der Windows Authentifizierungsmodus ermöglicht Benutzern die Verbindung über ein Windows-Benutzerkonto.  
  
**SQL Server-Authentifizierung**  
Wenn ein Benutzer eine Verbindung mit einem angegebenen Benutzernamen und einem Kennwort von einer nicht vertrauenswürdigen Verbindung herstellt, führt [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] die Authentifizierung durch, indem überprüft wird, ob ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Anmeldekonto eingerichtet wurde und ob das angegebene Kennwort mit dem zuvor aufgezeichneten übereinstimmt. Wenn kein Anmeldekonto in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] eingerichtet wurde, schlägt die Authentifizierung fehl, und der Benutzer erhält eine Fehlermeldung.  
  
> [!IMPORTANT]  
> Verwenden Sie nach Möglichkeit die Windows-Authentifizierung oder die Active Directory-Kennwort-Authentifizierung.  
  
**Universelle Active Directory-Authentifizierung**  
Universelle Active Directory-Authentifizierung ist ein interaktiver Workflow, in dem Azure Multi-Factor Authentication (MFA) unterstützt wird. Azure MFA bietet Schutz für den Zugriff auf Daten sowie Anwendungen und erfüllt gleichzeitig Benutzeranforderungen nach einem einfachen Anmeldevorgang. MFA stellt strenge Authentifizierung mit einigen einfachen Überprüfungsoptionen bereit (Telefonanruf, SMS, Smartcards mit PIN oder eine Benachrichtigung über mobile App), sodass Benutzer die von ihnen bevorzugte Methode auswählen können. Ist ein Benutzerkonto für MFA konfiguriert, ist für den interaktiven Authentifizierungswokflow eine zusätzliche Benutzerinteraktion über Popupdialogfelder, Verwenden von Smartcards usw. erforderlich. Ist ein Benutzerkonto für MFA konfiguriert, muss der Benutzer die Option für universelle Azure-Authentifizierung auswählen, um eine Verbindung herzustellen. Erfordert das Benutzerkonto keine MFA, kann der Benutzer weiterhin die beiden anderen Azure Active Directory-Authentifizierungsoptionen verwenden. Weitere Informationen hierzu finden Sie unter [SSMS-Unterstützung für Azure AD MFA mit SQL-Datenbank und SQL Data Warehouse](https://azure.microsoft.com/documentation/articles/sql-database-ssms-mfa-authentication/). Erfordert mindestens SSMS Version 16.3 (August 2016).

**Active Directory-Kennwortauthentifizierung**  
Azure Active Directory-Authentifizierung ist ein Mechanismus zum Herstellen einer Verbindung mit [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssSDSfull](../../includes/sssdsfull_md.md)] , wozu Identitäten in Azure Active Directory (Azure AD) verwendet werden.  Verwenden Sie diese Methode zum Herstellen von Verbindungen mit [!INCLUDE[ssSDS](../../includes/sssds_md.md)] , wenn Sie bei Windows mit Anmeldeinformationen aus einer Domäne angemeldet sind, die nicht mit Azure verbunden ist, oder wenn die Azure AD-Authentifizierung mithilfe von Azure AD auf Basis der ursprünglichen oder der Clientdomäne verwendet wird. Weitere Informationen finden Sie unter [Herstellen einer Verbindung mit SQL-Datenbank unter Verwendung der Azure Active Directory-Authentifizierung](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/).  
  
**Integrierte Active Directory-Authentifizierung**  
Azure Active Directory-Authentifizierung ist ein Mechanismus zum Herstellen einer Verbindung mit [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssSDSfull](../../includes/sssdsfull_md.md)] , wozu Identitäten in Azure Active Directory (Azure AD) verwendet werden. Verwenden Sie diese Methode zum Herstellen von Verbindungen mit [!INCLUDE[ssSDS](../../includes/sssds_md.md)] , wenn Sie bei Windows mit Ihren Azure Active Directory-Anmeldeinformationen aus einer Verbunddomäne angemeldet sind. Weitere Informationen finden Sie unter [Herstellen einer Verbindung mit SQL-Datenbank unter Verwendung der Azure Active Directory-Authentifizierung](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/).  
  
**Benutzername**  
Der Windows-Benutzername zum Herstellen der Verbindung. Diese Option ist nur verfügbar, wenn Sie **Active Directory-Kennwortauthentifizierung**ausgewählt haben, um eine Verbindung herzustellen. Der Benutzername ist schreibgeschützt, wenn Sie **Windows-Authentifizierung**ausgewählt haben.  
  
**Anmeldename**  
Geben Sie den Anmeldenamen für die Verbindung ein. Diese Option ist nur verfügbar, wenn Sie „ [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Authentifizierung“ oder „Active Directory-Kennwortauthentifizierung“ ausgewählt haben, um eine Verbindung herzustellen.  
  
**Kennwort**  
Geben Sie das Kennwort für die Anmeldung ein. Diese Option ist nur bearbeitbar, wenn Sie „ [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Authentifizierung“ oder „Active Directory-Kennwortauthentifizierung“ ausgewählt haben, um eine Verbindung herzustellen.  
  
**Verbinden**  
Klicken Sie hier, um eine Verbindung mit dem oben ausgewählten Server herzustellen.  
  
**enthalten**  
Klicken Sie auf diese Schaltfläche, um zusätzliche Optionen für die Serververbindung anzuzeigen, z. B. zum Registrieren eines Servers oder zum Speichern des Kennworts.  
  

