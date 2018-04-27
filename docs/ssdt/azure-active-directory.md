---
title: Azure Active Directory-Unterstützung in SQL Server Data Tools (SSDT) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/05/2018
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssdt
ms.reviewer: ''
ms.suite: sql
ms.technology:
- tools-ssdt
ms.tgt_pltfrm: ''
ms.topic: article
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Active
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 1e8f19c1dcc629ec6e97aa02cd23be1c101ad596
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="azure-active-directory-support-in-sql-server-data-tools-ssdt"></a>Azure Active Directory-Unterstützung in SQL Server Data Tools (SSDT)

[!INCLUDE[appliesto-xx-asdb-xxxx-xxx-md.md](../includes/appliesto-xx-asdb-xxxx-xxx-md.md)]

SQL Server Data Tools (SSDT) bietet mehrere [Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-whatis)-Authentifizierungsmethoden.

![SSDT-Verbindungsdialogfeld](media/azure-active-directory/interactive.png)

## <a name="active-directory-password-authentication"></a>Active Directory-Kennwortauthentifizierung

Die Active Directory-Kennwortauthentifizierung ist ein Mechanismus zum Herstellen einer Verbindung mit einer Azure SQL-Datenbank, wozu Identitäten in Azure Active Directory (Azure AD) verwendet werden.  Verwenden Sie diese Verbindungsmethode, wenn Sie bei Windows mit Anmeldeinformationen aus einer Domäne angemeldet sind, die nicht mit Azure verbunden ist, oder wenn die Azure AD-Authentifizierung mithilfe von Azure AD auf Basis der ursprünglichen oder der Clientdomäne verwendet wird. Weitere Informationen finden Sie unter [Herstellen einer Verbindung mit SQL-Datenbank unter Verwendung der Azure Active Directory-Authentifizierung](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication).  

## <a name="active-directory-integrated-authentication"></a>Integrierte Active Directory-Authentifizierung

Die integrierte Active Directory-Authentifizierung ist ein Mechanismus zum Herstellen einer Verbindung mit einer Azure SQL-Datenbank, wozu Identitäten in Azure Active Directory (Azure AD) verwendet werden. Verwenden Sie diese Verbindungsmethode, wenn Sie bei Windows mit Ihren Azure AD-Anmeldeinformationen aus einer Verbunddomäne angemeldet sind. Weitere Informationen finden Sie unter [Herstellen einer Verbindung mit SQL-Datenbank unter Verwendung der Azure Active Directory-Authentifizierung](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication).

## <a name="active-directory-interactive-authentication-preview"></a>Interaktive Active Directory-Authentifizierung (Vorschau)

SSDT bietet eine neue Authentifizierungsmethode für die Verbindung mit einer Azure SQL-Datenbank: die **interaktive Active Directory-Authentifizierung**.


> [!NOTE]
> Die interaktive Active Directory-Authentifizierung steht bei der Verbindung mit SSDT in [Visual Studio 2017 – Vorschau](https://www.visualstudio.com/vs/preview/) zur Verfügung und setzt die Installation von [.NET 4.7.2 – Vorschau (KB4038188)](https://go.microsoft.com/fwlink/?linkid=867317) auf dem Computer voraus, auf dem SSDT ausgeführt wird. Wenn die Vorschauversion von .NET 4.7.2 (KB4038188) nicht installiert ist, steht die interaktive Active Directory-Authentifizierung nicht zur Verfügung.


Die interaktive Active Directory-Authentifizierung unterstützt eine interaktive Authentifizierung zur Verwendung von Azure Active Directory (AD) Multi-Factor Authentication (MFA) für die Authentifizierung bei einer Azure SQL-Datenbank. Diese Methode bietet Unterstützung für native und verbundene Azure AD-Benutzer und -Gastbenutzer anderer Konten (einschließlich B2B-Benutzern sowie Microsoft- und Nicht-Microsoft-Konten wie z. B. @outlook.com, @hotmail.com, @live.com oder @gmail.com). Wenn diese Methode festgelegt wird, muss der **Benutzername** angegeben werden, und das Kennwortfeld wird deaktiviert. 

Wenn Sie sich mit *Interaktive Active Directory-Authentifizierung* authentifizieren, wird ein Authentifizierungsfenster geöffnet, in dem Benutzer ein Kennwort manuell eingeben müssen.

![Anmeldedialogfeld](media/azure-active-directory/sign-in.png)

Die MFA wird von Azure AD über dieses zusätzliche MFA-Popupfenster während des Authentifizierungsprozesses erzwungen.

> [!NOTE]
> Da die Option *Interaktive Active Directory-Authentifizierung* die manuelle (interaktive) Eingabe des Kennworts durch den Benutzer erfordert, wird sie für automatisierte Workflows nicht empfohlen.


## <a name="known-issues-and-limitations"></a>Einschränkungen und bekannte Probleme

- Die Option *Interaktive Active Directory-Authentifizierung* wird nur bei Verbindung mit einer Azure SQL-Datenbank unterstützt. Für SQL Server (lokal oder auf einem virtuellen Computer) oder Azure SQL Data Warehouse wird die Option nicht unterstützt.
- *Interaktive Active Directory-Authentifizierung* wird im Verbindungsdialog im *Server-Explorer* nicht unterstützt. Sie müssen eine Verbindung über SSDT mit *SQL Server-Objekt-Explorer* herstellen.
- Die Integration für einmaliges Anmelden mit dem aktuell angemeldeten Visual Studio-Konto wird für SSDT nicht unterstützt.
- Die SQLPackage.exe-Datei, die während der Installation von Visual Studio im Erweiterungsverzeichnis installiert wurde, ist nicht für die Verwendung von dort aus gedacht. Um „SQLpackage.exe“ mit AAD zu verwenden, wechseln Sie zu https://www.microsoft.com/en-us/download/details.aspx?id=55088. 
- Ein SSD-Datenvergleich wird für die AAD-Authentifizierung, einschließlich der neuen  Authentifizierungsmethode, nicht unterstützt.  





## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[Multi-Factor Authentication](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication)  
[Azure Active Directory-Authentifizierung mit SQL-Datenbank](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication-configure)  
[SQL Server Data Tools in Visual Studio](https://msdn.microsoft.com/library/hh272686(v=vs.103).aspx)  
[SSDT MSDN-Forum](https://social.msdn.microsoft.com/Forums/sqlserver/home?forum=ssdt)  
[SSDT-Team-Blog](http://blogs.msdn.com/b/ssdt/)  
[DACFx-API-Referenz](https://msdn.microsoft.com/library/dn645454.aspx)  
[Herunterladen von SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md)  
