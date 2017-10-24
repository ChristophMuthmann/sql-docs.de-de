---
title: "So wird Ihre Datenbank portabel – mit eigenständigen Datenbankbenutzern | Microsoft-Dokumentation"
ms.custom: 
ms.date: 08/17/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- contained database, users
- user [SQL Server], about contained database users
ms.assetid: e57519bb-e7f4-459b-ba2f-fd42865ca91d
caps.latest.revision: 33
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 0f6310afe6f8909a560fac0b7762c7aa94e3a1f3
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="contained-database-users---making-your-database-portable"></a>So wird Ihre Datenbank portabel – mit eigenständigen Datenbankbenutzern
[!INCLUDE[tsql-appliesto-ss2012-all_md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  Verwenden Sie eigenständige Datenbankbenutzer, um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]- und [!INCLUDE[ssSDS](../../includes/sssds-md.md)]-Verbindungen auf Datenbankebene zu authentifizieren. Eine eigenständige Datenbank ist eine Datenbank, die von anderen Datenbanken und der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/[!INCLUDE[ssSDS](../../includes/sssds-md.md)] (sowie der Masterdatenbank), der die Datenbank hostet, isoliert ist. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt eigenständige Datenbankbenutzer sowohl für die Windows- als auch für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Authentifizierung. Kombinieren Sie bei Verwendung von [!INCLUDE[ssSDS](../../includes/sssds-md.md)] eigenständige Datenbankbenutzer mit Firewallregeln auf Datenbankebene. In diesem Thema werden die Unterschiede und Vorteile der Verwendung des eigenständigen Datenbankmodells im Vergleich zum herkömmlichen Modell mit einer benutzerspezifischen Anmelde-ID sowie zu Firewallregeln für Windows bzw. auf Serverebene vorgestellt. Bestimmte Szenarien, Fragen zur Verwaltungsfähigkeit oder die bei den Anwendungen implementierte Geschäftslogik können dennoch den Einsatz des herkömmlichen Anmeldemodells mit Anmelde-IDs und Benutzern und von Firewallregeln auf Serverebene erfordern.  
  
> [!NOTE]  
>  Wenn [!INCLUDE[msCoName](../../includes/msconame-md.md)] den [!INCLUDE[ssSDS](../../includes/sssds-md.md)]-Dienst hin zu höheren garantierten SLAs weiterentwickelt, müssen Sie möglicherweise auf das Modell für eigenständige Datenbankbenutzer und datenbankbezogene Firewallregeln umstellen, um von den höheren garantierten SLAs sowie höheren Maximalwerten für Anmeldungen bei einer gegebenen Datenbank profitieren zu können. [!INCLUDE[msCoName](../../includes/msconame-md.md)] empfiehlt, solche Änderungen bereits jetzt zu berücksichtigen.  
  
## <a name="traditional-login-and-user-model"></a>Herkömmliches Modell mit Anmelde-IDs und Benutzern  
 Beim herkömmlichen Verbindungsmodell stellen Windows-Benutzer oder Mitglieder von Windows-Gruppen eine Verbindung mit dem [!INCLUDE[ssDE](../../includes/ssde-md.md)] her, indem sie Benutzer- oder Gruppenanmeldeinformationen eingeben, die von Windows authentifiziert werden. Alternativ können Sie einen Namen und ein Kennwort angeben und die Verbindung über die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Authentifizierung herstellen. In beiden Fällen muss in der Masterdatenbank eine Anmelde-ID vorhanden sein, die mit den bei der Verbindungsherstellung verwendeten Anmeldeinformationen übereinstimmt. Nachdem das [!INCLUDE[ssDE](../../includes/ssde-md.md)] die Anmeldeinformationen für die Windows-Authentifizierung bestätigt oder [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldeinformationen authentifiziert hat, wird normalerweise versucht, eine Verbindung mit einer Benutzerdatenbank herzustellen. Zum Herstellen einer solchen Verbindung mit einer Benutzerdatenbank muss die Anmelde-ID einem Benutzer in der Benutzerdatenbank zugeordnet werden können. Die Verbindungszeichenfolge kann auch angeben, dass eine Verbindung mit einer bestimmten Datenbank hergestellt werden soll, was in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] optional, in [!INCLUDE[ssSDS](../../includes/sssds-md.md)] jedoch erforderlich ist.  
  
 Das Grundprinzip besagt, dass sowohl die Anmelde-ID (in der Masterdatenbank) als auch der Benutzer (in der Benutzerdatenbank) vorhanden sein und beide einander zugeordnet sein müssen. Dies bedeutet, dass die Verbindung mit der Benutzerdatenbank von der Anmelde-ID in der Masterdatenbank abhängig ist. Hierdurch wird die Möglichkeiten zum Verschieben der Datenbank auf einen anderen hostenden [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]- oder [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]-Server eingeschränkt. Wenn aus irgendeinem Grund eine Verbindung mit der Masterdatenbank nicht vorhanden ist (beispielsweise wenn etwa ein Failover ausgeführt wird), wird die Gesamtverbindungsdauer erhöht. Auch ein Timeout ist möglich. Hierdurch kann die Skalierbarkeit der Verbindung beeinträchtigt werden.  
  
## <a name="contained-database-user-model"></a>Modell mit eigenständigen Datenbankbenutzern  
 Beim Modell mit eigenständigen Datenbankbenutzern gibt es keine Anmelde-ID in der Masterdatenbank. Stattdessen findet der Authentifizierungsprozess in der Benutzerdatenbank statt: Es gibt für den Datenbankbenutzer aus der Benutzerdatenbank gar keine zugeordnete Anmelde-ID in der Masterdatenbank. Das Modell mit eigenständigen Datenbankbenutzern unterstützt sowohl die Windows-Authentifizierung als auch die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Authentifizierung und kann in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und in [!INCLUDE[ssSDS](../../includes/sssds-md.md)] verwendet werden. Um als eigenständiger Datenbankbenutzer eine Verbindung herstellen zu können, muss die Verbindungszeichenfolge immer einen Parameter für die Benutzerdatenbank enthalten, damit das [!INCLUDE[ssDE](../../includes/ssde-md.md)] weiß, welche Datenbank für die Verwaltung des Authentifizierungsprozesses verantwortlich ist. Die Aktivität des eigenständigen Datenbankbenutzers ist auf den Authentifizierungsserver beschränkt. Beim Herstellen einer Verbindung als eigenständiger Datenbankbenutzer muss das Datenbankbenutzerkonto also in jeder Datenbank, die der Benutzer benötigt, separat erstellt werden. Um die Datenbanken zu wechseln, müssen [!INCLUDE[ssSDS](../../includes/sssds-md.md)]-Benutzer eine neue Verbindung erstellen. Eigenständige Datenbankbenutzer in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] können Datenbanken wechseln, wenn ein identischer Benutzer in der anderen Datenbank vorhanden ist.  
  
**Azure:** [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] und [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)] unterstützen Azure Active Directory-Identitäten für eigenständige Datenbankbenutzer. [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] unterstützt eigenständige Datenbankbenutzer bei Verwendung der [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]-Authentifizierung, [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)] tut dies hingegen nicht. Weitere Informationen finden Sie unter [Herstellen einer Verbindung mit SQL-Datenbank unter Verwendung der Azure Active Directory-Authentifizierung](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/). Wird die Azure Active Directory-Authentifizierung verwendet, dann können Verbindungen von SSMS über die universelle Active Directory-Authentifizierung hergestellt werden.  Administratoren können die universelle Authentifizierung so konfigurieren, dass die mehrstufige Authentifizierung verwendet werden muss. Hierbei wird die Identität mit einem Telefonanruf, einer SMS, einer Smartcard mit PIN oder einer Benachrichtigung über eine mobile App überprüft. Weitere Informationen hierzu finden Sie unter [SSMS-Unterstützung für Azure AD MFA mit SQL-Datenbank und SQL Data Warehouse](https://azure.microsoft.com/documentation/articles/sql-database-ssms-mfa-authentication/).  
  
 Für [!INCLUDE[ssSDS](../../includes/sssds-md.md)] und [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)] sind, weil der Datenbankname in der Verbindungszeichenfolge immer erforderlich ist, beim Wechseln vom traditionellen Modell auf das Modell mit eigenständigen Datenbankbenutzern keine Änderungen an der Verbindungszeichenfolge erforderlich. Für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Verbindungen muss der Name der Datenbank zur Verbindungszeichenfolge hinzugefügt werden, falls nicht bereits geschehen.  
  
> [!IMPORTANT]  
>  Wenn Sie das traditionelle Modell verwenden, können die Rollen und Berechtigungen auf Serverebene den Zugriff auf alle Datenbanken einschränken. Verwenden Sie dagegen das Modell mit eigenständigen Datenbankbenutzern, dann können Datenbankbesitzer und Datenbankbenutzer mit der ALTER ANY USER-Berechtigung Zugriff auf die Datenbank erteilen. Hierdurch wird die Zugriffssteuerung mithilfe hochprivilegierter Serveranmelde-IDs eingeschränkt. Gleichzeitig wird die Zugriffssteuerung jedoch um hochprivilegierte Datenbankbenutzer erweitert.  
  
## <a name="firewalls"></a>Firewalls  
  
### [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 Windows-Firewallregeln gelten für alle Verbindungen und funktionieren bei Anmelde-IDs (Verbindungen nach dem traditionellen Modell) und eigenständigen Datenbankbenutzern auf gleiche Weise. Weitere Informationen zur Windows-Firewall finden Sie unter [Konfigurieren einer Windows-Firewall für Datenbankmodulzugriff](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md).  
  
### <a name="includesssdsincludessssds-mdmd-firewalls"></a>[!INCLUDE[ssSDS](../../includes/sssds-md.md)] Firewalls  
 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] ermöglicht separate Firewallregeln für Verbindungen auf Serverebene (Anmelde-IDs) und für Verbindungen auf Datenbankebene (eigenständige Datenbankbenutzer). Bei der Verbindung mit einer Benutzerdatenbank werden zuerst die Datenbank-Firewallregeln überprüft. Wenn es keine Regel gibt, die den Zugriff auf die Datenbank erlaubt, werden die Firewallregeln auf Serverebene geprüft. Zu diesem Zweck ist ein Zugriff auf die logische Server-Masterdatenbank erforderlich. Firewallregeln auf Datenbankebene können in Kombination mit eigenständigen Datenbankbenutzern die Notwendigkeit beseitigen, während der Verbindung auf die Masterdatenbank des Servers zuzugreifen, was die Skalierbarkeit der Verbindung verbessert.  
  
 Weitere Informationen zu [!INCLUDE[ssSDS](../../includes/sssds-md.md)]-Firewall-Regeln finden Sie in den folgenden Themen:  
  
-   [Azure SQL-Datenbank-Firewall](http://msdn.microsoft.com/library/azure/ee621782.aspx)  
  
-   [Gewusst wie: Konfigurieren von Firewalleinstellungen (Azure SQL-Datenbank)](http://msdn.microsoft.com/library/azure/jj553530.aspx)  
  
-   [sp_set_firewall_rule &#40;Azure SQL-Datenbank&#41;](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md)  
  
-   [sp_set_database_firewall_rule &#40;Azure SQL-Datenbank&#41;](../../relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database.md)  
  
## <a name="syntax-differences"></a>Syntaxunterschiede  
  
|Herkömmliches Modell|Modell mit eigenständigen Datenbankbenutzern|  
|-----------------------|-----------------------------------|  
|Bei Verbindung mit der Masterdatenbank:<br /><br /> `CREATE LOGIN login_name  WITH PASSWORD = 'strong_password';`<br /><br /> Bei anschließender Verbindung mit einer Benutzerdatenbank:<br /><br /> `CREATE USER 'user_name' FOR LOGIN 'login_name';`|Bei Verbindung mit einer Benutzerdatenbank:<br /><br /> `CREATE USER user_name  WITH PASSWORD = 'strong_password';`|  
  
|Herkömmliches Modell|Modell mit eigenständigen Datenbankbenutzern|  
|-----------------------|-----------------------------------|  
|So ändern Sie das Kennwort im Kontext der Masterdatenbank:<br /><br /> `ALTER LOGIN login_name  WITH PASSWORD = 'strong_password';`|So ändern Sie das Kennwort im Kontext der Benutzerdatenbank:<br /><br /> `ALTER USER user_name  WITH PASSWORD = 'strong_password';`|  
  
## <a name="remarks"></a>Hinweise  
  
-   In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] muss die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz für die jeweiligen eigenständigen Datenbankbenutzer aktiviert werden. Weitere Informationen finden Sie unter [Contained Database Authentication (Serverkonfigurationsoption)](../../database-engine/configure-windows/contained-database-authentication-server-configuration-option.md).  
  
-   Eigenständige Datenbankbenutzer und Anmelde-IDs mit nicht überlappenden Namen können in Ihren Anwendungen koexistieren.  
  
-   Wenn es in der Masterdatenbank eine Anmelde-ID mit dem Namen **name1** gibt und Sie einen eigenständigen Datenbankbenutzer namens **name1** erstellen, hat, wenn ein Datenbankname in der Verbindungszeichenfolge angegeben ist, beim Herstellen der Datenbankverbindung der Kontext des Datenbankbenutzers Vorrang vor dem der Anmelde-ID. Eigenständige Datenbankbenutzer haben also Vorrang vor Anmelde-IDs mit demselben Namen.  
  
-   Der Name des eigenständigen Datenbankbenutzers darf in [!INCLUDE[ssSDS](../../includes/sssds-md.md)] nicht mit dem Namen des Serveradministratorkontos identisch sein.  
  
-   Das [!INCLUDE[ssSDS](../../includes/sssds-md.md)]-Serveradministratorkonto kann keinesfalls ein eigenständiger Datenbankbenutzer sein. Der Serveradministrator verfügt über ausreichende Berechtigungen zum Erstellen und Verwalten von eigenständigen Datenbankbenutzern. Der Serveradministrator kann eigenständigen Datenbankbenutzern Berechtigungen für die Benutzerdatenbanken erteilen.  
  
-   Da eigenständige Datenbankbenutzer Prinzipale auf Datenbankebene sind, müssen Sie sie in jeder Datenbank erstellen, die sie verwenden können sollen. Die Identität ist auf die Datenbank beschränkt und in jeder Hinsicht von einem Benutzer mit demselben Namen und demselben Kennwort in einer anderen Datenbank auf demselben Server unabhängig.  
  
-   Verwenden Sie Kennwörter der Stärke, wie Sie sie normalerweise auch für Anmelde-IDs verwenden.  
  
## <a name="see-also"></a>Siehe auch  
 [Eigenständige Datenbanken](../../relational-databases/databases/contained-databases.md)   
 [Bewährte Methoden für die Sicherheit eigenständiger Datenbanken](../../relational-databases/databases/security-best-practices-with-contained-databases.md)   
 [CREATE USER &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)   
 [Herstellen einer Verbindung mit SQL-Datenbank unter Verwendung der Azure Active Directory-Authentifizierung](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/)  
  
  

