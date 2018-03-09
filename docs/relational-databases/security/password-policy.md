---
title: Kennwortrichtlinie | Microsoft-Dokumentation
ms.custom: 
ms.date: 09/25/2015
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: security
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ALTER LOGIN statement
- passwords [SQL Server], policy enforcement
- logins [SQL Server], passwords
- CHECK_EXPIRATION option
- complex passwords [SQL Server]
- passwords [SQL Server], expiration
- manual bad password count resets
- MUST_CHANGE option
- expiration [SQL Server]
- expired password [SQL Server]
- symbols [SQL Server]
- NetValidatePasswordPolicy() API
- passwords [SQL Server]
- password policy [SQL Server]
- resetting bad password counts
- security [SQL Server], passwords
- CHECK_POLICY option
- passwords [SQL Server], symbols
- bad password counts
- passwords [SQL Server], complexity
- characters [SQL Server], password policies
ms.assetid: c0040c0a-a18f-45b9-9c40-0625685649b1
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: dc4da4aefa4cc0b92977af29df9d6992c48f74a4
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="password-policy"></a>Kennwortrichtlinie
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] kann Mechanismen der Windows-Kennwortrichtlinien verwenden. Die Kennwortrichtlinie gilt für eine Anmeldung, die die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Authentifizierung verwendet, und für einen eigenständige Datenbankbenutzer mit Kennwort.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] kann die gleichen Komplexitäts- und Ablaufrichtlinien anwenden, die in Windows für in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]verwendete Kennwörter verwendet werden. Diese Funktion basiert auf der `NetValidatePasswordPolicy` -API.  
  
 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] setzt die Kennwortkomplexität durch. Die Abschnitte zum Ablauf von Kennwörtern und zur Durchsetzung von Richtlinien gelten nicht für [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
## <a name="password-complexity"></a>Kennwortkomplexität  
 Richtlinien zur Kennwortkomplexität werden als Maßnahme gegen Brute Force-Angriffe entworfen. Dabei wird die Anzahl der möglichen Kennwörter erhöht. Wenn eine Richtlinie zur Kennwortkomplexität erzwungen wird, müssen neue Kennwörter die folgenden Richtlinien erfüllen:  
  
-   Das Kennwort enthält nicht den Kontonamen des Benutzers.  
  
-   Das Kennwort ist wenigstens acht Zeichen lang.  
  
-   Das Kennwort enthält Zeichen aus drei der folgenden vier Kategorien:  
  
    -   Lateinische Großbuchstaben (A - Z)  
  
    -   Lateinische Kleinbuchstaben (a - z)  
  
    -   10 Grundziffern (0 - 9)  
  
    -   Nicht alphanumerische Zeichen, wie z. B.: Ausrufezeichen (!), Dollarzeichen ($), Nummernzeichen (#) oder Prozentzeichen (%)  
  
 Kennwörter können bis zu 128 Zeichen lang sein. Sie sollten möglichst lange und komplexe Kennwörter verwenden.  
  
## <a name="password-expiration"></a>Ablauf des Kennworts  
 Richtlinien zum Ablauf von Kennwörtern werden verwendet, um die Lebensdauer von Kennwörtern zu verwalten. Wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die Richtlinie zum Ablauf von Kennwörtern durchsetzt, werden Benutzer daran erinnert, alte Kennwörter zu ändern. Konten mit abgelaufenen Kennwörtern werden deaktiviert.  
  
## <a name="policy-enforcement"></a>Richtliniendurchsetzung  
 Das Erzwingen der Kennwortrichtlinie kann für jede SQL Server-Anmeldung einzeln konfiguriert werden. Verwenden Sie [ALTER LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/alter-login-transact-sql.md) , um die Kennwortrichtlinienoptionen für eine SQL Server-Anmeldung zu konfigurieren. Die folgenden Regeln gelten für die Konfiguration zur Erzwingung der Kennwortrichtlinie:  
  
-   Wenn CHECK_POLICY in ON geändert wird, kommt es zu folgenden Verhaltensweisen:  
  
    -   Für CHECK_EXPIRATION wird ebenfalls ON festgelegt, es sei denn, der Wert OFF wurde ausdrücklich festgelegt.  
  
    -   Der Kennwortverlauf wird mit dem Wert des aktuellen Kennworthashes initialisiert.  
  
    -   **Kontosperrdauer**, **Kontensperrungsschwelle**und **Zurücksetzungsdauer des Kontosperrungszählers** sind ebenfalls aktiviert.  
  
-   Wenn CHECK_POLICY in OFF geändert wird, kommt es zu folgenden Verhaltensweisen:  
  
    -   CHECK_EXPIRATION wird ebenfalls auf OFF festgelegt.  
  
    -   Der Kennwortverlauf wird gelöscht.  
  
    -   Der Wert von `lockout_time` wird zurückgesetzt.  
  
 Einige Kombinationen von Richtlinienoptionen werden nicht unterstützt.  
  
-   Falls MUST_CHANGE angegeben wird, müssen CHECK_EXPIRATION und CHECK_POLICY auf ON festgelegt werden. Andernfalls erzeugt die Anweisung einen Fehler.  
  
-   Falls CHECK_POLICY auf OFF festgelegt ist, kann CHECK_EXPIRATION nicht auf ON festgelegt werden. Eine ALTER LOGIN-Anweisung mit dieser Kombination von Optionen erzeugt einen Fehler.  
  
 Durch Festlegen von CHECK_POLICY = ON wird die Erstellung von Kennwörtern mit folgenden Eigenschaften verhindert:  
  
-   NULL-Werte oder leere Kennwörter  
  
-   Kennwörter, die dem Computer- oder Anmeldenamen entsprechen  
  
-   Eines der folgenden Kennwörter: "kennwort", "admin", "administrator", "sa", "sysadmin"  
  
 Die Sicherheitsrichtlinie kann in Windows festgelegt oder von der Domäne abgerufen werden. Um die Kennwortrichtlinie auf dem Computer anzuzeigen, verwenden Sie das MMC-Snap-In „Lokale Sicherheitsrichtlinie“ (**secpol.msc**).  
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)  
  
 [ALTER LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/alter-login-transact-sql.md)  
  
 [CREATE USER &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)  
  
 [ALTER USER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-user-transact-sql.md)  
  
 [Erstellen eines Anmeldenamens](../../relational-databases/security/authentication-access/create-a-login.md)  
  
 [Erstellen eines Datenbankbenutzers](../../relational-databases/security/authentication-access/create-a-database-user.md)  
  
## <a name="related-content"></a>Verwandte Inhalte  
 [Sichere Kennwörter](../../relational-databases/security/strong-passwords.md)  
  
  
