---
title: OLE DB-Ziel | Microsoft-Dokumentation
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
- sql13.dts.designer.oledbdest.f1
- sql13.dts.designer.oledbdestadapter.connection.f1
- sql13.dts.designer.oledbdestadapter.mappings.f1
- sql13.dts.designer.oledbdestadapter.errorhandling.f1
helpviewer_keywords:
- fast-load data access mode [Integration Services]
- OLE DB destination [Integration Services]
- fast load options [Integration Services]
- fast-load options [Integration Services]
- destinations [Integration Services], OLE DB
- fast load data access mode [Integration Services]
- inserting data
ms.assetid: 873a2fa0-2a02-41fc-a80a-ec9767f36a8a
caps.latest.revision: 79
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 3a5dc3a25d85f872603e88a8ed0ef52fec5f4252
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="ole-db-destination"></a>OLE DB-Ziel
  Das OLE DB-Ziel lädt Daten mithilfe einer Datenbanktabelle, einer Sicht oder eines SQL-Befehls in eine Reihe von OLE DB-kompatible Datenbanken. Beispielsweise können aus der OLE DB-Quelle Daten in Tabellen in [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Access- und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbanken geladen werden.  
  
> [!NOTE]  
>  Wenn es sich bei der Datenquelle um [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2007 handelt, erfordert die Datenquelle einen anderen Verbindungs-Manager als frühere Versionen von Excel. Weitere Informationen finden Sie unter [Herstellen einer Verbindung mit einer Excel-Arbeitsmappe](../../integration-services/connection-manager/connect-to-an-excel-workbook.md).  
  
 Das OLE DB-Ziel stellt fünf verschiedene Datenzugriffsmodi zum Laden von Daten bereit:  
  
-   Eine Tabelle oder Sicht. Sie können eine vorhandene Tabelle oder Sicht angeben oder eine neue Tabelle erstellen.  
  
-   Eine Tabelle oder Sicht, die Optionen für schnelles Laden verwendet. Sie können eine vorhandene Tabelle angeben oder eine neue Tabelle erstellen.  
  
-   Eine in einer Variablen angegebene Tabelle oder Sicht.  
  
-   Eine in einer Variablen angegebene Tabelle oder Sicht, die Optionen für schnelles Laden verwendet.  
  
-   Die Ergebnisse einer SQL-Anweisung.  
  
> [!NOTE]  
>  Vom OLE DB-Ziel werden keine Parameter unterstützt. Wenn Sie eine parametrisierte INSERT-Anweisung ausführen müssen, ziehen Sie die Transformation für den OLE DB-Befehl in Betracht. Weitere Informationen finden Sie unter [OLE DB Command Transformation](../../integration-services/data-flow/transformations/ole-db-command-transformation.md).  
  
 Wenn das OLE DB-Ziel Daten lädt, die einen Doppelbyte-Zeichensatz (Double-Byte Character Set, DBCS) verwenden, werden die Daten möglicherweise beschädigt, falls der Datenzugriffsmodus nicht die Option für schnelles Laden verwendet und falls der OLE DB-Verbindungs-Manager den [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB-Anbieter für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SQLOLEDB) verwendet. Um die Integrität von Doppelbyte-Zeichensatzdaten sicherzustellen, sollten Sie für den OLE DB-Verbindungs-Manager die Verwendung des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client konfigurieren oder einen der Zugriffsmodi für das schnelle Laden verwenden: **Tabelle oder Sicht – schnelles Laden** oder **Variable für Tabellenname oder Sichtname – schnelles Laden**. Beide Optionen sind im Dialogfeld **Ziel-Editor für OLE DB** verfügbar. Bei der Programmierung des [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Objektmodells sollten Sie die AccessMode-Eigenschaft auf **OpenRowset Using FastLoad**oder **OpenRowset mit Using FastLoad From Variable**festlegen.  
  
> [!NOTE]  
>  Wenn Sie mithilfe des Dialogfelds **Ziel-Editor für OLE DB** im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer die Zieltabelle erstellen, in die das OLE DB-Ziel Daten einfügt, müssen Sie möglicherweise die neu erstellte Tabelle manuell auswählen. Die manuelle Auswahl ist erforderlich, wenn ein OLE DB-Anbieter, wie z. B. der OLE DB-Anbieter für DB2, dem Tabellennamen automatisch Schemabezeichner hinzufügt.  
  
> [!NOTE]  
>  Die CREATE TABLE-Anweisung, die das Dialogfeld **Ziel-Editor für OLE DB** generiert, muss eventuell je nach Zieltyp geändert werden. Beispielsweise unterstützen einige Ziele nicht die von der CREATE TABLE-Anweisung verwendeten Datentypen.  
  
 Dieses Ziel verwendet einen OLE DB-Verbindungs-Manager zum Herstellen einer Verbindung mit einer Datenquelle, und der Verbindungs-Manager gibt den zu verwendenden OLE DB-Anbieter an. Weitere Informationen finden Sie unter [OLE DB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md).  
  
 Ein [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekt stellt außerdem das Datenquellenobjekt bereit, von dem Sie einen OLE DB-Verbindungs-Manager erstellen können, um Datenquellen und Datenquellensichten für das OLE DB-Ziel zur Verfügung zu stellen.  
  
 Ein OLE DB-Ziel enthält Zuordnungen zwischen Eingabespalten und Spalten in der Zieldatenquelle. Sie müssen nicht allen Zielspalten Eingabespalten zuordnen. In Abhängigkeit von den Eigenschaften der Zielspalten können jedoch Fehler auftreten, falls den Zielspalten keine Eingabespalten zugeordnet sind. Wenn eine Zielspalte z. B. keine NULL-Werte zulässt, muss dieser Spalte eine Eingabespalte zugeordnet werden. Darüber hinaus müssen die Datentypen zugeordneter Spalten kompatibel sein. Beispielsweise kann eine Eingabespalte mit einem Zeichenfolgen-Datentyp keiner Zielspalte mit einem numerischen Datentyp zugeordnet werden.  
  
 Das OLE DB-Ziel weist eine reguläre Eingabe und eine Fehlerausgabe auf.  
  
 Weitere Informationen zu Datentypen finden Sie unter [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="fast-load-options"></a>Optionen für schnelles Laden  
 Wenn das OLE DB-Ziel einen Datenzugriffsmodus für schnelles Laden verwendet, können Sie für das Ziel die folgenden Optionen für schnelles Laden in der Benutzeroberfläche, dem **Ziel-Editor für OLE DB**, angeben:  
  
-   Identitätswerte aus der importierten Datendatei beibehalten oder von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]zugewiesene eindeutige Werte verwenden.  
  
-   Einen NULL-Wert während des Massenladevorgangs beibehalten.  
  
-   Während des Massenimportvorgangs Einschränkungen der Zieltabelle oder -sicht überprüfen.  
  
-   Sperre auf Tabellenebene für die Dauer des Massenladevorgangs abrufen.  
  
-   Die Zeilenanzahl im Batch und die Commitgröße angeben.  
  
 Einige Optionen für schnelles Laden werden in bestimmten Eigenschaften des OLE DB-Ziels gespeichert. FastLoadKeepIdentity gibt beispielsweise an, ob Werte weiterhin identifiziert werden sollen, während mit FastLoadKeepNulls angegeben wird, ob NULL-Werte beibehalten werden sollen. FastLoadMaxInsertCommitSize gibt wiederum die in einen Batch zu übernehmende Zeilenanzahl an. Andere Optionen für schnelles Laden werden in der FastLoadOptions-Eigenschaft in einer durch Trennzeichen getrennten Liste gespeichert. Wenn das OLE DB-Ziel alle in FastLoadOptions gespeicherten und im Dialogfeld **Ziel-Editor für OLE DB** aufgelisteten Optionen für schnelles Laden verwendet, wird der Wert der Eigenschaft auf **TABLOCK, CHECK_CONSTRAINTS, ROWS_PER_BATCH=1000**festgelegt. Der Wert 1000 gibt an, dass das Ziel zum Verwenden von Batches mit 1000 Zeilen konfiguriert wurde.  
  
> [!NOTE]  
>  Einschränkungsfehler am Ziel bewirken, dass der gesamte Batch mit Zeilen, die durch FastLoadMaxInsertCommitSize definiert sind, fehlschlägt.  
  
 Neben den im Dialogfeld **Ziel-Editor für OLE DB** verfügbar gemachten Optionen für schnelles Laden können Sie das OLE DB-Ziel so konfigurieren, dass die folgenden Optionen für das Massenladen verwendet werden, indem Sie die Optionen im Dialogfeld **Erweiterter Editor** in der FastLoadOptions-Eigenschaft eingeben.  
  
|Option für schnelles Laden|Description|  
|----------------------|-----------------|  
|KILOBYTES_PER_BATCH|Gibt die einzufügende Größe in Kilobyte an. Die Option hat die folgende Form: **KILOBYTES_PER_BATCH** = \<positive ganze Zahl**>**.|  
|FIRE_TRIGGERS|Gibt an, ob in der Einfügetabelle Trigger ausgelöst werden. Die Option hat die Form **FIRE_TRIGGERS**. Das Vorhandensein der Option gibt an, dass Trigger ausgelöst werden.|  
|ORDER|Gibt die Sortierung der Eingabedaten an. Die Option hat die folgende Form: ORDER \<Spaltenname> ASC&#124;DESC. Es kann eine beliebige Anzahl an Spalten aufgelistet werden. Optional kann die Sortierreihenfolge eingeschlossen werden. Wird die Sortierreihenfolge ausgelassen, geht der Einfügevorgang davon aus, dass die Daten nicht sortiert sind.<br /><br /> Hinweis: Die Leistung wird verbessert, wenn die Eingabedaten entsprechend dem gruppierten Index der Tabelle mit der ORDER-Option sortiert werden.|  
  
 Die [!INCLUDE[tsql](../../includes/tsql-md.md)] -Schlüsselwörter werden in der Regel in Großbuchstaben eingegeben. Bei den Schlüsselwörtern wird jedoch nicht nach Groß-/Kleinschreibung unterschieden.  
  
 Weitere Informationen zu den Optionen für schnelles Laden finden Sie unter [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md).  
  
## <a name="troubleshooting-the-ole-db-destination"></a>Problembehandlung des OLE DB-Zieles  
 Sie können die vom OLE DB-Ziel an externe Datenanbieter gerichteten Aufrufe protokollieren. Mithilfe dieser Protokollierungsfunktion können Sie Probleme beim Speichern von Daten in externen Datenquellen durch das OLE DB-Ziel behandeln. Aktivieren Sie zum Protokollieren der vom OLE DB-Ziel an externe Datenanbieter gerichteten Aufrufe die Paketprotokollierung, und wählen Sie das **Diagnostic** -Ereignis auf Paketebene aus. Weitere Informationen finden Sie unter [Behandeln von Problemen mit Paketausführungstools](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md).  
  
## <a name="configuring-the-ole-db-destination"></a>Konfigurieren des OLE DB-Zieles  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Das Dialogfeld **Erweiterter Editor** enthält die Eigenschaften, die programmgesteuert festgelegt werden können. Klicken Sie auf eines der folgenden Themen, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im Dialogfeld **Erweiterter Editor** oder programmgesteuert festlegen können:  
  
-   [Common Properties](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Benutzerdefinierte Eigenschaften für OLE DB](../../integration-services/data-flow/ole-db-custom-properties.md)  
  
 Klicken Sie auf eines der folgenden Themen, um weitere Informationen zum Festlegen von Eigenschaften anzuzeigen:  
  
-   [Laden von Daten mithilfe des OLE DB-Ziels](../../integration-services/data-flow/load-data-by-using-the-ole-db-destination.md)  
  
-   [Festlegen der Eigenschaften einer Datenflusskomponente](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## <a name="ole-db-destination-editor-connection-manager-page"></a>Ziel-Editor für OLE DB (Seite Verbindungs-Manager)
  Mithilfe der Seite **Verbindungs-Manager** des Dialogfelds **Ziel-Editor für OLE DB** können Sie die OLE DB-Verbindung für das Ziel auswählen. Außerdem können Sie auf dieser Seite eine Tabelle oder Sicht aus der Datenbank auswählen.  
  
> [!NOTE]  
>  Wenn es sich bei der Datenquelle um [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2007 handelt, erfordert die Datenquelle einen anderen Verbindungs-Manager als frühere Versionen von Excel. Weitere Informationen finden Sie unter [Herstellen einer Verbindung mit einer Excel-Arbeitsmappe](../../integration-services/connection-manager/connect-to-an-excel-workbook.md).  
  
> [!NOTE]  
>  Die **CommandTimeout** -Eigenschaft des OLE DB-Ziels ist nicht im **Ziel-Editor für OLE DB**verfügbar, sie kann jedoch mit dem Dialogfeld **Erweiterter Editor**festgelegt werden. Darüber hinaus sind bestimmte Optionen für schnelles Laden nur im Dialogfeld **Erweiterter Editor**verfügbar. Weitere Informationen zu diesen Eigenschaften finden Sie im Abschnitt OLE DB-Ziel von [OLE DB Custom Properties](../../integration-services/data-flow/ole-db-custom-properties.md).  
  
### <a name="static-options"></a>Statische Optionen  
 **Teilcache**  
 Wählen Sie in der Liste einen vorhandenen Verbindungs-Manager aus, oder erstellen Sie eine neue Verbindung, indem Sie auf **Neu**klicken.  
  
 **Neu**  
 Erstellen Sie mithilfe des Dialogfelds **OLE DB-Verbindungs-Manager konfigurieren** einen neuen Verbindungs-Manager.  
  
 **Datenzugriffsmodus**  
 Gibt das Verfahren für das Laden von Daten in das Ziel an. Für das Laden von Doppelbyte-Zeichensatzdaten (Double-Byte Character Set oder DBCS) ist die Verwendung einer der Optionen für schnelles Laden erforderlich. Weitere Informationen zu Datenzugriffsmodi für schnelles Laden, die für Masseneinfügungen optimiert sind, finden Sie unter [OLE DB Destination](../../integration-services/data-flow/ole-db-destination.md).  
  
|Option|Description|  
|------------|-----------------|  
|Tabelle oder Sicht|Lädt Daten in eine Tabelle oder Sicht im OLE DB-Ziel.|  
|Tabelle oder Sicht - schnelles Laden|Lädt Daten in eine Tabelle oder Sicht im OLE DB-Ziel und verwendet die Option für das schnelle Laden. Weitere Informationen zu Datenzugriffsmodi für schnelles Laden, die für Masseneinfügungen optimiert sind, finden Sie unter [OLE DB Destination](../../integration-services/data-flow/ole-db-destination.md).|  
|Variable für Tabellenname oder Sichtname|Gibt den Namen der Tabelle oder Sicht in einer Variablen an.<br /><br /> **Verwandte Informationen:** [Verwenden von Variablen in Paketen](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)|  
|Variable für Tabellenname oder Sichtname - schnelles Laden|Gibt den Namen der Tabelle oder Sicht in einer Variablen an und verwendet zum Laden der Daten die Option für das schnelle Laden. Weitere Informationen zu Datenzugriffsmodi für schnelles Laden, die für Masseneinfügungen optimiert sind, finden Sie unter [OLE DB Destination](../../integration-services/data-flow/ole-db-destination.md).|  
|SQL-Befehl|Lädt Daten mithilfe einer SQL-Abfrage in das OLE DB-Ziel.|  
  
 **Vorschau**  
 Zeigen Sie mithilfe des Dialogfelds **Vorschau der Abfrageergebnisse anzeigen** eine Vorschau der Ergebnisse an. In der Vorschau können bis zu 200 Zeilen angezeigt werden.  
  
### <a name="data-access-mode-dynamic-options"></a>Dynamische Optionen (Datenzugriffsmodus)  
 Für jede der Einstellungen für **Datenzugriffsmodus** werden spezifische dynamische Optionen angezeigt. In den folgenden Abschnitten werden alle dynamischen Optionen, die für die einzelnen Einstellungen für **Datenzugriffsmodus** verfügbar sind, beschrieben.  
  
#### <a name="data-access-mode--table-or-view"></a>Datenzugriffsmodus = Tabelle oder Sicht  
 **Name der Tabelle oder Sicht**  
 Wählen Sie den Namen der Tabelle oder Sicht aus einer Liste der verfügbaren Namen in der Datenquelle aus.  
  
 **Neu**  
 Erstellen Sie mithilfe des Dialogfelds **Tabelle erstellen** eine neue Tabelle.  
  
> [!NOTE]  
>  Wenn Sie auf **Neu**klicken, generiert [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] eine Standard-CREATE TABLE-Anweisung auf Grundlage der verbundenen Datenquelle. Diese Standard-CREATE TABLE-Anweisung enthält nicht das FILESTREAM-Attribut, selbst wenn die Quelltabelle eine Spalte mit der Erklärung des FILESTREAM-Attributs enthält. Um eine [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Komponente mit dem FILESTREAM-Attribut auszuführen, implementieren Sie zunächst die FILESTREAM-Speicherung in der Zieldatenbank. Fügen Sie dann das FILESTREAM-Attribut der CREATE TABLE-Anweisung im Dialogfeld **Tabelle erstellen** hinzu. Weitere Informationen finden Sie unter [Blob-Daten &#40;Binary Large Object, SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md).  
  
#### <a name="data-access-mode--table-or-view--fast-load"></a>Datenzugriffsmodus = Tabelle oder Sicht – schnelles Laden  
 **Name der Tabelle oder Sicht**  
 Wählen Sie mithilfe dieser Liste eine Tabelle oder Sicht in der Datenbank aus, oder erstellen Sie eine neue Tabelle, indem Sie auf **Neu**klicken.  
  
 **Neu**  
 Erstellen Sie mithilfe des Dialogfelds **Tabelle erstellen** eine neue Tabelle.  
  
> [!NOTE]  
>  Wenn Sie auf **Neu**klicken, generiert [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] eine Standard-CREATE TABLE-Anweisung auf Grundlage der verbundenen Datenquelle. Diese Standard-CREATE TABLE-Anweisung enthält nicht das FILESTREAM-Attribut, selbst wenn die Quelltabelle eine Spalte mit der Erklärung des FILESTREAM-Attributs enthält. Um eine [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Komponente mit dem FILESTREAM-Attribut auszuführen, implementieren Sie zunächst die FILESTREAM-Speicherung in der Zieldatenbank. Fügen Sie dann das FILESTREAM-Attribut der CREATE TABLE-Anweisung im Dialogfeld **Tabelle erstellen** hinzu. Weitere Informationen finden Sie unter [Blob-Daten &#40;Binary Large Object, SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md).  
  
 **Identität beibehalten**  
 Gibt an, ob beim Laden von Daten Identitätswerte kopiert werden sollen. Diese Eigenschaft ist nur für die Option für das schnelle Laden verfügbar. Der Standardwert dieser Eigenschaft ist **false**.  
  
 **NULL-Werte beibehalten**  
 Gibt an, ob beim Laden von Daten NULL-Werte kopiert werden sollen. Diese Eigenschaft ist nur für die Option für das schnelle Laden verfügbar. Der Standardwert dieser Eigenschaft ist **false**.  
  
 **Tabellensperre**  
 Gibt an, ob die Tabelle während des Ladens gesperrt ist. Der Standardwert dieser Eigenschaft ist **true**.  
  
 **Check-Einschränkungen**  
 Gibt an, ob das Ziel beim Laden von Daten Einschränkungen überprüft. Der Standardwert dieser Eigenschaft ist **true**.  
  
 **Zeilen pro Batch**  
 Geben Sie die Anzahl der Zeilen in einem Batch an. Der Standardwert dieser Eigenschaft lautet **-1**und zeigt an, dass kein Wert zugewiesen wurde.  
  
> [!NOTE]  
>  Löschen Sie im Dialogfeld **Ziel-Editor für OLE DB** den Inhalt des Textfelds, um anzugeben, dass für diese Eigenschaft kein benutzerdefinierter Wert zugewiesen werden soll.  
  
 **Maximale Einfügungscommitgröße**  
 Gibt die Batchgröße an, für die das OLE DB-Ziel bei schnellen Ladevorgängen die Durchführung eines Commits versucht. Der Wert **0** gibt an, dass nach dem Verarbeiten aller Zeilen für alle Daten in einem einzelnen Batch ein Commit ausgeführt wird.  
  
> [!NOTE]  
>  Der Wert **0** bewirkt möglicherweise, dass das Paket bei der Ausführung nicht mehr reagiert, wenn das OLE DB-Ziel und andere Datenflusskomponenten dieselbe Quelltabelle aktualisieren. Um zu verhindern, dass die Paketausführung beendet wird, legen Sie die Option **Maximale Einfügungscommitgröße** auf **2147483647**fest.  
  
 Wenn Sie für diese Eigenschaft einen Wert bereitstellen, führt das Ziel für Zeilen in Batches, die kleiner sind als (a) die **Maximale Einfügungscommitgröße**oder (b) die verbleibenden Zeilen im Puffer, der gerade verarbeitet wird, einen Commit durch.  
  
> [!NOTE]  
>  Einschränkungsfehler am Ziel bewirken, dass der gesamte Batch mit Zeilen, die durch **Maximale Einfügungscommitgröße** definiert sind, fehlschlägt.  
  
#### <a name="data-access-mode--table-name-or-view-name-variable"></a>Datenzugriffsmodus = Variable für Tabellenname oder Sichtname  
 **Variablenname**  
 Wählen Sie die Variable aus, die den Namen der Tabelle oder Sicht enthält.  
  
#### <a name="data-access-mode--table-name-or-view-name-variable--fast-load"></a>Datenzugriffsmodus = Variable für Tabellenname oder Sichtname – schnelles Laden  
 **Variablenname**  
 Wählen Sie die Variable aus, die den Namen der Tabelle oder Sicht enthält.  
  
 **Neu**  
 Erstellen Sie mithilfe des Dialogfelds **Tabelle erstellen** eine neue Tabelle.  
  
> [!NOTE]  
>  Wenn Sie auf **Neu**klicken, generiert [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] eine Standard-CREATE TABLE-Anweisung auf Grundlage der verbundenen Datenquelle. Diese Standard-CREATE TABLE-Anweisung enthält nicht das FILESTREAM-Attribut, selbst wenn die Quelltabelle eine Spalte mit der Erklärung des FILESTREAM-Attributs enthält. Um eine [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Komponente mit dem FILESTREAM-Attribut auszuführen, implementieren Sie zunächst die FILESTREAM-Speicherung in der Zieldatenbank. Fügen Sie dann das FILESTREAM-Attribut der CREATE TABLE-Anweisung im Dialogfeld **Tabelle erstellen** hinzu. Weitere Informationen finden Sie unter [Blob-Daten &#40;Binary Large Object, SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md).  
  
 **Identität beibehalten**  
 Gibt an, ob beim Laden von Daten Identitätswerte kopiert werden sollen. Diese Eigenschaft ist nur für die Option für das schnelle Laden verfügbar. Der Standardwert dieser Eigenschaft ist **false**.  
  
 **NULL-Werte beibehalten**  
 Gibt an, ob beim Laden von Daten NULL-Werte kopiert werden sollen. Diese Eigenschaft ist nur für die Option für das schnelle Laden verfügbar. Der Standardwert dieser Eigenschaft ist **false**.  
  
 **Tabellensperre**  
 Gibt an, ob die Tabelle während des Ladens gesperrt ist. Der Standardwert dieser Eigenschaft ist **false**.  
  
 **Check-Einschränkungen**  
 Gibt an, ob Einschränkungen vom Task überprüft werden sollen. Der Standardwert dieser Eigenschaft ist **false**.  
  
 **Zeilen pro Batch**  
 Geben Sie die Anzahl der Zeilen in einem Batch an. Der Standardwert dieser Eigenschaft lautet **-1**und zeigt an, dass kein Wert zugewiesen wurde.  
  
> [!NOTE]  
>  Löschen Sie im Dialogfeld **Ziel-Editor für OLE DB** den Inhalt des Textfelds, um anzugeben, dass für diese Eigenschaft kein benutzerdefinierter Wert zugewiesen werden soll.  
  
 **Maximale Einfügungscommitgröße**  
 Gibt die Batchgröße an, für die das OLE DB-Ziel bei schnellen Ladevorgängen die Durchführung eines Commits versucht. Der Standardwert **2147483647** zeigt an, dass nach dem Verarbeiten aller Zeilen für alle Daten in einem einzelnen Batch ein Commit durchgeführt wird.  
  
> [!NOTE]  
>  Der Wert **0** bewirkt möglicherweise, dass das Paket bei der Ausführung nicht mehr reagiert, wenn das OLE DB-Ziel und andere Datenflusskomponenten dieselbe Quelltabelle aktualisieren. Um zu verhindern, dass die Paketausführung beendet wird, legen Sie die Option **Maximale Einfügungscommitgröße** auf **2147483647**fest.  
  
#### <a name="data-access-mode--sql-command"></a>Datenzugriffsmodus = SQL-Befehl  
 **SQL-Befehlstext**  
 Geben Sie den Text einer SQL-Abfrage ein, und erstellen Sie die Abfrage, indem Sie auf **Abfrage erstellen**klicken, oder suchen Sie nach der Datei, die den Abfragetext enthält, indem Sie auf **Durchsuchen**klicken.  
  
> [!NOTE]  
>  Vom OLE DB-Ziel werden keine Parameter unterstützt. Wenn Sie eine parametrisierte INSERT-Anweisung ausführen müssen, ziehen Sie die Transformation für den OLE DB-Befehl in Betracht. Weitere Informationen finden Sie unter [OLE DB Command Transformation](../../integration-services/data-flow/transformations/ole-db-command-transformation.md).  
  
 **Abfrage erstellen**  
 Mithilfe des Dialogfelds **Abfrage-Generator** können Sie die SQL-Abfrage visuell erstellen.  
  
 **Durchsuchen**  
 Mithilfe des Dialogfelds **Öffnen** können Sie nach der Datei suchen, die den Text der SQL-Abfrage enthält.  
  
 **Abfrage analysieren**  
 Überprüft die Syntax des Abfragetexts.  
  
## <a name="ole-db-destination-editor-mappings-page"></a>Ziel-Editor für OLE DB (Seite Zuordnungen)
  Auf der Seite **Zuordnungen** des Dialogfelds **Ziel-Editor für OLE DB** können Sie eine Zuordnung von Eingabe- zu Zielspalten vornehmen.  
  
### <a name="options"></a>Tastatur  
 **Verfügbare Eingabespalten**  
 Zeigt die Liste der verfügbaren Eingabespalten an. Mithilfe eines Drag-und-Drop-Vorgangs können Sie verfügbare Eingabespalten in der Tabelle Zielspalten zuordnen.  
  
 **Verfügbare Zielspalten**  
 Zeigt die Liste der verfügbaren Zielspalten an. Mithilfe eines Drag-und-Drop-Vorgangs können Sie verfügbare Zielspalten in der Tabelle Eingabespalten zuordnen.  
  
 **Eingabespalte**  
 Zeigt die von Ihnen ausgewählten Eingabespalten an. Sie können Zuordnungen entfernen, indem Sie **\<ignore>** auswählen, um Spalten aus der Ausgabe auszuschließen.  
  
 **Zielspalte**  
 Zeigt alle verfügbaren Zielspalten an, ganz gleich, ob sie zugeordnet sind oder nicht.  
  
## <a name="ole-db-destination-editor-error-output-page"></a>Ziel-Editor für OLE DB (Seite Fehlerausgabe)
  Auf der Seite **Fehlerausgabe** des Dialogfelds **Ziel-Editor für OLE DB** geben Sie Optionen für die Fehlerbehandlung an.  
  
### <a name="options"></a>Tastatur  
 **Eingabe/Ausgabe**  
 Zeigt den Namen der Eingabe an.  
  
 **Column**  
 Wird nicht verwendet.  
  
 **Fehler**  
 Gibt an, was bei Auftreten eines Fehlers geschehen soll: den Fehler ignorieren, die Zeile umleiten oder die Komponente mit einem Fehler abbrechen.  
  
 **Verwandte Themen:** [Fehlerbehandlung in Daten](../../integration-services/data-flow/error-handling-in-data.md)  
  
 **Abschneiden**  
 Wird nicht verwendet.  
  
 **Beschreibung**  
 Zeigt die Beschreibung des Vorgangs an.  
  
 **Diesen Wert für ausgewählte Zellen festlegen**  
 Gibt an, was im Falle eines Fehlers oder einer Kürzung mit den ausgewählten Zellen geschehen soll: den Fehler ignorieren, die Zeile umleiten oder die Komponente mit einem Fehler abbrechen.  
  
 **Anwenden**  
 Wendet die Fehlerbehandlungsoption auf die ausgewählten Zellen an.  
  
## <a name="related-content"></a>Verwandte Inhalte  
 [OLE DB-Quelle](../../integration-services/data-flow/ole-db-source.md)  
  
 [Integration Services-Variablen &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md)  
  
 [Datenfluss](../../integration-services/data-flow/data-flow.md)  
  
  
