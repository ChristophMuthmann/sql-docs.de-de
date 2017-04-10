---
title: "Aktivieren oder Deaktivieren der R-Paketverwaltung | Microsoft Docs"
ms.custom: ""
ms.date: "12/22/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6e384893-04da-43f9-b100-bfe99888f085
caps.latest.revision: 7
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
---
# Aktivieren oder Deaktivieren der R-Paketverwaltung

Standardmäßig ist die Paketverwaltung in SQL Server-Instanzen deaktiviert, auch bei installierten R Services. Das Aktivieren dieses Features ist ein zweistufiger Vorgang, der von einem Datenbankadministrator ausgeführt werden muss: 

1. Aktivieren der Paketverwaltung in der SQL Server-Instanz (je einmal pro SQL Server-Instanz) 
2. Aktivieren der Paketverwaltung in der SQL Server-Datenbank (je einmal pro SQL Server-Datenbank) 


Kehren Sie beim Deaktivieren der Paketverwaltungsfunktion den Vorgang zum Entfernen von Paketen und Berechtigungen auf Datenbankebene um, und entfernen Sie die Rollen vom Server:
 
1. Deaktivieren der Paketverwaltung für die einzelnen Datenbanken (je einmal pro Datenbank) 
2. Deaktivieren der Paketverwaltung in der SQL Server-Instanz (je einmal pro Instanz) 

> [!IMPORTANT]
> Diese Funktion befindet sich in der Entwicklung. Beachten Sie, dass sich Syntax oder Funktionalität in kommenden Versionen ändern können. 

### <a name="to-enable-package-management"></a>So aktivieren Sie die Paketverwaltung

Das Aktivieren oder Deaktivieren der Paketverwaltung erfordert das Befehlszeilen-Hilfsprogramm **RegisterRExt.exe**, das im **RevoScaleR**-Paket enthalten ist, das zusammen mit den SQL Server R Services installiert wird. Der Standardspeicherort ist:

`<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRExe.exe` 
    
1. Öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten, und verwenden Sie den folgenden Befehl:

    `RegisterRExt.exe /installpkgmgmt [/instance:name] [/user:username] [/password:*|password]`

    Durch diesen Befehl werden auf dem SQL Server-Computer Artefakte auf Instanzebene erstellt, die für die Paketverwaltung erforderlich sind. 

2. Um Paketverwaltung auf der Datenbankebene hinzuzufügen, führen Sie an einer Eingabeaufforderung mit erhöhten Rechten für jede Datenbank, für die Pakete installiert werden müssen, den folgenden Befehl aus: 

    `RegisterRExt.exe /installpkgmgmt /database:databasename [/instance:name] [/user:username] [/password:*|password]` 

    Dieser Befehl erstellt einige Datenbankartefakte, einschließlich der folgenden Datenbankrollen, die für das Steuern von Benutzerberechtigungen erforderlich sind: **rpkgs-users**, **rpkgs-private** und **rpkgs-shared** 

### <a name="to-disable-package-management"></a>So deaktivieren Sie die Paketverwaltung 

1. Führen Sie an einer Eingabeaufforderung mit erhöhten Rechten den folgenden Befehl aus, um die Paketverwaltung auf Datenbankebene zu deaktivieren:

   `RegisterRExt.exe /uninstallpkgmgmt /database:databasename [/instance:name] [/user:username] [/password:*|password]` 

    Dieser Befehl entfernt Datenbankartefakte, die mit der Paketverwaltung zusammenhängen, aus der angegebenen Datenbank.  Der Befehl entfernt außerdem alle Pakete, die pro Datenbank aus dem geschützten Speicherort im Dateisystem auf dem SQL Server-Computer installiert wurden.
    
    Der Befehl muss einmal für jede Datenbank ausgeführt werden, in der die Paketverwaltung verwendet wurde.
 
2. (Optional) Um die Paketverwaltungsfunktion vollständig aus der Instanz zu entfernen, führen Sie den folgenden Befehl an einer Eingabeaufforderung mit erhöhten Rechten aus, nachdem die Pakete mithilfe des vorhergehenden Schritts aus allen Datenbanken entfernt wurden:

    `RegisterRExt.exe /uninstallpkgmgmt [/instance:name] [/user:username] [/password:*|password]`

    Dieser Befehl entfernt die Artefakte auf Instanzebene, die von der Paketverwaltung verwendet werden, aus der SQL Server-Instanz. 


## <a name="see-also"></a>Siehe auch
[R-Paketverwaltung für SQL Server R Services](../../advanced-analytics/r-services/r-package-management-for-sql-server-r-services.md)