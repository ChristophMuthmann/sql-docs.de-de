---
title: "Erste Schritte mit SQL Server Migration Assistant für Access | Microsoft Docs"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 08/15/2017
ms.reviewer: 
ms.suite: 
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- error list pane
- getting started
- menus
- metadata explorers
- output pane
- toolbars
- user interface
- user interface overview
ms.assetid: 462a731f-08f1-44e1-9eeb-4deac6d2f6c5
caps.latest.revision: "24"
author: Shamikg
ms.author: Shamikg
manager: murato
ms.workload: On Demand
ms.openlocfilehash: 5a2959f1904fb878f497eecfc6fe93802bee0941
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="getting-started-with-sql-server-migration-assistant-for-access-accesstosql"></a>Erste Schritte mit SQL Server Migration Assistant für Access (AccessToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]Migration Assistant (SSMA) for Access ermöglicht den Zugriff auf Datenbankobjekte zu schnell Konvertierung [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL-Datenbank Objekte, hochladen, die resultierenden Objekte in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL-Datenbank, und Migrieren von Daten aus den Zugriff auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL-Datenbank. Wenn erforderlich, Sie auch den Zugriff auf Tabellen zu verknüpfen können [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL-Datenbank Tabellen, sodass Sie den Vorgang fortsetzen können, verwenden Sie die vorhandenen Access-Front-End-Anwendungen mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL-Datenbank.  
  
Dieses Thema führt während des Installationsvorgangs und trägt dazu bei, die um Sie mit der SSMA-Benutzeroberfläche vertraut zu machen.  
  
## <a name="installing-ssma"></a>Installieren SSMA  
Um SSMA verwenden zu können, müssen Sie zunächst installieren das SSMA-Clientprogramm auf einem Computer, die beide Datenbanken zugreifen können Sie migrieren möchten, und der Zielinstanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL-Datenbank. Installationsanweisungen finden Sie unter [Installieren von SQL Server Migration Assistant für Access &#40; AccessToSQL &#41; ](../../ssma/access/installing-sql-server-migration-assistant-for-access-accesstosql.md).  
  
Um SSMA zu starten, klicken Sie auf **starten**, zeigen Sie auf **Programme**, zeigen Sie auf **SQL Server Migration Assistant für Access**, und wählen Sie dann **SQL Server Migration Assistant für Access**.  
  
## <a name="using-ssma"></a>Verwenden von SSMA  
Nach der Installation von SSMA werden können, um mit der SSMA-Benutzeroberfläche vertraut vor dem Verwenden des Tools zum Migrieren von Access-Datenbanken zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL-Datenbank. Die SSMA-Benutzeroberfläche, einschließlich der Metadaten-Explorer, Metadaten, Symbolleisten, Ausgabebereich und Listenbereich Fehler werden in der folgenden Abbildung gezeigt:  
  
![SSMA für Access-Benutzeroberfläche](../../ssma/access/media/ssmaforaccessgui.gif "SSMA für Access-Benutzeroberfläche")  
  
Um eine Migration zu starten, Erstellen eines neuen Projekts, und dann Access-Datenbanken Zugriff Metadaten-Explorer hinzufügen. Sie können Objekte in den Metadaten-Explorer zum Ausführen von Aufgaben wie z. B. den Zugriff per Rechtsklick:
- Exportieren eine Inventur der Zugriff auf Datenbankobjekte zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL-Datenbank.
- Erstellen von Berichten, die Bewertung der Konvertierungen in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL-Datenbank.
- Konvertieren von Access-Schemas zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL-Datenbank-Schemas.

Sie können auch diese Aufgaben ausführen, mit dem Symbolleisten und Menüs.  
  
Sie müssen auch eine Verbindung herstellen mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Nach einer erfolgreichen Verbindung eine Hierarchie von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbanken wird im [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Metadaten-Explorer. Nach der Konvertierung von Access-Schemas zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Schemas, wählen Sie die konvertierte Schemas in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Metadaten-Explorer, und Laden Sie die Schemas in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
Wenn Sie Azure SQL-Datenbank aus der Migration auf die Dropdownliste im Dialogfeld Neues Projekt ausgewählt haben, müssen Sie mit Azure SQL-Datenbank verbinden. Nach einer erfolgreichen Verbindung wird Sie eine Hierarchie von Azure SQL-Datenbank-Datenbanken in Azure SQL-DB-Metadaten-Explorer angezeigt. Nachdem Sie Schemas für den Zugriff auf Azure SQL-Datenbank-Schemas konvertieren, können Sie diese konvertierte Schemas in Azure SQL-DB-Metadaten-Explorer auswählen und Laden Sie die Schemas in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
Laden Sie konvertierte Schemas in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL-Datenbank, können Sie zurück zu Access-Metadaten-Explorer und Migrieren von Daten aus Access-Datenbanken in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL-Datenbank-Datenbanken. Wenn erforderlich, Sie auch den Zugriff auf Tabellen zu verknüpfen können [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Tabellen für Azure SQL-Datenbank.  
  
Weitere Informationen zu diesen Aufgaben und Informationen zu deren Ausführung finden Sie unter den folgenden Themen:  
  
-   [Access-Datenbanken vorbereitet für die Migration.](http://msdn.microsoft.com/9b80a9e0-08e7-4b4d-b5ec-cc998d3f5114)  
  
-   [Migrieren von Access-Datenbanken zu SQLServer](http://msdn.microsoft.com/76a3abcf-2998-4712-9490-fe8d872c89ca)  
  
-   [Verknüpfen von Access-Anwendungen mit SQLServer](http://msdn.microsoft.com/82374ad2-7737-4164-a489-13261ba393d4)  
  
In den folgenden Abschnitten werden die Funktionen von SSMA-Benutzeroberfläche beschrieben.  
  
### <a name="metadata-explorers"></a>Metadaten-Explorer  
SSMA enthält zwei Metadaten-Explorer, die Sie verwenden können, suchen und Ausführen von Aktionen für den Zugriff und [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL-Datenbank-Datenbanken.  
  
#### <a name="access-metadata-explorer"></a>Zugriff auf Metadaten-Explorer  
Access-Metadaten-Explorer zeigt Informationen zu den Access-Datenbanken, die dem Projekt hinzugefügt wurden. Wenn Sie eine Access-Datenbank hinzufügen, ruft SSMA Metadaten über die Datenbank, die Metadaten, die im Metadaten-Explorer für den Zugriff verfügbar ist.  
  
Access-Metadaten-Explorer können Sie die folgenden Aufgaben ausführen:  
  
-   Durchsuchen Sie die Tabellen in jeder Datenbank Zugriff.  
  
-   Wählen Sie Objekte für die Konvertierung aus, und konvertieren Sie die Objekte zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Syntax. Weitere Informationen finden Sie unter [den Zugriff auf Datenbankobjekte konvertieren](http://msdn.microsoft.com/e0ef67bf-80a6-4e6c-a82d-5d46e0623c6c).  
  
-   Wählen Sie Objekte für die Datenmigration, und migrieren Sie die Daten aus diesen Objekten zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Weitere Informationen finden Sie unter [Migrieren von Access-Daten in SQL Server](http://msdn.microsoft.com/f3b18af7-1af0-499d-a00d-a0af94895625).  
  
-   Verknüpfen und Aufheben der Verknüpfung Zugriff und [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Tabellen.  
  
#### <a name="sql-server-or-azure-sql-db-metadata-explorer"></a>SQLServer oder Azure SQL-DB-Metadaten-Explorer  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]oder Azure SQL-DB-Metadaten-Explorer zeigt Informationen zu einer Instanz des [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL-Datenbank. Wenn Sie beim Verbinden mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL-Datenbank, SSMA Ruft Metadaten für diese Instanz ab und speichert ihn in der Projektdatei.  
  
Können Sie die SQL Server- oder Azure SQL-DB-Metadaten-Explorer konvertierte den Zugriff auf Datenbankobjekte auswählen, und laden (synchronisiert) die Objekte in der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL-Datenbank.  
  
Weitere Informationen finden Sie unter [konvertiert Datenbankobjekte in SQL Server laden](http://msdn.microsoft.com/4e854eee-b10c-4f0b-9d9e-d92416e6f2ba).  
  
### <a name="metadata"></a>Metadaten  
Sind Sie rechts neben jeder Metadaten-Explorer-Registerkarten, die das ausgewählte Objekt zu beschreiben. Z. B. Wenn Sie eine Tabelle in der Access-Metadaten-Explorer auswählen, die vier Registerkarten angezeigt: **Tabelle**, **Type Mapping**, **Eigenschaften**, und **Daten**. Bei Auswahl eine Tabelle in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Metadaten-Explorer die drei Registerkarten angezeigt: **Tabelle**, **SQL**, und **Daten**.  
  
Die meisten Metadateneinstellungen für die sind schreibgeschützt. Sie können jedoch die folgende Metadaten ändern:  
  
-   In Access-Metadaten-Explorer können Sie die Zuordnungen ändern. Achten Sie darauf, dass Sie diese Änderungen vorzunehmen, bevor Sie Berichte erstellen, oder Konvertieren von Schemas.  
  
-   In [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Metadaten-Explorer können Sie Tabellen- und Eigenschaften ändern, auf die **Tabelle** Registerkarte. Diese Änderungen vornehmen, bevor Sie die Schemas in laden [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Weitere Informationen finden Sie unter [den Zugriff auf Datenbankobjekte konvertieren](http://msdn.microsoft.com/e0ef67bf-80a6-4e6c-a82d-5d46e0623c6c).  
  
### <a name="toolbars"></a>Symbolleisten  
SSMA hat zwei Symbolleisten: ein Projekt Symbolleisten und eine Migration.  
  
#### <a name="the-project-toolbar"></a>Der Projekt-Symbolleiste  
Die Projekt-Symbolleiste enthält Schaltflächen zum Arbeiten mit Projekten, Hinzufügen von Access-Datenbankdateien und Herstellen einer Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL-Datenbank. Diese Schaltflächen ähneln die Befehle auf den **Datei** Menü.  
  
#### <a name="the-migration-toolbar"></a>Der Migrations-Symbolleiste  
Die Migration-Symbolleiste enthält die folgenden Befehle:  
  
|Schaltfläche|Funktion|  
|----------|------------|  
|**Convert, Load, and Migrate (Konvertieren, Laden und Migrieren)**|Konvertiert den Zugriff auf Datenbanken, lädt die konvertierten Objekte in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL-Datenbank, und Migrieren von Daten in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL-Datenbank, in einem Schritt.|  
|**Bericht erstellen**|Konvertiert das ausgewählte Schema für den Zugriff auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder eine ungültige Syntax für Azure SQL-Datenbank, und klicken Sie dann einen Bericht, der zeigt, wie erfolgreich die Konvertierung wurde erstellt.<br /><br />Mit diesem Befehl steht nur, wenn Objekte im Access-Metadaten-Explorer ausgewählt werden.|  
|**Schema konvertieren**|Konvertiert das ausgewählte Schema für den Zugriff auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL-Datenbank-Schemas.<br /><br />Mit diesem Befehl steht nur, wenn Objekte im Access-Metadaten-Explorer ausgewählt werden.|  
|**Migrieren von Daten**|Migration von Daten aus der Access-Datenbank zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL-Datenbank. Vor dem Ausführen dieses Befehls müssen Sie die Access-Schemas zum Konvertieren [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL-Datenbank-Schemas, und Laden Sie die Objekte in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL-Datenbank.<br /><br />Mit diesem Befehl steht nur, wenn Objekte im Access-Metadaten-Explorer ausgewählt werden.|  
|**Beenden**|Beendet den aktuellen Prozess, z. B. Konvertieren von Objekten zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder eine ungültige Syntax für Azure SQL-Datenbank.|  
  
### <a name="menus"></a>Menüs  
SSMA enthält die folgenden Menüs:  
  
|Menü|Description|  
|--------|---------------|  
|**File**|Befehle für die Migrations-Assistenten arbeiten mit Projekten, hinzufügen und Entfernen von Access-Datenbankdateien und das Herstellen einer Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL-Datenbank.|  
|**Bearbeiten**|Enthält Befehle zum Suchen nach und Arbeiten mit Text in den Detailseiten, z. B. das Kopieren [!INCLUDE[tsql](../../includes/tsql_md.md)] aus dem SQL-Detailbereich. So öffnen die **Lesezeichen verwalten** Dialogfeld klicken Sie im Menü Bearbeiten, klicken Sie auf Verwalten von Lesezeichen. Klicken Sie im Dialogfeld sehen Sie eine Liste der vorhandenen Lesezeichen. Die Schaltflächen können auf der rechten Seite des Dialogfelds Sie um das Lesezeichen zu verwalten.|  
|**Sicht**|Enthält die **Synchronisieren der Metadaten-Explorer** Befehl. Hiermit erfolgt die Synchronisierung der Objekte zwischen Access-Metadaten-Explorer und [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL-DB-Metadaten-Explorer. Enthält auch Befehle zum Anzeigen und Ausblenden der **Ausgabe** und **Fehlerliste** Bereiche und eine Option **Layouts** mit Layouts verwalten.|  
|**Tools**|Enthält Befehle zum Erstellen von Berichten, Exportieren von Daten, Objekte und Daten migrieren, verknüpfen Sie Tabellen, und stellt den Zugriff auf globale und projekteinstellungen Dialogfelder bereit.|  
|**Hilfe**|Bietet Zugriff auf das SSMA-Hilfe und die **zu** (Dialogfeld).|  
  
### <a name="output-pane-and-error-list-pane"></a>Ausgabebereich und den Bereich Fehlerliste  
Die **Ansicht** Menü enthält Befehle zum Umschalten der Sichtbarkeit der im Ausgabebereich und den Bereich Fehlerliste:  
  
-   Im Ausgabebereich enthält statusmeldungen von SSMA bei Objekt Konvertierung, Synchronisierung und Migration von Daten.  
  
-   Der Bereich Fehlerliste zeigt Fehler-, Warn- und informationsmeldungen in einer Liste, die sortiert werden können.  
  
## <a name="see-also"></a>Siehe auch  
[Migrieren von Access-Datenbanken zu SQLServer](http://msdn.microsoft.com/76a3abcf-2998-4712-9490-fe8d872c89ca)  
  
