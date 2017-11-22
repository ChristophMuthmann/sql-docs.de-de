---
title: "Einführung in den SQLXMLOLEDB-Anbieter (SQLXML 4.0) | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: sqlxml
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-xml
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- SQLXMLOLEDB Provider, properties
- adExecuteStream flag
- SQLXMLOLEDB Provider, about SQLXMLOLEDB Provider
ms.assetid: 2e3f3817-4209-4bf4-9f46-248c95bc6f1b
caps.latest.revision: "16"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 87c5d06433a07ac722af92ed64b7c9551d340f96
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="introduction-to-the-sqlxmloledb-provider-sqlxml-40"></a>Einführung in den SQLXMLOLEDB-Anbieter (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]Der SQLXMLOLEDB-Anbieter ist ein OLE DB-Anbieter, der verfügbar macht [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML-Funktionalität durch ActiveX Data Objects (ADO). Der Anbieter kann Befehle jedoch nur im ADO-Modus zum Schreiben in einen Ausgabedatenstrom ausführen. Der SQLXMLOLEDB-Anbieter ist kein Rowsetanbieter. Wenn Sie einen Befehl ausführen, müssen Sie die AdExecuteStream-Flag angeben, die den Ausgabestream, den Sie angegeben haben, verwenden von ADO anweist.  
  
 Das folgende Beispiel zeigt die Syntax für die Execute-Befehl in dem die AdExecuteStream-Flag angegeben wird:  
  
```  
Dim oTestCommand As New ADODB.Command  
...  
oTestCommand.Properties("Output Stream").Value = oTestStream  
oTestCommand.Execute , , adExecuteStream  
...  
```  
  
## <a name="sqlxmloledb-provider-specific-properties"></a>Anbieterspezifische SQLXMLOLEDB-Eigenschaften  
 Der SQLXMLOLEDB-Anbieter stellt die folgenden anbieterspezifischen Verbindungseigenschaften zur Verfügung.  
  
|Verbindung<br /><br /> Eigenschaft|Standardwert<br /><br /> (ggf.)|Description|  
|-----------------------------|----------------------------|-----------------|  
|Datenanbieter||Stellt die PROGID des OLE DB-Anbieters zur Verfügung, durch die SQLXMLOLEDB die Befehle ausführt. Ab SQLXML 4.0 und [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] ist dieser Anbieter in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client enthalten. Daher ist dieser Eigenschaftswert auf "SQLNCLI11" beschränkt. Weitere Informationen finden Sie unter [SQL Server Native Client-Programmierung](../../../relational-databases/native-client/sql-server-native-client-programming.md).|  
  
 Der SQLXMLOLEDB-Anbieter stellt die folgenden anbieterspezifischen Befehlseigenschaften zur Verfügung.  
  
|Befehl<br /><br /> Eigenschaft|Standardwert<br /><br /> (ggf.)|Description|  
|--------------------------|----------------------------|-----------------|  
|Basispfad|""|Gibt den Basispfad der Datei an. Der Basispfad der Datei gibt den Speicherort der XSL-Dateien (XML Stylesheet Language) oder der Zuordnungsschemadateien an. Der Pfad für die Basisdatei dient außerdem zum Auflösen der relativen Pfade der XSL- oder zuordnungsschemadateien auf, die in den Eigenschaften der XSL- oder Zuordnungsschema angegeben wurden.<br /><br /> Ein Beispiel, in dem diese Eigenschaft wird verwendet, finden Sie unter [Ausführen von XPath-Abfragen &#40; SQLXMLOLEDB-Anbieter &#41; ](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/data-access-components-provider/executing-xpath-queries-sqlxmloledb-provider.md).|  
|ClientSideXML|False|Legen Sie diese Eigenschaft auf True fest, wenn die Konvertierung des Rowsets in XLM statt auf dem Server auf dem Client erfolgen soll. Dies ist nützlich, wenn Sie die Ladeleistungslast auf die mittlere Ebene verschieben möchten.<br /><br /> Ein Beispiel, in dem diese Eigenschaft wird verwendet, finden Sie unter [SQL-Abfragen ausführen &#40; SQLXMLOLEDB-Anbieter &#41; ](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/data-access-components-provider/executing-sql-queries-sqlxmloledb-provider.md) oder [Ausführen von Vorlagen, die SQL-Abfragen &#40; enthalten SQLXMLOLEDB-Anbieter &#41; ](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/data-access-components-provider/executing-templates-that-contain-sql-queries-sqlxmloledb-provider.md).|  
|Inhaltstyp||Gibt den Ausgabeinhaltstyp zurück. Dies ist eine schreibgeschützte Eigenschaft.<br /><br /> Diese Eigenschaft stellt dem Browser Informationen über den Inhaltstyp (z. B. TEXT/XML, TEXT/HTML, image/jpeg usw.) zur Verfügung. Der Wert dieser Eigenschaft wird die **Inhaltstyp** Feld, das an den Browser als Teil der HTTP-Header gesendet wird, die den MIME-Typ (Multipurpose Internet Mail Extensions), der als Textkörper gesendeten Dokuments enthält.|  
|Zuordnungsschema|NULL|Wenn eine Clientanwendung eine XPath-Abfrage für ein Zuordnungsschema (XDR oder XSD) ausführt, wird mit dieser Eigenschaft der Name des Zuordnungsschemas angegeben.<br /><br /> Der Pfad, der angegeben wird, kann relativ (xyz/abc/MySchema.xml) oder absolut (C:\MyFolder\abc\MySchema.xml) sein.<br /><br /> Wenn ein relativer Pfad angegeben wird, wird der Basispfad, der von der Basispfad-Eigenschaft angegeben wird zum Auflösen des relativen Pfads verwendet. Wenn kein Pfad in der Eigenschaft Base Pfad angegeben wurde, ist der relative Pfad relativ zum aktuellen Verzeichnis.<br /><br /> Geben Sie einen Wert für das Mapping-Schema-Eigenschaft, können Sie einen lokalen Verzeichnispfad oder eine URL (http://...) angeben. Wenn Sie eine URL angeben, müssen Sie WinHTTP für den Zugriff auf den HTTP- und den HTTPS-Server über einen Proxyserver konfigurieren. Führen Sie dazu das Hilfsprogramm Proxycfg.exe aus. Weitere Informationen finden Sie im Abschnitt über das Verwenden des WinHTTP-Proxy-Konfigurationshilfsprogramms in der MSDN Library.<br /><br /> Ein Beispiel, in dem diese Eigenschaft wird verwendet, finden Sie unter [Ausführen von XPath-Abfragen &#40; SQLXMLOLEDB-Anbieter &#41; ](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/data-access-components-provider/executing-xpath-queries-sqlxmloledb-provider.md).|  
|Namespaces||Diese Eigenschaft ermöglicht die Ausführung von XPath-Abfragen, die Namespaces verwenden. Ein Beispiel, in dem diese Eigenschaft wird verwendet, finden Sie unter [Ausführen von XPath-Abfragen mit Namespaces &#40; SQLXMLOLEDB-Anbieter &#41; ](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/data-access-components-provider/executing-xpath-queries-with-namespaces-sqlxmloledb-provider.md).|  
|ss Stream Flags||Diese Eigenschaft wird verwendet, um bestimmte Arten von Sicherheitseinschränkungen anzugeben. Beispielsweise sollen keine URL-Verweise auf Dateien oder absolute Pfade für Dateien (wie externe Websites) zugelassen werden. Oder es sollen keine Abfragen in den Vorlagen zulässig sein.<br /><br /> Der Eigenschaft können folgende Werte zugewiesen werden:<br /><br /> 1 = STREAM_FLAGS_DISALLOW_URL 2 = STREAM_FLAGS_DISALLOW_ABSOLUTE_PATH 4 = STREAM_FLAGS_DISALLOW_QUERY 8 = STREAM_FLAGS_ DONTCACHEMAPPINGSCHEMA 16 = STREAM_FLAGS_DONTCACHETEMPLATE 32 = STREAM_FLAGS_DONTCACHEXSL<br /><br /> Weitere Informationen über diese Werte sind in der nächsten Tabelle enthalten.|  
|XML-Stamm||Diese Eigenschaft wird verwendet, um ein Stammtag für das resultierende XML zu definieren. Wenn Sie beispielsweise SQL-Abfragen für die Datenbank ausführen und das resultierende XML-Dokument kein einzelnes Stammelement hat, wird der Wert der Eigenschaft dazu verwendet, dem Dokument ein einzelnes Stammelement hinzuzufügen.<br /><br /> Ein Beispiel, in dem diese Eigenschaft wird verwendet, finden Sie unter [SQL-Abfragen ausführen &#40; SQLXMLOLEDB-Anbieter &#41; ](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/data-access-components-provider/executing-sql-queries-sqlxmloledb-provider.md).|  
|XSL||Mit dieser Eigenschaft wird der XSL-Dateiname angegeben, wenn die XSL-Transformation auf das von der Abfrage zurückgegebene XML-Dokument angewendet werden soll.<br /><br /> Der Pfad, der angegeben wird, kann relativ (xyz/abc/MyXSL.xsl) oder absolut (C:\MyFolder\abc\MyXSL.xsl) sein.<br /><br /> Wenn ein relativer Pfad angegeben wird, wird der Basispfad, der von der Basispfad-Eigenschaft angegeben wird zum Auflösen des relativen Pfads verwendet. Wenn kein Pfad in der Eigenschaft Base Pfad angegeben wurde, ist der relative Pfad relativ zum aktuellen Verzeichnis.<br /><br /> Ein Beispiel, in dem diese Eigenschaft verwendet wird, finden Sie in der Anwenden einer XSL-Transformation (SQLXMLOLEDB-Anbieter).|  
  
 Die folgende Tabelle enthält Beschreibungen der ss Stream Flags-Eigenschaftswerte.  
  
|Eigenschaftswert|Description|  
|--------------------|-----------------|  
|STREAM_FLAGS_DISALLOW_URL|URLs werden nicht zum Zuordnen von Schemas oder XSL akzeptiert.|  
|STREAM_FLAGS_DISALLOW_ABSOLTE_PATH|Ein für das Zuordnungschema oder für XSL angegebener Pfad muss sich auf den Basispfad der Vorlage selbst beziehen.|  
|STREAM_FLAGS_DISALLOW_QUERY|Abfragen sind in einer Vorlage nicht zulässig.|  
|STREAM_FLAGS_DONTCACHEMAPPINGSCHEMA|Das Zuordnungsschema wird nicht zwischengespeichert. Dieser Eigenschaftswert ist während der Datenbankentwicklungsphase nützlich, wenn Datenbankschemas Änderungen unterliegen.|  
|STREAM_FLAGS_DONTCACHETEMPLATE|Vorlagen werden nicht zwischengespeichert.|  
|STREAM_FLAGS_DONTCACHEXSL|XSL wird nicht zwischengespeichert.|  
  
  
