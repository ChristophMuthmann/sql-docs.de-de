---
title: Mithilfe der Betriebssystem-Authentifizierung | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], authentication
- authentication [ODBC]
ms.assetid: 613daef7-3171-42d0-b7e3-3879280f864d
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: da8b5adf34774f2ee6f7b224d7ab18f20a4dd09e
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="using-operating-system-authentication"></a>Mithilfe der Betriebssystem-Authentifizierung
> [!IMPORTANT]  
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Nutzen Sie diese Funktionen bei Neuentwicklungen nicht mehr, und planen Sie die Änderung von Anwendungen, die diese Funktion zurzeit verwenden. Verwenden Sie stattdessen den ODBC-Treiber von Oracle bereitgestellt.  
  
 Oracle-betriebssystemauthentifizierung basiert auf das zugrunde liegende Betriebssystem, den Zugriff auf Konten für Datenbank steuern. Benutzer müssen kein Kennwort eingeben, wenn dieser Typ der Anmeldung.  
  
 Um dieses Feature nutzen zu können, geben Sie "/" als Benutzer-ID und ein Kennwort nicht angeben, beim Herstellen einer Verbindung mit einer der folgenden Verbindungs-APIs: [SQLBrowseConnect](../../odbc/microsoft/level-2-api-functions-odbc-driver-for-oracle.md), [SQLConnect](../../odbc/microsoft/core-level-api-functions-odbc-driver-for-oracle.md), oder [ SQLDriverConnect](../../odbc/microsoft/level-1-api-functions-odbc-driver-for-oracle.md).  
  
 Oracle-Datenbanken verwenden Sie SQL * Net Authentifizierungsdienste zum Authentifizieren von Benutzern, die protokolliert werden. Dieser Dienst funktioniert gut, wenn Benutzer in Oracle über SQLPlus angemeldet sind. jedoch, wenn der angemeldete Benutzer ein Dienst z. B. Internetinformationsdienste (IIS) ist, die Authentifizierung schlägt fehl. Dies ist eine bekannte Einschränkung SQL\*Net-Authentifizierung und erzeugt die folgende Fehlermeldung: "[Microsoft] [ODBC-Treiber für Oracle] [Oracle] ORA-12641: TNS:authentication-Dienst konnte nicht initialisiert werden."  
  
 Sie können dieses Problem beheben, indem Sie die Datei Sqlnet.ora bearbeiten. Diese Konfigurationsdatei wird in der Regel im Unterverzeichnis Network\Admin das Oracle home-Verzeichnis gespeichert. Fügen Sie die folgende Zeile zum Sqlnet.ora:  
  
```  
SQLNET.AUTHENTICATION_SERVICES = (none)  
```
