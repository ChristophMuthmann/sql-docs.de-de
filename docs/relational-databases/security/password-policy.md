---
title: "Kennwortrichtlinie | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "09/25/2015"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "ALTER LOGIN-Anweisung"
  - "Kennwörter [SQL Server], Durchsetzen von Richtlinien"
  - "Anmeldungen [SQL Server], Kennwörter"
  - "CHECK_EXPIRATION-Option"
  - "Komplexe Kennwörter [SQL Server]"
  - "Kennwörter [SQL Server], Ablauf"
  - "Manuelles Zurücksetzen von Zählungen ungültiger Kennwörter"
  - "MUST_CHANGE-Option"
  - "Ablaufzeitpunkt [SQL Server]"
  - "Abgelaufenes Kennwort [SQL Server]"
  - "Symbole [SQL Server]"
  - "NetValidatePasswordPolicy()-API"
  - "Kennwörter [SQL Server]"
  - "Kennwortrichtlinie [SQL Server]"
  - "Zurücksetzen von Zählungen ungültiger Kennwörter"
  - "Sicherheit [SQL Server], Kennwörter"
  - "CHECK_POLICY-Option"
  - "Kennwörter [SQL Server], Symbole"
  - "Zählungen ungültiger Kennwörter"
  - "Kennwörter [SQL Server], Komplexität"
  - "Zeichen [SQL Server], Kennwortrichtlinien"
ms.assetid: c0040c0a-a18f-45b9-9c40-0625685649b1
caps.latest.revision: 41
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 41
---
# Kennwortrichtlinie
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] kann Mechanismen der Windows-Kennwortrichtlinien verwenden. Die Kennwortrichtlinie gilt für eine Anmeldung, die die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Authentifizierung verwendet, und für einen eigenständige Datenbankbenutzer mit Kennwort.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] kann die gleichen Komplexitäts- und Ablaufrichtlinien anwenden, die in Windows für in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendete Kennwörter verwendet werden. Diese Funktion basiert auf der `NetValidatePasswordPolicy`-API.  
  
 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] setzt die Kennwortkomplexität durch. Die Abschnitte zum Ablauf von Kennwörtern und zur Durchsetzung von Richtlinien gelten nicht für [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
## Kennwortkomplexität  
 Richtlinien zur Kennwortkomplexität werden als Maßnahme gegen Brute Force-Angriffe entworfen. Dabei wird die Anzahl der möglichen Kennwörter erhöht. Wenn eine Richtlinie zur Kennwortkomplexität erzwungen wird, müssen neue Kennwörter die folgenden Richtlinien erfüllen:  
  
-   Das Kennwort enthält nicht den Kontonamen des Benutzers.  
  
-   Das Kennwort ist wenigstens acht Zeichen lang.  
  
-   Das Kennwort enthält Zeichen aus drei der folgenden vier Kategorien:  
  
    -   Lateinische Großbuchstaben (A - Z)   
  
    -   Lateinische Kleinbuchstaben (a - z)   
  
    -   10 Grundziffern (0 - 9)   
  
    -   Nicht alphanumerische Zeichen, wie z. B.: Ausrufezeichen (!), Dollarzeichen ($), Nummernzeichen (#) oder Prozentzeichen (%)  
  
 Kennwörter können bis zu 128 Zeichen lang sein. Sie sollten möglichst lange und komplexe Kennwörter verwenden.  
  
## Ablauf des Kennworts  
 Richtlinien zum Ablauf von Kennwörtern werden verwendet, um die Lebensdauer von Kennwörtern zu verwalten. Wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die Richtlinie zum Ablauf von Kennwörtern durchsetzt, werden Benutzer daran erinnert, alte Kennwörter zu ändern. Konten mit abgelaufenen Kennwörtern werden deaktiviert.  
  
## Richtliniendurchsetzung  
 Das Erzwingen der Kennwortrichtlinie kann für jede SQL Server-Anmeldung einzeln konfiguriert werden. Verwenden Sie [ALTER LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/alter-login-transact-sql.md), um die Kennwortrichtlinienoptionen für eine SQL Server-Anmeldung zu konfigurieren. Die folgenden Regeln gelten für die Konfiguration zur Erzwingung der Kennwortrichtlinie:  
  
-   Wenn CHECK_POLICY in ON geändert wird, kommt es zu folgenden Verhaltensweisen:  
  
    -   Für CHECK_EXPIRATION wird ebenfalls ON festgelegt, es sei denn, der Wert OFF wurde ausdrücklich festgelegt.  
  
    -   Der Kennwortverlauf wird mit dem Wert des aktuellen Kennworthashes initialisiert.  
  
    -   **Kontosperrdauer**, **Kontensperrungsschwelle** und **Zurücksetzungsdauer des Kontosperrungszählers** sind ebenfalls aktiviert.  
  
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
  
## Verwandte Aufgaben  
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)  
  
 [ALTER LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/alter-login-transact-sql.md)  
  
 [CREATE USER &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)  
  
 [ALTER USER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-user-transact-sql.md)  
  
 [Erstellen eines Anmeldenamens](../../relational-databases/security/authentication-access/create-a-login.md)  
  
 [Erstellen eines Datenbankbenutzers](../../relational-databases/security/authentication-access/create-a-database-user.md)  
  
## Verwandte Inhalte  
 [Sichere Kennwörter](../../relational-databases/security/strong-passwords.md)  
  
  