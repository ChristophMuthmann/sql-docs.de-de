---
title: Active Directory-Authentifizierung für SQL Server on Linux | Microsoft Docs
description: Dieser Artikel enthält eine Übersicht über Active Directory-Authentifizierung für SQL Server on Linux.
author: rothja
ms.date: 02/23/2018
ms.author: jroth
manager: craigg
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
helpviewer_keywords:
- Linux, AAD authentication
ms.workload: On Demand
ms.openlocfilehash: bd4ba9f12b7567f618db2aef1adb87a8f1f080f5
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="active-directory-authentication-for-sql-server-on-linux"></a>Active Directory-Authentifizierung für SQL Server on Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Dieser Artikel enthält eine Übersicht über Active Directory (AD)-Authentifizierung für [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] unter Linux. AD-Authentifizierung ist auch bekannt als integrierte Authentifizierung in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. 

## <a name="ad-authentication-overview"></a>AD-Authentifizierung (Übersicht)

AD-Authentifizierung ermöglicht Clients unter Windows oder Linux zu authentifizieren, die einer Domäne [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] mit ihren Domänenanmeldeinformationen und das Kerberos-Protokoll.

AD-Authentifizierung hat die folgenden Vorteile gegenüber [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Authentifizierung:

- Benutzer authentifizieren, ohne Aufforderung zur Kennworteingabe über einmaliges Anmelden.   
- Sie können durch Erstellen von Anmeldungen für AD-Gruppen, verwalten, Zugriff und Berechtigungen in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] mithilfe von AD-Gruppenmitgliedschaften.  
- Jeder Benutzer hat eine einzelne Identität in Ihrem Unternehmen, daher es nicht zum Nachverfolgen der ist [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Anmeldungen, welche Personen entsprechen.   
- AD ermöglicht es Ihnen, eine zentrale Kennwortrichtlinie in Ihrem Unternehmen zu erzwingen.   

## <a name="configuration-steps"></a>Konfigurationsschritte

Um Active Directory-Authentifizierung verwenden zu können, müssen Sie einen AD-Domänencontroller (Windows) in Ihrem Netzwerk verfügen.

Die Details zum Konfigurieren von AD-Authentifizierung finden Sie im Lernprogramm [Lernprogramm: Verwenden Sie Active Directory-Authentifizierung mit SQL Server on Linux](sql-server-linux-active-directory-authentication.md). Die folgende Liste enthält eine Zusammenfassung mit einem Link zu jedem Abschnitt des Lernprogramms:

1. [Einen SQL Server-Host zu einer Active Directory-Domäne beitreten](sql-server-linux-active-directory-authentication.md#join).
1. [Erstellen ein AD-Benutzers für SQL Server, und legen Sie den ServicePrincipalName](sql-server-linux-active-directory-authentication.md#createuser).
1. [Konfigurieren Sie die SQL Server-Dienst-Keytab](sql-server-linux-active-directory-authentication.md#configurekeytab).
1. [Erstellen von AD-basierte SQL Server-Anmeldungen in Transact-SQL](sql-server-linux-active-directory-authentication.md#createsqllogins).
1. [Herstellen einer Verbindung mit SQL Server mithilfe von AD-Authentifizierung](sql-server-linux-active-directory-authentication.md#connect).

## <a name="known-issues"></a>Bekannte Probleme

- Zu diesem Zeitpunkt ist die einzige Authentifizierungsmethode für Datenbank-Spiegelungsendpunkt unterstützt Zertifikat. WINDOWS-Authentifizierungsmethode wird in einer zukünftigen Version aktiviert.
- AD-Tools von Drittanbietern wie Centrify Powerbroker, und das Vintela werden nicht unterstützt.

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen zum Implementieren von Active Directory-Authentifizierung für SQL Server unter Linux finden Sie unter [Lernprogramm: Verwenden Sie Active Directory-Authentifizierung mit SQL Server on Linux](sql-server-linux-active-directory-authentication.md).