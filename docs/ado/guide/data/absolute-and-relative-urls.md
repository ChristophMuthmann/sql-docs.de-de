---
title: Absoluten und relativen URLs | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- relative URLs [ADO]
- absolute URLs [ADO]
- URLs [ADO]
ms.assetid: 6a34a7ef-50cc-4c3d-82f7-106b9a8f3caf
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ba1ab2c9bdc1adbc063cd05e88cf9d0001efb15c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="absolute-and-relative-urls"></a>Absoluten und relativen URLs
Eine URL gibt den Speicherort der ein Ziel auf einem Computer lokal oder im Netzwerk gespeichert. Das Ziel kann eine Datei, Verzeichnis, HTML-Seite, Bild, Programm usw.*.*  
  
 Ein *absolute URL* enthält alle Informationen, die erforderlich sind, um eine Ressource zu suchen.  
  
 Ein *relative URL* sucht nach einer Ressource eine absolute URL als Ausgangspunkt verwenden. Aktiviert ist, die "Vollständiger URL" des Ziels, werden angegeben durch Verketten der absoluten und relativen URLs.  
  
 Ein *absolute URL* verwendet das folgende Format: *Scheme://server/path/resource*  
  
 Eine relative URL in der Regel besteht ausschließlich aus der *Pfad*, und optional die *Ressource*, aber keine *Schema* oder *Server*. In den folgenden Tabellen definieren die einzelnen Bestandteile von der vollständigen URL-Format.  
  
 *Partitionsschema*  
 Gibt an, wie die *Ressource* erfolgen muss.  
  
 *server*  
 Gibt den Namen des Computers, auf dem die *Ressource* befindet.  
  
 *path*  
 Gibt die Sequenz von Verzeichnissen an das Ziel. Wenn *Ressource* wird weggelassen, ist das Ziel der letzten Verzeichnisses in *Pfad*.  
  
 *resource*  
 Wenn enthalten, *Ressource* ist das Ziel, und ist in der Regel der Name einer Datei. Möglicherweise eine *einfache Datei* , enthält einen einzelnen binären Datenstrom von Bytes, oder ein *strukturierte Dokument* , eine oder mehrere Speicher und binäre Streams von Bytes enthält.  
  
## <a name="url-scheme-registration"></a>URL-Schema-Registrierung  
 Wenn ein Anbieter URLs unterstützt, wird der Anbieter eine oder mehrere URL-Schemas registriert. Registrierung bedeutet, dass alle URLs, die mit dem Schema den registrierten Anbieter automatisch aufgerufen werden. Z. B. die *http* Schema registriert ist die [Microsoft OLE DB-Anbieter für Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). ADO wird davon ausgegangen, dass alle URLs, die mit dem Präfix "http" darstellen, Web-Ordner oder Dateien mit dem Internet Publishing-Anbieter verwendet werden soll. Informationen zu den Schemas, die von Ihrem Anbieter registriert finden Sie in der Dokumentation Ihres Anbieters.  
  
## <a name="defining-context-with-a-url"></a>Definieren von Kontext mit einer URL  
 Eine Funktion einer geöffneten Verbindung, dargestellt durch eine [Verbindung](../../../ado/reference/ado-api/connection-object-ado.md) -Objekt, um nachfolgende Vorgänge mit der Datenquelle zu beschränken liegt über diese Verbindung. Die Verbindung definiert, also den Kontext für nachfolgende Operationen.  
  
 Eine absolute URL kann auch einen Kontext definieren, mit ADO 2.7 oder höher. Z. B., wenn ein [Datensatz](../../../ado/reference/ado-api/record-object-ado.md) Objekt wird geöffnet, mit der eine absolute URL eine **Verbindung** Objekt wird implizit erstellt, um die von der URL angegebene Ressource darstellen.  
  
 Eine absolute URL, die einen Kontext definiert kann angegeben werden, der *ActiveConnection* Parameter von der **Datensatz** Objekt [öffnen](../../../ado/reference/ado-api/open-method-ado-record.md) Methode. Eine absolute URL kann auch angegeben werden, als Wert für die "URL**=**"-Schlüsselwort in der **Verbindung** Objekt [öffnen](../../../ado/reference/ado-api/open-method-ado-connection.md) Methode  *"ConnectionString"* Parameter, und die [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) Objekt [öffnen](../../../ado/reference/ado-api/open-method-ado-recordset.md) Methode *ActiveConnection* Parameter.  
  
 Kontext kann auch definiert werden, indem Sie öffnen ein **Datensatz** oder **Recordset** Objekt, das ein Verzeichnis darstellt, da diese Objekte bereits über einen implizit oder explizit deklarierten verfügen **Verbindung**  Objekt, das Kontext angibt.  
  
## <a name="scoped-operations"></a>Bereichsbezogene Vorgänge  
 Definiert der Kontext auch Bereich – d. h. das Verzeichnis und seinen Unterverzeichnissen, die in nachfolgenden Vorgängen teilnehmen kann. Die **Datensatz** Objekt verfügt über mehrere Bereichsbezogene Methoden, die in einem Verzeichnis ausgeführt werden und alle Unterverzeichnisse. Zu diesen Methoden gehören [CopyRecord](../../../ado/reference/ado-api/copyrecord-method-ado.md), [MoveRecord](../../../ado/reference/ado-api/moverecord-method-ado.md), und [DeleteRecord](../../../ado/reference/ado-api/deleterecord-method-ado.md).  
  
## <a name="relative-urls-as-command-text"></a>Relative URLs als Befehlstext  
 Können Sie angeben, einen Befehl für die Datenquelle ausgeführt wird, durch Eingabe einer Zeichenfolge in der *CommandText* Parameter von der **Verbindung** des Objekts [Execute](../../../ado/reference/ado-api/execute-method-ado-connection.md) -Methode, und in der  *Quelle* Parameter von der **Recordset** des Objekts [öffnen](../../../ado/reference/ado-api/open-method-ado-recordset.md) Methode.  
  
 Eine relative URL angegeben werden kann, der *CommandText* oder *Quelle* Parameter. Die relative URL stellt einen Befehl, z. B. ein SQL‑Befehl nicht tatsächlich dar; Es gibt nur die Parameter. Der Kontext der aktiven Verbindung muss eine absolute URL sein und die *Option* -Parameter muss festgelegt werden, um **AdCmdTableDirect**.  
  
 Beispielsweise wird im folgenden Codebeispiel wird gezeigt, wie zum Öffnen einer **Recordset** für die Datei ///Readme25.txt des Verzeichnisses "Winnt/System32":  
  
```  
recordset.Open "system32/Readme25.txt", "URL=http://YourServer/Winnt/",,,adCmdTableDirect  
```  
  
 Die absolute URL in der Verbindungszeichenfolge gibt den Server (`YourServer`) und den Pfad (`Winnt`). Diese URL definiert auch den Kontext.  
  
 Die relative URL im Befehlstext wird die absolute URL als Ausgangspunkt verwendet und gibt den Rest des Pfads (`system32`) und die zu öffnende Datei (`Readme25.txt`).  
  
 Das Feld "Options" (`adCmdTableDirect`) gibt an, dass der Befehlstyp eine relative URL ist.  
  
 Wenn Sie beispielsweise der folgende Code wird geöffnet eine **Recordset** auf dem Inhalt der `Winnt` Verzeichnis:  
  
```  
recordset.Open "", "URL=http://YourServer/Winnt/",,,adCmdTableDirect  
```  
  
## <a name="ole-db-provider-supplied-url-schemes"></a>OLE DB-Anbieter bereitgestellte URL-Schemas  
 Der erste Teil einer vollqualifizierten URL ist die *Schema* , die Zugriff auf die Ressource identifiziert, indem Sie den Rest der URL verwendet wird. Beispiele sind HTTP (Hypertext Transfer Protocol) und FTP (File Transfer Protocol).  
  
 ADO unterstützt OLE DB-Anbieter, mit die erkannt eigenen URL-Schemas. Z. B. die [Microsoft OLE DB-Anbieter für Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)*,* vorhandene HTTP-Protokollschema erkennt das "veröffentlichte" Windows 2000-Dateien zugegriffen wird.  
  
## <a name="see-also"></a>Siehe auch  
 [Verbindungsobjekt (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Das Datensatzobjekt (ADO)](../../../ado/reference/ado-api/record-object-ado.md)   
 [Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
