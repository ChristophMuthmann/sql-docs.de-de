---
title: SQL Server-Ziel | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: data-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.dts.designer.sqlserverdest.f1
- sql13.dts.designer.sqlserverdestadapter.connection.f1
- sql13.dts.designer.sqlserverdestadapter.mappings.f1
- sql13.dts.designer.sqlserverdestadapter.advanced.f1
helpviewer_keywords:
- SQL Server destination
- loading data
- destinations [Integration Services], SQL Server
- inserting data
- bulk load [Integration Services]
ms.assetid: a0227cd8-6944-4547-87e8-7b2507e26442
caps.latest.revision: 65
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: abc13529e3883faad8fd3e4191faec1a37162bed
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="sql-server-destination"></a>SQL Server-Ziel
  Das SQL Server-Ziel stellt eine Verbindung mit einer lokalen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank her und kopiert Daten per Massenladen in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Tabellen und -Sichten. Sie können das SQL Server-Ziel nicht in Paketen verwenden, die auf eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank auf einem Remoteserver zugreifen. Die Pakete sollten stattdessen ein OLE DB-Ziel verwenden. Weitere Informationen finden Sie unter [OLE DB Destination](../../integration-services/data-flow/ole-db-destination.md).  
  
## <a name="permissions"></a>Berechtigungen  
 Benutzer, die Pakete ausführen, die das SQL Server-Ziel einschließen, müssen über die Berechtigung "Erstellen globaler Objekte" verfügen. Sie können diese Berechtigung Benutzern erteilen, indem Sie das Tool Lokale Sicherheitsrichtlinie im Menü **Verwaltung** verwenden. Wenn Sie beim Ausführen eines Pakets, das das SQL Server-Ziel verwendet, eine Fehlermeldung erhalten, sollten Sie sicherstellen, dass das Konto, mit dem das Paket ausgeführt wird, über die Berechtigung "Erstellen globaler Objekte" verfügt.  
  
## <a name="bulk-inserts"></a>Masseneinfügungen  
 Wenn Sie versuchen, das SQL Server-Ziel zum Massenladen von Daten in eine Remote-Datenbank von SQL Server zu verwenden, wird eine Fehlermeldung der folgenden Form angezeigt: "Ein OLE DB-Datensatz ist verfügbar." Quelle: "Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client" Hresult: 0x80040E14 Beschreibung: "Massenladen war nicht möglich, weil das SSIS-Dateizuordnungsobjekt 'Global\DTSQLIMPORT' nicht geöffnet werden konnte. Betriebssystemfehlercode 2 (Die angegebene Datei wurde nicht gefunden.). Stellen Sie sicher, dass Sie auf einen lokalen Server mit der Windows-Sicherheit zugreifen.""  
  
 Das SQL Server-Ziel bietet das gleiche Hochgeschwindigkeitseinfügen von Daten in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wie der Masseneinfügungstask. Mit dem SQL Server-Ziel kann jedoch ein Paket Transformationen auf Spaltendaten anwenden, bevor die Daten in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]geladen werden.  
  
 Zum Laden von Daten in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]sollten Sie das Verwenden des SQL Server-Ziels anstelle des OLE DB-Ziels in Erwägung ziehen.  
  
### <a name="bulk-insert-options"></a>Masseneinfügungsoptionen  
 Falls das SQL Server-Ziel einen Datenzugriffsmodus für schnelles Laden verwendet, können Sie die folgenden Optionen für schnelles Laden angeben:  
  
-   Identitätswerte aus der importierten Datendatei beibehalten oder von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]zugewiesene eindeutige Werte verwenden.  
  
-   NULL-Werte während des Massenladevorgangs beibehalten.  
  
-   Während des Massenimportvorgangs Einschränkungen der Zieltabelle oder -sicht überprüfen.  
  
-   Sperre auf Tabellenebene für die Dauer des Massenladevorgangs abrufen.  
  
-   INSERT-Trigger, die für die Zieltabelle definiert sind, während des Massenladevorgangs ausführen.  
  
-   Die Nummer der ersten Zeile in der Eingabe angeben, die während des Masseneinfügungsvorgangs geladen werden soll.  
  
-   Die Nummer der letzten Zeile in der Eingabe angeben, die während des Masseneinfügungsvorgangs geladen werden soll.  
  
-   Die maximal zulässige Anzahl von Fehlern angeben, bevor der Massenladevorgang abgebrochen wird. Jede Zeile, die nicht importiert werden kann, wird als ein Fehler gezählt.  
  
-   Die Spalten in der Eingabe angeben, die sortierte Daten enthalten.  
  
 Weitere Informationen zu Massenladeoptionen finden Sie unter [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md).  
  
#### <a name="performance-improvements"></a>Leistungsverbesserungen  
 Sie sollten die Standardoptionen wie folgt ändern, um die Leistung einer Masseneinfügung und des Zugriffs auf Tabellendaten während des Masseneinfügungsvorgangs zu verbessern:  
  
-   Überprüfen Sie während des Massenimportvorgangs keine Einschränkungen der Zieltabelle oder -sicht.  
  
-   Führen Sie während des Massenladevorgangs keine INSERT-Trigger aus, die für die Zieltabelle definiert sind.  
  
-   Wenden Sie keine Sperre auf die Tabelle an. Auf diese Weise ist die Tabelle während des Masseneinfügungsvorgangs weiterhin für andere Benutzer und Anwendungen verfügbar.  
  
## <a name="configuration-of-the-sql-server-destination"></a>Konfiguration des SQL Server-Ziels  
 Es gibt folgende Möglichkeiten, um das SQL Server-Ziel zu konfigurieren:  
  
-   Geben Sie die Tabelle oder Sicht an, in die die Daten massengeladen werden sollen.  
  
-   Passen Sie den Massenladevorgang durch Angeben von Optionen an, wie z. B., ob Einschränkungen überprüft werden sollen.  
  
-   Geben Sie an, ob für alle Zeilen ein Commit in einem Batch ausgeführt werden soll, oder legen Sie die maximale Anzahl von Zeilen fest, für die ein Commit als Batch ausgeführt werden soll.  
  
-   Geben Sie ein Timeout für den Massenladevorgang an.  
  
 Dieses Ziel verwendet einen OLE DB-Verbindungs-Manager zum Herstellen einer Verbindung mit einer Datenquelle, und der Verbindungs-Manager gibt den zu verwendenden OLE DB-Anbieter an. Weitere Informationen finden Sie unter [OLE DB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md).  
  
 Ein [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekt stellt auch das Datenquellenobjekt bereit, von dem Sie einen OLE DB-Verbindungs-Manager erstellen können. Auf diese Weise sind Datenquellen und Datenquellensichten für das SQL Server-Ziel verfügbar.  
  
 Das SQL Server-Ziel besitzt eine Eingabe. Eine Fehlerausgabe wird nicht unterstützt.  
  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Das Dialogfeld **Erweiterter Editor** enthält die Eigenschaften, die programmgesteuert festgelegt werden können. Klicken Sie auf eines der folgenden Themen, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im Dialogfeld **Erweiterter Editor** oder programmgesteuert festlegen können:  
  
-   [Common Properties](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Benutzerdefinierte Eigenschaften des SQL Server-Ziels](../../integration-services/data-flow/sql-server-destination-custom-properties.md)  
  
 Klicken Sie auf eines der folgenden Themen, um weitere Informationen zum Festlegen von Eigenschaften anzuzeigen:  
  
-   [Massenladen von Daten mithilfe des SQL Server-Ziels](../../integration-services/data-flow/bulk-load-data-by-using-the-sql-server-destination.md)  
  
-   [Festlegen der Eigenschaften einer Datenflusskomponente](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [Massenladen von Daten mithilfe des SQL Server-Ziels](../../integration-services/data-flow/bulk-load-data-by-using-the-sql-server-destination.md)  
  
-   [Festlegen der Eigenschaften einer Datenflusskomponente](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-content"></a>Verwandte Inhalte  
  
-   Technischer Artikel [Möglicherweise wird bei UAC-fähigen Systemen der Fehler "Die SSIS-Masseneinfügung kann zum Einfügen von Daten nicht vorbereitet werden" angezeigt](http://go.microsoft.com/fwlink/?LinkId=199482)auf support.microsoft.com.  
  
-   Technischer Artikel [The Data Loading Performance Guide (Leistungsleitfaden für das Laden von Daten)](http://go.microsoft.com/fwlink/?LinkId=233700)auf msdn.microsoft.com  
  
-   Technischer Artikel [Using SQL Server Integration Services to Bulk Load Data](http://go.microsoft.com/fwlink/?LinkId=233701)(Verwenden von SQL Server Integration Services für das Massenladen von Daten) auf simple-talk.com.  
  
## <a name="sql-destination-editor-connection-manager-page"></a>Ziel-Editor für SQL (Seite Verbindungs-Manager)
  Mithilfe der Seite **Verbindungs-Manager** des Dialogfelds **Ziel-Editor für SQL** können Sie Informationen zur Datenquelle angeben und eine Vorschau der Ergebnisse anzeigen. Das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Ziel lädt die Daten in die Tabellen oder Sichten einer Datenbank in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
### <a name="options"></a>Tastatur  
 **Teilcache**  
 Wählen Sie eine vorhandene Verbindung aus der Liste aus, oder erstellen Sie eine neue Verbindung, indem Sie auf **Neu**klicken.  
  
 **Neu**  
 Erstellen Sie mithilfe des Dialogfelds **OLE DB-Verbindungs-Manager konfigurieren** eine neue Verbindung.  
  
 **Tabelle oder Sicht verwenden**  
 Wählen Sie eine vorhandene Tabelle oder Sicht aus der Liste aus, oder erstellen Sie eine neue Verbindung, indem Sie auf **Neu**klicken.  
  
 **Neu**  
 Erstellen Sie mithilfe des Dialogfelds **Tabelle erstellen** eine neue Tabelle.  
  
> [!NOTE]  
>  Wenn Sie auf **Neu**klicken, generiert [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] eine Standard-CREATE TABLE-Anweisung auf Grundlage der verbundenen Datenquelle. Diese Standard-CREATE TABLE-Anweisung enthält nicht das FILESTREAM-Attribut, selbst wenn die Quelltabelle eine Spalte mit der Erklärung des FILESTREAM-Attributs enthält. Um eine [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Komponente mit dem FILESTREAM-Attribut auszuführen, implementieren Sie zunächst die FILESTREAM-Speicherung in der Zieldatenbank. Fügen Sie dann das FILESTREAM-Attribut der CREATE TABLE-Anweisung im Dialogfeld **Tabelle erstellen** hinzu. Weitere Informationen finden Sie unter [Blob-Daten &#40;Binary Large Object, SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md).  
  
 **Vorschau**  
 Zeigen Sie mithilfe des Dialogfelds **Vorschau der Abfrageergebnisse anzeigen** eine Vorschau der Ergebnisse an. In der Vorschau können bis zu 200 Zeilen angezeigt werden.  
  
## <a name="sql-destination-editor-mappings-page"></a>Ziel-Editor für SQL (Seite Zuordnungen)
  Auf der Seite **Zuordnungen** des Dialogfelds **Ziel-Editor für SQL** können Sie eine Zuordnung von Eingabe- zu Zielspalten vornehmen.  
  
### <a name="options"></a>Tastatur  
 **Verfügbare Eingabespalten**  
 Zeigt die Liste der verfügbaren Eingabespalten an. Mithilfe eines Drag-und-Drop-Vorgangs können Sie verfügbare Eingabespalten in der Tabelle Zielspalten zuordnen.  
  
 **Verfügbare Zielspalten**  
 Zeigt die Liste der verfügbaren Zielspalten an. Mithilfe eines Drag-und-Drop-Vorgangs können Sie verfügbare Zielspalten in der Tabelle Eingabespalten zuordnen.  
  
 **Eingabespalte**  
 Zeigen Sie die in obiger Tabelle ausgewählten Eingabespalten an. Die Zuordnungen können Sie mithilfe der Liste **Verfügbare Eingabespalten**ändern.  
  
 **Zielspalte**  
 Zeigt alle verfügbaren Zielspalten an, und ob sie zugeordnet sind.  
  
## <a name="sql-destination-editor-advanced-page"></a>Ziel-Editor für SQL (Seite Erweitert)
  Auf der Seite **Erweitert** des Dialogfelds **Ziel-Editor für SQL** können Sie Optionen für die erweiterte Masseneinfügung angeben.  
  
### <a name="options"></a>Tastatur  
 **Identität beibehalten**  
 Gibt an, ob der Task Werte in Identitätsspalten einfügen soll. Der Standardwert dieser Eigenschaft ist **False**.  
  
 **NULL-Werte beibehalten**  
 Gibt an, ob der Task NULL-Werte beibehalten soll. Der Standardwert dieser Eigenschaft ist **False**.  
  
 **Tabellensperre**  
 Gibt an, ob die Tabelle beim Laden der Daten gesperrt wird. Der Standardwert dieser Eigenschaft ist **True**.  
  
 **Check-Einschränkungen**  
 Gibt an, ob Einschränkungen vom Task überprüft werden sollen. Der Standardwert dieser Eigenschaft ist **True**.  
  
 **Trigger auslösen**  
 Gibt an, ob die Masseneinfügung Trigger in Tabellen auslösen soll. Der Standardwert dieser Eigenschaft ist **False**.  
  
 **Erste Zeile**  
 Gibt die erste einzufügende Zeile an. Der Standardwert dieser Eigenschaft ist **-1**. Er zeigt an, dass kein Wert zugewiesen wurde.  
  
> [!NOTE]  
>  Löschen Sie den Inhalt des Textfelds im Dialogfeld **Ziel-Editor für SQL** , um anzugeben, dass Sie keinen Wert für diese Eigenschaft zuweisen möchten. Verwenden Sie im Fenster **Eigenschaften** , im Dialogfeld **Erweiterter Editor**und im Objektmodell den Wert -1.  
  
 **Letzte Zeile**  
 Gibt die letzte einzufügende Zeile an. Der Standardwert dieser Eigenschaft ist **-1**. Er zeigt an, dass kein Wert zugewiesen wurde.  
  
> [!NOTE]  
>  Löschen Sie den Inhalt des Textfelds im Dialogfeld **Ziel-Editor für SQL** , um anzugeben, dass Sie keinen Wert für diese Eigenschaft zuweisen möchten. Verwenden Sie im Fenster **Eigenschaften** , im Dialogfeld **Erweiterter Editor**und im Objektmodell den Wert -1.  
  
 **Maximale Anzahl von Fehlern**  
 Gibt die Anzahl der Fehler an, die auftreten können, bevor die Masseneinfügung abgebrochen wird. Der Standardwert dieser Eigenschaft ist **–1**. Er zeigt an, dass kein Wert zugewiesen wurde.  
  
> [!NOTE]  
>  Löschen Sie den Inhalt des Textfelds im Dialogfeld **Ziel-Editor für SQL** , um anzugeben, dass Sie keinen Wert für diese Eigenschaft zuweisen möchten. Verwenden Sie im Fenster **Eigenschaften** , im Dialogfeld **Erweiterter Editor**und im Objektmodell den Wert -1.  
  
 **Timeout**  
 Gibt die Anzahl der Sekunden an, die abgewartet werden, bevor die Masseneinfügung aufgrund eines Timeouts abgebrochen wird.  
  
 **Spalten sortieren**  
 Geben Sie die Namen der zu sortierenden Spalten an. Jede Spalte kann in auf- oder absteigender Reihenfolge sortiert werden. Wenn Sie mehrere Spalten verwenden, nach denen sortiert werden soll, trennen Sie die Namen in der Liste mit Kommas.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Datenfluss](../../integration-services/data-flow/data-flow.md)  
  
  
