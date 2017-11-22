---
title: Globalisierung Tipps und empfohlene Vorgehensweisen (Analysis Services) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: misc
ms.reviewer: 
ms.suite: sql
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- translations [Analysis Services], client applications
- date comparisons
- day-of-week comparisons [Analysis Services]
- time [Analysis Services]
- month comparisons [Analysis Services]
ms.assetid: 71a8c438-1370-4c69-961e-d067ee4e47c2
caps.latest.revision: "33"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: f4c7d23f5c48505bb91db780ee2aaf742c7c1e22
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="globalization-tips-and-best-practices-analysis-services"></a>Tipps und Best Practices für die Globalisierung (Analysis Services)
  [!INCLUDE[applies](../includes/applies-md.md)] Nur Multidimensional  
  
 Diese Tipps und Richtlinien können helfen, die Portabilität von Business Intelligence-Lösungen zu erhöhen und Fehler zu vermeiden, die direkt mit der Sprache und Sortierung verbunden sind.  
  
##  <a name="bkmk_sameColl"></a> Verwenden ähnlicher Sortierungen im ganzen Stapel  
 Versuchen Sie, möglichst dieselben Sortierungseinstellungen in [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] wie für das Datenbankmodul zu verwenden. Legen Sie entsprechende Einstellungen für Unterscheidung nach Breite, Groß-/Kleinschreibung und Akzent fest.  
  
 Jeder Dienst besitzt eigene Einstellungen für die Sortierreihenfolge. Der Standardwert ist für das Datenbankmodul auf "SQL_Latin1_General_CP1_CI_AS" und für Analysis Services auf "Latin1_General_AS" festgelegt. Die Standardwerte sind bezüglich Unterscheidung nach Groß-/Kleinschreibung, Breite und Akzent kompatibel. Beachten Sie, dass durch Ändern der Einstellungen einer der Sortierungen Probleme auftreten können, wenn sich die Sortierungseigenschaften grundlegend unterscheiden.  
  
 Auch wenn Sortierungseinstellungen funktionell gleichwertig sind, kann ein spezieller Fall auftreten, bei dem ein Leerzeichen in einer Zeichenfolge von jedem Dienst anders interpretiert wird.  
  
 Das Leerzeichen ist ein besonderer Fall, da es in Unicode als Single-Byte- (SBCS) oder Double-Byte-Zeichensatz (DBCS) dargestellt werden kann. Im relationalen Modul werden zwei durch ein Leerzeichen getrennte, zusammengesetzte Zeichenfolgen – eine in SBCS, die andere in DBCS – als identisch betrachtet. In Analysis Services sind während der Verarbeitung die gleichen zwei zusammengesetzten Zeichenfolgen nicht identisch, und die zweite Instanz wird als Duplikat gekennzeichnet.  
  
 Weitere Details und mögliche Problemumgehungen finden Sie unter [Leerzeichen in einer Unicode-Zeichenfolge liefern je nach Sortierung unterschiedliche Verarbeitungsergebnisse](http://social.technet.microsoft.com/wiki/contents/articles/23979.ssas-processing-error-blanks-in-a-unicode-string-have-different-processing-outcomes-based-on-collation-and-character-set.aspx).  
  
##  <a name="bkmk_recos"></a> Allgemeine Empfehlungen für die Sortierung  
 Analysis Services stellt immer die vollständige Liste aller verfügbaren Sprachen und Sortierungen bereit; die Sortierungen werden nicht anhand der ausgewählten Sprache gefiltert. Achten Sie darauf, eine praktikable Kombination auswählen.  
  
 Einige der häufig verwendeten Sortierungen sind in der folgenden Liste aufgeführt.  
  
 Betrachten Sie diese Liste als Ausgangspunkt für weitere Untersuchungen, statt als definitive Empfehlung, die andere Optionen ausschließt. Unter Umständen stellen Sie fest, dass eine nicht ausdrücklich empfohlene Sortierung am besten für Ihre Daten geeignet ist. Gründliche Tests sind die einzige Möglichkeit zu überprüfen, ob Datenwerte richtig sortiert und verglichen werden. Achten Sie wie immer darauf, beim Testen der Sortierung sowohl Verarbeitungs- als auch Abfragearbeitsauslastungen auszuführen.  
  
-   Für Anwendungen, die die 26 Zeichen des lateinischen Alphabets verwenden, wird häufig [Latin1_General_100_AS](http://en.wikipedia.org/wiki/ISO_basic_Latin_alphabet)verwendet.  
  
-   Nordeuropäische Sprachen, die skandinavische Buchstaben (z. B. ø) enthalten, können Finnish_Swedish_100 verwenden.  
  
-   Osteuropäische Sprachen wie z. B. Russisch verwenden häufig Cyrillic_General_100.  
  
-   Die chinesische Sprache und Sortierung variiert je nach Region, ist im Allgemeinen jedoch entweder vereinfachtes Chinesisch oder traditionelles Chinesisch.  
  
     In der Volksrepublik China und Singapur wird vom Microsoft Support vornehmlich vereinfachtes Chinesisch beobachtet, mit Pinyin als bevorzugter Sortierreihenfolge. Die empfohlenen Sortierungen sind Chinese_PRC (für SQL Server 2000), Chinese_PRC_90 (für SQL Server 2005) oder Chinese_Simplified_Pinyin_100 (für SQL Server 2008 und höher).  
  
     In Taiwan kommt häufiger traditionelles Chinesisch vor, bei dem die empfohlene Sortierreihenfolge auf der Anzahl der Striche basiert: Chinese_Taiwan_Stroke (für SQL Server 2000), Chinese_Taiwan_Stroke_90 (für SQL Server 2005) oder Chinese_Traditional_Stroke_Count_100 (für SQL Server 2008 und höher).  
  
     Auch andere Regionen (z. B. Hongkong und Macau) verwenden traditionelles Chinesisch. Für Sortierungen in Hongkong wird häufig Chinese_Hong_Kong_Stroke_90 (in SQL Server 2005) verwendet. In Macau wird Chinese_Traditional_Stroke_Count_100 (in SQL Server 2008 und höher) recht häufig verwendet.  
  
-   Für Japanisch ist die am häufigsten verwendete Sortierung Japanese_CI_AS. Japanese_XJIS_100 wird bei Installationen verwendet, die [JIS2004](http://en.wikipedia.org/wiki/JIS_X_0213)unterstützen. Japanese_BIN2 wird in der Regel in Datenmigrationsprojekten verwendet, deren Daten von anderen als Windows-Plattformen oder aus anderen Datenquellen als dem relationalen Datenbankmodul von SQL Server stammen.  
  
     Japanese_Bushu_Kakusu_100 wird selten auf Servern verwendet, die Analysis Services-Arbeitsauslastungen ausführen.  
  
-   Korean_100 wird für Koreanisch empfohlen. Obwohl Korean_Wansung_Unicode weiterhin in der Liste verfügbar ist, ist es veraltet.  
  
##  <a name="bkmk_objid"></a> Unterscheidung nach Groß-/Kleinschreibung von Objektbezeichnern  
 Ab SQL Server 2012 SP2 wird die Unterscheidung nach Groß-/Kleinschreibung von Objektbezeichnern unabhängig von der Sortierung erzwungen, aber das Verhalten ist je nach Sprache unterschiedlich:  
  
|Sprachschrift|Unterscheidung nach Groß-/Kleinschreibung|  
|---------------------|----------------------|  
|**Standardlateinisches Alphabet**|Bei Objektbezeichnern in lateinischer Schrift (beliebige der 26 englischen Groß- oder Kleinbuchstaben) wird unabhängig von der Sortierung die Groß-und Kleinschreibung nicht unterschieden. Beispielsweise werden die folgenden Objekt-IDs als identisch angesehen: 54321**abcdef**, 54321**ABCDEF**, 54321**AbCdEf**. Intern werden in Analysis Services die Zeichen in der Zeichenfolge behandelt, als wären alle Großbuchstaben, und dann wird ein einfacher Bytevergleich ausgeführt, der unabhängig von der Sprache ist.<br /><br /> Beachten Sie, dass nur die 26 Zeichen betroffen sind. Wenn die Sprache Westeuropäisch ist, jedoch skandinavische Zeichen verwendet, wird das zusätzliche Zeichen nicht groß geschrieben.|  
|**Kyrillisch, Griechisch, Koptisch, Armenisch**|Bei Objektbezeichnern in nicht-lateinischer Schrift mit Groß-/Kleinschreibung, z. B. Kyrillisch, wird immer nach Groß-/Kleinschreibung unterschieden. Beispielsweise werden Измерение und измерение als zwei unterschiedliche Werte betrachtet, obwohl der einzige Unterschied die Großschreibung des ersten Buchstabens ist.|  
  
 **Auswirkungen der Unterscheidung nach Groß-/Kleinschreibung für Objektkennungen**  
  
 Die in der Tabelle beschriebenen Verhaltensweisen bezüglich Groß-/Kleinschreibung gelten nur für Objektbezeichner und nicht für Objektnamen. Wenn Sie eine geänderte Funktionsweise Ihrer Lösung beobachten (bei einem Vorher/nachher-Vergleich nach der Installation von SQL Server 2012 SP2 oder höher), handelt es sich wahrscheinlich um ein Problem der Verarbeitung. Abfragen werden nicht von Objektbezeichnern betroffen. Für beide Abfragesprachen (DAX und MDX) verwendet das Formelmodul den Objektnamen (nicht den Bezeichner).  
  
> [!NOTE]  
>  Codeänderungen, die im Zusammenhang mit der Groß-/Kleinschreibung stehen, bedeuteten eine erhebliche Änderung für einige Anwendungen. Weitere Informationen finden Sie unter [Wichtige Änderungen von Analysis Services-Funktionen in SQL Server 2016](../analysis-services/breaking-changes-to-analysis-services-features-in-sql-server-2016.md) .  
  
##  <a name="bkmk_test"></a> Testen des Gebietsschemas mithilfe von Excel, SQL Server Profiler und SQL Server Management Studio  
 Beim Testen von Übersetzungen muss die Verbindung den LCID-Wert der Übersetzung angeben. Wie in [Übernehmen anderer Sprachen aus SSAS in Excel](http://extremeexperts.com/sql/Tips/ExcelDiffLocale.aspx)dokumentiert ist, können Sie Excel zum Testen Ihrer Übersetzungen verwenden.  
  
 Dazu können Sie die ODC-Datei von Hand bearbeiten und die Verbindungszeichenfolgeneigenschaft für die Gebietsschema-ID einfügen. Probieren Sie dies mit der mehrdimensionalen Adventure Works-Beispieldatenbank aus.  
  
-   Suchen Sie nach vorhandenen ODC-Dateien. Wenn Sie die für mehrdimensionales Adventure Works gefunden haben, klicken Sie mit der rechten Maustaste auf die Datei, um sie in Editor zu öffnen.  
  
-   Fügen Sie der Verbindungszeichenfolge `Locale Identifier=1036` hinzu. Speichern und schließen Sie die Datei.  
  
-   Öffnen Sie Excel | **Daten** | **Vorhandene Verbindungen**. Filtern Sie die Liste, um nur Verbindungsdateien auf diesem Computer anzuzeigen. Suchen Sie die Verbindung für Adventure Works (sehen Sie sich den Namen genau an, es könnte mehrere geben). Öffnen Sie die Verbindung.  
  
     Die französischen Übersetzungen aus der Adventure Works-Beispieldatenbank sollten angezeigt werden.  
  
     ![Excel-PivotTable mit französischen Übersetzungen](../analysis-services/media/ssas-localetest-excel.png "Excel-PivotTable mit französischen Übersetzungen")  
  
 Anschließend können Sie mit SQL Server Profiler das Gebietsschema bestätigen. Klicken Sie auf ein `Session Initialize` -Ereignis, und suchen Sie dann in der Eigenschaftenliste im Textbereich unten nach `<localeidentifier>1036</localeidentifier>`.  
  
 In Management Studio können Sie die Gebietsschema-ID für eine Serververbindung angeben.  
  
-   Klicken Sie im Objekt-Explorer | **Verbinden** | **Analysis Services** | **Optionen**auf die Registerkarte **Zusätzliche Verbindungsparameter** .  
  
-   Geben Sie `Local Identifier=1036` ein, und klicken Sie dann auf **Verbinden**.  
  
-   Führen Sie eine MDX-Abfrage für die Adventure Works-Datenbank aus. Die Abfrageergebnisse sollten die französischen Übersetzungen sein.  
  
     ![MDX-Abfrage mit französischen Übersetzungen in SSMS](../analysis-services/media/ssas-localetest-ssms.png "MDX-Abfrage mit französischen Übersetzungen in SSMS")  
  
##  <a name="bkmk_mdx"></a> Schreiben von MDX-Abfragen in einer Projektmappe mit Übersetzungen  
 Übersetzungen stellen Anzeigeinformationen für die Namen von [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] -Objekten zur Verfügung, wobei die Bezeichner für diese Objekte jedoch nicht übersetzt werden. Verwenden Sie nach Möglichkeit die Bezeichner und Schlüssel für [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] -Objekte, nicht die übersetzten Beschriftungen und Namen. Verwenden Sie z. B. Elementschlüssel anstelle von Elementnamen für MDX-Anweisungen und -Skripts (Multidimensional Expressions, MDX), um sprachübergreifende Portabilität sicherzustellen.  
  
> [!NOTE]  
>  Beachten Sie, dass für tabellarische Objektnamen unabhängig von der Sortierung nie die Groß-/Kleinschreibung unterschieden wird. Mehrdimensionale Objektnamen hingegen folgen der Groß-/Kleinschreibung der Sortierung. Da für mehrdimensionale Objektnamen die Groß-/Kleinschreibung unterschieden wird, stellen Sie sicher, dass alle MDX-Abfragen, die auf mehrdimensionale Objekte verweisen, die korrekte Groß-/Kleinschreibung verwenden.  
  
##  <a name="bkmk_datetime"></a> Schreiben von MDX-Abfragen mit Datums- und Uhrzeitwerten  
 Die folgenden Vorschläge sollen die Verwendung Ihrer datums- und zeitbasierten MDX-Abfragen in verschiedenen Sprachen erleichtern:  
  
1.  **Verwenden numerischer Teile für Vergleiche und Vorgänge**  
  
     Verwenden Sie beim Ausführen von Monats- und Wochentagvergleichen und -operationen anstelle der Zeichenfolgenäquivalente die numerischen Datums- und Uhrzeitangaben (z. B. "MonthNumberofYear" anstelle von "MonthName"). Numerische Werte sind am wenigsten von den Unterschieden in den Sprachübersetzungen betroffen.  
  
2.  **Verwenden von Zeichenfolgenäquivalenten in einem Resultset**  
  
     Ziehen Sie beim Erstellen von Resultsets für Endbenutzer in Erwägung, die Zeichenfolge (z. B. "MonthName") zu verwenden, sodass Ihr mehrsprachiges Publikum von den Übersetzungen profitieren kann, die Sie bereitgestellt haben.  
  
3.  **Verwenden der ISO-Datumsformate für universelle Datums- und Uhrzeitangaben**  
  
     Ein [Analysis Services-Experte](http://geekswithblogs.net/darrengosbell/Default.aspx) hat diese Empfehlung: "Ich verwende für Datumszeichenfolgen, die ich an SQL- oder MDX-Abfragen übergebe, immer das ISO-Datumsformat yyyy-mm-dd, da es eindeutig ist und unabhängig von den regionalen Einstellungen des Clients oder Servers funktioniert. Ich stimme zu, dass der Server bei der Analyse eines mehrdeutigen Datumsformats auf seine regionalen Einstellungen zurückgreifen sollte. Aber ich denke auch, wenn Sie eine Möglichkeit haben, die nicht der Interpretationen unterworfen ist, sollten Sie besser diese wählen".  
  
4.  **Verwenden der Format-Funktion, um ein bestimmtes Format unabhängig von den Regions- und Spracheinstellungen zu erzwingen**  
  
     Die folgende MDX-Abfrage aus einem Forumsbeitrag veranschaulicht, wie mit der Funktion Format Datumsangaben in einem bestimmten Format zurückgegeben werden, unabhängig von den zugrunde liegenden regionalen Einstellungen.  
  

    ```  
    WITH MEMBER [LinkTimeAdd11Date_Manual] as Format(dateadd("d",15,"2014-12-11"), "mm/dd/yyyy")  
    member [LinkTimeAdd15Date_Manual] as Format(dateadd("d",11,"2014-12-13"), "mm/dd/yyyy")  
    SELECT  
    { [LinkTimeAdd11Date_Manual]  
    ,[LinkTimeAdd15Date_Manual]  
    }  
    ON COLUMNS   
    FROM [Adventure Works]  
  
    ```  
  
## <a name="see-also"></a>Siehe auch  
 [Globalisierungsszenarien für Analysis Services](../analysis-services/globalization-scenarios-for-analysis-services.md)   
 [Schreiben internationaler Transact-SQL-Anweisungen](../relational-databases/collations/write-international-transact-sql-statements.md)  
  
  
