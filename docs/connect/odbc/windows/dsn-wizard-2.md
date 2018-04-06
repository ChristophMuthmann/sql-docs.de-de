---
title: Datenquellen (Assistentenbildschirm 2) (Odbcdriver for SQLServer) | Microsoft Docs
ms.custom: ''
ms.date: 03/21/2018
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 76326eeb-1144-4b9f-85db-50524c655d30
caps.latest.revision: 22
author: MightyPen
ms.author: v-jizho2
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 624888902e260baa03ad30aee8608f921deb73a4
ms.sourcegitcommit: 8b332c12850c283ae413e0b04b2b290ac2edb672
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/05/2018
---
# <a name="data-source-wizard-screen-2"></a>Datenquellen-Assistent (Bildschirm 2)

Geben Sie die Methode der Authentifizierung, und richten Sie Microsoft SQL Server Einträge des erweiterten Clients und dem Anmeldenamen und Kennwort, mit der ODBC-Treiber für SQL Server mit SQL Server herstellen, während der Konfiguration der Datenquelle.

## <a name="options"></a>enthalten

### <a name="with-integrated-windows-authentication"></a>Mit der integrierten Windows-Authentifizierung

Gibt an, dass der Treiber eine sichere (oder vertrauenswürdige) Verbindung mit einem SQL-Server anfordern. Wenn diese Option aktiviert ist, verwendet SQL Server unabhängig vom aktuellen Anmeldesicherheitsmodus auf dem Server die integrierte Anmeldesicherheit, um Verbindungen mit dieser Datenquelle herzustellen. Alle angegebenen Anmelde-IDs oder Kennwörter werden ignoriert. Der SQL Server-Systemadministrator muss Ihren Windows-Anmeldenamen mit einer SQL Server-Anmelde-ID verknüpft haben (z. B. durch Verwendung von SQL Server Management Studio).

Optional können Sie einen Dienstprinzipalnamen (Service Principal Name, SPN) für den Server angeben.

### <a name="with-active-directory-integrated-authentication"></a>Mit Active Directory-integrierte Authentifizierung

Gibt an, dass der Treiber mit SQL Server mithilfe von Azure Active Directory authentifiziert. Bei Auswahl dieser Option verwendet SQL Server Azure Active Directory-integrierte anmeldesicherheit zum Herstellen einer Verbindung mit dieser Datenquelle, unabhängig vom aktuellen anmeldesicherheitsmodus auf dem Server.

### <a name="with-sql-server-authentication"></a>Mit SQL Server-Authentifizierung

Gibt an, dass der Treiber mit SQL Server mithilfe der Anmelde-ID und Kennwort authentifizieren.

### <a name="with-active-directory-password-authentication"></a>Mit Active Directory-Kennwortauthentifizierung

Gibt an, dass der Treiber mit SQL Server mit einem Azure Active Directory-Anmelde-ID und Kennwort authentifizieren.

### <a name="with-active-directory-interactive-authentication"></a>Mit interaktiven für Active Directory-Authentifizierung

Gibt an, dass der Treiber mit SQL Server mithilfe von Azure Active Directory interaktiven Modus durch Bereitstellen der Anmelde-ID zu authentifizieren. Dadurch wird das Dialogfeld mit der Windows Azure-Authentifizierung Eingabeaufforderung ausgelöst.

### <a name="login-id"></a>Login ID

Gibt die Anmelde-ID, die der Treiber verwendet, wenn SQL Server herstellen können, wenn **mit SQL Server-Authentifizierung mit Anmelde-ID und Kennwort, die vom Benutzer eingegebenen** oder **mit Active Directory-Kennwort-Authentifizierung mit Anmelde-ID und das Kennwort, die vom Benutzer eingegebenen** oder **mit Active Directory interaktive Authentifizierung mit Anmelde-ID, die vom Benutzer eingegebenen** ausgewählt ist. Die gilt nur für die Verbindung, die zum Bestimmen der Standardeinstellungen des Servers hergestellt wird; es gilt nicht für folgende Verbindungen, die nach dem Erstellen mit der Datenquelle hergestellt werden.

### <a name="password"></a>Kennwort

Gibt das Kennwort, das der Treiber verwendet, wenn SQL Server herstellen können, wenn **mit SQL Server-Authentifizierung mit Anmelde-ID und Kennwort, die vom Benutzer eingegebenen** oder **mit Active Directory-Kennwort-Authentifizierung mit Anmelde-ID und das Kennwort, die vom Benutzer eingegebenen** ausgewählt ist. Die gilt nur für die Verbindung, die zum Bestimmen der Standardeinstellungen des Servers hergestellt wird; es gilt nicht für folgende Verbindungen, die mit der neuen Datenquelle hergestellt werden.

Sowohl die **Anmelde-ID** und **Kennwort** sind deaktiviert, wenn **mit integrierter Windows-Authentifizierung** oder **mit Active Directory-integriert Authentifizierung** ausgewählt ist.

### <a name="next"></a>Weiter

Fährt mit dem nächsten Bildschirm des Assistenten.

### <a name="back"></a>Zurück

Zurück zum vorherigen Bildschirm des Assistenten.

## <a name="next-steps"></a>Nächste Schritte

[Data Source-Assistentenbildschirm 1](../../../connect/odbc/windows/dsn-wizard-1.md)

[Assistent Datenquellenbildschirm 3](../../../connect/odbc/windows/dsn-wizard-3.md)

