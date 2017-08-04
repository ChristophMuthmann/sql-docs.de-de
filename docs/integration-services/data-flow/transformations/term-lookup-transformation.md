---
title: "Transformation für Ausdruckssuche | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.termlookuptrans.f1
helpviewer_keywords:
- extracting data [Integration Services]
- match extracted terms [Integration Services]
- text extraction [Integration Services]
- term extractions [Integration Services]
- lookups [Integration Services]
- counting extracted items
- Term Lookup transformation
ms.assetid: 3c0fa2f8-cb6a-4371-b184-7447be001de1
caps.latest.revision: 56
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 3eefbab1c6f9b3cd5e51faa9e875a44218c33b3f
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="term-lookup-transformation"></a>Transformation für Ausdruckssuche
  Die Transformation für Ausdruckssuche vergleicht aus Text in einer Transformationseingabespalte extrahierte Ausdrücke mit Ausdrücken in einer Verweistabelle. Anschließend wird gezählt, wie häufig ein Ausdruck in der Nachschlagetabelle im Eingabedataset vorkommt. Dieser Wert wird zusammen mit dem Ausdruck aus der Verweistabelle in Spalten in der Transformationsausgabe geschrieben. Mit dieser Transformation können Sie eine benutzerdefinierte Kennwortliste basierend auf dem Eingabetext erstellen, einschließlich Worthäufigkeitsstatistiken.  
  
 Bevor die Transformation für Ausdruckssuche eine Suche ausführt, werden Wörter aus dem Text in eine Eingabespalte extrahiert. Hierbei wird die gleiche Methode wie bei der Transformation für Ausdrucksextrahierung verwendet:  
  
-   Der Text wird in Sätze unterteilt.  
  
-   Die Sätze werden in Wörter unterteilt.  
  
-   Die Wörter werden normalisiert.  
  
 Um die Suche nach Ausdrücken weiter anzupassen, können Sie für die Transformation für Ausdruckssuche konfigurieren, dass eine Suche mit Unterscheidung nach Groß-/Kleinschreibung ausgeführt wird.  
  
## <a name="matches"></a>Stimmt überein  
 Die Ausdruckssuche führt eine Suche aus und gibt einen Wert mithilfe der folgenden Regeln zurück:  
  
-   Falls für die Transformation eine Suche mit Unterscheidung nach Groß-/Kleinschreibung konfiguriert ist, werden Übereinstimmungen mit unterschiedlicher Groß-/Kleinschreibung verworfen. Beispielsweise werden *student* und *STUDENT* als separate Wörter behandelt.  
  
    > [!NOTE]  
    >  Ein klein geschriebenes Wort kann mit einem Wort übereinstimmen, das am Satzanfang groß geschrieben wird. Beispielsweise ist der Vergleich von *student* und *Student* erfolgreich, wenn *Student* das erste Wort im Satz ist.  
  
-   Wenn eine Pluralform des Nomens oder des nominalen Ausdrucks in der Verweistabelle vorhanden ist, findet die Suche nur die Pluralform des Nomens oder des nominalen Ausdrucks als Übereinstimmung. Beispielsweise würden alle Instanzen von *students* separat von den Instanzen von *student*gezählt.  
  
-   Wenn nur die Singularform des Worts in der Verweistabelle gefunden wird, sind die Singularform und die Pluralform des Worts oder Satzes Übereinstimmungen mit der Singularform. Wenn beispielsweise die Nachschlagetabelle *student*enthält und die Transformation die Wörter *student* und *students*findet, würden beide Wörter als Übereinstimmung für den Suchausdruck *student*gezählt.  
  
-   Wenn der Text in der Eingabespalte ein lemmatisierter nominaler Ausdruck ist, ist nur das letzte Wort des nominalen Ausdrucks von der Normalisierung betroffen. Die lemmatisierte Version von *doctors appointments* lautet beispielsweise *doctors appointment*.  
  
 Wenn ein Suchelement Ausdrücke enthält, die sich im Verweissatz überlappen (d. h. ein Unterausdruck ist in mehreren Verweisdatensätzen zu finden), gibt die Transformation für Ausdruckssuche nur ein Suchergebnis zurück. Das folgende Beispiel zeigt das Ergebnis für den Fall, dass ein Suchelement einen sich überlappenden Unterausdruck enthält. In diesem Fall ist *Windows*der überlappende Unterausdruck, der sich in zwei Verweisausdrücken findet. Die Transformation gibt jedoch keine zwei Ergebnisse, sondern nur einen Verweisausdruck zurück: *Windows*. Der zweite Verweisausdruck, *Windows 7 Professional*, wird nicht zurückgegeben.  
  
|Element|Wert|  
|----------|-----------|  
|Eingabeausdruck|Windows 7 Professional|  
|Verweisausdrücke|Windows, Windows 7 Professional|  
|Ausgabe|Windows|  
  
 Die Transformation für Ausdruckssuche kann Nomen und nominale Ausdrücke vergleichen, die Sonderzeichen enthalten, und die Daten in der Verweistabelle können diese Zeichen enthalten. Sonderzeichen sind wie folgt: %, @, &, $, #, \*,:,,., **,** ,!,?, \<, >, +, =, ^, ~, |, \\, /, (,), [,], {,}, ", und".  
  
## <a name="data-types"></a>Datentypen  
 Die Transformation für Ausdruckssuche kann nur eine Spalte vom Datentyp DT_WSTR oder DT_NTEXT verwenden. Wenn eine Spalte Text enthält, aber keinen dieser Datentypen aufweist, kann die Transformation für Datenkonvertierung dem Datenfluss eine Spalte vom Datentyp DT_WSTR oder DT_NTEXT hinzufügen und die Spaltenwerte in die neue Spalte kopieren. Die Ausgabe von der Transformation für Datenkonvertierung kann dann als Eingabe für die Transformation für Ausdruckssuche verwendet werden. Weitere Informationen finden Sie unter [Data Conversion Transformation](../../../integration-services/data-flow/transformations/data-conversion-transformation.md).  
  
## <a name="configuration-the-term-lookup-transformation"></a>Konfiguration der Transformation für Ausdruckssuche  
 Die Eingabespalte der Transformation für Ausdruckssuche enthält die InputColumnType-Eigenschaft, die auf die Verwendung der Spalte hinweist. InputColumnType kann die folgenden Werte enthalten:  
  
-   Der Wert 0 zeigt an, dass die Spalte nur an die Ausgabe übergeben und nicht in der Suche verwendet wird.  
  
-   Der Wert 1 zeigt an, dass die Spalte nur in der Suche verwendet wird.  
  
-   Der Wert 2 zeigt an, dass die Spalte an die Ausgabe übergeben und auch in der Suche verwendet wird.  
  
 Transformations-Ausgabespalten, deren InputColumnType-Eigenschaft auf 0 oder 2 festgelegt ist, umfassen die CustomLineageID-Eigenschaft für eine Spalte, die den Herkunftsbezeichner enthält, der einer Spalte durch einen Upstreamdatenfluss-Komponenten zugewiesen wird.  
  
 Die Transformation für Ausdruckssuche fügt der Transformationsausgabe zwei Spalten hinzu, die standardmäßig **Term** und **Frequency**heißen. **Term** enthält einen Ausdruck aus der Nachschlagetabelle, und **Frequency** enthält die Angabe, wie häufig der Ausdruck in der Verweistabelle im Eingabedataset vorkommt. Diese Spalten beinhalten keine CustomLineageID-Eigenschaft.  
  
 Die Nachschlagetabelle muss eine Tabelle in einer der Datenbanken von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] oder einer Access-Datenbank sein. Wenn die Ausgabe der Transformation für Ausdrucksextrahierung in einer Tabelle gespeichert wird, kann diese Tabelle als Verweistabelle verwendet werden, andere Tabellen können allerdings ebenfalls verwendet werden. Text in Flatfiles, Excel-Arbeitsmappen oder sonstige Quellen müssen in eine [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Datenbank oder eine Access-Datenbank importiert werden, bevor die Transformation für Ausdruckssuche verwendet werden kann.  
  
 Die Transformation für Ausdruckssuche verwendet eine separate OLE DB-Verbindung, um eine Verbindung mit der Verweistabelle herzustellen. Weitere Informationen finden Sie unter [OLE DB Connection Manager](../../../integration-services/connection-manager/ole-db-connection-manager.md).  
  
 Die Transformation für Ausdruckssuche arbeitet im vollständigen Zwischenspeicherungsmodus. Zur Laufzeit liest die Transformation für Ausdruckssuche die Ausdrücke aus der Verweistabelle und speichert sie im privaten Arbeitsspeicher, bevor Transformationseingabezeilen verarbeitet werden.  
  
 Da sich die Ausdrücke in einer Eingabespalte wiederholen können, weist die Ausgabe der Transformation für Ausdruckssuche in der Regel mehr Zeilen als die Transformationseingabe auf.  
  
 Diese Transformation weist je eine Eingabe und Ausgabe auf. Fehlerausgaben werden nicht unterstützt.  
  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Klicken Sie auf eines der folgenden Themen, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im Dialogfeld **Transformations-Editor für Ausdruckssuche** festlegen können:  
  
-   [Transformations-Editor für Ausdruckssuche &#40;Registerkarte „Verweistabelle“&#41;](../../../integration-services/data-flow/transformations/term-lookup-transformation-editor-reference-table-tab.md)  
  
-   [Transformations-Editor für Ausdruckssuche &#40;Registerkarte Ausdruckssuche&#41;](../../../integration-services/data-flow/transformations/term-lookup-transformation-editor-term-lookup-tab.md)  
  
-   [Transformations-Editor für Ausdruckssuche &#40;Registerkarte Erweitert&#41;](../../../integration-services/data-flow/transformations/term-lookup-transformation-editor-advanced-tab.md)  
  
 Klicken Sie auf eines der folgenden Themen, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im Dialogfeld **Erweiterter Editor** oder programmgesteuert festlegen können:  
  
-   [Allgemeine Eigenschaften](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Benutzerdefinierte Eigenschaften von Transformationen](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 Informationen zum Festlegen von Eigenschaften finden Sie unter [Festlegen der Eigenschaften einer Datenflusskomponente](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
  
