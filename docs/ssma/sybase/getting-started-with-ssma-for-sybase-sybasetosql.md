---
title: Erste Schritte mit SSMA für SAP ASE (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/30/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-sybase
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: c4098516-f0fc-4690-97bb-3766dfd43156
caps.latest.revision: 10
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 4a7402493afc20037c7e0b16201bc1c6b49dfe27
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="getting-started-with-ssma-for-sap-ase-sybasetosql"></a>Erste Schritte mit SSMA für SAP ASE (SybaseToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Migration Assistant (SSMA), SAP ASE können Sie schnell konvertieren Datenbankschemas auf SAP Adaptive Server Enterprise (ASE) [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL-Datenbank-Schemas, laden die resultierenden Schemas in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL-Datenbank und Migrieren von Daten aus SAP ASE zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL-Datenbank.  
  
Dieses Thema führt während des Installationsvorgangs und anschließend hilft er Sie mit der SSMA-Benutzeroberfläche vertraut zu machen.  
  
## <a name="installing-and-licensing-ssma"></a>Installieren und Lizenzieren von SSMA  
Um SSMA verwenden zu können, müssen Sie zunächst installieren das SSMA-Clientprogramm auf einem Computer, die sowohl der Zielinstanz von SAP ASE und der Zielinstanz von zugreifen kann [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL-Datenbank. Um serverseitige Datenmigration verwenden zu können, müssen Sie Erweiterung Pack und bei mindestens einer der SAP ASE-Anbieter (OLE DB oder ADO.NET) installieren, auf dem Computer, auf denen ausgeführt wird [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Diese Komponenten unterstützen die Migration von Daten und die Emulation von SAP ASE Systemfunktionen. Installationsanweisungen finden Sie unter [Installieren von SSMA für SAP ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-sybasetosql.md).  
  
Um SSMA zu starten, klicken Sie auf **starten**, zeigen Sie auf **Programme**, zeigen Sie auf  **[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Migration Assistant für Sybase**, und wählen Sie dann  **[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Migration Assistant für Sybase**. Zum ersten Mal starten von SSMA, wird ein Dialogfeld Lizenzierung angezeigt. Sie müssen die SSMA mithilfe einer Windows Live ID vor der Verwendung von SSMA lizenzieren. Lizenzierung Anweisungen sind in den installationsanweisungen im enthalten die [Installieren von SSMA für Sybase Client &#40;SybaseToSQL&#41; ](../../ssma/sybase/installing-ssma-for-sybase-client-sybasetosql.md) Thema.  
  
## <a name="ssma-for-sap-ase-user-interface"></a>SSMA für die Benutzeroberfläche von SAP ASE  
Nachdem SSMA installiert und lizenziert ist, können Sie SSMA um SAP ASE-Datenbanken zu migrieren [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL-Datenbank. Er erleichtert damit vertraut machen, mit der SSMA-Benutzeroberfläche vor. Das folgende Diagramm zeigt die Benutzeroberfläche für SSMA, einschließlich der Metadaten-Explorer, Metadaten, Symbolleisten, Ausgabebereich und Listenbereich Fehler:  
  
![SSMA für die Benutzeroberfläche des SAP ASE](../../ssma/sybase/media/ssmaforsybaseuserinterface.jpg "SSMA für die Benutzeroberfläche des SAP ASE")  
  
Um eine Migration zu starten, müssen Sie zunächst ein neues Projekt erstellen. Klicken Sie dann die Verbindung zur SAP ASE. Nach einer erfolgreichen Verbindung wird eine Hierarchie von SAP ASE Datenbanken in Sybase-Metadaten-Explorer angezeigt. Sie können dann mit der rechten Maustaste Objekte in Sybase-Metadaten-Explorer zum Ausführen von Aufgaben wie z. B. Berichte erstellen, die Konvertierungen zu bewerten [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL-Datenbank. Außerdem können Sie diese Aufgaben über Symbolleisten und Menüs ausführen.  
  
Sie außerdem müssen die Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL-Datenbank. Nach einer erfolgreichen Verbindung eine Hierarchie von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL-Datenbanken werden in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Metadaten-Explorer. Nach der Konvertierung von Schemas SAP ASE [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL-Datenbank-Schemas, wählen Sie diese konvertierte Schemas in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Metadaten-Explorer, und Laden Sie die Schemas in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL-Datenbank.  
  
Laden Sie konvertierte Schemas in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL-Datenbank können Sie zurück zu Sybase-Metadaten-Explorer und Migrieren von Daten aus SAP ASE Datenbanken in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL-Datenbanken.  
  
Weitere Informationen zu diesen Aufgaben und Informationen zu deren Ausführung finden Sie unter [SAP ASE-Datenbanken zu SQL Server - Azure SQL-Datenbank migrieren &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md).  
  
In den folgenden Abschnitten werden die Funktionen von SSMA-Benutzeroberfläche beschrieben.  
  
### <a name="metadata-explorers"></a>Metadaten-Explorer  
SSMA enthält zwei Metadaten-Explorer zum Suchen und Ausführen von Aktionen für SAP ASE und [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL-Datenbanken.  
  
#### <a name="sybase-metadata-explorer"></a>Sybase-Metadaten-Explorer  
Sybase-Metadaten-Explorer zeigt Informationen zu Datenbanken auf der Zielinstanz von SAP ASE.  
  
Mithilfe von Sybase-Metadaten-Explorer können Sie die folgenden Aufgaben ausführen:  
  
-   Durchsuchen Sie die Tabellen in jeder Datenbank.  
  
-   Wählen Sie Objekte für die Konvertierung aus, und klicken Sie dann die Objekte zu konvertieren [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL Database-Syntax. Weitere Informationen finden Sie unter [Konvertieren von SAP ASE Datenbankobjekte &#40;SybaseToSQL&#41;](../../ssma/sybase/converting-sybase-ase-database-objects-sybasetosql.md).  
  
-   Wählen Sie Objekte für die Datenmigration, und migrieren Sie die Daten aus diesen Objekten zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL-Datenbank. Weitere Informationen finden Sie unter [SAP ASE-Daten in SQL Server - Azure SQL-Datenbank migrieren &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-data-into-sql-server-azure-sql-db-sybasetosql.md).  
  
#### <a name="sql-server-or-sql-azure-metadata-explorer"></a>SQL Server- oder SQL Azure-Metadaten-Explorer  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Metadaten-Explorer zeigt Informationen zu einer Instanz des [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL-Datenbank. Wenn Sie beim Verbinden mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL-Datenbank, SSMA Ruft Metadaten für diese Instanz ab und speichert ihn in der Projektdatei.  
  
Können Sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Metadaten-Explorer konvertierte SAP ASE Datenbankobjekte auswählen, und klicken Sie dann laden (synchronisiert) die Objekte in der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL-Datenbank.  
  
Weitere Informationen finden Sie unter [konvertiert Datenbankobjekte in SQL Server laden &#40;SybaseToSQL&#41;](../../ssma/sybase/loading-converted-database-objects-into-sql-server-sybasetosql.md).  
  
### <a name="metadata"></a>Metadaten  
Sind Sie rechts neben jeder Metadaten-Explorer-Registerkarten, die das ausgewählte Objekt zu beschreiben. Z. B. Wenn Sie eine Tabelle in der Sybase-Metadaten-Explorer auswählen, die sechs Registerkarten angezeigt: **Tabelle**, **SQL**, **Type Mapping**, **Daten**,  **Eigenschaften**, und **Bericht**. Die **Bericht** Registerkarte enthält Informationen, nachdem Sie einen Bericht mit dem ausgewählten Objekt erstellt. Bei Auswahl eine Tabelle in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Metadaten-Explorer die drei Registerkarten angezeigt: **Tabelle**, **SQL**, und **Daten**.  
  
Die meisten Metadateneinstellungen für die sind schreibgeschützt. Sie können jedoch die folgende Metadaten ändern:  
  
-   Sybase-Metadaten-Explorer können Sie Prozeduren alter und Zuordnungen geben. Nehmen Sie diese Änderungen vor, bevor Sie Schemas konvertieren.  
  
-   In [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Metadaten-Explorer können Sie ändern die [!INCLUDE[tsql](../../includes/tsql_md.md)] für gespeicherte Prozeduren. Diese Änderungen vornehmen, bevor Sie die Schemas in laden [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
In einer Metadaten-Explorer vorgenommene Änderungen werden in die Projektmetadaten, nicht in den Quell- oder Zieltabelle Datenbanken wiedergegeben.  
  
### <a name="toolbars"></a>Symbolleisten  
SSMA hat zwei Symbolleisten: ein Projekt Symbolleisten und eine Migration.  
  
#### <a name="the-project-toolbar"></a>Der Projekt-Symbolleiste  
Die Projekt-Symbolleiste enthält Schaltflächen zum Arbeiten mit Projekten, Herstellen einer Verbindung mit SAP ASE und Herstellen einer Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL-Datenbank. Diese Schaltflächen ähneln die Befehle auf den **Datei** Menü.  
  
#### <a name="the-migration-toolbar"></a>Der Migrations-Symbolleiste  
Die Migration-Symbolleiste enthält die folgenden Befehle:  
  
|Schaltfläche|Funktion|  
|----------|------------|  
|**Bericht erstellen**|Konvertiert die ausgewählten SAP ASE Objekte [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Syntax, und erstellt dann einen Bericht, der zeigt, wie erfolgreich das Konvertierung war.<br /><br />Mit diesem Befehl steht nur, wenn Objekte in Sybase-Metadaten-Explorer ausgewählt sind.|  
|**Schema konvertieren**|Konvertiert die ausgewählten SAP ASE Objekte [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL-Datenbankobjekte.<br /><br />Mit diesem Befehl steht nur, wenn Objekte in Sybase-Metadaten-Explorer ausgewählt sind.|  
|**Migrieren von Daten**|Migration von Daten aus der Datenbank SAP ASE [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL-Datenbank. Vor dem Ausführen dieses Befehls müssen Sie die SAP ASE Schemata konvertieren [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL-Datenbank-Schemas, und Laden Sie die Objekte in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL-Datenbank.<br /><br />Mit diesem Befehl steht nur, wenn Objekte in Sybase-Metadaten-Explorer ausgewählt sind.|  
|**Beenden**|Beendet den aktuellen Prozess, z. B. Konvertieren von Objekten zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL Database-Syntax.|  
  
### <a name="menus"></a>Menüs  
SSMA enthält die folgenden Menüs:  
  
|Menü|Description|  
|--------|---------------|  
|**File**|Enthält Befehle zum Arbeiten mit Projekten, Herstellen einer Verbindung mit SAP ASE und Herstellen einer Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL-Datenbank.|  
|**Bearbeiten**|Enthält Befehle zum Suchen nach und Arbeiten mit Text in den Detailseiten, z. B. das Kopieren [!INCLUDE[tsql](../../includes/tsql_md.md)] aus dem SQL-Detailbereich. Enthält auch die **Lesezeichen verwalten** auswählen, wo Sie eine Liste der vorhandenen Lesezeichen finden können. Die Schaltflächen können auf der rechten Seite des Dialogfelds Sie um das Lesezeichen zu verwalten.|  
|**Ansicht**|Enthält die **Synchronisieren der Metadaten-Explorer** Befehl. Hiermit erfolgt die Synchronisierung der Objekte zwischen Sybase-Metadaten-Explorer und [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Metadaten-Explorer. Enthält auch Befehle zum Anzeigen und Ausblenden der **Ausgabe** und **Fehlerliste** Bereiche und eine Option **Layouts** Layouts verwalten.|  
|**Tools**|Enthält Befehle zum Erstellen von Berichten, Exportieren von Daten und Objekte und Daten migrieren. Bietet außerdem Zugriff auf die **globale Einstellungen** und **Projekteinstellungen** Dialogfelder.|  
|**Tester**|Enthält Befehle zum Erstellen von Testfällen, Anzeigen von Testergebnissen und Befehle für die sicherungsverwaltung Datenbank.|  
|**Hilfe**|Bietet Zugriff auf das SSMA-Hilfe und die **zu** (Dialogfeld).|  
  
### <a name="output-pane-and-error-list-pane"></a>Ausgabebereich und den Bereich Fehlerliste  
Die **Ansicht** Menü enthält Befehle zum Umschalten der Sichtbarkeit der im Ausgabebereich und den Bereich Fehlerliste:  
  
-   Im Ausgabebereich enthält statusmeldungen von SSMA bei Objekt Konvertierung, Synchronisierung und Migration von Daten.  
  
-   Der Bereich Fehlerliste zeigt Fehler-, Warn- und informationsmeldungen in einer Liste, die sortiert werden können.  
  
## <a name="see-also"></a>Siehe auch  
[Migrieren von SAP ASE-Datenbanken zu SQLServer – Azure SQL-Datenbank &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
[Referenz zur Benutzeroberfläche &#40;SybaseToSQL&#41;](../../ssma/sybase/user-interface-reference-sybasetosql.md)  
