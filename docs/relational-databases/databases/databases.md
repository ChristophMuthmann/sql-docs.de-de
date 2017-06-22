---
title: Datenbanken | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data warehouse [SQL Server]
- OLTP databases [SQL Server]
- databases [SQL Server], about databases
ms.assetid: 316eea58-81b8-4bf3-a1fc-801946740e94
caps.latest.revision: 27
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 05f9976284e6207a1057f1b7308e7276d833daae
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="databases"></a>Datenbanken
  Eine Datenbank in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] besteht aus einer Auflistung von Tabellen, in der eine bestimmte Menge strukturierter Daten gespeichert ist. Eine Tabelle enthält eine Auflistung von Zeilen, auch als Datensätze oder Tupel bezeichnet, sowie Spalten, auch als Attribute bezeichnet. Jede Spalte in der Tabelle dient zum Speichern eines bestimmten Informationstyps, z. B. Datumsangaben, Namen, Geldbeträge und Zahlen.  
  
## <a name="basic-information-about-databases"></a>Grundlegende Informationen zu Datenbanken  
 Auf einem Computer können eine oder mehrere Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installiert werden. Jede Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] kann eine Datenbank oder viele Datenbanken enthalten.  Innerhalb einer Datenbank gibt es eine oder mehrere Objektbesitzgruppen, so genannte Schemas. In jedem Schema gibt es Datenbankobjekte wie Tabellen, Sichten und gespeicherte Prozeduren. Einige Objekte, z. B. Zertifikate und asymmetrische Schlüssel, sind in der Datenbank, jedoch nicht in einem Schema enthalten. Weitere Informationen zum Erstellen von Tabellen finden Sie unter [Tables](../../relational-databases/tables/tables.md).  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbanken sind im Dateisystem in Dateien gespeichert. Dateien können in Dateigruppen gruppiert werden. Weitere Informationen zu Dateien und Dateigruppen finden Sie unter [Database Files and Filegroups](../../relational-databases/databases/database-files-and-filegroups.md).  
  
 Wenn Personen Zugriff auf eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erhalten, werden sie über einen Anmeldenamen identifiziert. Wenn Personen Zugriff auf eine Datenbank erhalten, werden sie als Datenbankbenutzer identifiziert. Ein Datenbankbenutzer kann auf einer Anmeldung basieren. Wenn eigenständige Datenbanken aktiviert werden, kann ein Datenbankbenutzer erstellt werden, der nicht auf einer Anmeldung basiert. Weitere Informationen über Benutzer finden Sie unter [CREATE USER &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md).  
  
 Einem Benutzer mit Zugriff auf eine Datenbank kann die Berechtigung zum Zugreifen auf die Objekte in der Datenbank erteilt werden. Obwohl Berechtigungen einzelnen Benutzern erteilt werden können, sollten Datenbankrollen erstellt, den Rollen Datenbankbenutzer hinzugefügt und dann Zugriffsberechtigungen für die Rollen erteilt werden. Indem Berechtigungen für Rollen und nicht für Benutzer erteilt werden, können die Berechtigungen leichter konsistent und verständlich gehalten werden, während die Anzahl der Benutzer wächst und sich laufend ändert. Weitere Informationen zu Rollenberechtigungen finden Sie unter [CREATE ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-role-transact-sql.md) und [Prinzipale &#40;Datenbankmodul&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md).  
  
## <a name="working-with-databases"></a>Arbeiten mit Datenbanken  
 Die meisten Personen, die mit Datenbanken arbeiten, verwenden das Tool [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] . Das [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] -Tool besitzt eine grafische Benutzeroberfläche zum Erstellen von Datenbanken und den Objekten in den Datenbanken. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] enthält außerdem einen Abfrage-Editor für die Interaktion mit Datenbanken durch das Schreiben von [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] kann vom [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Installationsdatenträger installiert oder von MSDN heruntergeladen werden.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
|||  
|-|-|  
|[Systemdatenbanken](../../relational-databases/databases/system-databases.md)|[Löschen von Daten- oder Protokolldateien aus einer Datenbank](../../relational-databases/databases/delete-data-or-log-files-from-a-database.md)|  
|[Eigenständige Datenbanken](../../relational-databases/databases/contained-databases.md)|[Anzeigen von Informationen zum Daten- und Protokollspeicherplatz einer Datenbank](../../relational-databases/databases/display-data-and-log-space-information-for-a-database.md)|  
|[SQL Server-Datendateien in Microsoft Azure](../../relational-databases/databases/sql-server-data-files-in-microsoft-azure.md)|[Erhöhen der Größe einer Datenbank](../../relational-databases/databases/increase-the-size-of-a-database.md)|  
|[Datenbankdateien und Dateigruppen](../../relational-databases/databases/database-files-and-filegroups.md)|[Umbenennen einer Datenbank](../../relational-databases/databases/rename-a-database.md)|  
|[Datenbankstatus](../../relational-databases/databases/database-states.md)|[Festlegen des Einzelbenutzermodus für eine Datenbank](../../relational-databases/databases/set-a-database-to-single-user-mode.md)|  
|[Dateistatus](../../relational-databases/databases/file-states.md)|[Verkleinern einer Datenbank](../../relational-databases/databases/shrink-a-database.md)|  
|[Schätzen der Größe einer Datenbank](../../relational-databases/databases/estimate-the-size-of-a-database.md)|[Verkleinern einer Datei](../../relational-databases/databases/shrink-a-file.md)|  
|[Kopieren von Datenbanken auf andere Server](../../relational-databases/databases/copy-databases-to-other-servers.md)|[Anzeigen oder Ändern der Eigenschaften einer Datenbank](../../relational-databases/databases/view-or-change-the-properties-of-a-database.md)|  
|[Anfügen und Trennen von Datenbanken &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)|[Anzeigen einer Liste der Datenbanken in einer Instanz von SQL Server](../../relational-databases/databases/view-a-list-of-databases-on-an-instance-of-sql-server.md)|  
|[Hinzufügen von Daten- oder Protokolldateien zu einer Datenbank](../../relational-databases/databases/add-data-or-log-files-to-a-database.md)|[Anzeigen oder Ändern des Kompatibilitätsgrads einer Datenbank](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md)|  
|[Ändern der Konfigurationseinstellungen für eine Datenbank](../../relational-databases/databases/change-the-configuration-settings-for-a-database.md)|[Verwenden des Wartungsplanungs-Assistenten](../../relational-databases/maintenance-plans/use-the-maintenance-plan-wizard.md)|  
|[Erstellen einer Datenbank](../../relational-databases/databases/create-a-database.md)|[Erstellen eines benutzerdefinierten Datentypalias](../../relational-databases/databases/create-a-user-defined-data-type-alias.md)|  
|[Löschen einer Datenbank](../../relational-databases/databases/delete-a-database.md)|[Datenbank-Momentaufnahmen &#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md)|  
  
## <a name="related-content"></a>Verwandte Inhalte  
 [Indizes](../../relational-databases/indexes/indexes.md)  
  
 [Sichten](../../relational-databases/views/views.md)  
  
 [Gespeicherte Prozeduren &#40;Datenbankmodul&#41;](../../relational-databases/stored-procedures/stored-procedures-database-engine.md)  
  
  
