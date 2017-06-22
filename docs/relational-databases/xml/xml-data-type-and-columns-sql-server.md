---
title: XML-Datentyp und -Spalten (SQL Server) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 00db8f21-7d4b-4347-ae43-3a7c314d2fa1
caps.latest.revision: 6
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 457cf9fb3c207a89467b96e0f1744f9371edb9a4
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="xml-data-type-and-columns-sql-server"></a>XML-Datentyp und -Spalten (SQL Server)
  In diesem Thema werden die Vorteile und die Einschränkungen des **XML** -Datentyps für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]erläutert. Es soll Ihnen zudem die Entscheidung vereinfachen, wie XML-Daten gespeichert werden.  
  
## <a name="relational-or-xml-data-model"></a>Relationales oder XML-Datenmodell  
 Wenn Ihre Daten sehr strukturiert sind und ein bekanntes Schema aufweisen, ist das relationale Modell möglicherweise zur Datenspeicherung am besten geeignet. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] stellt die dazu erforderliche Funktionalität und die benötigten Tools bereit. Wenn Ihre Daten dagegen halbstrukturiert oder nicht strukturiert sind oder ihre Struktur unbekannt ist, müssen Sie das Modellieren dieser Daten in Erwägung ziehen.  
  
 XML ist eine gute Wahl, wenn Sie ein plattformunabhängiges Modell anstreben, um die Übertragbarkeit der Daten durch Verwendung von strukturellen und semantischen Markups sicherzustellen. XML ist darüber hinaus eine geeignete Option, wenn einige der folgenden Eigenschaften erfüllt sind:  
  
-   Ihre Daten besitzen nur eine geringe Dichte, Sie kennen die Struktur der Daten nicht, oder die Struktur Ihrer Daten kann sich in Zukunft erheblich ändern.  
  
-   Ihre Daten stellen keine Verweise zwischen Entitäten dar, sondern entsprechen einer Einkapselungshierarchie, die auch rekursiv sein kann.  
  
-   Ihre Daten weisen eine inhärente Reihenfolge auf.  
  
-   Sie wollen basierend auf der Struktur Ihrer Daten Abfragen in den Daten ausführen oder Teile der Daten aktualisieren.  
  
 Wenn keine dieser Bedingungen zutrifft, sollten Sie das relationale Datenmodell verwenden. Wenn die Daten z.B. im XML-Format vorliegen, die Anwendung die Datenbank jedoch ausschließlich zum Speichern und Abrufen der Daten verwendet, benötigen Sie lediglich eine **[n]varchar(max)** -Spalte. Das Speichern der Daten in einer XML-Spalte bietet weitere Vorteile. Beispielsweise kann mit dem Modul ermittelt werden, ob die Daten wohlgeformt oder gültig sind, und es werden auch differenzierte Abfragen und Updates der XML-Daten unterstützt.  
  
## <a name="reasons-for-storing-xml-data-in-sql-server"></a>Gründe für das Speichern von XML-Daten in SQL Server  
 Im Folgenden werden einige Gründe angeführt, die dafür sprechen, Ihre Daten nicht im Dateisystem zu verwalten, sondern die systemeigenen XML-Funktionen in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zu verwenden.  
  
-   Sie wollen Ihre XML-Daten auf effiziente und transaktive Weise freigeben, abfragen und ändern. Ein differenzierter Datenzugriff ist für Ihre Anwendung sehr wichtig. Sie wollen z. B. einige der Abschnitte innerhalb eines XML-Dokuments extrahieren, oder Sie wollen einen neuen Abschnitt einfügen, ohne Ihr gesamtes Dokument ersetzen zu müssen.  
  
-   Sie verfügen über relationale Daten und XML-Daten und wollen innerhalb Ihrer Anwendung die Interoperabilität zwischen den relationalen Daten und den XML-Daten gewährleisten.  
  
-   Sie benötigen die Sprachenunterstützung für Abfragen und Möglichkeiten zur Datenänderung für domänenübergreifende Anwendungen.  
  
-   Sie wollen vom Server sicherstellen lassen, dass die Daten wohlgeformt sind, und Ihre Daten auch optional gemäß XML-Schemas überprüfen lassen.  
  
-   Sie wünschen eine Indizierung von XML-Daten, um ein effizientes Verarbeiten von Abfragen und eine gute Skalierbarkeit zu ermöglichen, und wollen einen erstklassigen Abfrageoptimierer verwenden.  
  
-   Sie wünschen den SOAP-, ADO.NET- und OLE DB-Zugriff auf XML-Daten.  
  
-   Sie möchten Verwaltungsfunktionen für den Datenbankserver verwenden, um Ihre XML-Daten zu verwalten. Dazu gehören z. B. Sicherung, Wiederherstellung und Replikation der Daten.  
  
 Wenn keine dieser Bedingungen zutrifft, kann es besser sein, die Daten in einem Nicht-XML-Datentyp für große Objekte zu speichern, beispielsweise in **[n]varchar(max)** oder **varbinary(max)**.  
  
## <a name="xml-storage-options"></a>XML-Speicheroptionen  
 Für das Speichern von XML in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] stehen die folgenden Optionen zur Verfügung:  
  
-   Systemeigenes Speichern als **xml** -Datentyp  
  
     Die Daten werden in einer internen Darstellung gespeichert, die den XML-Inhalt der Daten beibehält. Diese interne Darstellung umfasst Informationen über die Einkapselungshierarchie, die Dokumentreihenfolge sowie die Element- und Attributwerte. Insbesondere bleibt der InfoSet-Inhalt der XML-Daten erhalten. Weitere Informationen zu InfoSet finden Sie unter [http://www.w3.org/TR/xml-infoset](http://go.microsoft.com/fwlink/?LinkId=48843). Der InfoSet-Inhalt ist möglicherweise keine identische Kopie der Text-XML, weil die folgenden Informationen nicht erhalten bleiben: insignifikante Leerzeichen, Reihenfolge der Attribute, Namespace-Präfixe und XML-Deklaration.  
  
     Für den typisierten **XML** -Datentyp, ein an **XML** -Schemas gebundener -Datentyp, werden durch das PSVI (Post-Schema Validation InfoSet) dem InfoSet Typinformationen hinzugefügt und in der internen Darstellung codiert. Das führt zu einer erheblichen Steigerung der Analysegeschwindigkeit. Weitere Informationen finden Sie in den Spezifikationen zum W3C XML-Schema unter [http://www.w3.org/TR/xmlschema-1](http://go.microsoft.com/fwlink/?LinkId=48881) und [http://www.w3.org/TR/xmlschema-2](http://go.microsoft.com/fwlink/?LinkId=4871).  
  
-   Zuordnung zwischen XML- und relationaler Speicherung  
  
     Durch Verwenden eines mit Anmerkungen versehenen Schemas (AXSD) wird der XML-Code in Spalten in einer oder mehreren Tabellen zerlegt. Damit bleibt die Genauigkeit der Daten auf der relationalen Ebene erhalten. Das führt dazu, dass die hierarchische Struktur erhalten bleibt, obwohl die Reihenfolge unter den Elementen ignoriert wird. Das Schema kann nicht rekursiv sein.  
  
-   Speichern von großen Objekten, **[n]varchar(max)** und **varbinary(max)**  
  
     Eine identische Kopie der Daten wird gespeichert. Dies ist nützlich für Anwendungen mit einem besonderen Zweck wie z. B. zum Speichern juristischer Dokumente. Die meisten Anwendungen benötigen jedoch keine exakte Kopie, und es reicht der XML-Inhalt aus (InfoSet-Genauigkeit).  
  
 Im Allgemeinen müssen Sie eine Kombination aus diesen beiden Vorgehensweisen verwenden. Sie wollen z. B. die XML-Daten in einer **xml** -Datentypspalte speichern und Eigenschaften daraus in relationale Spalten heraufstufen. Oder Sie möchten die Zuordnungstechnologie verwenden, um nicht rekursive Teile in Nicht-XML-Spalten und ausschließlich die rekursiven Teile in **XML** -Datentypspalten zu speichern.  
  
### <a name="choice-of-xml-technology"></a>Auswählen der XML-Technologie  
 Die Auswahl der XML-Technologie – also systemeigene XML oder XML-Sicht – richtet sich im Allgemeinen nach den folgenden Faktoren:  
  
-   Speicheroptionen  
  
     Ihre XML-Daten können besser für die Speicherung großer Objekte geeignet sein (z. B. ein Produkthandbuch) oder kommen eher für die Speicherung in relationalen Spalten in Frage (z. B. ein in XML konvertierter Einzelposten). Mit jeder Speicheroption wird die Dokumentgenauigkeit in einem unterschiedlichen Ausmaß beibehalten.  
  
-   Abfragemöglichkeiten  
  
     Ausgehend vom Charakter Ihrer Abfragen und vom Ausmaß, in dem Sie Ihre XML-Daten abfragen, erscheint Ihnen möglicherweise eine Speicheroption geeigneter als eine andere. So wird mit den beiden Speicheroptionen die differenzierte Abfrage Ihrer XML-Daten, z. B. die Prädikatauswertung für XML-Knoten, in einem unterschiedlichen Ausmaß unterstützt.  
  
-   Indizieren von XML-Daten  
  
     Sie möchten möglicherweise die XML-Daten indizieren, um die Geschwindigkeit der XML-Abfrage zu erhöhen. Die Indexoptionen sind bei den beiden Speicheroptionen unterschiedlich, und Sie müssen die geeignete Auswahl treffen, um Ihre Arbeitsauslastung zu optimieren.  
  
-   Möglichkeiten zur Datenänderung  
  
     Bestimmte Arbeitsauslastungen erfordern ein differenziertes Ändern der XML-Daten. Das kann z. B. das Hinzufügen eines neuen Abschnitts zu einem Dokument einschließen, was bei anderen Arbeitsauslastungen wie z. B. Webinhalt nicht der Fall ist. Für Ihre Anwendung kann die Sprachenunterstützung bei der Datenänderung wichtig sein.  
  
-   Unterstützung von Schemas  
  
     Ihre XML-Daten können durch ein Schema beschrieben sein, bei dem es sich um ein XML-Schemadokument handeln kann oder auch nicht. Die Unterstützung für an Schemas gebundenen XML-Code richtet sich nach der ausgewählten XML-Technologie.  
  
 Die verschiedenen Auswahlmöglichkeiten sind auch mit unterschiedlichen Leistungsmerkmalen verbunden.  
  
### <a name="native-xml-storage"></a>Systemeigene XML-Speicherung  
 Sie können die XML-Daten einer **xml** -Datentypspalte auf dem Server speichern. Dies ist eine geeignete Option, wenn folgende Aussagen zutreffen:  
  
-   Sie benötigen eine einfache Methode zum Speichern Ihrer XML-Daten auf dem Server und wollen gleichzeitig die Dokumentreihenfolge und die Dokumentstruktur beibehalten.  
  
-   Für Ihre XML-Daten kann ein Schema vorhanden sein, was aber nicht unbedingt der Fall sein muss.  
  
-   Sie wollen Ihre XML-Daten abfragen und bearbeiten.  
  
-   Sie wollen die XML-Daten indizieren, um die Abfrageverarbeitung zu beschleunigen.  
  
-   Ihre Anwendung benötigt Systemkatalogsichten zum Verwalten Ihrer XML-Daten und XML-Schemas.  
  
 Die systemeigene XML-Speicherung ist nützlich, wenn Sie über XML-Dokumente mit vielfältigen Strukturen verfügen oder wenn Sie über XML-Dokumente verfügen, die verschiedenen oder komplexen Schemas entsprechen, sodass sie keinen relationalen Strukturen zugeordnet werden können.  
  
#### <a name="example-modeling-xml-data-using-the-xml-data-type"></a>Beispiel: Modellieren von XML-Daten mit dem xml-Datentyp  
 Stellen wir uns ein Produkthandbuch im XML-Format vor, das aus einem getrennten Kapitel für jedes Thema besteht und bei dem jedes Kapitel wiederum mehrere Abschnitte umfasst. Ein Abschnitt kann jeweils Unterabschnitte enthalten. Deshalb ist \<section> (Abschnitt) ein rekursives Element. Produkthandbücher enthalten eine riesige Menge gemischter Inhalte, Diagramme und technischer Materialien; die Daten sind deshalb halbstrukturiert. Benutzer wollen möglicherweise eine Kontextsuche nach Themen von Interesse durchführen. So könnten sie z. B. nach dem Abschnitt zum Thema "gruppierter Index" innerhalb des Kapitels zum Thema "Indizieren" suchen und technische Mengen abfragen.  
  
 Ein geeignetes Speichermodell für die XML-Dokumente ist eine **xml** -Datentypspalte. Dabei bleibt der InfoSet-Inhalt Ihrer XML-Daten erhalten. Durch Indizieren der XML-Spalte wird die Abfrageleistung gesteigert.  
  
#### <a name="example-retaining-exact-copies-of-xml-data"></a>Beispiel: Beibehalten exakter Kopien von XML-Daten  
 Nehmen wir zur Veranschaulichung an, dass Sie durch gesetzliche Bestimmungen dazu verpflichtet sind, exakte Textkopien Ihrer XML-Dokumente beizubehalten. Bei diesen Dokumenten könnte es sich z. B. um unterschriebene Dokumente, juristisch relevante Dokumente oder Unterlagen zu Börsengeschäften handeln. Möglicherweise möchten Sie anschließend die Dokumente in einer **[n]varchar(max)** -Spalte speichern.  
  
 Zu Abfragezwecken konvertieren Sie die Daten in den **xml** -Datentyp zur Laufzeit und führen daran XQuery-Abfragen aus. Die Konvertierung zur Laufzeit kann jedoch teuer sein, insbesondere wenn es sich um ein großes Dokument handelt. Wenn Sie häufig Abfragen ausführen, können Sie die Dokumente redundant in einer **XML** -Datentypspalte speichern und diese indizieren, während Sie genaue Dokumentkopien aus der **[n]varchar(max)** -Spalte zurückgeben.  
  
 Bei der XML-Spalte kann es sich um eine berechnete Spalte handeln, basierend auf der **[n]varchar(max)** -Spalte. Allerdings ist es nicht möglich, einen XML-Index für eine berechnete XML-Spalte zu erstellen, und auch für **[n]varchar(max)** - oder **varbinary(max)** -Spalten kann kein XML-Index erstellt werden.  
  
### <a name="xml-view-technology"></a>XML-Sichttechnologie  
 Durch Definieren einer Zuordnung zwischen Ihren XML-Schemas und den Tabellen in einer Datenbank erstellen Sie eine "XML-Sicht" Ihrer persistenten Daten. Mithilfe von XML-Massenladen können die zugrunde liegenden Tabellen anhand der XML-Sicht aufgefüllt werden. Sie können die XML-Sicht mithilfe von XPath Version 1.0 abfragen; die Abfrage wird in SQL-Abfragen für die Tabellen übersetzt. In gleicher Weise werden auch Updates an diese Tabellen weitergegeben.  
  
 Diese Technologie kann in folgenden Situationen nützlich sein:  
  
-   Sie benötigen ein XML-zentriertes Programmierungsmodell mit Verwendung von XML-Sichten für Ihre vorhandenen relationalen Daten.  
  
-   Sie verfügen über ein Schema (XSD, XDR) für Ihre XML-Daten, das eventuell von einem externen Partner stammt.  
  
-   Die Reihenfolge spielt in Ihren Daten keine Rolle, oder Ihre Abfragetabelle ist nicht rekursiv, oder die maximale Rekursionstiefe ist bereits im Vorfeld bekannt.  
  
-   Sie wollen die Daten über die XML-Sicht abfragen und bearbeiten, indem Sie XPath Version 1.0 verwenden.  
  
-   Sie wollen einen Massenladevorgang für XML-Daten durchführen und diese mithilfe der XML-Sicht in die zugrunde liegenden Tabellen zerlegen.  
  
 Zu den Beispielen zählen relationale Daten, die als XML zum Datenaustausch und für Webdienste zugänglich gemacht werden, sowie XML-Daten mit festem Schema. Weitere Informationen finden Sie in der [MSDN-Onlinebibliothek](http://go.microsoft.com/fwlink/?linkid=31174).  
  
#### <a name="example-modeling-data-using-an-annotated-xml-schema-axsd"></a>Beispiel: Modellieren von Daten mithilfe eines XML-Schemas mit Anmerkungen (AXSD)  
 Zur Veranschaulichung nehmen wir an, dass Sie über relationale Daten (z. B. zu Kunden, Bestellungen und Einzelposten) verfügen, die Sie als XML handhaben möchten. Definieren Sie eine XML-Sicht, indem Sie AXDS auf die relationalen Daten anwenden. Die XML-Sicht ermöglicht Ihnen, einen Massenladevorgang der XML-Daten in Ihren Tabellen durchzuführen und die relationalen Daten mithilfe der XML-Sicht abzufragen und zu aktualisieren. Dieses Modell ist nützlich, wenn Sie Daten, die XML-Markups enthalten, mit anderen Anwendungen austauschen müssen, während Ihre SQL-Anwendungen ununterbrochen weiterarbeiten.  
  
### <a name="hybrid-model"></a>Hybridmodell  
 Häufig ist für die Datenmodellierung eine Kombination aus relationalen Spalten und **xml** -Datentypspalten geeignet. Einige der Werte aus Ihren XML-Daten können in relationalen Spalten gespeichert werden, während der Rest oder der gesamte XML-Wert in einer XML-Spalte gespeichert wird. Das kann zu einer besseren Leistung führen, indem Sie über bessere Steuerungsmöglichkeiten für die Indizes, die für die relationalen Spalten erstellt wurden, und über bessere Sperrenmerkmale verfügen können.  
  
 Die Werte, die in relationalen Spalten gespeichert werden sollen, richten sich nach Ihrer Arbeitsauslastung. Wenn Sie z.B. alle XML-Werte auf der Basis des Pfadausdrucks /Customer/@CustId abrufen, kann das Heraufstufen des Werts des **CustId**-Attributs in eine relationale Spalte und deren Indizierung zu einer Beschleunigung des Abfragevorgangs führen. Wenn Ihre XML-Daten andererseits umfangreich und nicht redundant in relationale Spalten zerlegt sind, können die Kosten für die Reassemblierung erheblich sein.  
  
 Wurde z. B. für stark strukturierte XML-Daten der Inhalt einer Tabelle in XML konvertiert, können Sie alle Werte relationalen Spalten zuordnen und möglicherweise die XML-Sichttechnologie verwenden.  
  
## <a name="granularity-of-xml-data"></a>Granularität von XML-Daten  
 Die Granularität der in einer XML-Spalte gespeicherten XML-Daten ist für Sperren sehr wichtig und ist, in einem geringeren Ausmaß, auch für Updates wichtig. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet denselben Sperrmechanismus sowohl für XML- als auch für Nicht-XML-Daten. Deshalb führt eine Sperre auf Zeilenebene dazu, dass alle XML-Instanzen in der Zeile gesperrt werden. Bei hoher Granularität führt die Sperre großer XML-Instanzen für Updates in einem Szenario mit mehreren Benutzern zur Verringerung des Datendurchsatzes. Andererseits geht bei starker Dekomposition die Objekteinkapselung verloren, und die Kosten für die Reassemblierung steigen.  
  
 Um einen guten Entwurf zu erzielen, muss ein Kompromiss aus den Anforderungen der Datenmodellierung und den Sperren- und Updatemerkmalen gefunden werden. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ist jedoch die Größe der tatsächlich gespeicherten XML-Instanzen nicht von so entscheidender Bedeutung.  
  
 Beispielsweise wird für Updates einer XML-Instanz die neue Unterstützung für partielle BLOB- (Binary Large Object) und partielle Indexupdates genutzt, bei denen die vorhandene gespeicherte XML-Instanz mit ihrer aktualisierten Version verglichen wird. Beim BLOB-Update wird ein differenzieller Vergleich zwischen den beiden XML-Instanzen durchgeführt, und es werden nur die Differenzen aktualisiert. Partielle Indexupdates nehmen im XML-Index nur Änderungen an solchen Zeilen vor, die geändert werden müssen.  
  
## <a name="limitations-of-the-xml-data-type"></a>Einschränkungen des XML-Datentyps  
 Für den **xml** -Datentyp gelten die folgenden allgemeinen Einschränkungen:  
  
-   Die gespeicherte Darstellung von **xml** -Datentypinstanzen darf 2 GB nicht überschreiten.  
  
-   Er kann nicht als Untertyp einer **sql_variant** -Instanz verwendet werden.  
  
-   Er unterstützt keine Umwandlung oder Konvertierung in **text** oder **ntext**. Verwenden Sie stattdessen **varchar(max)** oder **nvarchar(max)** .  
  
-   Er kann weder verglichen noch sortiert werden. Dies bedeutet, dass ein **xml** -Datentyp nicht in einer GROUP BY-Anweisung verwendet werden kann.  
  
-   Er kann für integrierte Skalarfunktionen außer ISNULL, COALESCE und DATALENGTH nicht als Parameter verwendet werden.  
  
-   Er kann nicht als Schlüsselspalte für einen Index verwendet werden. Er kann jedoch als Daten in einen gruppierten Index aufgenommen werden oder über das Schlüsselwort INCLUDE explizit zu einem nicht gruppierten Index hinzugefügt werden, wenn der nicht gruppierte Index erstellt wird.  
  
## <a name="see-also"></a>Siehe auch  
 [Beispiele für den Massenimport und -export von XML-Dokumenten &#40;SQL Server&#41;](../../relational-databases/import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)  
  
  
