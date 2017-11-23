---
title: "Datensätze und Datenströme | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- streams [ADO]
- streams [ADO], about streams
- records [ADO]
ms.assetid: 4d68868e-2611-4b5c-9a89-7caa5f753151
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: cfe5f8e48eb88233949102e988f3a2296cf373b4
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="records-and-streams"></a>Datensätze und Datenströme
ADO stellt derzeit die [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) Objekt als das primäre Mittel, um den Zugriff auf Daten in Datenquellen, z. B. relationalen Datenbanken. Einige Anbieter unterstützen jedoch die [Datensatz](../../../ado/reference/ado-api/record-object-ado.md) und [Stream](../../../ado/reference/ado-api/stream-object-ado.md) Objekte als alternative oder Ergänzung Objekte, mit denen Daten von Anbietern bearbeitet werden können. Besonderheiten zur **Datensatz** Verhalten, finden Sie in der Dokumentation Ihres Anbieters.  
  
## <a name="records"></a>Datensätze  
 **Datensatz** Objekte funktionieren im Wesentlichen als einzelne Zeilen **Recordset**s. Allerdings **Datensätze** haben eingeschränkte Funktionalität, die im Vergleich zu **Recordsets** und verfügen über unterschiedliche Eigenschaften und Methoden. Die Quelle für die Daten in einem **Datensatz** -Objekt eines Befehls, der eine Zeile mit Daten vom Anbieter zurückgegeben werden kann. Mit **Datensatz** Objekte statt **Recordset** -Objekten, die die Ergebnisse aus einer Abfrage zu erhalten, die eine Zeile mit Daten zurückgibt, beseitigt den Mehraufwand der Instanziierung je komplexer **Recordset**  Objekt.  
  
 **Datensatz** Objekte können einen anderen Zweck dienen, insbesondere bei Anbietern für andere Datenquellen als herkömmliche relationale Datenbanken, wie z. B. die [Microsoft OLE DB-Anbieter für Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Ein Großteil der Informationen, die verarbeitet werden muss, vorhanden ist, nicht als Tabellen in Datenbanken, sondern als Nachrichten in e-Mail-Systeme und Dateien in modernen Dateisystemen. Die **Datensatz** und **Stream** Objekte zu ermöglichen, den Zugriff auf in anderen Quellen als relationalen Datenbanken gespeicherten Informationen.  
  
 Die **Datensatz** Objekt darstellen und Daten, z. B. Verzeichnisse und Dateien in einem Dateisystem oder Ordner und Nachrichten in einem e-Mail-System verwalten kann. Für diese Zwecke wird die Quelle für die **Datensatz** kann die aktuelle Zeile eines geöffneten **Recordset**, eine absolute URL oder eine relative URL in Verbindung mit einem geöffneten [Verbindung](../../../ado/reference/ado-api/connection-object-ado.md) -Objekt.  
  
 In der Regel eine **Recordset** können verwendet werden, um einen Container oder das übergeordnete Element in einer Hierarchie, z. B. einen Ordner oder Verzeichnis darstellen. Ein **Datensatz** können verwendet werden, um bestimmte Informationen zu einem Knoten in den übergeordneten Container, z. B. eine Datei oder des Dokuments zurückzugeben. Der wichtigste Grund **Datensätze** verwendet, um diese Art von Informationen darzustellen, dass diese Datenquellen heterogen sind. Dies bedeutet, dass jedes **Datensatz** möglicherweise einen anderen Satz und die Anzahl der Felder. Herkömmliche **Recordsets** enthaltenen Zeilen aus einer Datenbank sind homogenen, was bedeutet, dass jede Zeile die gleiche Anzahl und Typ der Felder aufweist.  
  
 Weitere Informationen zum Verwenden der **Datensatz** -Objekt für die Verarbeitung dieser heterogene Daten von Anbietern wie z. B. die Publishing Internetanbieter, finden Sie unter [mithilfe von ADO für Internet Publishing](../../../ado/guide/data/using-ado-for-internet-publishing.md).  
  
## <a name="streams"></a>Datenströme  
 Die **Stream** Objekt bietet die Möglichkeit zum Lesen, schreiben und verwalten einen Datenstrom von Bytes. Dieser Bytedatenstrom kann Text oder binär sein und in der Größe nur durch die verfügbaren Systemressourcen begrenzt ist. In der Regel ADO **Stream** Objekte werden für folgende Zwecke verwendet:  
  
-   Um die Daten enthalten ein **Recordset** im XML-Format gespeichert. Diese XML-Streams aus gespeicherten **Recordset**s kann als Quelle verwendet werden, wenn Sie ein neues öffnen **Recordset**. Weitere Informationen finden Sie unter [Streams und Persistenz](../../../ado/guide/data/streams-and-persistence.md).  
  
-   Enthält [CommandStreams](../../../ado/reference/ado-api/commandstream-property-ado.md) für den Anbieter als Alternative zur auszuführenden [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md). Beispielsweise kann XML-UpdateGrams als Quelle für einen Befehl für den Microsoft OLE DB-Anbieter für SQL Server verwendet werden.  
  
-   Zum Empfangen von Ergebnissen vom Anbieter in einem Format außer einem **Recordset**, z. B. XML-Ergebnisse aus der Microsoft OLE DB-Anbieter für SQL Server. Weitere Informationen finden Sie unter [Abrufen von Resultsets in Streams](../../../ado/guide/data/retrieving-resultsets-into-streams.md).  
  
-   Enthält den Text oder Bytes, die eine Datei oder eine Meldung, in der Regel mit Anbietern wie z. B. der Microsoft OLE DB-Anbieter für Internet Publishing verwendet bilden. Weitere Informationen über diese Verwendung von **Stream** anzuzeigen, [mithilfe von ADO für Internet Publishing](../../../ado/guide/data/using-ado-for-internet-publishing.md).  
  
 Ein **Stream** Objekt kann auf geöffnet werden:  
  
-   Eine einfache Datei mit einer URL angegeben.  
  
-   Ein Feld von einem **Datensatz** oder **Recordset** , enthält eine **Stream** Objekt.  
  
-   Die Standarddatenstrom von einer **Datensatz** oder **Recordset** Objekt, das ein Verzeichnis oder eine Verbunddatei darstellt.  
  
-   Ein Feld für die Ressource, die eine einfache Datei-URL enthält.  
  
-   Keine bestimmte Quelle. In diesem Fall eine **Stream** Objekt im Arbeitsspeicher geöffnet wird. Daten können darauf geschrieben und anschließend in einer anderen gespeichert **Stream** oder Datei.  
  
-   Ein BLOB-Feld in einem **Recordset**.  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [Streams und Persistenz](../../../ado/guide/data/streams-and-persistence.md)  
  
-   [Command-Streams](../../../ado/guide/data/command-streams.md)  
  
-   [Abrufen von Resultsets in Streams](../../../ado/guide/data/retrieving-resultsets-into-streams.md)  
  
-   [Using ADO for Internet Publishing (Verwenden von ADO für Internet-Publishing)](../../../ado/guide/data/using-ado-for-internet-publishing.md)
