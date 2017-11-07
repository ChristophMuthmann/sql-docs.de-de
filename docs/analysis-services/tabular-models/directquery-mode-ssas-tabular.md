---
title: DirectQuery-Modus | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 07/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.asvs.bidtoolset.realtime.f1
ms.assetid: 45ad2965-05ec-4fb1-a164-d8060b562ea5
caps.latest.revision: 64
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e6434897c1a69ee12d6ce13d0ba4c5d7e5558261
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="directquery-mode"></a>DirectQuery-Modus

[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  In diesem Thema wird beschrieben, *DirectQuery-Modus* für tabellarische Analysis Services-Modelle mit dem Kompatibilitätsgrad 1200 oder höher. Der DirectQuery-Modus kann für Modelle aktiviert werden, die Sie in SSDT entwerfen. Sie können auch tabellarische Modelle, die bereits bereitgestellt wurden, in SSMS in den DirectQuery-Modus ändern. Bevor Sie die DirectQuery-Modus auswählen, sollten Sie dessen Vorteile und die Einschränkungen verstehen.
  
##  <a name="bkmk_Benefits"></a> Vorteile
 Standardmäßig verwenden Tabellenmodelle einen Cache im Arbeitsspeicher, um Daten zu speichern und abzufragen. Wenn Tabellenmodelle Daten aus dem Arbeitsspeicher abfragen, können selbst komplexe Abfragen äußerst schnell ausgeführt werden. Trotzdem hat die Verwendung von zwischengespeicherten Daten auch Einschränkungen. Große Datasets können nämlich den verfügbaren Arbeitsspeicher übersteigen, und die Anforderungen an die Datenaktualität können innerhalb eines regulären Verarbeitungszeitplans nur schwer oder überhaupt nicht erfüllt werden.  
  
 DirectQuery überwindet diese Einschränkungen, während es gleichzeitig die RDBMS-Funktionen nutzt, die die Ausführung von Abfragen effizienter gestalten können. Mit DirectQuery:  
  
-   Die Daten sind aktuell, und es entsteht kein zusätzlicher Verwaltungsaufwand für die Verwaltung einer separaten Kopie der Daten (im In-Memory-Cache). Änderungen an den zugrunde liegenden Quelldaten werden umgehend in Abfragen des Datenmodells sichtbar.  
  
-   Datasets können die Arbeitsspeicherkapazität des Analysis Services-Servers übersteigen.  
  
-   DirectQuery kann Anbieter abfragebeschleunigung, z. B. von speicheroptimierten Indizes nutzen.  
  
-   Sicherheit kann durch die Back-End-Datenbank mithilfe der Sicherheitsfunktionen auf Zeilenebene der Datenbank erzwungen werden (alternativ können Sie die Sicherheit auf Zeilenebene im Modell über DAX verwenden).  
  
-   Wenn das Modell komplexe Formeln enthält, die unter Umständen mehrere Abfragen erfordern, kann Analysis Services eine Optimierung ausführen, um sicherzustellen, dass der Abfrageplan für die Abfrage, die für die Back-End-Datenbank ausgeführt wird, so effizient wie möglich ist.  
  
##  <a name="bkmk_prereq"></a>Einschränkungen
Für tabellarische Modelle im DirectQuery-Modus gelten einige Einschränkungen. Vor einem Moduswechsel sollten Sie entscheiden, ob die Vorteile einer Ausführung der Abfrage auf dem Back-End-Server gegenüber einer Verringerung der Funktionalität überwiegen.  
  
 Wenn Sie den Modus eines in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]vorhandenen Modells ändern, wird Sie der Modell-Designer über Funktionen im Modell benachrichtigen, die mit dem DirectQuery-Modus nicht kompatibel sind.  
  
 Die folgende Liste gibt einen Überblick über die wichtigsten Funktionseinschränkungen, die Sie berücksichtigen sollten:  
  
|||  
|-|-|  
|**Funktionsbereich**|**Einschränkung**|  
|**Datenquellen**|DirectQuery-Modelle können nur Daten aus einer einzelnen relationalen Datenbank verwenden, die vom Typ SQL Server, Oracle oder Teradata sein muss.  Informationen zu Versionen und Anbietern finden Sie im Abschnitt „Für DirectQuery unterstützte Datenquellen“ in diesem Artikel.| 
|**Gespeicherte SQL-Prozeduren**|Gespeicherte Prozeduren können für DirectQuery-Modelle nicht als SQL-Anweisung angegeben werden, um Tabellen bei Verwendung des Assistenten zum Importieren von Daten zu definieren. |   
|**Berechnete Tabellen**|Berechnete Tabellen werden in DirectQuery-Tabellenmodellen nicht unterstützt, berechnete Spalten hingegen schon. Wenn Sie versuchen, ein Tabellenmodell zu konvertieren, das eine berechnete Tabelle enthält, tritt eine Fehlermeldung auf, die besagt, dass das Modell keine eingefügten Daten enthalten darf.|  
|**Abfragelimits**|Das standardmäßige Zeilenlimit liegt bei einer Million Zeilen, welches Sie durch Angabe von **MaxIntermediateRowSize** in der Datei „msmdsrv.ini“ erhöhen können. Weitere Informationen finden Sie unter [DAX Eigenschaften](../../analysis-services/server-properties/dax-properties.md) .
|**DAX-Formeln**|Bei einer Abfrage eines tabellarischen Modells im DirectQuery-Modus konvertiert [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] alle DAX-Formeln und Measuredefinitionen in SQL-Anweisungen. DAX-Formeln mit Elementen, die nicht in SQL-Syntax konvertiert werden können, lösen Überprüfungsfehler für das Modell aus.<br /><br /> Diese Einschränkung ist größtenteils auf bestimmte DAX-Funktionen beschränkt. Bei Measures werden DAX-Formeln mit dem relationalen Datenspeicher in setbasierte Vorgänge konvertiert. Das bedeutet, dass alle implizit erstellten Measures unterstützt werden. <br /><br /> Wenn ein Überprüfungsfehler auftritt, müssen Sie die Formel neu schreiben, durch eine andere Funktion ersetzen oder dieses Problem umgehen, indem Sie in der Datenquelle mit abgeleiteten Spalten arbeiten.  Wenn ein tabellarisches Modell Formeln enthält, die nicht kompatible Funktionen enthalten, werden diese beim Wechsel in den DirectQuery-Modus im Designer gemeldet. <br /><br />**Hinweis:**  Einige Formeln im Modell führen möglicherweise eine Überprüfung aus, wenn das Modell auf den DirectQuery-Modus umgestellt wird, geben jedoch andere Ergebnisse zurück, wenn sie für den Cache und nicht den relationalen Datenspeicher ausgeführt werden. Dies liegt daran, dass bei Berechnungen für den Cache die Semantik der In-Memory-Analyse verwendet wird. Dabei handelt es sich um ein Modul mit Funktionen, die das Verhalten von Excel emulieren sollen. Abfragen von in der relationalen Datenquelle gespeicherten Daten verwenden hingegen die Semantik von SQL Server.<br /><br /> SQL Gespeichert  <br /><br /> Weitere Informationen finden Sie unter [DAX-Formelkompatibilität im DirectQuery-Modus](../../analysis-services/tabular-models/dax-formula-compatibility-in-directquery-mode-ssas-2016.md).|  
|**Formelkonsistenz**|In bestimmten Fällen gibt dieselbe Formel in einem zwischengespeicherten Modell andere Ergebnisse zurück als in einem DirectQuery-Modell, in dem nur der relationale Datenspeicher verwendet wird. Diese Unterschiede sind eine Folge der semantischen Unterschiede zwischen dem In-Memory-Analysemodul und SQL Server.<br /><br /> Eine vollständige Liste der Kompatibilitätsprobleme, einschließlich der Funktionen, die bei der Bereitstellung eines Modells in Echtzeit möglicherweise andere Ergebnisse zurückgeben, finden Sie unter [DAX-Formelkompatibilität im DirectQuery-Modus (SSAS 2016)](http://msdn.microsoft.com/en-us/981b6a68-434d-4db6-964e-d92f8eb3ee3e).|  
|**MDX-Einschränkungen**|Keine relativen Objektnamen. Alle Objektnamen müssen vollqualifiziert sein.<br /><br /> MDX-Anweisungen auf Sitzungsebene (benannte Mengen, berechnete Elemente, berechnete Zellen, sichtbare Gesamtwerte, Standardelemente usw.). Allerdings können Sie abfragebasierte Konstrukte wie die „WITH“-Klausel verwenden.<br /><br /> Kein Tupel mit Elementen aus verschiedenen Ebenen in einzeln ausgewählten MDX-Klauseln für Unterauswahl.<br /><br /> Keine benutzerdefinierten Hierarchien.<br /><br /> Keine nativen SQL-Abfragen (normalerweise unterstützt Analysis Services eine Teilmenge von T-SQL, allerdings nicht bei DirectQuery-Modellen).|  

## <a name="data-sources-supported-for-directquery"></a>Für DirectQuery unterstützte Datenquellen
Tabellarische DirectQuery-Modelle mit Kompatibilitätsgrad 1200 oder höher sind kompatibel mit den folgenden Datenquellen und Anbietern:

Datenquelle   |Versionen  |Anbieter
---------|---------|---------
Microsoft SQL Server    |  2008 und höher      |       OLE DB-Anbieter für SQL Server, OLE DB-Anbieter für SQL Server Native Client, .NET Framework-Datenanbieter für SQL Client  
Microsoft Azure SQL-Datenbank    |   Alle      |  OLE DB-Anbieter für SQL Server, OLE DB-Anbieter für SQL Server Native Client, .NET Framework-Datenanbieter für SQL Client            
Microsoft Azure SQL Data Warehouse     |   Alle     |  .NET Framework-Datenanbieter für SQL Client       
Microsoft SQL Analytics Platform System (APS)     |   Alle      |  OLE DB-Anbieter für SQL Server, OLE DB-Anbieter für SQL Server Native Client, .NET Framework-Datenanbieter für SQL Client       
Relationale Oracle-Datenbanken     |  Oracle 9i und höher       |  OLE DB-Anbieter für Oracle       
Relationale Teradata-Datenbanken    |  Teradata V2R6 und höher     | .NET-Datenanbieter für Teradata        

## <a name="connecting-to-a-data-source"></a>Herstellen einer Verbindung mit einer Datenquelle
Beim Entwerfen eines DirectQuery-Modells in SSDT funktioniert das Herstellen einer Verbindung mit einer Datenquelle und das Auswählen der Tabellen und Felder, die enthalten sein sollen, für Ihr Modell ähnlich wie für gespeicherte Modelle. 

Wenn Sie DirectQuery bereits aktiviert, aber noch keine Verbindung mit einer Datenquelle hergestellt haben, können Sie den Tabellenimport-Assistenten für die Verbindungsherstellung zur Datenquelle, das Auswählen von Tabellen und Feldern, das Angeben einer SQL-Abfrage usw. verwenden. Der Unterschied besteht darin, dass nach Beendigung keine Daten in den In-Memory-Cache importiert werden. 

![DirectQuery-Importerfolg](../../analysis-services/tabular-models/media/directquery-import-success.png)

Wenn Sie bereits den Tabellenimport-Assistenten zum Importieren von Daten verwendet, den DirectQuery-Modus aber noch nicht aktiviert haben, wird der In-Memory-Cache gelöscht, wenn Sie den DirectQuery-Modus aktivieren.

  
## <a name="additional-topics-in-this-section"></a>Weitere Themen in diesem Abschnitt:
[Aktivieren des DirectQuery-Modus in SSDT](../../analysis-services/tabular-models/enable-directquery-mode-in-ssdt.md)

[Aktivieren des DirectQuery-Modus in SSMS](../../analysis-services/tabular-models/enable-directquery-mode-in-ssms.md)

[Hinzufügen von Beispieldaten zu einem DirectQuery-Modell im Entwurfsmodus](../../analysis-services/tabular-models/add-sample-data-to-a-directquery-model-in-design-mode.md)

[Definieren von Partitionen im DirectQuery-Modellen](../../analysis-services/tabular-models/define-partitions-in-directquery-models-ssas-tabular.md)
  
[Testen eines Modells im DirectQuery-Modus](../../analysis-services/tabular-models/test-a-model-in-directquery-mode.md)

[DAX-Formelkompatibilität im DirectQuery-Modus](../../analysis-services/tabular-models/dax-formula-compatibility-in-directquery-mode-ssas-2016.md)
  

