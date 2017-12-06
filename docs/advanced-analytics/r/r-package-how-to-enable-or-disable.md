---
title: "Aktivieren oder Deaktivieren der Verwaltung von R-Paket für SQL Server | Microsoft Docs"
ms.custom: 
ms.date: 10/05/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6e384893-04da-43f9-b100-bfe99888f085
caps.latest.revision: "7"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 59f7522a8065a733be49b24435563b1b033b1b8f
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/01/2017
---
# <a name="enable-or-disable-r-package-management-for-sql-server"></a>Aktivieren Sie oder deaktivieren Sie der Verwaltung von R-Paket für SQL Server

Dieser Artikel beschreibt den Prozess der aktivieren oder deaktivieren das neue Paket-Management-Feature in SQL Server-2017. Diese Funktion kann der Datenbankadministrator Paketinstallation auf der Instanz zu steuern. Die Funktion basiert auf neuen Datenbankrollen, erteilen Sie Benutzern die Möglichkeit zum Installieren der R-Pakete, die sie benötigen, oder Pakete für andere Benutzer freigeben.

Standardmäßig wird die Verwaltungsfunktion externe Paket für SQL Server deaktiviert, auch wenn Machine Learning-Funktionen installiert wurden.

Um [aktivieren](#bkmk_enable) diese Funktion ist ein zweistufiger Prozess und erfordert einige Hilfe von einem Datenbankadministrator:

1.  Aktivieren der Paketverwaltung in der SQL Server-Instanz (je einmal pro SQL Server-Instanz)

2.  Aktivieren der Paketverwaltung in der SQL Server-Datenbank (je einmal pro SQL Server-Datenbank)

Um [deaktivieren](#bkmk_disable) die Paket-Verwaltungsfunktion Umkehren des Prozesses zum Entfernen von Paketen auf Datenbankebene oder Berechtigungen, und entfernen Sie die Rollen vom Server:

1.  Deaktivieren der Paketverwaltung für die einzelnen Datenbanken (je einmal pro Datenbank)

2.  Deaktivieren der Paketverwaltung in der SQL Server-Instanz (je einmal pro Instanz)

## <a name="bkmk_enable"></a>Aktivieren Sie die paketverwaltung

So aktivieren oder Deaktivieren der paketverwaltung erfordert das Befehlszeile-Hilfsprogramm **RegisterRExt.exe**, ist die im Lieferumfang der **"revoscaler"** Paket.

1. Öffnen Sie ein Eingabeaufforderungsfenster mit erhöhten Rechten, und navigieren Sie zu dem Ordner mit dem Hilfsprogramm RegisterRExt.exe. Der Standardspeicherort ist `<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRExe.exe`.

2. Führen Sie den folgenden Befehl, geeignete Argumente für Ihre Umgebung bereitstellen:

    `RegisterRExt.exe /installpkgmgmt [/instance:name] [/user:username] [/password:*|password]`

    Dieser Befehl erstellt die Objekte auf Instanzebene auf dem SQL Server-Computer, die für die paketverwaltung erforderlich sind. Er startet auch des LaunchPads für die Instanz neu.

    Wenn Sie keine Instanz angeben, wird die Standardinstanz verwendet.

    Wenn Sie keinen Benutzer angeben, wird der aktuelle Sicherheitskontext verwendet.

2.  Um paketverwaltung auf Datenbankebene hinzuzufügen, führen Sie den folgenden Befehl von einer Eingabeaufforderung mit erhöhten Rechten aus:

    `RegisterRExt.exe /installpkgmgmt /database:databasename [/instance:name] [/user:username] [/password:*|password]`
   
    Dieser Befehl erstellt eine Datenbank-Elementen, z. B. die folgenden Datenbankrollen, die zum Steuern von Benutzerberechtigungen verwendet werden: `rpkgs-users`, `rpkgs-private`, und `rpkgs-shared`.

    Wenn Sie keinen Benutzer angeben, wird der aktuelle Sicherheitskontext verwendet.

3. Wiederholen Sie den Befehl für jede Datenbank, in dem Pakete installiert werden muss.

4.  Um sicherzustellen, dass die neuen Rollen erfolgreich erstellt wurden, klicken Sie in SQL Server Management Studio auf die Datenbank, erweitern Sie **Sicherheit**, und erweitern Sie **Datenbankrollen**.

    Sie können auch eine Abfrage auf Sys. database_principals, z. B. Folgendes ausführen:

    ```SQL
    SELECT pr.principal_id, pr.name, pr.type_desc,   
        pr.authentication_type_desc, pe.state_desc,   
        pe.permission_name, s.name + '.' + o.name AS ObjectName  
    FROM sys.database_principals AS pr  
    JOIN sys.database_permissions AS pe  
        ON pe.grantee_principal_id = pr.principal_id  
    JOIN sys.objects AS o  
        ON pe.major_id = o.object_id  
    JOIN sys.schemas AS s  
        ON o.schema_id = s.schema_id;
    ```

4.  Nachdem die Funktion aktiviert wurde, kann jeder Benutzer mit den entsprechenden Berechtigungen verwenden die [externe Bibliothek erstellen](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) -Anweisung in T-SQL-Pakete hinzufügen. Ein Beispiel dafür, wie dies funktioniert, finden Sie unter [Installieren zusätzlicher Pakete unter SQL Server](install-additional-r-packages-on-sql-server.md).

## <a name="bkmk_disable"></a>Deaktivieren der paketverwaltung

1.  Führen Sie an einer Eingabeaufforderung mit erhöhten Rechten den folgenden Befehl aus, um die Paketverwaltung auf Datenbankebene zu deaktivieren:

    `RegisterRExt.exe /uninstallpkgmgmt /database:databasename [/instance:name] [/user:username] [/password:*|password]`

    Führen Sie diesen Befehl einmal für jede Datenbank, in dem paketverwaltung verwendet wurde. Mit diesem Befehl werden die Datenbankobjekte, die im Zusammenhang mit paketverwaltung aus der angegebenen Datenbank entfernt. Es entfernt auch alle Pakete, die von der gesicherten Speicherort im Dateisystem auf dem SQL Server-Computer installiert wurden.

2.  (Optional) Nachdem alle Datenbanken von Paketen, die mit dem vorherigen Schritt gelöscht haben, führen Sie den folgenden Befehl von einer Eingabeaufforderung mit erhöhten Rechten aus:

    `RegisterRExt.exe /uninstallpkgmgmt [/instance:name] [/user:username] [/password:*|password]`

    Dieser Befehl entfernt die Paket-Verwaltungsfunktion aus der Instanz an.

## <a name="see-also"></a>Siehe auch

[R-Paketverwaltung für SQL Server](r-package-management-for-sql-server-r-services.md)
