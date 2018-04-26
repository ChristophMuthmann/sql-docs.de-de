---
title: Erste Schritte mit SSMA für DB2 (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-db2
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 48ca32fc-1830-4d1f-add7-480ba5ad02e8
caps.latest.revision: 6
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 11e0869f3e15c01337f2e86cb3294cbf9c94eb5b
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="getting-started-with-ssma-for-db2-db2tosql"></a>Erste Schritte mit SSMA für DB2 (DB2ToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Migration Assistant (SSMA) DB2 können Sie schnell zu DB2-Datenbank-Schemas konvertieren [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Schemas Hochladen der resultierenden Schemas in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] und Migrieren von Daten aus DB2 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
Dieses Thema führt während des Installationsvorgangs und anschließend hilft er Sie mit der SSMA-Benutzeroberfläche vertraut zu machen.  
  
## <a name="installing-ssma"></a>Installieren SSMA  
Um SSMA verwenden zu können, müssen Sie zunächst installieren das SSMA-Clientprogramm auf einem Computer, die die DB2-Quelldatenbank und der Zielinstanz von zugreifen kann [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. DB2 OLE DB-Anbieter auf dem Computer, auf denen ausgeführt wird, ist [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Diese Komponenten unterstützen die Migration von Daten und die Emulation der DB2-Systemfunktionen. Installationsanweisungen finden Sie unter [Installieren von SSMA für DB2 &#40;DB2ToSQL&#41;](../../ssma/db2/installing-ssma-for-db2-db2tosql.md).  
  
Um SSMA zu starten, klicken Sie auf **starten**, zeigen Sie auf **Programme**, zeigen Sie auf  **[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Migration Assistant für DB2**, und klicken Sie dann auf  **[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Migration Assistant für DB2**.  
  
## <a name="ssma-for-db2-user-interface"></a>SSMA für die DB2-Benutzeroberfläche  
Nachdem SSMA installiert ist, können Sie mithilfe von SSMA um DB2-Datenbanken zu migrieren [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Er erleichtert damit vertraut machen, mit der SSMA-Benutzeroberfläche vor. Das folgende Diagramm zeigt die Benutzeroberfläche für SSMA, einschließlich der Metadaten-Explorer, Metadaten, Symbolleisten, Ausgabebereich und Listenbereich Fehler:  
  
![SSMA-Benutzeroberfläche](../../ssma/db2/media/ssma_db2_ui.png "SSMA-Benutzeroberfläche")  
  
Um eine Migration zu starten, müssen Sie zunächst ein neues Projekt erstellen. Anschließend verbinden Sie sich mit einer DB2-Datenbank. Nach einer erfolgreichen Verbindung werden der DB2-Schemas in DB2-Metadaten-Explorer angezeigt. Sie können dann mit der rechten Maustaste Objekte in DB2-Metadaten-Explorer zum Ausführen von Aufgaben wie z. B. Berichte erstellen, die Bewertung der Konvertierungen in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Sie können auch diese Aufgaben ausführen, mit dem Symbolleisten und Menüs.  
  
Sie müssen auch eine Verbindung herstellen mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Nach einer erfolgreichen Verbindung eine Hierarchie von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbanken erscheint im [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Metadaten-Explorer. Nachdem Sie die Konvertierung zu DB2-Schemas [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Schemas, wählen Sie die konvertierte Schemas in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Metadaten-Explorer, und synchronisieren Sie die Schemas mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
Nach dem Synchronisieren von konvertierten Schemas mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], können Sie zurück zu DB2-Metadaten-Explorer und Migrieren von Daten aus DB2-Schemas in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbanken.  
  
Weitere Informationen zu diesen Aufgaben und Informationen zu deren Ausführung finden Sie unter [DB2-Datenbanken zu SQL Server Migration &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md).  
  
In den folgenden Abschnitten werden die Funktionen von SSMA-Benutzeroberfläche beschrieben.  
  
### <a name="metadata-explorers"></a>Metadaten-Explorer  
SSMA enthält zwei Metadaten-Explorer zum Suchen und Ausführen von Aktionen für DB2 und [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbanken.  
  
#### <a name="db2-metadata-explorer"></a>DB2-Metadaten-Explorer  
DB2-Metadaten-Explorer zeigt Informationen zu DB2-Schemas. Mithilfe von DB2-Metadaten-Explorer können Sie die folgenden Aufgaben ausführen:  
  
-   Durchsuchen Sie die Objekte in den einzelnen Schemas.  
  
-   Wählen Sie Objekte für die Konvertierung aus, und klicken Sie dann die Objekte zu konvertieren [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Syntax. Weitere Informationen finden Sie unter [DB2-Schemas konvertieren &#40;DB2ToSQL&#41;](../../ssma/db2/converting-db2-schemas-db2tosql.md).  
  
-   Wählen Sie die Tabellen für die Datenmigration, und migrieren Sie die Daten aus diesen Tabellen in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Weitere Informationen finden Sie unter [DB2-Datenbanken zu SQL Server Migration &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md).  
  
#### <a name="sql-server-metadata-explorer"></a>SQL Server-Metadaten-Explorer  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Metadaten-Explorer zeigt Informationen zu einer Instanz des [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Wenn Sie beim Verbinden mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], SSMA Ruft Metadaten für diese Instanz ab und speichert sie in der Projektdatei.  
  
Sie können [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Metadaten-Explorer, um die konvertierte DB2-Datenbankobjekte auswählen und dann diese Objekte mit der Instanz von synchronisieren [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
### <a name="metadata"></a>Metadaten  
Sind Sie rechts neben jeder Metadaten-Explorer-Registerkarten, die das ausgewählte Objekt zu beschreiben. Z. B. Wenn Sie eine Tabelle in DB2-Metadaten-Explorer auswählen, sechs Registerkarten werden angezeigt: **Tabelle**, **SQL**, **Type Mapping, Bericht**, **Eigenschaften**, und **Daten**. Die **Bericht** Registerkarte enthält Informationen, nachdem Sie einen Bericht erstellen, die das ausgewählte Objekt enthält. Bei Auswahl eine Tabelle in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Metadaten-Explorer die drei Registerkarten werden angezeigt: **Tabelle**, **SQL**, und **Daten**.  
  
Die meisten Metadateneinstellungen für die sind schreibgeschützt. Sie können jedoch die folgende Metadaten ändern:  
  
-   In DB2-Metadaten-Explorer können Sie Prozeduren alter und datentypzuordnungen. Um die geänderten Verfahren konvertieren, und geben Sie die Zuordnungen, können nehmen Sie Änderungen vor, bevor Sie Schemas konvertieren.  
  
-   In [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Metadaten-Explorer können Sie ändern die [!INCLUDE[tsql](../../includes/tsql_md.md)] für gespeicherte Prozeduren. Diese Änderungen im anzeigen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], diese Änderungen vornehmen, bevor Sie die Schemas in laden [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
In einer Metadaten-Explorer vorgenommene Änderungen werden in die Projektmetadaten, nicht in den Quell- oder Zieltabelle Datenbanken wiedergegeben.  
  
### <a name="toolbars"></a>Symbolleisten  
SSMA hat zwei Symbolleisten: ein Projekt Symbolleisten und eine Migration.  
  
#### <a name="the-project-toolbar"></a>Der Projekt-Symbolleiste  
Die Projekt-Symbolleiste enthält Schaltflächen zum Arbeiten mit Projekten, Herstellen einer Verbindung mit DB2 und Herstellen einer Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Diese Schaltflächen ähneln die Befehle auf den **Datei** Menü.  
  
#### <a name="migration-toolbar"></a>Migration-Symbolleiste  
Die folgende Tabelle zeigt die Migration Symbolleistenbefehle:  
  
|Schaltfläche|Funktion|  
|------|--------|  
|**Bericht erstellen**|Konvertiert die ausgewählten DB2-Objekte zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Syntax, und erstellt dann einen Bericht, der zeigt, wie erfolgreich das Konvertierung war.<br /><br />Dieser Befehl ist deaktiviert, es sei denn, die Objekte in DB2-Metadaten-Explorer ausgewählt werden.|  
|**Schema konvertieren**|Konvertiert die ausgewählten DB2-Objekte zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Objekte.<br /><br />Dieser Befehl ist deaktiviert, es sei denn, die Objekte in DB2-Metadaten-Explorer ausgewählt werden.|  
|**Migrieren von Daten**|Migration von Daten aus der Datenbank DB2 zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Vor dem Ausführen dieses Befehls müssen Sie die DB2-Schemas zum Konvertieren [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Schemas, und Laden Sie die Objekte in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].<br /><br />Dieser Befehl ist deaktiviert, es sei denn, die Objekte in DB2-Metadaten-Explorer ausgewählt werden.|  
|**Beenden**|Hält den aktuellen Prozess an.|  
  
### <a name="menus"></a>Menüs  
Die folgende Tabelle zeigt die SSMA-Menüs.  
  
|Menü|Description|  
|----|-----------|  
|**File**|Enthält Befehle zum Arbeiten mit Projekten, Herstellen einer Verbindung mit DB2 und Herstellen einer Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].|  
|**Bearbeiten**|Enthält Befehle zum Suchen nach und Arbeiten mit Text in den Detailseiten, z. B. das Kopieren [!INCLUDE[tsql](../../includes/tsql_md.md)] aus dem SQL-Detailbereich. Enthält auch die **Lesezeichen verwalten** Option eine Liste der vorhandenen Lesezeichen angezeigt, in denen werden. Die Schaltflächen können auf der rechten Seite des Dialogfelds Sie um das Lesezeichen zu verwalten.|  
|**Ansicht**|Enthält die **Synchronisieren der Metadaten-Explorer** Befehl. Die die Objekte zwischen DB2-Metadaten-Explorer synchronisiert und [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Metadaten-Explorer. Enthält auch Befehle anzeigen oder Ausblenden der **Ausgabe** und **Fehlerliste** Bereiche und eine Option **Layouts** Layouts verwalten.|  
|**Tools**|Enthält Befehle zum Erstellen von Berichten und Migrieren von Objekten und Daten. Bietet außerdem Zugriff auf die **globale Einstellungen** und **Projekteinstellungen** Dialogfelder.|  
|**Hilfe**|Bietet Zugriff auf das SSMA-Hilfe und die **zu** (Dialogfeld).|  
  
### <a name="output-pane-and-error-list-pane"></a>Ausgabebereich und Fehler Listenbereich  
Die **Ansicht** Menü enthält Befehle zum Umschalten der Sichtbarkeit der im Ausgabebereich und den Bereich Fehlerliste:  
  
-   Im Ausgabebereich enthält statusmeldungen von SSMA bei Objekt Konvertierung, Synchronisierung und Migration von Daten.  
  
-   Bereich Fehlerliste werden Fehler-, Warn- und informationsmeldungen in einem sortierbaren angezeigt.  
  
## <a name="see-also"></a>Siehe auch  
[Migrieren von DB2-Daten in SQLServer &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-data-into-sql-server-db2tosql.md)  
[Referenz zur Benutzeroberfläche &#40;DB2ToSQL&#41;](../../ssma/db2/user-interface-reference-db2tosql.md)  
  
