---
title: Dialogfeld "SQL Server-Anmeldung" (ODBC) | Microsoft Docs
ms.custom: 
ms.date: 09/27/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 76326eeb-1144-4b9f-85db-50524c655d30
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: ea362cd05de5d1ba17ca717d94354d5786119bab
ms.openlocfilehash: 67aa8fc08a75efbcf77eb839b1999961a17e2a9f
ms.contentlocale: de-de
ms.lasthandoff: 10/06/2017

---
# <a name="sql-server-login-dialog-box-odbc"></a>Dialogfeld „SQL Server-Anmeldung“ (ODBC)

Wenn Sie eine ODBC-Verbindung aufrufen, ohne ausreichende Informationen für den Treiber für die Verbindung zu SQL Server, zeigt der ODBC-Treiber anzugeben, die **SQL Server-Anmeldung** (Dialogfeld).

## <a name="options"></a>enthalten

### <a name="server"></a>Server

Der Name einer Instanz von SQL Server in Ihrem Netzwerk. Wählen Sie einen Server-/ Instanzennamen aus der Liste aus, oder geben Sie die Server-/ Instanzennamen in das **Server** Feld. Optional können Sie einen Server-Alias erstellen, auf dem Client-Computer unter Verwendung **SQL Server-Konfigurations-Manager**, und geben Sie den Namen in der **Server** Feld.

Sie können "(local)" eingeben, wenn Sie den gleichen Computer wie SQL Server. Sie können dann mit einer lokalen Instanz von SQL Server, selbst wenn eine nicht vernetzte Version von SQL Server ausgeführt verbinden.

Weitere Informationen über Servernamen für verschiedene Typen von Netzwerken finden Sie in der Dokumentation der SQL Server-Installation in der SQL Server-Onlinedokumentation.

### <a name="authentication-mode"></a>Authentifizierungsmodus

Wählt den Authentifizierungsmodus aus einem der folgenden:
- **SQL Server** mit Anmelde-ID und Kennwort
- **Integrierte Windows-** Authentifizierung mithilfe des aktuell angemeldeten Benutzers-Kontos
- **Active Directory-Kennwortauthentifizierung** mit Anmelde-ID und Kennwort
- **Active Directory-integrierte** Authentifizierung mithilfe des aktuell angemeldeten Benutzers-Kontos

Finden Sie unter [Data Source-Assistent Bildschirm 2](../../../connect/odbc/windows/dsn-wizard-2.md) für Weitere Informationen zu den Authentifizierungsmodi.

### <a name="server-spn"></a>Server-SPN

Wenn Sie eine vertrauenswürdige Verbindung verwenden, können Sie einen Dienstprinzipalnamen (SPN) für den Server angeben.

### <a name="login-id"></a>Login ID

Gibt an, die SQL Server oder Azure Active Directory-Anmelde-ID für die Verbindung verwendet werden sollen, wenn **Authentifizierungsmodus** festgelegt ist, um **SQL Server** oder **Active Directory-Kennwortauthentifizierung**. Andernfalls die **Anmelde-ID** ist deaktiviert.

### <a name="password"></a>Kennwort

Gibt das Kennwort für die SQL Server oder Azure Active Directory Anmelde-ID, die für die Verbindung verwendet wird, wenn **Authentifizierungsmodus** festgelegt ist, um **SQL Server** oder **Active Directory-Kennwortauthentifizierung**. Andernfalls die **Kennwort** ist deaktiviert.

### <a name="options"></a>enthalten

Zeigt an, oder blendet Sie aus der **Optionen** Gruppe. Die **Optionen** Schaltfläche ist aktiviert, wenn **Server** über einen Wert verfügt.

### <a name="change-password"></a>Ändern des Kennworts

Wenn dieses Kontrollkästchen aktiviert ist, zeigt der **neues Kennwort** und **neues Kennwort bestätigen** Felder.

### <a name="new-password"></a>Neues Kennwort

Gibt das neue Kennwort an.

### <a name="confirm-new-password"></a>Neues Kennwort bestätigen

Gibt das neue Kennwort zur Bestätigung ein zweites Mal an.

### <a name="database"></a>Datenbank

Gibt die Standarddatenbank an, die für die Verbindung verwendet werden soll. Diese Einstellung überschreibt die für die Anmeldung auf dem Server festgelegte Standarddatenbank. Wenn keine Datenbank angegeben ist, wird für die Verbindung die Standarddatenbank verwendet, die für die Anmeldung auf dem Server angegeben ist.

### <a name="mirror-server"></a>Spiegelserver

Gibt den Namen des Failoverpartners der zu spiegelnden Datenbank an.

### <a name="mirror-spn"></a>Spiegelserver-SPN

Optional können Sie einen SPN für den Spiegelserver angeben. Der SPN für den Spiegelserver wird zur gegenseitigen Authentifizierung zwischen Client und Server verwendet.

### <a name="language"></a>Sprache

Gibt die Landessprache für SQL Server-systemmeldungen verwendet. Der Computer mit SQL Server muss die Sprache installiert sein. Diese Einstellung überschreibt die für die Anmeldung auf dem Server festgelegte Standardsprache. Wenn keine Sprache angegeben ist, wird für die Verbindung die Standardsprache verwendet, die für die Anmeldung auf dem Server angegeben ist.

### <a name="application-name"></a>ApplicationName

(Optional) Gibt den Anwendungsnamen in gespeichert werden die **Program_name** Spalte in der Zeile für diese Verbindung in **sys.sysprocesses**.

### <a name="workstation-id"></a>Workstation ID

(Optional) Gibt die Workstation ID zu speichernde in der **Hostname** Spalte in der Zeile für diese Verbindung in **sys.sysprocesses**.

### <a name="use-strong-encryption-for-data"></a>Starke Verschlüsselung für Daten verwenden

Bei Auswahl dieser Option werden die Daten, die über die Verbindung übergeben werden verschlüsselt. Anmeldungen werden standardmäßig verschlüsselt, auch wenn das Kontrollkästchen deaktiviert wird.

### <a name="trust-server-certificate"></a>Serverzertifikat zu vertrauen

Diese Option ist nur anwendbar, wenn **starken Verschlüsselung für Daten verwenden** aktiviert ist. Bei Auswahl dieser Option wird das Zertifikat des Servers nicht überprüft werden, um, der richtige Hostname des Servers und von einer vertrauenswürdigen Zertifizierungsstelle ausgestellt werden.

## <a name="see-also"></a>Siehe auch

[Microsoft ODBC Driver for SQL Server on Windows](../../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)

