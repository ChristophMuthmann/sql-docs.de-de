---
title: "Aktivieren oder Deaktivieren der remote-paketverwaltung für SQL Server | Microsoft Docs"
ms.custom: 
ms.date: 02/20/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6e384893-04da-43f9-b100-bfe99888f085
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: feb30d37f9c22d6620a7c6a734172ef43c15e253
ms.sourcegitcommit: c08d665754f274e6a85bb385adf135c9eec702eb
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/28/2018
---
# <a name="enable-or-disable-remote-package-management-for-sql-server"></a>Aktivieren Sie oder deaktivieren Sie der remote-paketverwaltung für SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Dieser Artikel beschreibt die Verwaltung von R-Pakete aus einer Remoteinstanz von Machine Learning-Server zu ermöglichen. Nachdem das Paket-Feature aktiviert wurde, können Sie "revoscaler"-Befehle verwenden, um Pakete auf einer Datenbank von einem Remoteclient aus installieren.

> [!NOTE]
> Derzeit wird die Verwaltung von R-Bibliotheken unterstützt. Unterstützung für Python geplant ist.

Standardmäßig wird die Verwaltungsfunktion externe Paket für SQL Server deaktiviert, auch wenn Machine Learning-Funktionen installiert wurden. Sie müssen ein separates Skript, um die Funktion zu aktivieren, wie im nächsten Abschnitt beschrieben ausführen.

## <a name="overview-of-process-and-tools"></a>Übersicht über Prozess- und tools

Zum Aktivieren oder Deaktivieren der paketverwaltung, verwenden Sie das Befehlszeile-Hilfsprogramm **RegisterRExt.exe**, ist die im Lieferumfang der **"revoscaler"** Paket.

[Aktivieren der](#bkmk_enable) diese Funktion ist ein zweistufiger Prozess, einen Datenbankadministrator muss dann: Sie paketverwaltung auf SQL Server-Instanz (einmal pro SQL Server-Instanz) zu aktivieren, und klicken Sie dann aktivieren paketverwaltung für die SQL-Datenbank (einmal pro SQL Server -Datenbank).

[Deaktivieren von](#bkmk_disable) die Paket-Verwaltungsfunktion sind auch Multipel Schritte erforderlich: Sie Pakete auf Datenbankebene und Berechtigungen (eine pro Datenbank) zu entfernen, und entfernen Sie die Rollen vom Server (einmal pro Instanz).

## <a name="bkmk_enable"></a> Aktivieren Sie die paketverwaltung

1. Öffnen Sie ein Eingabeaufforderungsfenster mit erhöhten Rechten, und navigieren Sie zu dem Ordner mit dem Hilfsprogramm RegisterRExt.exe. Der Standardspeicherort ist `<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRExe.exe`.

2. Führen Sie den folgenden Befehl, der entsprechenden Argumente für Ihre Umgebung bereitstellen:

    `RegisterRExt.exe /installpkgmgmt [/instance:name] [/user:username] [/password:*|password]`

    Dieser Befehl erstellt die Objekte auf Instanzebene auf dem SQL Server-Computer, die für die paketverwaltung erforderlich sind. Er startet auch des LaunchPads für die Instanz neu.

    Wenn Sie keine Instanz angeben, wird die Standardinstanz verwendet. Wenn Sie keinen Benutzer angeben, wird der aktuelle Sicherheitskontext verwendet. So ermöglicht z. B. der folgende Befehl paketverwaltung für die Instanz im Pfad RegisterRExt.exe, mit den Anmeldeinformationen des Benutzers, der die Eingabeaufforderung geöffnet:

    `REgisterRExt.exe /installpkgmgmt`

3. Um eine bestimmte Datenbank paketverwaltung hinzugefügt haben, führen Sie den folgenden Befehl von einer Eingabeaufforderung mit erhöhten Rechten aus:

    `RegisterRExt.exe /installpkgmgmt /database:databasename [/instance:name] [/user:username] [/password:*|password]`
   
    Dieser Befehl erstellt eine Datenbank-Elementen, z. B. die folgenden Datenbankrollen, die zum Steuern von Benutzerberechtigungen verwendet werden: `rpkgs-users`, `rpkgs-private`, und `rpkgs-shared`.

    Aktivieren Sie der folgende Befehl beispielsweise paketverwaltung in der Datenbank, auf die Instanz, die dem RegisterRExt ausgeführt wird. Wenn Sie keinen Benutzer angeben, wird der aktuelle Sicherheitskontext verwendet.

    `RegisterRExt.exe /installpkgmgmt /database:TestDB`

4. Wiederholen Sie den Befehl für jede Datenbank, in dem Pakete installiert werden muss.

5. Um sicherzustellen, dass die neuen Rollen erfolgreich erstellt wurden, klicken Sie in SQL Server Management Studio auf die Datenbank, erweitern Sie **Sicherheit**, und erweitern Sie **Datenbankrollen**.

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

Nachdem Sie diese Funktion aktiviert haben, können Sie "revoscaler"-Funktion zu installieren oder Deinstallieren von Paketen von einem Remoteclient von R verwenden.

## <a name="bkmk_disable"></a> Deaktivieren der paketverwaltung

1. Eine Eingabeaufforderung mit erhöhten Rechten führen Sie das Dienstprogramm RegisterRExt erneut aus, und deaktivieren Sie paketverwaltung auf Datenbankebene:

    `RegisterRExt.exe /uninstallpkgmgmt /database:databasename [/instance:name] [/user:username] [/password:*|password]`

    Dieser Befehl entfernt die Datenbankobjekte, die im Zusammenhang mit paketverwaltung aus der angegebenen Datenbank. Es entfernt auch alle Pakete, die von der gesicherten Speicherort im Dateisystem auf dem SQL Server-Computer installiert wurden.

2. Wiederholen Sie diesen Befehl für jede Datenbank, in denen paketverwaltung verwendet wurde.

3.  (Optional) Nachdem alle Datenbanken von Paketen, die mit dem vorherigen Schritt gelöscht haben, führen Sie den folgenden Befehl von einer Eingabeaufforderung mit erhöhten Rechten aus:

    `RegisterRExt.exe /uninstallpkgmgmt [/instance:name] [/user:username] [/password:*|password]`

    Dieser Befehl entfernt die Paket-Verwaltungsfunktion aus der Instanz an. Sie müssen möglicherweise einmal, um Änderungen finden Sie unter den Launchpad-Dienst manuell neu zu starten.

