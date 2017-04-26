---
title: Verbindung mit Server herstellen (Seite Anmeldung im Datenbankmodul) | Microsoft-Dokumentation
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
- sql13.swb.connecttosqlserver.login.f1
ms.assetid: e08cfbc3-bed5-4401-a13b-1c66d902fe32
caps.latest.revision: 6
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 1556c7facc4a671767fe2d6c061b4f6655ba521b
ms.lasthandoff: 04/11/2017

---
# <a name="connect-to-server-login-page-database-engine"></a>Verbindung mit Server herstellen (Seite Anmeldung im Datenbankmodul)
Auf dieser Registerkarte können Sie Optionen für Verbindungen mit Computern mit [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)] anzeigen oder angeben.  
  
> [!NOTE]  
> Zum Herstellen einer Verbindung mit der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Authentifizierung muss [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] im [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] - und Windows-Authentifizierungsmodus konfiguriert werden. Weitere Informationen zum Bestimmen und Ändern des Authentifizierungsmodus finden Sie unter [Vorgehensweise: Ändern des Serverauthentifizierungsmodus](http://msdn.microsoft.com/en-us/79babcf8-19fd-4495-b8eb-453dc575cac0).  
  
## <a name="options"></a>enthalten  
**Servertyp**  
Wenn Sie einen Server über den Objekt-Explorer registrieren, wählen Sie den Typ des Servers aus, mit dem eine Verbindung hergestellt wird: [!INCLUDE[ssDE](../../includes/ssde_md.md)], Analysis Services, Reporting Services oder Integration Services. Im verbleibenden Bereich des Dialogfelds werden nur die Optionen angezeigt, die auf den ausgewählten Servertyp zutreffen. Wenn Sie einen Server über „Registrierte Server“ registrieren, ist das Feld **Servertyp** schreibgeschützt, wobei der Feldeintrag mit dem in der Komponente „Registrierte Server“ angezeigten Servertyp übereinstimmt. Zum Registrieren eines anderen Servertyps wählen Sie auf der Symbolleiste "Registrierte Server" die Option [!INCLUDE[ssDE](../../includes/ssde_md.md)], "Analysis Services", "Reporting Services" oder "Integration Services" aus. Anschließend können Sie mit der Registrierung eines neuen Servers beginnen.  
  
Wenn Sie über die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] eine Verbindung mit einer Instanz des [!INCLUDE[ssSDSfull](../../includes/sssdsfull_md.md)]-Datenbankmoduls herstellen, müssen Sie die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Authentifizierung verwenden und im Dialogfeld **Verbindung mit Server herstellen** auf der Registerkarte **Verbindungseigenschaften** eine Datenbank angeben. Das Kontrollkästchen **Verbindung verschlüsseln** muss aktiviert sein.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] stellt standardmäßig eine Verbindung mit der **master**-Datenbank her. Wenn Sie eine Benutzerdatenbank angeben, wird im Objekt-Explorer nur diese Datenbank mit den zugehörigen Objekten angezeigt. Wenn Sie eine Verbindung mit der **master**-Datenbank herstellen, werden alle Datenbanken angezeigt. Weitere Informationen finden Sie in der [Übersicht zu Windows Azure SQL-Datenbanken](http://go.microsoft.com/fwlink/?LinkId=163948).  
  
**Servername**  
Wählen Sie die Serverinstanz aus, mit der eine Verbindung hergestellt werden soll. Standardmäßig wird die Serverinstanz angezeigt, mit der zuletzt eine Verbindung bestanden hat.  
  
**Authentifizierung**  
Beim Herstellen einer Verbindung mit einer Instanz von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]sind zwei Authentifizierungsmodi verfügbar:  
  
Wenn Sie über die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] eine Verbindung mit einer Instanz des [!INCLUDE[ssSDS](../../includes/sssds_md.md)]-Datenbankmoduls herstellen, müssen Sie die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Authentifizierung verwenden und im Dialogfeld **Verbindung mit Server herstellen** auf der Registerkarte **Verbindungseigenschaften** eine Datenbank angeben. Das Kontrollkästchen **Verbindung verschlüsseln** muss aktiviert sein.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] stellt standardmäßig eine Verbindung mit der **master**-Datenbank her. Wenn Sie eine Benutzerdatenbank angeben, wird im Objekt-Explorer nur diese Datenbank mit den zugehörigen Objekten angezeigt. Wenn Sie eine Verbindung mit der **master**-Datenbank herstellen, werden alle Datenbanken angezeigt. Weitere Informationen finden Sie in der [Übersicht zu Windows Azure SQL-Datenbanken](http://go.microsoft.com/fwlink/?LinkId=163948).  
  
**Windows-Authentifizierung**  
[!INCLUDE[msCoName](../../includes/msconame_md.md)] Der Windows Authentifizierungsmodus ermöglicht Benutzern die Verbindung über ein Windows-Benutzerkonto.  
  
**SQL Server-Authentifizierung**  
Wenn ein Benutzer eine Verbindung mit einem angegebenen Benutzernamen und einem Kennwort von einer nicht vertrauenswürdigen Verbindung herstellt, führt [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] die Authentifizierung durch, indem überprüft wird, ob ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Anmeldekonto eingerichtet wurde und ob das angegebene Kennwort mit dem zuvor aufgezeichneten übereinstimmt. Wenn kein Anmeldekonto in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] eingerichtet wurde, schlägt die Authentifizierung fehl, und der Benutzer erhält eine Fehlermeldung.  
  
> [!IMPORTANT]  
> Verwenden Sie nach Möglichkeit die Windows-Authentifizierung.  
  
**Universelle Active Directory-Authentifizierung**  
Universelle Active Directory-Authentifizierung ist ein interaktiver Workflow, in dem Azure Multi-Factor Authentication (MFA) unterstützt wird. Azure MFA bietet Schutz für den Zugriff auf Daten sowie Anwendungen und erfüllt gleichzeitig Benutzeranforderungen nach einem einfachen Anmeldevorgang. MFA stellt strenge Authentifizierung mit einigen einfachen Überprüfungsoptionen bereit (Telefonanruf, SMS, Smartcards mit PIN oder eine Benachrichtigung über mobile App), sodass Benutzer die von ihnen bevorzugte Methode auswählen können. Ist ein Benutzerkonto für MFA konfiguriert, ist für den interaktiven Authentifizierungswokflow eine zusätzliche Benutzerinteraktion über Popupdialogfelder, Verwenden von Smartcards usw. erforderlich. Ist ein Benutzerkonto für MFA konfiguriert, muss der Benutzer die Option für universelle Azure-Authentifizierung auswählen, um eine Verbindung herzustellen. Erfordert das Benutzerkonto keine MFA, kann der Benutzer weiterhin die beiden anderen Azure Active Directory-Authentifizierungsoptionen verwenden. Weitere Informationen hierzu finden Sie unter [SSMS-Unterstützung für Azure AD MFA mit SQL-Datenbank und SQL Data Warehouse](https://azure.microsoft.com/documentation/articles/sql-database-ssms-mfa-authentication/). Erfordert mindestens SSMS Version 16.3 (August 2016).
  
**Active Directory-Kennwortauthentifizierung**  
Azure Active Directory-Authentifizierung ist ein Mechanismus zum Herstellen einer Verbindung mit [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssSDSfull](../../includes/sssdsfull_md.md)] , wozu Identitäten in Azure Active Directory (Azure AD) verwendet werden.  Verwenden Sie diese Methode zum Herstellen von Verbindungen mit [!INCLUDE[ssSDS](../../includes/sssds_md.md)] , wenn Sie bei Windows mit Anmeldeinformationen aus einer Domäne angemeldet sind, die nicht mit Azure verbunden ist, oder wenn die Azure AD-Authentifizierung mithilfe von Azure AD auf Basis der ursprünglichen oder der Clientdomäne verwendet wird. Weitere Informationen finden Sie unter [Herstellen einer Verbindung mit SQL-Datenbank unter Verwendung der Azure Active Directory-Authentifizierung](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/).  
  
**Integrierte Active Directory-Authentifizierung**  
Azure Active Directory-Authentifizierung ist ein Mechanismus zum Herstellen einer Verbindung mit [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssSDSfull](../../includes/sssdsfull_md.md)] , wozu Identitäten in Azure Active Directory (Azure AD) verwendet werden. Verwenden Sie diese Methode zum Herstellen von Verbindungen mit [!INCLUDE[ssSDS](../../includes/sssds_md.md)] , wenn Sie bei Windows mit Ihren Azure Active Directory-Anmeldeinformationen aus einer Verbunddomäne angemeldet sind. Weitere Informationen finden Sie unter [Herstellen einer Verbindung mit SQL-Datenbank unter Verwendung der Azure Active Directory-Authentifizierung](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/).  
  
**Benutzername**  
Der Windows-Benutzername zum Herstellen der Verbindung. Diese Option ist nur verfügbar, wenn Sie **Active Directory-Kennwortauthentifizierung**ausgewählt haben, um eine Verbindung herzustellen. Der Benutzername ist schreibgeschützt, wenn Sie **Windows-Authentifizierung**ausgewählt haben.  
  
**Anmeldename**  
Geben Sie den Anmeldenamen für die Verbindung ein. Diese Option ist nur verfügbar, wenn Sie zum Verbinden die Authentifizierung von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ausgewählt haben.  
  
**Kennwort**  
Geben Sie das Kennwort für die Anmeldung ein. Sie können diese Option nur bearbeiten, wenn Sie zum Verbinden die Authentifizierung von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ausgewählt haben.  
  
**Kennwort speichern**  
Aktivieren Sie dieses Kontrollkästchen, damit [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] das eingegebene Kennwort speichert. Diese Option wird nur angezeigt, wenn Sie zum Verbinden die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Authentifizierung ausgewählt haben.  
  
**Connect**  
Klicken Sie hier, um eine Verbindung mit dem oben ausgewählten Server herzustellen.  
  
**enthalten**  
Klicken Sie hier, um die Anzeige des Dialogfelds zu ändern und die zusätzlichen Serververbindungsoptionen, z. B. Speichern des Kennworts, auszublenden.  
  

