---
title: "Erste Schritte mit SSMA für Sybase (SybaseToSQL) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: c4098516-f0fc-4690-97bb-3766dfd43156
caps.latest.revision: 10
author: sabotta
ms.author: carlasab
manager: lonnyb
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 6a25db175cd6d67b71a0fc72bde969898e4bdadd
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="getting-started-with-ssma-for-sybase-sybasetosql"></a>Erste Schritte mit SSMA für Sybase (SybaseToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]Migration Assistant (SSMA) für Sybase können Sie schnell konvertieren Sybase Adaptive Server Enterprise (ASE) Datenbankschemas auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Schemas, laden die resultierenden Schemas in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure, und Migrieren von Daten aus Sybase ASE zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure.  
  
Dieses Thema führt während des Installationsvorgangs und anschließend hilft er Sie mit der SSMA-Benutzeroberfläche vertraut zu machen.  
  
## <a name="installing-and-licensing-ssma"></a>Installieren und Lizenzieren von SSMA  
Um SSMA verwenden zu können, müssen Sie zunächst installieren das SSMA-Clientprogramm auf einem Computer, die sowohl der Zielinstanz von Sybase ASE und der Zielinstanz von zugreifen kann [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure. Zum Server Side Datenmigration verwenden zu können, müssen Sie Erweiterung Pack und bei mindestens einer der Sybase-Anbieter (OLE DB oder ADO.NET) installieren, auf dem Computer, auf denen ausgeführt wird [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Diese Komponenten unterstützen die Migration von Daten und die Emulation von Sybase ASE Systemfunktionen. Installationsanweisungen finden Sie unter [Installieren von SSMA für Sybase &#40; SybaseToSQL &#41; ](../../ssma/sybase/installing-ssma-for-sybase-sybasetosql.md).  
  
Um SSMA zu starten, klicken Sie auf **starten**, zeigen Sie auf **Programme**, zeigen Sie auf  **[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Migration Assistant für Sybase**, und wählen Sie dann  **[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Migration Assistant für Sybase**. Zum ersten Mal starten von SSMA, erscheint ein Dialogfeld Lizenzierung. Sie müssen die SSMA mithilfe einer Windows Live ID vor der Verwendung von SSMA lizenzieren. Lizenzierung Anweisungen sind in den installationsanweisungen im enthalten die [Installieren von SSMA für Sybase Client &#40; SybaseToSQL &#41; ](../../ssma/sybase/installing-ssma-for-sybase-client-sybasetosql.md) Thema.  
  
## <a name="ssma-for-sybase-user-interface"></a>SSMA für die Sybase-Benutzeroberfläche  
Nachdem SSMA installiert und lizenziert ist, können Sie SSMA Migrieren von Datenbanken von Sybase ASE zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure. Er erleichtert damit vertraut machen, mit der SSMA-Benutzeroberfläche vor. Das folgende Diagramm zeigt die Benutzeroberfläche für SSMA, einschließlich der Metadaten-Explorer, Metadaten, Symbolleisten, Ausgabebereich und Listenbereich Fehler:  
  
![SSMA für Sybase-Benutzeroberfläche](../../ssma/sybase/media/ssmaforsybaseuserinterface.jpg "SSMA für Sybase-Benutzeroberfläche")  
  
Um eine Migration zu starten, müssen Sie zunächst ein neues Projekt erstellen. Klicken Sie dann die Verbindung zur Sybase ASE. Nach einer erfolgreichen Verbindung wird eine Hierarchie von Datenbanken von Sybase ASE in Sybase-Metadaten-Explorer angezeigt. Sie können dann mit der rechten Maustaste Objekte in Sybase-Metadaten-Explorer zum Ausführen von Aufgaben wie z. B. Berichte erstellen, die Konvertierungen zu bewerten [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure. Außerdem können Sie diese Aufgaben über Symbolleisten und Menüs ausführen.  
  
Sie müssen auch eine Verbindung herstellen mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure. Nach einer erfolgreichen Verbindung eine Hierarchie von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Datenbanken werden in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Metadaten-Explorer. Nach der Konvertierung von Sybase ASE Schemas [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] , oder wählen Sie diese konvertierte Schemas in SQL Azure-Schemas [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Metadaten-Explorer, und Laden Sie die Schemas in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure.  
  
Laden Sie konvertierte Schemas in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure können Sie zurück zu Sybase-Metadaten-Explorer und Migrieren von Daten aus Sybase ASE Datenbanken in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Datenbanken.  
  
Weitere Informationen zu diesen Aufgaben und Informationen zu deren Ausführung finden Sie unter [Sybase ASE Datenbanken migrieren zu SQL Server - Azure SQL-Datenbank &#40; SybaseToSQL &#41; ](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md).  
  
In den folgenden Abschnitten werden die Funktionen von SSMA-Benutzeroberfläche beschrieben.  
  
### <a name="metadata-explorers"></a>Metadaten-Explorer  
SSMA enthält zwei Metadaten-Explorer zum Suchen und Ausführen von Aktionen für Sybase ASE und [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Datenbanken.  
  
#### <a name="sybase-metadata-explorer"></a>Sybase-Metadaten-Explorer  
Sybase-Metadaten-Explorer zeigt Informationen zu Datenbanken auf der Zielinstanz von Sybase ASE.  
  
Mithilfe von Sybase-Metadaten-Explorer können Sie die folgenden Aufgaben ausführen:  
  
-   Durchsuchen Sie die Tabellen in jeder Datenbank.  
  
-   Wählen Sie Objekte für die Konvertierung aus, und klicken Sie dann die Objekte zu konvertieren [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Syntax. Weitere Informationen finden Sie unter [Konvertierung von Sybase ASE Datenbankobjekte &#40; SybaseToSQL &#41; ](../../ssma/sybase/converting-sybase-ase-database-objects-sybasetosql.md).  
  
-   Wählen Sie Objekte für die Datenmigration, und migrieren Sie die Daten aus diesen Objekten zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure. Weitere Informationen finden Sie unter [Migrieren von Sybase ASE Daten in SQL Server - Azure SQL-Datenbank &#40; SybaseToSQL &#41; ](../../ssma/sybase/migrating-sybase-ase-data-into-sql-server-azure-sql-db-sybasetosql.md).  
  
#### <a name="sql-server-or-sql-azure-metadata-explorer"></a>SQL Server- oder SQL Azure-Metadaten-Explorer  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]oder SQL Azure-Metadaten-Explorer zeigt Informationen zu einer Instanz des [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure. Wenn Sie beim Verbinden mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure, SSMA Ruft Metadaten für diese Instanz ab und speichert ihn in der Projektdatei.  
  
Können Sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Metadaten-Explorer konvertierte Sybase ASE Datenbankobjekte auswählen, und klicken Sie dann zu laden (synchronisiert) die Objekte in der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure.  
  
Weitere Informationen finden Sie unter [laden konvertiert-Datenbankobjekte in SQL Server &#40; SybaseToSQL &#41; ](../../ssma/sybase/loading-converted-database-objects-into-sql-server-sybasetosql.md).  
  
### <a name="metadata"></a>Metadaten  
Sind Sie rechts neben jeder Metadaten-Explorer-Registerkarten, die das ausgewählte Objekt zu beschreiben. Z. B. Wenn Sie eine Tabelle in der Sybase-Metadaten-Explorer auswählen, sechs Registerkarten werden angezeigt: **Tabelle**, **SQL**, **Type Mapping**, **Daten, die Eigenschaften** und **Bericht**. Die **Bericht** Registerkarte enthält Informationen, nachdem Sie einen Bericht mit dem ausgewählten Objekt erstellt. Bei Auswahl eine Tabelle in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Metadaten-Explorer, die folgenden drei Registerkarten angezeigt werden: **Tabelle**, **SQL**, und **Daten**.  
  
Die meisten Metadateneinstellungen für die sind schreibgeschützt. Sie können jedoch die folgende Metadaten ändern:  
  
-   Sybase-Metadaten-Explorer können Sie Prozeduren alter und Zuordnungen geben. Sie sollten diese Änderungen vornehmen, bevor Sie Schemas konvertieren.  
  
-   In [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Metadaten-Explorer können Sie ändern die [!INCLUDE[tsql](../../includes/tsql_md.md)] für gespeicherte Prozeduren. Sie sollten diese Änderungen vornehmen, bevor Sie die Schemas in laden [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
In einer Metadaten-Explorer vorgenommene Änderungen werden in die Projektmetadaten, nicht in den Quell- oder Zieltabelle Datenbanken wiedergegeben.  
  
### <a name="toolbars"></a>Symbolleisten  
SSMA hat zwei Symbolleisten: ein Projekt Symbolleisten und eine Migration.  
  
#### <a name="the-project-toolbar"></a>Der Projekt-Symbolleiste  
Die Projekt-Symbolleiste enthält Schaltflächen zum Arbeiten mit Projekten, Herstellen einer Verbindung mit der Sybase ASE und Herstellen einer Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure. Diese Schaltflächen ähneln die Befehle auf den **Datei** Menü.  
  
#### <a name="migration-toolbar"></a>Migration-Symbolleiste  
Die Migration-Symbolleiste enthält die folgenden Befehle:  
  
|Schaltfläche|Funktion|  
|----------|------------|  
|**Bericht erstellen**|Konvertiert die ausgewählten Sybase ASE Objekte [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Syntax, und erstellt dann einen Bericht, der zeigt, wie erfolgreich das Konvertierung war.<br /><br />Mit diesem Befehl steht nur, wenn Objekte in Sybase-Metadaten-Explorer ausgewählt sind.|  
|**Schema konvertieren**|Konvertiert die ausgewählten Sybase ASE Objekte [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Objekte.<br /><br />Mit diesem Befehl steht nur, wenn Objekte in Sybase-Metadaten-Explorer ausgewählt sind.|  
|**Migrieren von Daten**|Migration von Daten aus der Datenbank Sybase ASE [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure. Vor dem Ausführen dieses Befehls müssen Sie die Sybase zu Schemas konvertieren [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Schemas, und Laden Sie die Objekte in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure.<br /><br />Mit diesem Befehl steht nur, wenn Objekte in Sybase-Metadaten-Explorer ausgewählt sind.|  
|**Beenden**|Beendet den aktuellen Prozess, z. B. Konvertieren von Objekten zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Syntax.|  
  
### <a name="menus"></a>Menüs  
SSMA enthält die folgenden Menüs.  
  
|Menü|Description|  
|--------|---------------|  
|**File**|Enthält Befehle zum Arbeiten mit Projekten, Herstellen einer Verbindung mit der Sybase ASE und Herstellen einer Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure.|  
|**Bearbeiten**|Enthält Befehle zum Suchen nach und Arbeiten mit Text in den Detailseiten, z. B. das Kopieren [!INCLUDE[tsql](../../includes/tsql_md.md)] aus dem SQL-Detailbereich. Enthält auch die **Lesezeichen verwalten** Option eine Liste der vorhandenen Lesezeichen angezeigt, in denen werden. Die Schaltflächen können auf der rechten Seite des Dialogfelds Sie um das Lesezeichen zu verwalten.|  
|**Ansicht**|Enthält die **Synchronisieren der Metadaten-Explorer** Befehl. Hiermit erfolgt die Synchronisierung der Objekte zwischen Sybase-Metadaten-Explorer und [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Metadaten-Explorer. Enthält auch Befehle zum Anzeigen und Ausblenden der **Ausgabe** und **Fehlerliste** Bereiche und eine Option **Layouts** Layouts verwalten.|  
|**Tools**|Enthält Befehle zum Erstellen von Berichten, Exportieren von Daten und Objekte und Daten migrieren. Bietet außerdem Zugriff auf die **globale Einstellungen** und **Projekteinstellungen** Dialogfelder.|  
|**Tester**|Enthält Befehle zum Erstellen von Testfällen, Anzeigen von Testergebnissen und Befehle für die sicherungsverwaltung Datenbank.|  
|**Hilfe**|Bietet Zugriff auf das SSMA-Hilfe und die **zu** (Dialogfeld).|  
  
### <a name="output-pane-and-error-list-pane"></a>Ausgabebereich und Fehler Listenbereich  
Die **Ansicht** Menü enthält Befehle zum Umschalten der Sichtbarkeit der im Ausgabebereich und den Bereich Fehlerliste:  
  
-   Im Ausgabebereich enthält statusmeldungen von SSMA bei Objekt Konvertierung, Synchronisierung und Migration von Daten.  
  
-   Der Bereich Fehlerliste zeigt Fehler-, Warn- und informationsmeldungen in einer Liste, die sortiert werden können.  
  
## <a name="see-also"></a>Siehe auch  
[Migrieren von Sybase ASE-Datenbanken zu SQLServer - Azure SQL-Datenbank &#40; SybaseToSQL &#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
[Referenz zur Benutzeroberfläche &#40; SybaseToSQL &#41;](../../ssma/sybase/user-interface-reference-sybasetosql.md)  
  

