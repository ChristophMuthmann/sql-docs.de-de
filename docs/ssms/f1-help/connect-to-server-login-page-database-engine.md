---
title: Verbindung mit Server herstellen (Seite Anmeldung im Datenbankmodul) | Microsoft-Dokumentation
ms.custom: 
ms.date: 08/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssms-f1
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.swb.connecttosqlserver.login.f1
ms.assetid: e08cfbc3-bed5-4401-a13b-1c66d902fe32
caps.latest.revision: "6"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 29528a0e9409ea44ec1d7b60a611db3c9d8712c3
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="connect-to-server-login-page-database-engine"></a>Verbindung mit Server herstellen (Seite Anmeldung im Datenbankmodul)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Auf dieser Registerkarte können Sie Optionen für Verbindungen mit Computern mit [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)] anzeigen oder angeben. In den meisten Fällen können Sie eine Verbindung herstellen, indem Sie im Feld **Servername** den Computernamen des Datenbankservers eingeben und dann auf **Verbinden**klicken. Wenn Sie eine Verbindung mit einer benannte Instanz herstellen, verwenden Sie den Computernamen, gefolgt von einem umgekehrten Schrägstrich und dem Namen der Instanz. Beispiel: `mycomputer\myinstance`. Geben Sie beim Herstellen der Verbindung mit [!INCLUDE[ssExpress](../../includes/ssexpress_md.md)]den Computernamen gefolgt von **\sqlexpress**an.  
  
Viele Faktoren können Auswirkungen auf die Fähigkeit zum Herstellen der Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]haben. Hilfe finden Sie in den folgenden Artikeln:  
- [Lektion 1: Herstellen einer Verbindung mit dem Datenbankmodul](../../relational-databases/lesson-1-connecting-to-the-database-engine.md)  
- [Beheben von Verbindungsfehlern mit dem SQL Server-Datenbankmodul](../../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md)  
- [Solving Connectivity errors to SQL Server (Lösen von Verbindungsproblemen in SQL Server)](https://support.microsoft.com/help/4009936/solving-connectivity-errors-to-sql-server)    
  
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
Die aktuelle Version von SSMS stellt fünf verschiedene Authentifizierungsmodi beim Verbinden mit einer Instanz von [!INCLUDE[ssDE](../../includes/ssde_md.md)] bereit. Wenn das Authentifizierungsdialogfeld nicht mit der folgenden Liste übereinstimmt, laden Sie die aktuellste Version von SSMS unter [Herunterladen von SQL Server Management Studio (SSMS)](../download-sql-server-management-studio-ssms.md) herunter.     
  
Wenn Sie über die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] eine Verbindung mit einer Instanz des [!INCLUDE[ssSDS](../../includes/sssds_md.md)]-Datenbankmoduls herstellen, müssen Sie die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Authentifizierung verwenden und im Dialogfeld **Verbindung mit Server herstellen** auf der Registerkarte **Verbindungseigenschaften** eine Datenbank angeben. Das Kontrollkästchen **Verbindung verschlüsseln** muss aktiviert sein.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] stellt standardmäßig eine Verbindung mit der **master**-Datenbank her. Wenn Sie eine Benutzerdatenbank beim Verbinden mit [!INCLUDE[ssSDS](../../includes/sssds_md.md)]angeben, wird im Objekt-Explorer nur diese Datenbank mit den zugehörigen Objekten angezeigt. Wenn Sie eine Verbindung mit der **master**-Datenbank herstellen, werden alle Datenbanken angezeigt. Weitere Informationen finden Sie in der [Übersicht zu Windows Azure SQL-Datenbanken](http://go.microsoft.com/fwlink/?LinkId=163948).  
  
  > **Windows-Authentifizierung**  
[!INCLUDE[msCoName](../../includes/msconame_md.md)] Der Windows Authentifizierungsmodus ermöglicht Benutzern die Verbindung über ein Windows-Benutzerkonto.  
  
  > **SQL Server-Authentifizierung**  
Wenn ein Benutzer eine Verbindung mit einem angegebenen Benutzernamen und einem Kennwort von einer nicht vertrauenswürdigen Verbindung herstellt, führt [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] die Authentifizierung durch, indem überprüft wird, ob ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Anmeldekonto eingerichtet wurde und ob das angegebene Kennwort mit dem zuvor aufgezeichneten übereinstimmt. Wenn kein Anmeldekonto in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] eingerichtet wurde, schlägt die Authentifizierung fehl, und der Benutzer erhält eine Fehlermeldung. Verwenden Sie nach Möglichkeit die Windows-Authentifizierung.  
  
  > **Active Directory: Universell mit MFA-Unterstützung**  
Universelle Active Directory-Authentifizierung mit MFA ist ein interaktiver Workflow, in dem Azure Multi-Factor Authentication (MFA) unterstützt wird. Azure MFA bietet Schutz für den Zugriff auf Daten sowie Anwendungen und erfüllt gleichzeitig Benutzeranforderungen nach einem einfachen Anmeldevorgang. MFA stellt strenge Authentifizierung mit einigen einfachen Überprüfungsoptionen bereit (Telefonanruf, SMS, Smartcards mit PIN oder eine Benachrichtigung über mobile App), sodass Benutzer die von ihnen bevorzugte Methode auswählen können. Ist ein Benutzerkonto für MFA konfiguriert, ist für den interaktiven Authentifizierungswokflow eine zusätzliche Benutzerinteraktion über Popupdialogfelder, Verwenden von Smartcards usw. erforderlich. Ist ein Benutzerkonto für MFA konfiguriert, muss der Benutzer die Option für universelle Azure-Authentifizierung auswählen, um eine Verbindung herzustellen. Erfordert das Benutzerkonto keine MFA, kann der Benutzer weiterhin die beiden anderen Azure Active Directory-Authentifizierungsoptionen verwenden. Weitere Informationen hierzu finden Sie unter [SSMS-Unterstützung für Azure AD MFA mit SQL-Datenbank und SQL Data Warehouse](https://azure.microsoft.com/documentation/articles/sql-database-ssms-mfa-authentication/). Falls nötig können Sie die Domäne ändern, die die Anmeldung authentifiziert, indem Sie auf **Optionen** und dann auf die Registerkarte **Verbindungseigenschaften** klicken und anschließend das Feld **AD-Domänenname oder Mandanten-ID** ausfüllen.  

  > **Active Directory: Kennwort**  
Azure Active Directory-Authentifizierung ist ein Mechanismus zum Herstellen einer Verbindung mit [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssSDSfull](../../includes/sssdsfull_md.md)] , wozu Identitäten in Azure Active Directory (Azure AD) verwendet werden.  Verwenden Sie diese Methode zum Herstellen von Verbindungen mit [!INCLUDE[ssSDS](../../includes/sssds_md.md)], wenn Sie bei Windows mit Anmeldeinformationen aus einer Domäne angemeldet sind, die nicht mit Azure verbunden ist, oder wenn die Azure AD-Authentifizierung mithilfe von Azure AD auf Basis der ursprünglichen oder der Clientdomäne verwendet wird. Weitere Informationen finden Sie unter [Herstellen einer Verbindung mit SQL-Datenbank unter Verwendung der Azure Active Directory-Authentifizierung](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/).  
  
  > **Active Directory – Integriert**  
Azure Active Directory-Authentifizierung ist ein Mechanismus zum Herstellen einer Verbindung mit [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssSDSfull](../../includes/sssdsfull_md.md)] , wozu Identitäten in Azure Active Directory (Azure AD) verwendet werden. Verwenden Sie die Methode zum Verbinden mit [!INCLUDE[ssSDS](../../includes/sssds_md.md)], wenn Sie bei Windows mit Ihren Azure AD-Anmeldeinformationen aus einer Verbunddomäne angemeldet sind. Weitere Informationen finden Sie unter [Herstellen einer Verbindung mit SQL-Datenbank unter Verwendung der Azure Active Directory-Authentifizierung](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/).  
  
**Benutzername**  
Der Windows-Benutzername zum Herstellen der Verbindung. Diese Option ist nur verfügbar, wenn Sie **Active Directory-Kennwortauthentifizierung**ausgewählt haben, um eine Verbindung herzustellen. Sie ist schreibgeschützt, wenn Sie die Authentifizierungen **Windows-Authentifizierung** oder **Active Directory – Integriert** auswählen.  
  
**Anmeldename**  
Geben Sie den Anmeldenamen für die Verbindung ein. Diese Option ist nur verfügbar, wenn Sie die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]-Authentifizierung oder die Active Directory-Kennwortauthentifizierung ausgewählt haben, um eine Verbindung herzustellen.  
  
**Kennwort**  
Geben Sie das Kennwort für die Anmeldung ein. Diese Option ist nur bearbeitbar, wenn Sie die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]-Authentifizierung oder die Active Directory-Kennwortauthentifizierung ausgewählt haben, um eine Verbindung herzustellen.  
  
**Kennwort speichern**  
Aktivieren Sie dieses Kontrollkästchen, damit [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] das eingegebene Kennwort speichert. Diese Option wird nur angezeigt, wenn Sie zum Verbinden die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Authentifizierung ausgewählt haben.  
  
**Verbinden**  
Klicken Sie darauf, um eine Verbindung mit dem Server herzustellen.  
  
**Optionen**  
Klicken Sie darauf, um die **Verbindungseigenschaften** und die Registerkarte **Zusätzliche Verbindungsparameter** anzuzeigen.  
   
  
