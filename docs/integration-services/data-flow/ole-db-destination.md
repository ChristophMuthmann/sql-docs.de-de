---
title: "OLE DB-Ziel | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.oledbdest.f1"
helpviewer_keywords: 
  - "Datenzugriffsmodus für schnelles Laden [Integration Services]"
  - "OLE DB-Ziel [Integration Services]"
  - "Optionen für schnelles Laden [Integration Services]"
  - "Optionen für schnelles Laden [Integration Services]"
  - "Ziele [Integration Services], OLE DB"
  - "Datenzugriffsmodus für schnelles Laden [Integration Services]"
  - "Einfügen von Daten"
ms.assetid: 873a2fa0-2a02-41fc-a80a-ec9767f36a8a
caps.latest.revision: 79
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 79
---
# OLE DB-Ziel
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
  
 Wenn das OLE DB-Ziel Daten lädt, die einen Doppelbyte-Zeichensatz (Double-Byte Character Set, DBCS) verwenden, werden die Daten möglicherweise beschädigt, falls der Datenzugriffsmodus nicht die Option für schnelles Laden verwendet und falls der OLE DB-Verbindungs-Manager den [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB-Anbieter für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SQLOLEDB) verwendet. Um die Integrität von Doppelbyte-Zeichensatzdaten sicherzustellen, sollten Sie für den OLE DB-Verbindungs-Manager die Verwendung des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client konfigurieren oder einen der Zugriffsmodi für das schnelle Laden verwenden: **Tabelle oder Sicht – schnelles Laden** oder **Variable für Tabellenname oder Sichtname – schnelles Laden**. Beide Optionen sind im Dialogfeld **Ziel-Editor für OLE DB** verfügbar. Bei der Programmierung des [!INCLUDE[ssIS](../../includes/ssis-md.md)]-Objektmodells sollten Sie die AccessMode-Eigenschaft auf **OpenRowset Using FastLoad** oder **OpenRowset mit Using FastLoad From Variable** festlegen.  
  
> [!NOTE]  
>  Wenn Sie mithilfe des Dialogfelds **Ziel-Editor für OLE DB** im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer die Zieltabelle erstellen, in die das OLE DB-Ziel Daten einfügt, müssen Sie möglicherweise die neu erstellte Tabelle manuell auswählen. Die manuelle Auswahl ist erforderlich, wenn ein OLE DB-Anbieter, wie z. B. der OLE DB-Anbieter für DB2, dem Tabellennamen automatisch Schemabezeichner hinzufügt.  
  
> [!NOTE]  
>  Die CREATE TABLE-Anweisung, die das Dialogfeld **Ziel-Editor für OLE DB** generiert, muss eventuell je nach Zieltyp geändert werden. Beispielsweise unterstützen einige Ziele nicht die von der CREATE TABLE-Anweisung verwendeten Datentypen.  
  
 Dieses Ziel verwendet einen OLE DB-Verbindungs-Manager zum Herstellen einer Verbindung mit einer Datenquelle, und der Verbindungs-Manager gibt den zu verwendenden OLE DB-Anbieter an. Weitere Informationen finden Sie unter [OLE DB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md).  
  
 Ein [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekt stellt außerdem das Datenquellenobjekt bereit, von dem Sie einen OLE DB-Verbindungs-Manager erstellen können, um Datenquellen und Datenquellensichten für das OLE DB-Ziel zur Verfügung zu stellen.  
  
 Ein OLE DB-Ziel enthält Zuordnungen zwischen Eingabespalten und Spalten in der Zieldatenquelle. Sie müssen nicht allen Zielspalten Eingabespalten zuordnen. In Abhängigkeit von den Eigenschaften der Zielspalten können jedoch Fehler auftreten, falls den Zielspalten keine Eingabespalten zugeordnet sind. Wenn eine Zielspalte z. B. keine NULL-Werte zulässt, muss dieser Spalte eine Eingabespalte zugeordnet werden. Darüber hinaus müssen die Datentypen zugeordneter Spalten kompatibel sein. Beispielsweise kann eine Eingabespalte mit einem Zeichenfolgen-Datentyp keiner Zielspalte mit einem numerischen Datentyp zugeordnet werden.  
  
 Das OLE DB-Ziel weist eine reguläre Eingabe und eine Fehlerausgabe auf.  
  
 Weitere Informationen zu Datentypen finden Sie unter [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
## Optionen für schnelles Laden  
 Wenn das OLE DB-Ziel einen Datenzugriffsmodus für schnelles Laden verwendet, können Sie für das Ziel die folgenden Optionen für schnelles Laden in der Benutzeroberfläche, dem **Ziel-Editor für OLE DB**, angeben:  
  
-   Identitätswerte aus der importierten Datendatei beibehalten oder von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]zugewiesene eindeutige Werte verwenden.  
  
-   Einen NULL-Wert während des Massenladevorgangs beibehalten.  
  
-   Während des Massenimportvorgangs Einschränkungen der Zieltabelle oder -sicht überprüfen.  
  
-   Sperre auf Tabellenebene für die Dauer des Massenladevorgangs abrufen.  
  
-   Die Zeilenanzahl im Batch und die Commitgröße angeben.  
  
 Einige Optionen für schnelles Laden werden in bestimmten Eigenschaften des OLE DB-Ziels gespeichert. FastLoadKeepIdentity gibt beispielsweise an, ob Werte weiterhin identifiziert werden sollen, während mit FastLoadKeepNulls angegeben wird, ob NULL-Werte beibehalten werden sollen. FastLoadMaxInsertCommitSize gibt wiederum die in einen Batch zu übernehmende Zeilenanzahl an. Andere Optionen für schnelles Laden werden in der FastLoadOptions-Eigenschaft in einer durch Trennzeichen getrennten Liste gespeichert. Wenn das OLE DB-Ziel alle in FastLoadOptions gespeicherten und im Dialogfeld **Ziel-Editor für OLE DB** aufgelisteten Optionen für schnelles Laden verwendet, wird der Wert der Eigenschaft auf **TABLOCK, CHECK_CONSTRAINTS, ROWS_PER_BATCH=1000** festgelegt. Der Wert 1000 gibt an, dass das Ziel zum Verwenden von Batches mit 1000 Zeilen konfiguriert wurde.  
  
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
  
## Problembehandlung des OLE DB-Zieles  
 Sie können die vom OLE DB-Ziel an externe Datenanbieter gerichteten Aufrufe protokollieren. Mithilfe dieser Protokollierungsfunktion können Sie Probleme beim Speichern von Daten in externen Datenquellen durch das OLE DB-Ziel behandeln. Aktivieren Sie zum Protokollieren der vom OLE DB-Ziel an externe Datenanbieter gerichteten Aufrufe die Paketprotokollierung, und wählen Sie das **Diagnostic** -Ereignis auf Paketebene aus. Weitere Informationen finden Sie unter [Behandeln von Problemen mit Paketausführungstools](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md).  
  
## Konfigurieren des OLE DB-Zieles  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Klicken Sie auf eines der folgenden Themen, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im Dialogfeld **Ziel-Editor für OLE DB** festlegen können:  
  
-   [Ziel-Editor für OLE DB &#40;Seite „Verbindungs-Manager“&#41;](../../integration-services/data-flow/ole-db-destination-editor-connection-manager-page.md)  
  
-   [Ziel-Editor für OLE DB &#40;Seite „Zuordnungen“&#41;](../../integration-services/data-flow/ole-db-destination-editor-mappings-page.md)  
  
-   [Ziel-Editor für OLE DB &#40;Seite „Fehlerausgabe“&#41;](../../integration-services/data-flow/ole-db-destination-editor-error-output-page.md)  
  
 Das Dialogfeld **Erweiterter Editor** enthält die Eigenschaften, die programmgesteuert festgelegt werden können. Klicken Sie auf eines der folgenden Themen, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im Dialogfeld **Erweiterter Editor** oder programmgesteuert festlegen können:  
  
-   [Allgemeine Eigenschaften](../Topic/Common%20Properties.md)  
  
-   [Benutzerdefinierte Eigenschaften für OLE DB](../../integration-services/data-flow/ole-db-custom-properties.md)  
  
 Klicken Sie auf eines der folgenden Themen, um weitere Informationen zum Festlegen von Eigenschaften anzuzeigen:  
  
-   [Laden von Daten mithilfe des OLE DB-Ziels](../../integration-services/data-flow/load-data-by-using-the-ole-db-destination.md)  
  
-   [Festlegen der Eigenschaften einer Datenflusskomponente](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## Verwandte Inhalte  
 [OLE DB-Quelle](../../integration-services/data-flow/ole-db-source.md)  
  
 [Integration Services-Variablen &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md)  
  
 [Datenfluss](../../integration-services/data-flow/data-flow.md)  
  
  