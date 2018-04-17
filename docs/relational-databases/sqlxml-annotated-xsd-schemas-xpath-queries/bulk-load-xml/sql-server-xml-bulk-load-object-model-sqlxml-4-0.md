---
title: SQL Server XML Bulk Load-Objektmodell (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- bulk load [SQLXML], object model
- ErrorLogFile property
- SGDropTables property
- SGUseID property
- KeepNulls property
- ConnectionCommand property
- SchemaGen property
- XMLFragment property
- SQLXMLBulkLoad object
- ForceTableLock property
- CheckConstraints property
- BulkLoad property
- TempFilePath property
- IgnoreDuplicateKeys property
- Transaction property
- KeepIdentity property
- ConnectionString property
- FireTriggers property
- Execute method
- XML Bulk Load [SQLXML], object model
ms.assetid: a9efbbde-ed2b-4929-acc1-261acaaed19d
caps.latest.revision: 27
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: b3b3798be063dd586d74cf4f44d72a48c5f39ccf
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sql-server-xml-bulk-load-object-model-sqlxml-40"></a>SQL Server XML Bulk Load-Objektmodell (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Die Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] XML-Massenladen-Objektmodell besteht aus den SQLXMLBulkLoad-Objekt. Dieses Objekt unterstützt die folgenden Methoden und Eigenschaften.  
  
## <a name="methods"></a>Methoden  
 Execute  
 Lädt die Daten mithilfe der als Parameter bereitgestellten Schema- und Datendatei (oder Datenstrom) in einem Massenvorgang.  
  
## <a name="properties"></a>Eigenschaften  
 BulkLoad  
 Gibt an, ob ein Massenladen durchgeführt werden soll. Diese Eigenschaft ist nützlich, wenn Sie möchten nur die Schemas (siehe "schemagen" SGDropTables und SGUseID-Eigenschaften, die folgen) generieren und nicht ausgeführt werden, ein Massenladen. Hierbei handelt es sich um eine boolesche Eigenschaft. Wenn die Eigenschaft auf TRUE festgelegt ist, wird das XML-Massenladen ausgeführt. Wenn sie auf FALSE festgelegt ist, wird das XML-Massenladen nicht ausgeführt.  
  
 Der Standardwert ist TRUE.  
  
 CheckConstraints  
 Gibt an, ob die Einschränkungen (etwa Einschränkungen aufgrund der Primär-/Fremdschlüsselbeziehung zwischen Spalten), die für die jeweilige Spalte angegeben sind, überprüft werden sollen, sobald beim XML-Massenladen Daten in die Spalten eingefügt werden. Hierbei handelt es sich um eine boolesche Eigenschaft.  
  
 Wenn die Eigenschaft auf TRUE gesetzt ist, werden mit XML-Massenladen die Einschränkungen für jeden eingefügten Wert überprüft (was bedeutet, dass jede verletzte Einschränkung zu einem Fehler führt).  
  
> [!NOTE]  
>  Um diese Eigenschaft auf "false" zu belassen, benötigen Sie **ALTER TABLE** -Berechtigungen für Zieltabellen. Weitere Informationen finden Sie unter [ALTER TABLE &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-table-transact-sql.md).  
  
 Der Standardwert ist FALSE. Wenn sie auf FALSE gesetzt ist, werden die Einschränkungen während des Einfügens ignoriert. In der aktuellen Implementierung müssen Sie die Tabellen in der Reihenfolge der Primär-/Fremdschlüsselbeziehungen im Zuordnungsschema definieren. Eine Tabelle mit einem Primärschlüssel muss also vor der entsprechenden Tabelle mit dem Fremdschlüssel definiert werden; anderenfalls schlägt das XML-Massenladen fehl.  
  
 Hinweis: Wenn ID-Propagierung erfolgt, kommt diese Option nicht zur Anwendung, und Einschränkungen werden weiter überprüft. Dies ist der Fall, wenn `KeepIdentity=False` gilt und eine Beziehung definiert ist, in der es sich beim übergeordneten Element um ein Identitätsfeld handelt und der Wert bei der Generierung an das untergeordnete Element übertragen wird.  
  
 "Connectioncommand"  
 Gibt ein vorhandenes Verbindungsobjekt (zum Beispiel das ADO- oder ICommand Command-Objekt), das XML-Massenladen verwendet werden soll. Sie können der "connectioncommand"-Eigenschaft verwenden, anstatt eine Verbindungszeichenfolge anzugeben, mit der ConnectionString-Eigenschaft. Die Transaktionseigenschaft muss auf "true" festgelegt werden, wenn Sie "connectioncommand" verwenden.  
  
 Wenn Sie die "ConnectionString" und "connectioncommand"-Eigenschaft verwenden, verwendet XML-Massenladen die zuletzt angegebene Eigenschaft.  
  
 Der Standardwert ist NULL.  
  
 ConnectionString  
 Kennzeichnet die OLE DB-Verbindungszeichenfolge mit den Informationen, die notwendig sind, um eine Verbindung zu einer Instanz der Datenbank herzustellen. Wenn Sie die "ConnectionString" und "connectioncommand"-Eigenschaft verwenden, verwendet XML-Massenladen die zuletzt angegebene Eigenschaft.  
  
 Der Standardwert ist NULL.  
  
 ErrorLogFile  
 Gibt den Dateinamen an, in dem Fehler und Meldungen protokolliert werden. Der Standardwert ist eine leere Zeichenfolge; in diesem Fall erfolgt keine Protokollierung.  
  
 FireTriggers  
 Gibt an, ob auf Zieltabellen definierte Trigger während des Massenladevorgangs ausgelöst werden sollen. Der Standardwert lautet FALSE.  
  
 Wenn dieser Wert auf TRUE gesetzt ist, werden Trigger während der Einfügevorgänge normal ausgelöst.  
  
> [!NOTE]  
>  Um diese Eigenschaft auf "false" zu belassen, benötigen Sie **ALTER TABLE** -Berechtigungen für Zieltabellen. Weitere Informationen finden Sie unter [ALTER TABLE &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-table-transact-sql.md).  
  
 Hinweis: Wenn ID-Propagierung erfolgt, kommt diese Option nicht zur Anwendung, und Trigger werden weiter ausgelöst. Dies ist der Fall, wenn `KeepIdentity=False` gilt und eine Beziehung definiert ist, in der es sich beim übergeordneten Element um ein Identitätsfeld handelt und der Wert bei der Generierung an das untergeordnete Element übertragen wird.  
  
 ForceTableLock  
 Gibt an, ob die Tabellen, in die beim XML-Massenladen Daten kopiert werden, während des Massenladens gesperrt sein sollen. Hierbei handelt es sich um eine boolesche Eigenschaft. Wenn die Eigenschaft auf TRUE gesetzt ist, werden während des Massenladens Tabellensperren eingerichtet. Wenn der Wert auf FALSE gesetzt ist, wird immer dann eine Tabellensperre eingerichtet, sobald ein Datensatz in eine Tabelle eingefügt wird.  
  
 Der Standardwert ist FALSE.  
  
 IgnoreDuplicateKeys  
 Gibt an, was geschieht, wenn versucht wird, doppelte Werte in einer Schlüsselspalte einzufügen. Wenn diese Eigenschaft auf TRUE gesetzt ist und versucht wird, einen Datensatz mit doppelten Werten in einer Schlüsselspalte einzufügen, fügt [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] diesen Datensatz nicht ein. Stattdessen wird der nachfolgende Datensatz eingefügt; dadurch schlägt der Massenladevorgang nicht fehl. Wenn diese Eigenschaft auf FALSE gesetzt ist und versucht wird, doppelte Werte in einer Schlüsselspalte einzufügen, schlägt der Massenladevorgang fehl.  
  
 Wenn die IgnoreDuplicateKeys-Eigenschaft auf "true" festgelegt ist, wird für jeden Datensatz in die Tabelle eingefügt eine COMMIT-Anweisung ausgegeben. Dies verlangsamt die Leistung. Die Eigenschaft kann festgelegt werden, auf "true" nur, wenn die Transaktionseigenschaft auf "false" festgelegt ist, da das Transaktionsverhalten mithilfe von Dateien implementiert wird.  
  
 Der Standardwert ist FALSE.  
  
 KeepIdentity  
 Gibt an, wie mit den Werten für eine Identitätsspalte in der Quelldatei verfahren wird. Hierbei handelt es sich um eine boolesche Eigenschaft. Wenn die Eigenschaft auf TRUE gesetzt ist, werden der Identitätsspalte die in der Quelldatei angegebenen Werte zugewiesen. Wenn die Eigenschaft auf FALSE gesetzt ist, werden die in der Quelldatei für die Identitätsspalte angegebenen Werte beim Massenladen ignoriert. In diesem Fall weist [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] der Identitätsspalte einen Wert zu.  
  
 Wenn der Massenladevorgang eine Spalte betrifft, bei der es sich um einen Fremdschlüssel handelt, der auf eine Identitätsspalte verweist, in der wiederum [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-generierte Werte gespeichert sind, werden beim Massenladen diese Identitätswerte entsprechend in die Fremdschlüsselspalte propagiert.  
  
 Der Wert dieser Eigenschaft gilt für alle vom Massenladen betroffene Spalten. Der Standardwert ist TRUE.  
  
> [!NOTE]  
>  Um diese Eigenschaft auf "true" zu belassen, benötigen Sie **ALTER TABLE** -Berechtigungen für Zieltabellen. Andernfalls muss sie auf FALSE gesetzt werden. Weitere Informationen finden Sie unter [ALTER TABLE &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-table-transact-sql.md).  
  
 KeepNulls  
 Gibt an, welcher Wert für eine Spalte verwendet wird, in deren XML-Dokument das entsprechende Attribut oder untergeordnete Element fehlt. Hierbei handelt es sich um eine boolesche Eigenschaft. Wenn die Eigenschaft auf TRUE gesetzt ist, wird der Spalte der Wert Null zugewiesen. Es wird nicht der gegebenenfalls auf dem Server gesetzte Standardwert der Spalte zugewiesen. Der Wert dieser Eigenschaft gilt für alle vom Massenladen betroffene Spalten.  
  
 Der Standardwert ist FALSE.  
  
 "Schemagen"  
 Gibt an, ob die erforderlichen Tabellen vor dem Ausführen eines Massenladevorgangs erstellt werden sollen. Hierbei handelt es sich um eine boolesche Eigenschaft. Wenn diese Eigenschaft auf TRUE gesetzt ist, werden die im Zuordnungsschema angegebenen Tabellen erstellt (die Datenbank muss vorhanden sein). Wenn mindestens eine der Tabellen in der Datenbank bereits vorhanden sind, bestimmt SGDropTables-Eigenschaft an, ob diese bereits vorhandenen Tabellen gelöscht und neu erstellt werden.  
  
 Der Standardwert für die Eigenschaft "schemagen" ist "false". "Schemagen" erstellt keine PRIMARY KEY-Einschränkungen auf den neu erstellten Tabellen. "Schemagen" der Fall ist, FOREIGN KEY-Einschränkungen jedoch in der Datenbank erstellt werden, wenn übereinstimmende gefunden werden kann **SQL: Relationship** und **SQL: Key-Felder** Anmerkungen im Zuordnungsschema und das Schlüsselfeld aus besteht. eine einzelne Spalte.  
  
 Beachten Sie, dass Sie die Eigenschaft "schemagen" auf "true" festlegen, XML-Massenladen die wie folgt vorgeht:  
  
-   Erstellt die notwendigen Tabellen aus dem Element und den Attributnamen. Aus diesem Grund ist es wichtig, dass Sie im Schema für die Element- und Attributnamen keine [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-reservierten Wörter verwenden.  
  
-   Gibt "Überlauf", Daten für jede Spalte mit dem [Overflow-Feld](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sql-overflow-field.md) in [Xml-Datentyp](../../../t-sql/xml/xml-transact-sql.md) Format.  
  
 SGDropTables  
 Gibt an, ob vorhandene Tabellen gelöscht und neu erstellt werden sollen. Sie können diese Eigenschaft verwenden, wenn die Eigenschaft "schemagen" auf "true" festgelegt ist. Wenn SGDropTables "false" ist, werden die vorhandenen Tabellen beibehalten. Wenn diese Eigenschaft auf TRUE gesetzt ist, werden die vorhandenen Tabellen gelöscht und neu erstellt.  
  
 Der Standardwert ist FALSE.  
  
 SGUseID  
 Gibt an, ob das Attribut im Zuordnungsschema wird, die als gekennzeichnete **Id** kann bei der Erstellung einer PRIMARY KEY-Einschränkung beim Erstellen der Tabelle verwendet werden. Verwenden Sie diese Eigenschaft, wenn die Eigenschaft "schemagen" auf "true" festgelegt ist. Wenn SGUseID "true" ist, verwendet das Hilfsprogramm "schemagen" ein Attribut für die **dt: Type = "Id"** als Primärschlüsselspalte angegeben ist, und fügt die entsprechende PRIMARY KEY-Einschränkung beim Erstellen der Tabelle.  
  
 Der Standardwert ist FALSE.  
  
 TempFilePath  
 Gibt den Dateipfad an, wo beim XML-Massenladen die temporären Dateien für ein transaktives Massenladen erstellt werden. (Diese Eigenschaft ist nur hilfreich, wenn die Transaktionseigenschaft auf TRUE gesetzt ist.) Das beim XML-Massenladen verwendete [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Konto muss auf diesen Pfad zugreifen können. Wenn diese Eigenschaft nicht gesetzt ist, werden die Temporärdateien in dem in der Umgebungsvariable TEMP angegebenen Verzeichnis gespeichert.  
  
 Transaction  
 Gibt an, ob das Massenladen als Transaktion erfolgen soll. Bei einem Fehlschlagen des Massenspeicherns ist ein Rollback gewährleistet. Hierbei handelt es sich um eine boolesche Eigenschaft. Wenn die Eigenschaft auf TRUE gesetzt ist, erfolgt das Massenladen in einem Transaktionskontext. Die TempFilePath-Eigenschaft ist nützlich, nur, wenn Transaktion auf "true" festgelegt ist.  
  
> [!NOTE]  
>  Wenn Sie Binärdaten laden (z. B. bin.hex, bin. Base64 XML-Datentypen in die binären Bild [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Datentypen), muss die Transaktionseigenschaft auf "false" festgelegt werden.  
  
 Der Standardwert ist FALSE.  
  
 XMLFragment  
 Gibt an, ob es sich bei den Quelldaten um ein XML-Fragment handelt. Ein XML-Fragment ist ein XML-Dokument, dem das Einzelelement der obersten Ebene (Stammelement) fehlt. Hierbei handelt es sich um eine boolesche Eigenschaft. Diese Eigenschaft muss auf TRUE gesetzt sein, wenn die Quelldatei aus einem XML-Fragment besteht.  
  
 Der Standardwert ist FALSE.  
  
  
