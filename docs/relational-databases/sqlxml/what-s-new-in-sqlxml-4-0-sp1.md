---
title: Was&#39;s in SQLXML 4.0 SP1 | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- registry keys [SQLXML]
- SQLNCLI, SQLXML
- what's new [SQLXML]
- SQLXML, what's new
- migrating SQLXML applications
- redistributing SQLXML
- SQL Server Native Client, SQLXML
- side-by-side installations [SQLXML]
ms.assetid: 48f7720b-1705-402d-93ce-097ff1737877
caps.latest.revision: 67
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: cb8a328b862a22cc0d7f909b7e1e6b4f0f1fb17a
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="what39s-new-in-sqlxml-40-sp1"></a>Was&#39;s in SQLXML 4.0 SP1
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] SQLXML 4.0 SP1 umfasst verschiedene Updates und Erweiterungen. Dieses Thema fasst die Updates zusammen und enthält Links zu ausführlicheren Informationen, sofern verfügbar. SQLXML 4.0 SP1 bietet zusätzliche Erweiterungen zur Unterstützung der neuen Datentypen [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]. Dieses Thema enthält die folgenden Themen:  
  
-   Installieren von SQLXML 4.0 SP1  
  
-   Probleme bei gleichzeitiger Installation  
  
-   SQLXML 4.0 und MSXML  
  
-   Neuverteilen von SQLXML 4.0  
  
-   Unterstützung für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client  
  
-   Unterstützung für in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] eingeführte Datentypen  
  
-   Änderungen für XML-Massenladen für SQLXML 4.0  
  
-   Änderungen des Registrierungsschlüssels für SQLXML 4.0  
  
-   Migrationsprobleme  
  
## <a name="installing-sqlxml-40-sp1"></a>Installieren von SQLXML 4.0 SP1  
 Vor der Veröffentlichung von [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] wurde SQLXML 4.0 mit SQL Server veröffentlicht und war Bestandteil der Standardinstallation aller SQL Server-Versionen mit Ausnahme von SQL Server Express. Beginnend mit [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], die neueste Version von SQLXML (SQLXML 4.0 SP1) ist in SQL Server nicht mehr enthalten. Zum Installieren von SQLXML 4.0 SP1 laden Sie dieses von [Installationspfad für SQLXML 4.0 SP1](http://www.microsoft.com/download/details.aspx?id=30403)herunter.  
  
 Die SQLXML 4.0 SP1-Dateien werden an folgendem Speicherort installiert:  
  
 `%PROGRAMFILES%\SQLXML 4.0\`  
  
> [!NOTE]  
>  Alle entsprechenden Registrierungseinstellungen für SQLXML 4.0 werden im Rahmen des Installationsprozesses festgelegt.  
  
 Um die Ausführung von 32-Bit-SQLXML-Anwendungen unter Windows on Windows (WOW64) auf 64-Bit-Windows-Betriebssystemen zu ermöglichen, führen Sie das 64-Bit-SQLXML 4.0 SP1-Paket mit dem Namen sqlxml4.msi aus, das Sie im Download Center finden.  
  
#### <a name="uninstalling-sqlxml-40-sp1"></a>Deinstallieren von SQLXML 4.0 SP1  
 Bestimmte Registrierungsschlüssel werden von SQLXML 3.0 SP3, SQLXML 4.0 und SQLXML 4.0 SP1 gemeinsam verwendet. Wenn spätere SQLXML-Versionen auf einem Computer deinstalliert werden, auf dem auch SQLXML 3.0 SP3 installiert ist, müssen Sie SQLXML 3.0 SP3 möglicherweise neu installieren.  
  
## <a name="side-by-side-installation-issues"></a>Probleme bei gleichzeitiger Installation  
 Durch die Installation von SQLXML 4.0 werden keine Dateien, die von früheren Versionen von SQLXML installiert wurden, entfernt. Daher können auf dem Computer DLLs für verschiedene versionsabhängige Installationen von SQLXML vorhanden sein. Sie können die Installationen parallel ausführen. SQLXML 4.0 umfasst sowohl versionsunabhängige als auch versionsabhängige Programm-IDs. Es wird empfohlen, für alle Produktionsanwendungen versionsabhängige Programm-IDs zu verwenden.  
  
## <a name="sqlxml-40-sp1-and-msxml"></a>SQLXML 4.0 SP1 und MSXML  
 MSXML wird von SQLXML 4.0 nicht installiert. SQLXML 4.0 verwendet MSXML 6.0, das im Rahmen der Installation von [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] oder höher installiert wird.  
  
## <a name="redistributing-sqlxml-40-sp1"></a>Verteilen von SQLXML 4.0 SP1  
 Sie können SQLXML 4.0 SP1 mit dem weitervertreibbaren Installer-Paket weitergeben. Eine Möglichkeit, mehrere Pakete in mehreren Installationen, die für den Benutzer wie eine Installation aussehen, zu installieren, besteht in der Verwendung der Chainer- und Bootstrappertechnologie. Weitere Informationen finden Sie unter Authoring a Custom Bootstrapper Package for Visual Studio 2005 und Adding Custom Prerequisites.  
  
 Wenn Ihre Anwendung für eine andere Plattform als für diejenige vorgesehen ist, auf der sie entwickelt wurde, können Sie Versionen von sqlncli.msi für x64, Itanium und x86 vom Microsoft Download Center herunterladen.  
  
 Es gibt auch separate weitervertreibbare Installationsprogramme für MSXML 6.0 (msxml6.msi). Diese befinden sich auf der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Installations-CD an folgendem Speicherort:  
  
 `%CD%\Setup\`  
  
 Mit diesen Installationsdateien kann MSXML 6.0 direkt von der CD installiert werden. Mit den Dateien können MSXML 6.0 zusammen mit SQLXML 4.0 SP1 auch mit eigenen benutzerdefinierten Anwendungen kostenlos verteilt werden.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client muss ebenfalls neu verteilt werden, wenn Sie es mit Ihrer Anwendung als Datenanbieter verwenden. Weitere Informationen finden Sie unter [Installing SQL Server Native Client](../../relational-databases/native-client/applications/installing-sql-server-native-client.md).  
  
## <a name="support-for-sql-server-native-client"></a>Unterstützung für SQL Server Native Client  
 SQLXML 4.0 unterstützt den SQLOLEDB- und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client-Anbieter. Es wird empfohlen, Sie die gleiche Version von verwenden [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client-Anbieter und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client wurde entwickelt, um die neuen Datentypen unterstützen, die auf dem Server, z. B. ausgeliefert die **Date, Time**, **DateTime2**, und **"DateTimeOffset"** Datentypen in [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] und vom unterstützt [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Native Client.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ist eine neue Datenzugriffstechnologie, die in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] eingeführt wurde. Dabei werden die SQLOLEDB-Anbieter und der SQLODBC-Treiber in einer systemeigenen DLL (Dynamic Link Library) zusammengeführt. Außerdem wird eine neue eigenständige Funktionalität bereitgestellt, die sich von Microsoft Data Access Components (MDAC) unterscheidet.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client kann verwendet werden, um die Erstellung neuer Anwendungen oder zur Verbesserung vorhandener Anwendungen, die in eingeführte Funktionen nutzen müssen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , können nicht von SQLOLEDB und SQLODBC in MDAC und [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows. Beispielsweise [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ist erforderlich für clientseitige SQLXML-Funktionen, z. B. FOR XML verwendet das **Xml** -Datentyp. Weitere Informationen finden Sie unter [clientseitige XML-Formatierung &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml/formatting/client-side-xml-formatting-sqlxml-4-0.md), [mithilfe von ADO zum Ausführen von SQLXML 4.0-Abfragen](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md), und [SQL Server Native Client-Programmierung](../../relational-databases/native-client/sql-server-native-client-programming.md).  
  
> [!NOTE]  
>  SQLXML 4.0 ist mit SQLXML 3.0 nicht vollkommen abwärts kompatibel. Virtuelle IIS-Verzeichnisse können aufgrund einiger Fehlerbehebungen und anderer funktioneller Änderungen, insbesondere der Einstellung der SQLXML ISAPI-Unterstützung, nicht mit SQLXML 4.0 verwendet werden. Obwohl die meisten Anwendungen mit geringfügigen Änderungen ausgeführt werden können, müssen sie vor der Inbetriebnahme mit SQLXML 4.0 getestet werden.  
  
## <a name="support-for-data-types-introduced-in-sql-server-2005-and-sql-server-2008"></a>Unterstützung für in SQL Server 2005 und SQL Server 2008 neue Datentypen  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] eingeführt wurden die **Xml** -Datentyp und SQLXML 4.0 unterstützt die **Xml** -Datentyp. Weitere Informationen finden Sie unter [Xml-Datentypunterstützung für SQLXML 4.0](../../relational-databases/sqlxml/xml-data-type-support-in-sqlxml-4-0.md).  
  
 Beispiele, wie der **xml** -Datentyp in SQLXML zum Zuordnen von XML-Sichten, Massenladen von XML oder Ausführen von XML-Updategrams verwendet wird, finden Sie in den folgenden Themen.  
  
-   [Standardzuordnung von XSD-Elementen und-Attributen zu Tabellen und Spalten](../../relational-databases/sqlxml-annotated-xsd-schemas-using/default-mapping-of-xsd-elements-and-attributes-to-tables-and-columns-sqlxml-4-0.md)  
  
-   [Einfügen von Daten mithilfe von XML-Updategrams](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/inserting-data-using-xml-updategrams-sqlxml-4-0.md)  
  
-   [Beispiele für den Massenimport von XML-Dokumenten](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/xml-bulk-load-examples-sqlxml-4-0.md)  
  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] eingeführt wurden die **Datum, Zeit**, **DateTime2**, und **"DateTimeOffset"** -Datentypen. SQLXML 4.0 SP1 aktiviert diese vier neuen Datentypen als integrierte skalare Typen, die bei Verwendung mit [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Native Client OLE DB-Anbieter (SQLNCLI11) gelieferten [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
## <a name="xml-bulk-load-changes-for-sqlxml-40-sp1"></a>Änderungen für XML-Massenladen für SQLXML 4.0 SP1  
  
-   Für SQLXML 4.0 wird das Überlauffeld "schemagen" erstellt, mit der **Xml** -Datentyp. Weitere Informationen finden Sie unter [SQL Server XML Bulk Load-Objektmodell](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/sql-server-xml-bulk-load-object-model-sqlxml-4-0.md).  
  
-   Wenn Sie zuvor [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic-Anwendungen erstellt haben und SQLXML 4.0 verwenden möchten, müssen Sie die Anwendung mit einem Verweis auf Xblkld4.dll erneut kompilieren.  
  
-   Für VBScript-Anwendungen (Visual Basic Scripting Edition) müssen Sie die DLL registrieren, die Sie verwenden möchten. Wenn Sie im folgenden Beispiel versionsunabhängige Programm-IDs angeben, hängt die Anwendung von der zuletzt registrierten DLL ab:  
  
    ```  
    set objBulkLoad = CreateObject("SQLXMLBulkLoad.SQLXMLBulkLoad")   
    ```  
  
    > [!NOTE]  
    >  Die versionsabhängige Programm-ID ist SQLXMLBulkLoad.SQLXMLBulkLoad.4.0.  
  
## <a name="registry-key-changes-for-sqlxml-40"></a>Änderungen des Registrierungsschlüssels für SQLXML 4.0  
 In SQLXML 4.0 wurden die Registrierungsschlüssel aus den früheren Versionen wie folgt geändert:  
  
 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SQLXML4\TemplateCacheSize  
  
 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SQLXML4\SchemaCacheSize  
  
 Sie müssen die Einstellungen ändern, wenn diese Schlüssel für SQLXML 4.0 gültig sein sollen.  
  
 Außerdem führt SQLXML 4.0 die folgenden Registrierungsschlüssel ein:  
  
-   `HKEY_LOCAL_MACHINE\Software\Microsoft\MSSQLServer\Client\SQLXML4\ReportErrorsWithSQLInfo`  
  
     Standardmäßig gibt SQLXML 4.0 von OLE DB-bereitgestellte systemeigene Fehlerinformationen und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] statt eines allgemeinen SQLXML-Fehlers (wie in früheren Versionen von SQLXML der Fall war). Ist dieses Verhalten nicht erwünscht, muss der Wert dieses Registrierungsschlüssels des Typs DWORD auf 0 (NULL) gesetzt werden (der Standardwert ist 1).  
  
-   HKEY_LOCAL_MACHINE\Software\Microsoft\MSSQLServer\Client\SQLXML4\FORXML_GenerateGUIDBraces  
  
     Standardmäßig gibt SQLXML SQL Server GUID-Werte ohne geschweifte Klammern zurück. Wenn der GUID-Wert in geschweiften Klammern zurückgegeben werden soll (z.&nbsp;B. {*GUID*}) muss der Wert für diesen Registrierungsschlüssel auf 1 gesetzt werden (der Standardwert ist 0).  
  
-   HKEY_LOCAL_MACHINE\Software\Microsoft\MSSQLServer\Client\SQLXML4\SQL2000CompatMode  
  
     Wenn der XML-Parser die Daten lädt, werden Leerzeichen standardmäßig den XML 1.0-Regeln entsprechend normalisiert. Dadurch gehen einige Leerzeichen in Ihren Daten verloren. Daher ist die Textdarstellung Ihrer Daten nach der Analyse möglicherweise nicht unverändert, wobei die Daten semantisch jedoch identisch sind.  
  
     Dieser Schlüssel wurde eingeführt, sodass Sie die Leerzeichen in den Daten bei Bedarf beibehalten können. Wenn Sie diesen Registrierungsschlüssel hinzufügen und seinen Wert auf 0 (NULL) setzen, werden Leerzeichen (LF, CR und TAB) in XML bei Attributwerten codiert zurückgegeben. Bei Elementwerten wird nur CR codiert zurückgegeben.  
  
     Beispiel:  
  
    ```  
    CREATE TABLE T( Col1 int, Col2 nvarchar(100));  
    GO  
    -- Insert data with tab, line feed and carriage return).  
    INSERT INTO T VALUES (1, 'This is a tab    . This is a line feed and CR   
     more text');  
    GO  
    -- Test this query (without the registry key).  
    SELECT * FROM T   
    FOR XML AUTO;  
    -- This is the result (no encoding of special characters).  
    <?xml version="1.0" encoding="utf-8" ?>  
    <r>  
      <T Col1="1"   
         Col2="This is a tab    . This is a line feed and CR   
     more text"/>  
    </r>  
    -- Now add registry key with value 0 and execute the query again.  
    -- Note the encoding for carriage return, line-feed and tab in the attribute value.  
    <?xml version="1.0" encoding="utf-8" ?>  
    <r>  
      <T Col1="1"   
         Col2="This is a tab    . This is a line feed and CR   
     more text"/>  
    </r>  
  
    -- Update the query and specify ELEMENTS directive  
    SELECT * FROM T  
    FOR XML AUTO, ELEMENTS  
    -- Only the carriage return is returned encoded.  
    <?xml version="1.0" encoding="utf-8" ?>  
    <r>  
       <T>  
          <Col1>1</Col1>  
          <Col2>This is a tab    . This is a line feed and CR   
     more text</Col2>  
       </T>  
    </r>  
    ```  
  
## <a name="migration-issues"></a>Migrationsprobleme  
 Die folgenden Probleme können sich negativ auf die Migration der älteren SQLXML-Anwendungen auf SQLXML 4.0 auswirken.  
  
### <a name="ado-and-sqlxml-40-queries"></a>ADO- und SQLXML 4.0-Abfragen  
 In früheren Versionen von SQLXML wurde die URL-basierte Abfrageausführung mit virtuellen IIS-Verzeichnissen und dem SQLXML ISAPI-Filter unterstützt. Für Anwendungen, die SQLXML 4.0 verwenden, ist diese Unterstützung nicht mehr verfügbar.  
  
 Stattdessen können SQLXML-Abfragen, -Vorlagen und -Updategrams mit den SQLXML-Erweiterungen für ActiveX Data Objects (ADO) ausgeführt werden, die in Microsoft Data Access Components (MDAC) 2.6 eingeführt wurden.  
  
 Weitere Informationen finden Sie unter [mithilfe von ADO zum Ausführen von SQLXML 4.0-Abfragen](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
### <a name="supportability-for-sqlxml-30-isapi-and-data-types-introduced-in-sql-server-2005"></a>Unterstützung für SQLXML 3.0 ISAPI und in SQL Server eingeführte Datentypen  
 Da die ISAPI-Unterstützung von SQLXML 4.0 entfernt wurde, wenn Ihre Lösung die erweiterten Daten eingeben erfordert eingeführte Funktionen [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] wie z. B. die [Xml-Datentyp](../../t-sql/xml/xml-transact-sql.md) oder [benutzerdefinierte Datentypen (UDTs)](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)und Web-based Access müssen Sie eine andere Lösung verwenden, z. B. [verwaltete SQLXML-Klassen](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/sqlxml-4-0-net-framework-support-managed-classes.md) oder anderen HTTP-Handler, wie z. B. systemeigene XML-Webdienste für SQL Server 2005.  
  
 Wenn diese typerweiterungen nicht erforderlich ist, können Sie alternativ weiter SQLXML 3.0 zu verwenden, für die Verbindung [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] und [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] Installationen. Die SQLXML 3.0 ISAPI-Unterstützung wird für diese neueren Versionen funktionieren jedoch nicht unterstützt oder erkennt die **Xml** -Datentyp oder UDT-typunterstützung eingeführten [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
  
### <a name="xml-bulk-load-security-changes-for-temporary-files"></a>Sicherheitsänderungen für das XML-Massenladen für temporäre Dateien  
 Für SQLXML 4.0 und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] werden dem Benutzer, der den Massenladenvorgang ausführt, Dateiberechtigungen für das XML-Massenladen erteilt. Lese- und Schreibberechtigungen werden vom Dateisystem geerbt. In früheren Versionen von SQLXML und SQL Server wurden durch das XML-Massenladen unter SQLXML temporäre Dateien erstellt, die nicht sicher waren und von allen Benutzern gelesen werden konnten.  
  
### <a name="migration-issues-for-client-side-for-xml"></a>Migrationsprobleme für clientseitiges FOR XML  
 Aufgrund von Änderungen im Ausführungsmodul gibt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] möglicherweise unterschiedliche Werte in den Metadaten für eine Basistabelle zurück, als würde zurückgegeben, wenn Sie mit die FOR XML-Abfrage ausgeführt wurde [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]. In diesen Fällen hat die clientseitige Formatierung der FOR XML-Abfrageergebnisse abhängig von der Version, mit der die Abfrage ausgeführt wird, eine andere Ausgabe.  
  
 Wenn eine FOR XML-Abfrage clientseitig mit SQLXML 3.0 über eine **xml** -Datentypspalte ausgeführt wird, werden die Daten in den Ergebnissen als vollständige in Entitäten geänderte Zeichenfolge zurückgegeben. In SQLXML 4.0 Wenn die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client (SQLNCLI11) als Datenanbieter angegeben ist, die Daten werden werden als XML zurückgegeben.  
  
  
