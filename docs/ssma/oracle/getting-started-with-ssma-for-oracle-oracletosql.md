---
title: "Erste Schritte mit SSMA für Oracle (OracleToSQL) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-oracle
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SSMA for Oracle, Metadata Explorers
- SSMA for Oracle, Toolbars
ms.assetid: df79664c-972e-4bef-865a-ce609789fee7
caps.latest.revision: "9"
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: On Demand
ms.openlocfilehash: 1765ceb5cb1f4100d60a0f429635f9fc80d14e82
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="getting-started-with-ssma-for-oracle-oracletosql"></a>Erste Schritte mit SSMA für Oracle (OracleToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]Migration Assistant (SSMA) für Oracle können Sie schnell, konvertieren Sie Oracle-Datenbankschemas auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Schemas Hochladen der resultierenden Schemas in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] und Migrieren von Daten aus Oracle in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
Dieses Thema führt während des Installationsvorgangs und anschließend hilft er Sie mit der SSMA-Benutzeroberfläche vertraut zu machen.  
  
## <a name="installing-ssma"></a>Installieren SSMA  
Um SSMA verwenden zu können, müssen Sie zunächst installieren das SSMA-Clientprogramm auf einem Computer, auf die Oracle-Quelldatenbank und die Zielinstanz des zugreifen kann [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Dann müssen Sie eine Erweiterung Pack und installieren mindestens einer der Oracle-Anbieter (OLE DB oder [!INCLUDE[vstecado](../../includes/vstecado_md.md)]) auf dem Computer, auf denen ausgeführt wird, ist [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Diese Komponenten unterstützen die Migration von Daten und die Emulation der Oracle-Systemfunktionen. Installationsanweisungen finden Sie unter [Installieren von SSMA für Oracle &#40; OracleToSQL &#41;](../../ssma/oracle/installing-ssma-for-oracle-oracletosql.md).  
  
Um SSMA zu starten, klicken Sie auf **starten**, zeigen Sie auf **Programme**, zeigen Sie auf  **[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Migration Assistant für Oracle**, und klicken Sie dann auf  **[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Migration Assistant für Oracle**.  
  
## <a name="ssma-for-oracle-user-interface"></a>SSMA für die Oracle-Benutzeroberfläche  
Nachdem SSMA installiert ist, können Sie SSMA Migrieren von Oracle-Datenbanken zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Er erleichtert damit vertraut machen, mit der SSMA-Benutzeroberfläche vor. Das folgende Diagramm zeigt die Benutzeroberfläche für SSMA, einschließlich der Metadaten-Explorer, Metadaten, Symbolleisten, Ausgabebereich und Listenbereich Fehler:  
  
![SSMA für die Oracle-Benutzeroberfläche](../../ssma/oracle/media/ssma_oracle_ui.jpg "SSMA für die Oracle-Benutzeroberfläche")  
  
Um eine Migration zu starten, müssen Sie zunächst ein neues Projekt erstellen. Anschließend verbinden Sie mit einer Oracle-Datenbank. Nach einer erfolgreichen Verbindung werden die Oracle-Schemas in Oracle-Metadaten-Explorer angezeigt. Sie können dann mit der rechten Maustaste-Objekte in der Oracle-Metadaten-Explorer zum Ausführen von Aufgaben wie z. B. Berichte erstellen, die Bewertung der Konvertierungen in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Sie können auch diese Aufgaben ausführen, mit dem Symbolleisten und Menüs.  
  
Sie müssen auch eine Verbindung herstellen mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Nach einer erfolgreichen Verbindung eine Hierarchie von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbanken erscheint im [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Metadaten-Explorer. Nachdem Sie die Konvertierung zu Oracle-Schemas [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Schemas, wählen Sie die konvertierte Schemas in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Metadaten-Explorer, und synchronisieren Sie die Schemas mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
Nach dem Synchronisieren von konvertierten Schemas mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], können Sie zurück zu Oracle-Metadaten-Explorer und Migrieren von Daten aus Oracle-Schemas in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbanken.  
  
Weitere Informationen zu diesen Aufgaben und Informationen zu deren Ausführung finden Sie unter [Migrieren von Oracle-Datenbanken zu SQL Server &#40; OracleToSQL &#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md).  
  
In den folgenden Abschnitten werden die Funktionen von SSMA-Benutzeroberfläche beschrieben.  
  
### <a name="metadata-explorers"></a>Metadaten-Explorer  
SSMA enthält zwei Metadaten-Explorer zum Suchen und Ausführen von Aktionen für Oracle und [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbanken.  
  
#### <a name="oracle-metadata-explorer"></a>Oracle-Metadaten-Explorer  
Oracle-Metadaten-Explorer zeigt Informationen zu Oracle-Schemas. Mithilfe der Oracle-Metadaten-Explorer können Sie die folgenden Aufgaben ausführen:  
  
-   Durchsuchen Sie die Objekte in den einzelnen Schemas.  
  
-   Wählen Sie Objekte für die Konvertierung aus, und klicken Sie dann die Objekte zu konvertieren [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Syntax. Weitere Informationen finden Sie unter [Oracle-Schemas konvertieren &#40; OracleToSQL &#41;](../../ssma/oracle/converting-oracle-schemas-oracletosql.md).  
  
-   Wählen Sie die Tabellen für die Datenmigration, und migrieren Sie die Daten aus diesen Tabellen in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Weitere Informationen finden Sie unter [Migrieren von Oracle-Daten in SQL Server &#40; OracleToSQL &#41;](../../ssma/oracle/migrating-oracle-data-into-sql-server-oracletosql.md).  
  
#### <a name="sql-server-metadata-explorer"></a>SQL Server-Metadaten-Explorer  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]Metadaten-Explorer zeigt Informationen zu einer Instanz des [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Wenn Sie beim Verbinden mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], SSMA Ruft Metadaten für diese Instanz ab und speichert sie in der Projektdatei.  
  
Sie können [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Metadaten-Explorer, wählen Sie konvertierte Objekte der Oracle-Datenbank, und klicken Sie dann diese Objekte zu synchronisieren, mit der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
Weitere Informationen finden Sie unter [in SQL Server &#40; OracleToSQL &#41; konvertiert Datenbankobjekte laden](../../ssma/oracle/loading-converted-database-objects-into-sql-server-oracletosql.md).  
  
### <a name="metadata"></a>Metadaten  
Sind Sie rechts neben jeder Metadaten-Explorer-Registerkarten, die das ausgewählte Objekt zu beschreiben. Z. B. Wenn Sie eine Tabelle in der Oracle-Metadaten-Explorer auswählen, sechs Registerkarten werden angezeigt: **Tabelle**, **SQL**, **Type Mapping, Bericht**, **Eigenschaften**, und **Daten**. Die **Bericht** Registerkarte enthält Informationen, nachdem Sie einen Bericht erstellen, die das ausgewählte Objekt enthält. Bei Auswahl eine Tabelle in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Metadaten-Explorer die drei Registerkarten werden angezeigt: **Tabelle**, **SQL**, und **Daten**.  
  
Die meisten Metadateneinstellungen für die sind schreibgeschützt. Sie können jedoch die folgende Metadaten ändern:  
  
-   In Oracle-Metadaten-Explorer können Sie Prozeduren alter und datentypzuordnungen. Um die geänderten Verfahren konvertieren, und geben Sie die Zuordnungen, können nehmen Sie Änderungen vor, bevor Sie Schemas konvertieren.  
  
-   In [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Metadaten-Explorer können Sie ändern die [!INCLUDE[tsql](../../includes/tsql_md.md)] für gespeicherte Prozeduren. Diese Änderungen im anzeigen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], diese Änderungen vornehmen, bevor Sie die Schemas in laden [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
In einer Metadaten-Explorer vorgenommene Änderungen werden in die Projektmetadaten, nicht in den Quell- oder Zieltabelle Datenbanken wiedergegeben.  
  
### <a name="toolbars"></a>Symbolleisten  
SSMA hat zwei Symbolleisten: ein Projekt Symbolleisten und eine Migration.  
  
#### <a name="the-project-toolbar"></a>Der Projekt-Symbolleiste  
Die Projekt-Symbolleiste enthält Schaltflächen zum Arbeiten mit Projekten und Herstellen einer Verbindung mit Oracle Herstellen einer Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Diese Schaltflächen ähneln die Befehle auf den **Datei** Menü.  
  
#### <a name="migration-toolbar"></a>Migration-Symbolleiste  
Die folgende Tabelle zeigt die Migration Symbolleistenbefehle:  
  
|Schaltfläche|Funktion|  
|------|--------|  
|**Bericht erstellen**|Konvertiert die ausgewählte Oracle-Objekte zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Syntax, und erstellt dann einen Bericht, der zeigt, wie erfolgreich das Konvertierung war.<br /><br />Dieser Befehl ist deaktiviert, es sei denn, die Objekte in der Oracle-Metadaten-Explorer ausgewählt werden.|  
|**Schema konvertieren**|Konvertiert die ausgewählte Oracle-Objekte zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Objekte.<br /><br />Dieser Befehl ist deaktiviert, es sei denn, die Objekte in der Oracle-Metadaten-Explorer ausgewählt werden.|  
|**Migrieren von Daten**|Migration von Daten aus der Oracle-Datenbank für [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Vor dem Ausführen dieses Befehls müssen Sie die Oracle-Schemas zum Konvertieren [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Schemas, und Laden Sie die Objekte in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].<br /><br />Dieser Befehl ist deaktiviert, es sei denn, die Objekte in der Oracle-Metadaten-Explorer ausgewählt werden.|  
|**Beenden**|Hält den aktuellen Prozess an.|  
  
### <a name="menus"></a>Menüs  
Die folgende Tabelle zeigt die SSMA-Menüs.  
  
|Menü|Description|  
|----|-----------|  
|**Zuletzt geöffnete Dateien**|Enthält Befehle zum Arbeiten mit Projekten und Herstellen einer Verbindung mit Oracle Herstellen einer Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].|  
|**Bearbeiten**|Enthält Befehle zum Suchen nach und Arbeiten mit Text in den Detailseiten, z. B. das Kopieren [!INCLUDE[tsql](../../includes/tsql_md.md)] aus dem SQL-Detailbereich. Enthält auch die **Lesezeichen verwalten** Option eine Liste der vorhandenen Lesezeichen angezeigt, in denen werden. Die Schaltflächen können auf der rechten Seite des Dialogfelds Sie um das Lesezeichen zu verwalten.|  
|**Ansicht**|Enthält die **Synchronisieren der Metadaten-Explorer** Befehl. Die die Objekte zwischen Oracle Metadaten-Explorer synchronisiert und [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Metadaten-Explorer. Enthält auch Befehle anzeigen oder Ausblenden der **Ausgabe** und **Fehlerliste** Bereiche und eine Option **Layouts** Layouts verwalten.|  
|**Tools**|Enthält Befehle zum Erstellen von Berichten und Migrieren von Objekten und Daten. Bietet außerdem Zugriff auf die **globale Einstellungen** und **Projekteinstellungen** Dialogfelder.|  
|**Tester**|Enthält Befehle zum Erstellen und Verwenden von Testfällen, Repository und backup-Management-System.|  
|**Hilfe**|Bietet Zugriff auf das SSMA-Hilfe und die **zu** (Dialogfeld).|  
  
### <a name="output-pane-and-error-list-pane"></a>Ausgabebereich und Fehler Listenbereich  
Die **Ansicht** Menü enthält Befehle zum Umschalten der Sichtbarkeit der im Ausgabebereich und den Bereich Fehlerliste:  
  
-   Im Ausgabebereich enthält statusmeldungen von SSMA bei Objekt Konvertierung, Synchronisierung und Migration von Daten.  
  
-   Bereich Fehlerliste werden Fehler-, Warn- und informationsmeldungen in einem sortierbaren angezeigt.  
  
## <a name="see-also"></a>Siehe auch  
[Migrieren von Oracle-Daten in SQLServer &#40; OracleToSQL &#41;](../../ssma/oracle/migrating-oracle-data-into-sql-server-oracletosql.md)  
[Referenz zur Benutzeroberfläche &#40; OracleToSQL &#41;](../../ssma/oracle/user-interface-reference-oracletosql.md)  
  
