---
title: "Erste Schritte mit SSMA für MySQL (MySQLToSQL) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-mysql
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Getting started, MySQL metadata explorer
- Getting started, SQL Server or SQL Azure metadata explorer
- Getting started,Installing and licensing
ms.assetid: 8ebfa061-be6f-4a07-923f-8dc832a82f70
caps.latest.revision: "19"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 961ab39ffc76be1ce2bd7dd36234163d3c8229bf
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="getting-started-with-ssma-for-mysql-mysqltosql"></a>Erste Schritte mit SSMA für MySQL (MySQLToSQL)
SQL Server Migration Assistant (SSMA) for MySQL können Sie schnell MySQL-Datenbankschemas in SQL Server oder Azure SQL-Datenbank-Schemas konvertieren, die resultierenden Schemas in SQL Server oder Azure SQL-Datenbank hochladen und Migrieren von Daten aus MySQL zu SQL Server oder Azure SQL-Datenbank.  
  
Dieses Thema führt während des Installationsvorgangs und anschließend hilft er Sie mit der SSMA-Benutzeroberfläche vertraut zu machen.  
  
## <a name="installing-ssma"></a>Installieren SSMA  
Um SSMA verwenden zu können, müssen Sie zuerst das SSMA-Clientprogramm auf einem Computer installieren, die die Quelle MySQL-Datenbank und der Zielinstanz von SQL Server oder Azure SQL-Datenbank zugreifen können. Anschließend installieren Sie die MySQL-Anbieter (MySQL 5.1 Odbcdriver (vertrauenswürdigen)), auf dem Computer, auf der SSMA-Clientprogramm ausgeführt wird. Installationsanweisungen finden Sie unter [Installieren von SSMA für MySQL &#40; MySqlToSql &#41;](../../ssma/mysql/installing-ssma-for-mysql-mysqltosql.md)  
  
Um SSMA zu starten, klicken Sie auf **starten**, zeigen Sie auf **Programme**, zeigen Sie auf **SQL Server Migration Assistant für MySQL**, und klicken Sie dann auf **SQL Server Migration Assistant für MySQL**.  
  
## <a name="ssma-for-mysql-user-interface"></a>SSMA für die MySQL-Benutzeroberfläche  
Nachdem SSMA installiert und lizenziert ist, können Sie SSMA zum Migrieren von MySQL-Datenbanken zu SQL Server oder Azure SQL-Datenbank verwenden. Er erleichtert damit vertraut machen, mit der SSMA-Benutzeroberfläche vor. Das folgende Diagramm zeigt die Benutzeroberfläche für SSMA, einschließlich der Metadaten-Explorer, Metadaten, Symbolleisten, Ausgabebereich und Listenbereich Fehler:  
  
![SSMA für die Grafische Benutzeroberfläche MySql](../../ssma/mysql/media/ssmaformysqlgui.gif "SSMA für die Grafische MySql-Benutzeroberfläche")  
  
Um eine Migration zu starten, müssen Sie folgende Aktionen ausführen:  
  
1.  Erstellen Sie ein neues Projekt.  
  
2.  Verbinden Sie mit einer MySQL-Datenbank.  
  
3.  Nach einer erfolgreichen Verbindung werden die MySQL-Schemas in MySQL-Metadaten-Explorer angezeigt. Mit der rechten Maustaste Objekte MySQL Metadaten-Explorer, um Aufgaben auszuführen, beispielsweise erstellen Berichte, die Konvertierungen in SQL Server/Azure SQL-Datenbank zu bewerten.  
  
Sie können auch diese Aufgaben ausführen, mit dem Symbolleisten und Menüs.  
  
Sie müssen auch eine Verbindung mit einer Instanz von SQL Server herstellen. Nach einer erfolgreichen Verbindung wird eine Hierarchie von SQL Server-Datenbanken in SQL Server-Metadaten-Explorer angezeigt. Nach der Konvertierung von MySQL-Schemas in SQL Server-Schemas wählen Sie diese konvertierte Schemas in SQL Server-Metadaten-Explorer, und synchronisieren Sie die Schemas mit SQL Server.  
  
Sie müssen mit Azure SQL-Datenbank verbinden, wenn Sie Azure SQL-Datenbank aus der Migration auf die Dropdownliste im Dialogfeld Neues Projekt ausgewählt haben. Nach einer erfolgreichen Verbindung wird eine Hierarchie von Azure SQL-Datenbank-Datenbanken in Azure SQL-DB-Metadaten-Explorer angezeigt. Nach der Konvertierung von MySQL-Schemas in Azure SQL-Datenbank-Schemas wählen Sie diese konvertierte Schemas in Azure SQL-DB-Metadaten-Explorer, und klicken Sie dann synchronisieren Sie die Schemas mit Azure SQL-Datenbank zu.  
  
Nachdem Sie konvertierte Schemas mit SQL Server oder Azure SQL-Datenbank zu synchronisieren, können Sie zurück zu MySQL-Metadaten-Explorer und Migrieren von Daten aus MySQL-Schemas in SQL Server oder Azure SQL-Datenbank-Datenbanken.  
  
Weitere Informationen zu diesen Aufgaben und Informationen zu deren Ausführung finden Sie unter [Migrieren von MySQL-Datenbanken zu SQL Server - Azure SQL-Datenbank &#40; MySQLToSql &#41; ](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md).  
  
In den folgenden Abschnitten werden die Funktionen von SSMA-Benutzeroberfläche beschrieben.  
  
### <a name="metadata-explorers"></a>Metadaten-Explorer  
SSMA enthält zwei Metadaten-Explorer zum Suchen und Ausführen von Aktionen für MySQL und SQL Server-Datenbanken.  
  
### <a name="mysql-metadata-explorer"></a>MySQL-Metadaten-Explorer  
MySQL-Metadaten-Explorer zeigt Informationen zur MySQL-Schemas. Mithilfe von MySQL-Metadaten-Explorer können Sie die folgenden Aufgaben ausführen:  
  
-   Durchsuchen Sie die Objekte in den einzelnen Schemas.  
  
-   Wählen Sie Objekte für die Konvertierung aus, und klicken Sie dann konvertieren Sie die Objekte in SQL Server-Syntax. Weitere Informationen finden Sie unter [MySQL-Datenbanken konvertieren &#40; MySQLToSQL &#41;](../../ssma/mysql/converting-mysql-databases-mysqltosql.md)  
  
-   Wählen Sie die Tabellen für die Datenmigration, und migrieren Sie die Daten aus diesen Tabellen mit SQL Server. Weitere Informationen finden Sie unter [Migrieren von MySQL-Daten in SQL Server - Azure SQL-Datenbank &#40; MySQLToSQL &#41;](../../ssma/mysql/migrating-mysql-data-into-sql-server-azure-sql-db-mysqltosql.md)  
  
### <a name="sql-server-or-azure-sql-db-metadata-explorer"></a>SQLServer oder Azure SQL-DB-Metadaten-Explorer  
SQL Server oder Azure SQL-DB-Metadaten-Explorer zeigt Informationen zu einer Instanz von SQL Server oder Azure SQL-Datenbank. Wenn Sie eine Verbindung mit einer Instanz von SQL Server oder Azure SQL-Datenbank herstellen, wird SSMA Ruft Metadaten für diese Instanz ab und speichert ihn in der Projektdatei.  
  
Sie können diesen Metadaten-Explorer verwenden, konvertierte Objekte der MySQL-Datenbank auswählen und dann diese Objekte mit der Instanz von SQL Server oder Azure SQL-Datenbank zu synchronisieren.  
  
Weitere Informationen finden Sie unter [Synchronisierung (MySQL zu SQL Server / Azure SQL-Datenbank)](http://msdn.microsoft.com/en-us/ac993a6d-0283-4823-8793-6b217677dfa3)  
  
### <a name="metadata"></a>Metadaten  
Sind Sie rechts neben jeder Metadaten-Explorer-Registerkarten, die das ausgewählte Objekt zu beschreiben. Z. B. Wenn Sie eine Tabelle in MySQL-Metadaten-Explorer auswählen, neun Registerkarten werden angezeigt: **Tabelle**, **SQL**, **Type Mapping**, **Daten**, **Einstellungen**, **Charset Zuordnung**, **SQL Modi**, **Eigenschaften**, und **Bericht**. Die **Bericht** Registerkarte enthält Informationen, nachdem Sie einen Bericht erstellen, die das ausgewählte Objekt enthält. Wenn Sie eine Tabelle in SQL Server-Metadaten-Explorer auswählen, werden drei Registerkarten angezeigt: **Tabelle**, **SQL** und **Daten**.  
  
Die meisten Metadateneinstellungen für die sind schreibgeschützt. Sie können jedoch die folgende Metadaten ändern:  
  
-   In MySQL-Metadaten-Explorer können Sie die datentypzuordnungen, Zuordnen von Charset SQL Modi ändern. Um die geänderte Typmappings oder Charset zuordnen oder SQL-Modi zu konvertieren, können nehmen Sie Änderungen vor, bevor Sie Schemas konvertieren.  
  
-   In SQL Server-Metadaten-Explorer können Sie die Tabellen- und Eigenschaften auf der Registerkarte "Tabelle" zu ändern. Um diese Änderungen in SQL Server angezeigt wird, werden nehmen Sie diese Änderungen vor, bevor Sie die Schemas in SQL Server laden.  
  
In einer Metadaten-Explorer vorgenommene Änderungen werden in die Projektmetadaten, nicht in den Quell- oder Zieltabelle Datenbanken wiedergegeben.  
  
### <a name="toolbars"></a>Symbolleisten  
SSMA hat zwei Symbolleisten: ein Projekt Symbolleisten und eine Migration.  
  
### <a name="the-project-toolbar"></a>Der Projekt-Symbolleiste  
Die Projekt-Symbolleiste enthält Schaltflächen zum Arbeiten mit Projekten, Herstellen einer Verbindung mit MySQL und Herstellen einer Verbindung mit SQL Server oder Azure SQL-Datenbank. Diese Schaltflächen ähneln die Befehle auf den **Datei** Menü.  
  
### <a name="migration-toolbar"></a>Migration-Symbolleiste  
Die folgende Tabelle zeigt die Migration Symbolleistenbefehle:  
  
|||  
|-|-|  
|**Schaltfläche**|**Funktion**|  
|**Bericht erstellen**|Konvertiert die ausgewählten MySQL-Objekte in SQL Server oder Azure SQL-Datenbank Objekte, und erstellt dann einen Bericht, der zeigt, wie erfolgreich das Konvertierung war.<br /><br />Dieser Befehl ist deaktiviert, es sei denn, die Objekte in MySQL-Metadaten-Explorer ausgewählt werden.|  
|**Schema konvertieren**|Konvertiert die ausgewählten MySQL-Objekten auf Objekte von SQL Server oder Azure SQL-Datenbank.<br /><br />Dieser Befehl ist deaktiviert, es sei denn, die Objekte in MySQL-Metadaten-Explorer ausgewählt werden.|  
|**Migrieren von Daten**|Werden Daten aus der MySQL-Datenbank in SQL Server oder Azure SQL-Datenbank migriert. Bevor Sie diesen Befehl ausführen müssen Sie die MySQL-Schemas in SQL Server oder Azure SQL-Datenbank-Schemas konvertieren und Laden Sie die Objekte in SQL Server oder Azure SQL-Datenbank.<br /><br />Dieser Befehl ist deaktiviert, es sei denn, die Objekte in MySQL-Metadaten-Explorer ausgewählt werden.|  
|**Beenden**|Hält den aktuellen Prozess an.|  
  
### <a name="menus"></a>Menüs  
Die folgende Tabelle zeigt die SSMA-Menüs.  
  
|||  
|-|-|  
|**Menü**|**Beschreibung**|  
|**Zuletzt geöffnete Dateien**|Enthält Befehle zum Arbeiten mit Projekten, Herstellen einer Verbindung mit MySQL und Herstellen einer Verbindung mit SQL Server oder Azure SQL-Datenbank.|  
|**Bearbeiten**|Enthält Befehle zum Suchen nach und Arbeiten mit Text in den Detailseiten. So öffnen **Lesezeichen verwalten** Dialogfeld im Menü Bearbeiten, klicken Sie auf Verwalten von Lesezeichen. Klicken Sie im Dialogfeld sehen Sie eine Liste der vorhandenen Lesezeichen. Die Schaltflächen können auf der rechten Seite des Dialogfelds Sie um das Lesezeichen zu verwalten.|  
|**Ansicht**|Enthält die **Synchronisieren der Metadaten-Explorer** Befehl. Die synchronisiert Objekte zwischen Metadaten-Explorer MySQL und SQL Server oder Azure SQL-DB-Metadaten-Explorer. Enthält auch Befehle anzeigen oder Ausblenden der **Ausgabe** und **Fehlerliste** Bereiche und eine Option **Layouts** mit Layouts verwalten.|  
|**Tools**|Enthält Befehle zum Erstellen von Berichten, Schema konvertieren, aus der Datenbank aktualisieren, Migrieren von Objekten und Daten und als Skript zu speichern. Bietet außerdem Zugriff auf die **globale Einstellungen, Projekt-Standardeinstellungen** und **Projekteinstellungen** Dialogfelder.|  
|**Hilfe**|Bietet Zugriff auf das SSMA-Hilfe und die **zu** (Dialogfeld).|  
  
### <a name="output-pane-and-error-list-pane"></a>Ausgabebereich und Fehler Listenbereich  
Die **Ansicht** Menü enthält Befehle zum Umschalten der Sichtbarkeit der im Ausgabebereich und den Bereich Fehlerliste:  
  
-   Im Ausgabebereich enthält statusmeldungen von SSMA bei Objekt Konvertierung, Synchronisierung und Migration von Daten.  
  
-   Bereich Fehlerliste werden Fehler-, Warn- und informationsmeldungen in einem sortierbaren angezeigt.  
  
## <a name="see-also"></a>Siehe auch  
[Referenz zur Benutzeroberfläche &#40; MySQLToSQL &#41;](../../ssma/mysql/user-interface-reference-mysqltosql.md)  
[Migrieren von MySQL-Daten in SQLServer - Azure SQL-Datenbank &#40; MySQLToSQL &#41;](../../ssma/mysql/migrating-mysql-data-into-sql-server-azure-sql-db-mysqltosql.md)  
  
