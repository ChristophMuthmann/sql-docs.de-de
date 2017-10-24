---
title: ADO-Glossar | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: H1Hack27Feb2017
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ADO, glossary
ms.assetid: b0478836-4123-4357-969a-c5784fc28be5
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: da1566fc59ac51e0923392a3cc0bee6d24dd3bfa
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="ado-glossary-terms"></a>ADO-Glossar
In diesem Thema werden Begriffe, die relevant für ADO definiert.

## <a name="a"></a>Ein
 absolute URL eine vollqualifizierte URL, der den Speicherort einer Ressource, deren befindet sich im Internet oder Intranet angibt. Siehe auch *URL* und *relative URL*.

 ActiveX-Steuerelement selbst registrieren, die in-Process-COM-Komponente, die häufig ein visuelles Element entweder zur Entwurfszeit oder zur Laufzeit verfügt. ActiveX-Steuerelemente haben auch die Möglichkeit für die Kommunikation mit Active Document-Container, z. B. Microsoft Internet Explorer.

 ADISAPI (erweiterter Data Internet Server Application Programming Interface) ein-ISAPI-DLL, die Analyse von Automation-Steuerelement, Recordset Marshalling und MIME-Paket bereitstellt. Die ADISAPI-Komponente wird durch die API von Internet Information Services (IIS) bereitgestellt. Siehe auch *ISAPI*.

 Aggregate-Funktion In einer Abfrage, einer Funktion wie COUNT, AVG und STDEV, die einen Wert mit der alle Zeilen in einer Spalte einer Tabelle berechnet. Das Schreiben von Ausdrücken und beim Programmieren können Sie SQL-Aggregatfunktionen (einschließlich der drei oben aufgeführten) und Domänenaggregatfunktionen verwenden, um verschiedene Statistiken zu ermitteln.

 Alias übergeben ein alternativer Name Sie an eine Spalte oder einen Ausdruck in einer SQL SELECT-Anweisung, häufig kürzere oder aussagekräftigere. Beispielsweise ist ///BobSales Alias in der folgenden SELECT-Anweisung: "Wählen Sie verla Sales als ///BobSales from SalesDB". Ein Alias kann verwendet werden, auf dem RDS-Bindungen Spalten dynamisch zuweisen.

 Apartmentthreading ein COM-Threadingmodell alle Aufrufe an ein Objekt in einem Thread erfolgen. Apartmentthreading COM synchronisiert und marshallt Aufrufe. Siehe auch *COMmddefcom*.

 asynchronen Vorgang ein Vorgang, der ohne zu warten, die zum Abschließen des Vorgangs die Steuerung an das aufrufende Programm zurückgibt. Bevor der Vorgang abgeschlossen ist, wird die Ausführung von Code fortgesetzt. Siehe auch *synchronen Vorgang*.

## <a name="b"></a>B
 Binden Eintrag eine Zuordnung zwischen einem Feld in einer Tabelle und einer Variablen an. In den Visual C++ ADO-Erweiterungen **Recordset** Felder C/C++-Variablen zugeordnet werden.

 Bitmaske ein numerischer Wert für die ein Bit für Bit Wertvergleich mit anderen numerischen Werten in der Regel mit Flagoptionen, die im Parameter oder Rückgabewerte vorgesehen. Dieser Vergleich erfolgt normalerweise mit bitweisen logischen Operatoren, wie z. B. **und** und **oder** in Visual Basic ** & ** und **&#124;** in C++.

 Zum Beispiel das ADO- **FieldAttributeEnum** Werte können als Bitmasken verwendet werden, um die Attribute eines Felds zu bestimmen. Angenommen Sie, Sie möchten, um festzustellen, ob ein Feld aktualisiert wurde. Sie können mit dem folgenden Ausdruck in Visual Basic dafür testen:`Field.Attributes AND adFldUpdatable`

 Wenn das Ergebnis "true" ist, ist das Feld aktualisierbar.

 versehen Sie einen Marker, der eine Zeile in einer Gruppe von Zeilen eindeutig identifiziert wird, sodass Benutzer schnell darauf navigieren können einem Lesezeichen.

 Business-Objekt ein Objekt, das einen definierten Satz von Vorgängen, z. B. datenvalidierung oder Geschäftslogik für die Regel ausführt. Geschäftsobjekte befinden sich in der Regel auf der mittleren Ebene.

 Die Geschäftsregel die Kombination von Überprüfung Bearbeitungen, Anmeldung Überprüfungen DatenbankSuchen, Richtlinien und algorithmische Transformationen, die Möglichkeit, ein Unternehmen Geschäftsaktivitäten zu bilden. Auch bekannt als *Geschäftslogik*.

## <a name="c"></a>C
 berechnete Ausdruck einen Ausdruck, der nicht konstant ist allerdings, dessen Wert hängt von anderen Werten. Um ausgewertet werden, muss ein berechneter Ausdruck abrufen und Werte aus anderen Quellen, in der Regel in anderen Feldern oder Zeilen zu berechnen.

 Kapitel ein Verweis auf einen Bereich von Zeilen aus einer Datenquelle. In ADO ist ein Kapitel in der Regel einen Verweis auf eine andere **Recordset**.

 Kapitelspalten stellen das Definieren einer *über-/* Beziehung, in dem die *übergeordneten* ist die **Recordset** , enthält der Kapitelspalte und die * untergeordnete* ist die **Recordset** durch das Kapitel dargestellt.

 Kapitel-Alias ein Alias, der auf die Spalte verweist, die an das übergeordnete Element angefügt wird.

 Eine Zuordnung eines Satzes von Zeichen Zeichensatz zu ihren numerischen Werten. Unicode ist beispielsweise ein 16-Bit-Zeichensatz kann alle bekannten Zeichen codiert und als eine weltweite Standard zum Codieren von Zeichen verwendet.

 Die abhängige Seite einer hierarchischen Beziehung untergeordnet ist. Ein untergeordnetes Element ist ein Knoten in einer hierarchischen Struktur, die einen anderen Knoten darüber liegenden aufweist (näher am Stamm). Siehe auch *untergeordnete-Alias*, *über-/ unterordnungsbeziehung*, *übergeordneten*.

 untergeordnete-Alias ein Alias, der auf das untergeordnete Element verweist. Siehe auch *Alias*, *untergeordneten*.

 CLSID (Klassen-ID) ein universell eindeutige Bezeichner (UUID), der eine COM-Komponente identifiziert. Jede COM-Komponente hat seines CLSID in der Windows-Registrierung, damit sie von einer anderen Anwendung geladen werden können. Siehe auch *ProgID*, *COM*.

 Client-Ebene eine logische Ebene von einem verteilten System, in dem in der Regel Daten und Prozesse, die Eingabe des Benutzers dargestellt auch bezeichnet als das *front-End-*. In der Regel die Clientebene fordert Daten von einem Server, auf Grundlage der Eingabe, dann formatiert und das Ergebnis wird angezeigt. Siehe auch *Mittelschicht*, *Quelle Datenebene*, *verteilte Anwendung*.

 COM (Component Object Model) ein binäres Standard, Objekte ermöglicht für die Zusammenarbeit in einer vernetzten Umgebung, unabhängig von der Sprache, in der sie entwickelt wurden, oder auf welchen Computern sie sich befinden. COM-basierte Technologien zählen ActiveX-Steuerelemente, Automatisierung und verlinken und einbetten (OLE)-Objekt. COM einem Objekt Gelegenheit zu seiner Funktionalität mit anderen Komponenten und zum Hosten von Anwendungen verfügbar zu machen. Es definiert, wie das Objekt selbst verfügbar macht und Funktionsweise dieses Offenlegen über Prozesse und Netzwerke hinweg. COM definiert auch die Lebensdauer des Objekts.

 COM-Komponenten-Binärdatei – z. B. dll-, ".ocx" und einige .exe-Dateien –, die die COM-Standard zum Bereitstellen von Objekten unterstützt. Eine solche Datei enthält Code für eine oder mehrere Klassenfactorys, COM-Klassen Registrierungseintrag Mechanismen, Code zum Laden und So weiter.

 Vergleichsoperator ein Operator, der vergleicht zwei Ausdrücke, und gibt einen booleschen Wert zurück.

 Ein Kriterienparameter, der als ausgedrückt werden kann ">" (größer als), "\<" (kleiner als), "=" (gleich), "> =" (größer als oder gleich), "< =" (kleiner oder gleich), "<>" (ungleich) oder "like" (Mustervergleich).

 Ein Objekt, das sowohl Daten als auch Code kapselt, und bietet eine wohldefinierte Reihe öffentlich verfügbarer Dienste-Komponente.

 Eine Implementierung von COM-Verbunddatei strukturierten Speicher für Dateien. Eine Verbunddatei speichert separate Objekte in einer einzelnen, strukturierten-Datei, bestehend aus zwei Hauptelemente: Speicherobjekte und Streamobjekten. Zusammen funktionieren wie ein Dateisystem in einer Datei.

 Eine Anzahl von einzelnen Dateien, die zusammen in einer physischen Datei gebunden. Jede einzelne Datei in einer Verbunddatei kann zugegriffen werden, als handele es sich um einen einzelnen physischen Datei.

 Konstante ein numerisch oder String-Wert, der nicht geändert wird. Benannte ADO-Enumerationen (Enumerationskonstanten) können z. B. in Ihrem Code anstelle der eigentlichen Werte verwendet werden **AdUseClient** ist eine Konstante, deren Wert 3 ist. (Const AdUseClient = 3). Siehe auch *Enumeration*.

 Cursor ein Datenbankelement, das zum Navigieren in Datensätzen, Updateability der Daten und die Sichtbarkeit von Änderungen an der Datenbank vorgenommen werden, die von anderen Benutzern gesteuert.

## <a name="d"></a>D
 Den Vorgang des Verbindens Objekte oder Steuerelemente von einer Anwendung an eine Datenquelle binden von Daten. Ein Steuerelement mit einer Datenquelle verknüpfte heißt ein *datengebundenes Steuerelement*.

 Der Inhalt eines datengebundenen Steuerelements werden Werte aus einer Datenbank zugeordnet. Z. B. ein Grid-Steuerelement, das an gebunden ist ein **Recordset** Objekt kann es sich aktualisiert, wenn die Zeilen in der **Recordset** aktualisiert werden. Wenn werden neue Werte abgerufen, indem die **Recordset**, neue Werte werden im Raster angezeigt.

 Datenanbieter Software, die Daten in eine ADO-Anwendung verfügbar macht entweder direkt oder über einen Dienstanbieter. Siehe auch Dienstanbieter.

 strukturiert werden, eine Technik, die Daten der formalisierter-Syntax verwenden (aufgerufen **Form Sprache**) ein spezieller definieren **Recordset** Objekt (bezeichnet eine *geformten Recordset*), enthält nicht nur die Daten, aber auch Verweise auf andere **Recordset** Objekte bzw. berechnete Werte basierend auf den anderen **Recordset** Objekte.

 Datenquellen-Ebene eine logische Ebene von einem verteilten System, das einen Computer mit einem DBMS, z. B. ein SQL Server-Datenbank darstellt. Siehe auch *Clientebene*, *Mittelschicht*, *verteilte Anwendung*.

 DCOM A Wire-Protokoll, mit der COM-Komponenten direkt miteinander über ein Netzwerk kommunizieren kann. Siehe auch *COM*, *Komponente*.

 DDL (Data Definition Language) diese Anweisungen in SQL, die im Gegensatz zum Bearbeiten von Daten definieren. Das Schema einer Datenbank erstellt oder mit DDL geändert. Beispielsweise **CREATE TABLE**, **CREATE INDEX**, **GRANT**, und **widerrufen** werden SQL-DDL-Anweisungen.

 Standardmäßig stream einen Text- oder Binärdaten-Datenstrom (dargestellt durch eine **Stream** Objekt), zugeordnet ist **Datensatz** oder **Recordset** -Objekte bei der Verwendung bestimmter OLE DB-Anbieter z. B. der Microsoft OLE DB-Anbieter für Internet Publishing. Der Standarddatenstrom enthält in der Regel den Inhalt einer Datei z. B. der HTML-Code für den Stamm einer Website.

 verteilte Anwendung ein Programm so geschrieben, dass die Verarbeitung auf mehreren Computern über ein Netzwerk verteilt werden kann. In der Regel eine verteilte Anwendung aufgeteilt Präsentation, Geschäftslogik und Data Store Ebenen oder *Ebenen*. Siehe auch die Clientebene, mittlere Ebene und Datenebenen-Quelle.

 Recordset A getrennt **Recordset** Objekt im Cache des Clients, die über eine live-Verbindung mit dem Server nicht mehr verfügt. Die Verbindung muss erneut eingerichtet werden, wenn die ursprüngliche Datenquelle erneut für aus irgendeinem Grund, z. B. Aktualisieren von Daten, zugegriffen werden muss. Allerdings die Auflistungen, Eigenschaften und Methoden von einer nicht verbundenen **Recordset** weiterhin zugegriffen werden kann.

 DML (Data Manipulation Language) diese Anweisungen in SQL, die im Gegensatz um zu definieren, Daten zu bearbeiten. Die Werte in einer Datenbank werden ausgewählt und mit DML geändert. Beispielsweise **einfügen**, **UPDATE**, **löschen**, und **wählen** SQL-DML-Anweisungen sind.

 Ein Anbieter eine Sonderklasse von Anbietern, die Ordner und Dokumente zu verwalten. Wenn ein Dokument dargestellt wird, durch eine **Datensatz** Objekt oder einem Ordner Dokumente wird durch dargestellt eine **Recordset** -Objekt, das Dokumentquellenanbieter füllt diese Objekte mit einem eindeutigen Satz von Feldern, Beschreiben Sie die Merkmale des Dokuments, anstatt das Dokument selbst. Siehe auch Ressourceneintrag.

 DSN (Data Source Name) die Auflistung der Informationen verwendet, um Ihre Anwendung mit einer bestimmten ODBC-Datenbank verbinden. Der ODBC-Treiber-Manager verwendet diese Informationen, um eine Verbindung mit der Datenbank zu erstellen. Ein DSN kann in einer Datei (Datei-DSN) oder in der Windows-Registrierung (Computer-DSN) gespeichert werden.

 dynamische Eigenschaft A-Eigenschaft für einen Datenanbieter oder die Cursordienst spezifisch. Die **Eigenschaften** Auflistung eines Objekts wird automatisch mit diesen ausgefüllt ("dynamisch"). Ein Objekt hat keine dynamischen Eigenschaften, bis er mit einer Datenquelle über einen bestimmten Datenanbieter verbunden ist. Siehe auch Data-Anbieter, Cursor.

## <a name="e"></a>E
 Die Liste der änderungsbereiche ein benannter Konstanten. Aufgezählter Werte müssen nicht eindeutig sein. Jedoch muss der Name der einzelnen Werte innerhalb des Bereichs eindeutig sein, in dem die Enumeration definiert ist. In ADO Enumerationen dienen zum numerischen Parameter und Rückgabewerte, Bedeutung in ADO-Code hinzufügen und den Entwickler von numerischen Werten geschützt werden (die sich von Version zu Version ändern können). Um beispielsweise einen statischen Öffnen **Recordset**, verwenden Sie die **AdOpenStatic** Enumerationswert:`Recordset.Open ,,adOpenStatic`

 Auch bezeichnet als *Enumerationskonstante*. Siehe auch *Konstanten*.

 das Ereignis eine Aktion erkannt wird durch ein Objekt, für die Sie Code zum reagieren schreiben können. Ereignisse können durch Ausführung des Befehls, transaktionsabschluss Recordsetnavigation und Datenupdates Aktionen generiert werden. Siehe auch *Ereignishandler*.

 -Ereignishandler ein Ereignishandler ist der Code, der beim Eintreten eines Ereignisses ausgeführt wird. Siehe auch-Ereignis.

## <a name="h"></a>H
 Ein Handlerroutine, die eine allgemeine und relativ einfache Bedingung oder einen Vorgang, wie z. B. Fehler Wiederherstellungs- oder Verwaltung verwaltet.

 hierarchische Recordset A **Recordset** , enthält eine andere **Recordset**. Siehe auch Daten strukturieren, Kapitel.

 Weitere Informationen finden Sie unter [zugreifen auf Zeilen in einem hierarchischen Recordset](../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md).

 Hierarchie im Allgemeinen gilt eine Hierarchie ist eine geordneten Struktur mit einer oberen Ebene und untergeordneten Ebenen. In ADO hierarchische **Recordsets** verwendet, um die über-/ unterordnungsbeziehung zwischen einem Datensatz und einem Kapitel darzustellen. Auch in ADO **Datensatz** und **Stream** Objekte können verwendet werden, z. B. einen Ordner und Dokumente der hierarchischen Struktur auf. ADO MD umfasst auch **Hierarchie** -Objekten zur Darstellung einer Beziehung zwischen den Ebenen einer Dimension in einem OLAP-Cube. Siehe auch hierarchische Recordsets über-/ unterordnungsbeziehung, Kapitel, Struktur.

## <a name="i-l"></a>ICH-L
 ISAPI-(Internet Server Application Programming Interface) ein Satz von Funktionen für Internetserver, z. B. eine Windows NT® Server-Windows 2000 Server, die Microsoft® Internet Information Services (IIS) ausgeführt.

 Schlüssel, eine Spalte oder Spalten in einer Tabelle, die eine Zeile eindeutig zu identifizieren; häufig verwendet, um eine Tabelle zu indizieren.

## <a name="m"></a>M
 Marshalling das Packen, senden und Entpackens Schnittstelle Methodenparameter Prozess oder Thread hinweg.

 mittlere Ebene der logischen Ebene in einem verteilten System zwischen einer Benutzeroberfläche oder WebClient und der Datenbank. Dies ist in der Regel an, an dem Geschäftsobjekte instanziiert werden. Die mittlere Ebene ist eine Auflistung von Geschäftsregeln und Funktionen, die zu generieren und nach dem Empfang von Informationen ausgeführt werden. Dies erreichen sie anhand von Geschäftsregeln, die häufig ändern können, und deshalb in Komponenten, die physisch getrennt von der Anwendungslogik selbst gekapselt werden. Auch bekannt als *Anwendungsserverebene*. Siehe auch verteilte Anwendung, die Clientebene, Data-Tier-Quelle.

 MIME (Mehrzweck Internet Mail Extension) ein Internet Protocol entwickelt sich ursprünglich auf um Exchange von e-Mail-Nachrichten mit umfangreichen Inhalten in heterogenen Netzwerk, Computer und e-Mail-Umgebungen zu ermöglichen. In der Praxis wurde MIME auch übernommen und erweitert, indem nicht-e-Mail-Anwendungen.

 MIME ist ein Standard, der binäre Daten veröffentlicht und auf das Internet gelesen werden kann. Der Header einer Datei mit Binärdaten enthält den MIME-Typ der Daten; Dieser informiert Clientprogramme (Web-z. B. Browser und e-Mail-Pakete), müssen sie die Daten auf andere Weise zu behandeln, als einfachen Text. Beispielsweise enthält der Header eines Webdokuments, die eine JPEG-Grafik enthält den MIME-Typ, die speziell für das JPEG-Dateiformat. Dies ermöglicht einen Browser, um die Datei mit der JPEG-Viewer anzuzeigen, sofern eins vorhanden ist.

## <a name="n-o"></a>N-O
 Knoten ein Element in einer hierarchischen Struktur. Ein Knoten kann die Stamm- oder das untergeordnete Element eines anderen Knotens sein. Ein Knoten kann auch das übergeordnete Element des mehrere untergeordnete Elemente sein. Siehe auch Hierarchie, Struktur, Root, untergeordneten und übergeordneten.

 Objekt die Variable A-Variable, die einen Verweis auf ein Objekt enthält. Beispielsweise `objCustomObject` ist eine Variable, die auf ein Objekt des Typs Benutzerobjekt verweist:`Set objCustomObject = CreateObject(adodb.Recordset)`

 ODBC (Open Database Connectivity) verwendet eine standardmäßige Sprache Programmierschnittstelle für die Verbindung mit einer Vielzahl von Datenquellen. Dies ist in der Regel über systemsteuerung zugegriffen, in dem Datenquellennamen (DSNs) zugewiesen werden kann, zu bestimmten ODBC-Treiber verwenden.

 OLE DB ein Satz von Schnittstellen, die Daten aus einer Vielzahl von Quellen mithilfe von COM verfügbar machen. OLE DB-Schnittstellen bieten die Anwendungen mit einheitlichen Zugriff auf Daten in verschiedenen Datenquellen gespeichert. Diese Schnittstellen unterstützen die DBMS-Funktionen, die der Datenquelle, sodass die Daten gemeinsam nutzen. Siehe auch COM.

 optimistische Sperren einen Typ von Sperren, in dem die Datenseite mit einem oder mehreren Datensätzen, einschließlich des Datensatzes, die bearbeitet wird, ist nicht verfügbar ist, anderen Benutzern nur dabei wird der Datensatz aktualisiert wird durch die **Update** Methode, ist jedoch verfügbar vor und nach dem Aufruf von **Update**.

 Eingeschränktes Sperren wird verwendet, wenn die **Recordset** -Objekt wird geöffnet, mit der **LockType** Parameter oder die Eigenschaft auf festgelegt **AdLockOptimistic** oder ** AdLockBatchOptimistic**. Siehe auch eingeschränkte sperren.

 Ordnungswert die numerische Position eines Elements innerhalb einer Bestellung. In einer Auflistung ADO ist der Ordinalwert des ersten Elements 0 (null). Das nächste Element ist eins (1) und So weiter.

## <a name="p"></a>P
 parametrisierte Befehle eine Abfrage oder einen Befehl, mit dem Sie serverstandardparameterwerte festlegen, bevor der Befehl ausgeführt wird. Durch das Einbetten von parametermarkierungen in der SQL-Zeichenfolge kann z. B. eine SQL-Zeichenfolge parametrisiert sein (bezeichneten das "?" Zeichen). Die Anwendung dann gibt Werte für jeden Parameter an und führt den Befehl.

 übergeordnete Element der steuernde Seite einer hierarchischen Beziehung. In einer hierarchischen Struktur besitzt ein übergeordnetes Element ein oder mehrere untergeordnete Knoten direkt unter ihm in der Hierarchie. Siehe auch übergeordneten Alias, über-/ unterordnungsbeziehung, untergeordnetes Element.

 übergeordneten Alias einen Alias, der auf das übergeordnete Element verweist. Siehe auch alias übergeordneten.

 über-und untergeordnete Beziehung eine Beziehung in einer hierarchischen Struktur, in der das übergeordnete Element eine Ebene höher und direkt eine oder mehrere untergeordnete Elemente zugeordnet ist. Ein untergeordnetes Element ist eine Ebene niedriger und ein übergeordnetes Element aufweisen. Siehe auch übergeordnete, untergeordnete.

 eingeschränktes Sperren einen Typ von Sperren in der ist die Seite, die eine oder mehrere Datensätze, einschließlich des Datensatzes, die bearbeitet wird, enthält nicht von anderen Benutzern, um sicherzustellen, dass ein Update hergestellt wird. Eingeschränkte Sperrverhalten wird durch den OLE DB-Anbieter definiert. In der Regel Datensätze bei der Bearbeitung gesperrt sind und bleiben nicht verfügbar, bis die **Update** -Methode abgeschlossen wurde.

 Vollständige Sperren aktiviert ist, wenn die **Recordset** -Objekt wird geöffnet, mit der **LockType** Parameter oder die Eigenschaft auf festgelegt **AdLockPessimistic**. Siehe auch optimistischen Sperre.

 Pooling von basierend auf der Verwendung von vorab zugeordneten Ressourcen, z. B. Objekte oder Datenbankverbindungen Sammlungen zur Optimierung der Leistung. Es ist effizienter, zeichnen eine vorhandene Ressource aus dem Pool als neue Ressource zu erstellen.

 ProgID (Programmbezeichner) ein eindeutiger Name der Windows-Registrierung von einer COM-Anwendung zugeordnet. Die ProgID für eine ADO-Verbindung ist "ADODB. "Verbindung". Siehe auch CLSID COM.

 Proxy eine Schnittstelle-spezifische-Objekt, das die Parameter-Marshalling bereitstellt und Kommunikation erforderlich, damit ein Client ein Anwendungsobjekt aufrufen, die in eine andere ausführungsumgebung, z. B. in einem anderen Thread oder in einem anderen Prozess ausgeführt wird. Der Proxy befindet, mit dem Client und kommuniziert mit einem entsprechenden Stub, der sich auf das Anwendungsobjekt befindet, die aufgerufen wird. Siehe auch Stub.

## <a name="r"></a>R
 relativer URL ein qualifiziert teilweise URL, die eine Ressource, auf das Internet oder einem Intranet angibt, deren Speicherort relativ zum Ausgangspunkt durch eine absolute URL oder einen entsprechenden ADO-Verbindungsobjekt angegeben ist. Aktiviert die verketteten absoluten und relativen URLs bilden eine vollständige URL. Siehe auch URL und die absolute URL.

 Remote-Datenquelle eine Datenquelle, die auf einem anderen Computer und nicht auf dem lokalen System vorhanden (wobei die Clientanwendung ausgeführt wird).

 Datensatz A-Ressourceneintrag von einem Anbieter der Dokument-Quelle, der Felder für die Definition und die Beschreibung eines Ordners oder Dokuments enthält. Das Dokument selbst nicht in den Ressourceneintrag enthalten ist, sondern in der Regel von der Standard-Stream oder ein Feld in den Ressourceneintrag, enthält eine URL zugegriffen werden kann. Siehe auch "Dokumentquellenanbieter, Standarddatenstrom, URL".

 Rowset ein Satz von Zeilen aus einer Datenquelle, mit immer das gleiche Feldschema. Ein Rowset kann alle oder einige Felder aus einer Tabelle darstellen. Ein Rowset kann auch eine virtuelle Tabelle, die von einer Abfrage oder ein Join von zwei oder mehr Tabellen erstellt repräsentieren. In ADO werden Rowsets durch dargestellt **Recordset** Objekte.

## <a name="s"></a>S
 Beschränken Sie den Bereich der Verweis für ein Objekt oder eine Variable oder einen Bereich von Datensätzen in einer Sicht oder Tabelle. Lokale Variablen können beispielsweise nur innerhalb der Prozedur verwiesen werden in denen sie definiert wurden. Öffentliche Variablen werden an einer beliebigen Stelle in der Anwendung zugegriffen werden. Objekte, z. B. der aktuellen Datenbank befinden sich im Gültigkeitsbereich, wenn Suchpfad definiert werden. Datensatz Bereiche können mit einer Scope-Klausel in zahlreichen Befehlen angegeben werden.

 Dienstanbieter-Software, die einen Dienst kapselt, erzeugen und Nutzen von Daten, Erweitern der Funktionen in den ADO-Anwendungen. Ein Anbieter, der Daten nicht direkt verfügbar ist, stellt es einen Dienst, wie die abfrageverarbeitung. Der Dienstanbieter kann Daten von einem Datenanbieter verarbeiten bereitgestellt. Siehe auch Datenanbieter.

 Recordset A geformten **Recordset** , dessen Spalten enthalten nicht nur Daten, sondern auch Verweise (Kapitel bezeichnet) auf andere speziell definiert wurden **Recordset** Objekte bzw. berechnete Werte basierend auf andere **Recordset** Objekte.

 gleichgeordnetes Element jeder mindestens zwei Knoten in einer hierarchischen Struktur, die auf der gleichen Ebene in der Hierarchie sind. Der Stammknoten in einer Hierarchie verfügt keine Elemente.

 gespeicherte Prozedur eine vorkompilierte Auflistung von Code, z. B. SQL-Anweisungen und optionalen Control-of-Flow-Anweisungen, die unter einem Namen gespeichert und als Einheit verarbeitet. Gespeicherte Prozeduren werden in einer Datenbank gespeichert. Sie können mit einem Aufruf in einer Anwendung ausgeführt werden und benutzerdefinierte Variablen, bedingte Ausführung und andere leistungsstarken Programmierfunktionen zulassen.

 Stub-eine Schnittstelle spezifischen-Objekt, das die Parameter-Marshalling bereitstellt und die Kommunikation für ein Anwendungsobjekt, um Aufrufe von einem Client empfangen, die in eine andere ausführungsumgebung, z. B. in einem anderen Thread oder in einem anderen Prozess ausgeführt wird. Der Stub des Application-Objekts befindet und kommuniziert mit einem entsprechenden Proxy aus, der mit dem Client befindet, die ihn aufruft. Siehe auch "Proxy".

 untergeordnete Knoten finden Sie unter untergeordnet ist.

 synchroner Vorgang einen Vorgang gestartet, indem Code, der vor dem nächsten Vorgang abschließt kann gestartet werden. Siehe auch asynchronen Vorgang.

## <a name="t-z"></a>T-Z
 Eine Struktur, die eine hierarchische Beziehung zwischen Elementen (Knoten) darstellt. Ein Knoten ist auf der obersten Ebene einer Struktur (Stamm) vorhanden. Unter dem Stammelement kann mehrere untergeordnete Elemente vorhanden sein. Jedes untergeordnete Element kann wiederum das übergeordnete Element eines weiteren untergeordneten Elementen, Verzweigen wie eine Struktur sein. Ein Ordner, Dokumente und andere Ordner enthält ist ein typisches Beispiel für eine Struktur. Siehe auch Hierarchie, Knoten, Root, untergeordneten und übergeordneten.

 Webserver ein Computer, Webdienste und Seiten für Intranet- und Internet-Benutzer bereitgestellt.

