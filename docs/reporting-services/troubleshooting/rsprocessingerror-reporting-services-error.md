---
title: 'rsProcessingError: Reporting Services-Fehler | Microsoft-Dokumentation'
ms.custom: 
ms.date: 03/15/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: troubleshooting
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: rsProcessingError
ms.assetid: 414ee58a-8251-4367-9a8e-10c068d17280
caps.latest.revision: "29"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: ab52b302e3dddfd4ab42d2cd09019f0fa62f5a91
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="rsprocessingerror---reporting-services-error"></a>rsProcessingError – Reporting Services-Fehler
    
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|Ereignis-ID|rsProcessingError|  
|Ereignisquelle|Microsoft.ReportingServices.Diagnostics.Utilities.ErrorStrings.resources|  
|Komponente|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|  
|Meldungstext|Fehler bei der Berichtsverarbeitung.|  
  
## <a name="explanation"></a>Erklärung  
 Beim Veröffentlichen, Verarbeiten, Anzeigen einer lokalen Vorschau, Anzeigen über den Berichtsserver oder Erstellen eines Abonnements für einen Bericht ist mindestens ein Fehler aufgetreten. Mit dieser Fehlermeldung wird angegeben, dass mindestens ein Fehler aufgetreten ist.  
  
### <a name="possible-causes"></a>Mögliche Ursachen  
 Folgende Ereignisse zählen zu den möglichen Ursachen:  
  
-   Auf dem Berichtsserver ist ein Verarbeitungsfehler aufgetreten.  
  
-   Während der lokalen Berichtsverarbeitung ist in der Vorschau für einen Bericht ein Verarbeitungsfehler aufgetreten.  
  
-   Ein Gruppierungsausdruck ergab einen falschen Datentyp.  
  
-   Eine Filterdefinition hat zwei Ausdrücke angegeben, die in Datentypen ausgewertet wurden, die nicht verglichen werden konnten.  
  
-   Ein Ausdruck verweist auf ein Field-Objekt, das in der Fields-Auflistung nicht vorhanden ist.  
  
-   Ein Ausdruck hat einen Aggregatfunktionsaufruf mit einem ungültigen oder konfliktverursachenden Bereich enthalten.  
  
-   Ein Ausdruck verweist auf einen Parameter, der in der Auflistung der Berichtsparameter nicht vorhanden ist.  
  
-   Eine benutzerdefinierte Assembly oder eine [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Assembly, die falsch bereitgestellt wurde, konnte nicht geladen werden.  
  
-   Ein Parameter, für den die Nullable-Eigenschaft auf **FALSE** festgelegt wurde, hat einen NULL-Wert im Parameter erkannt.  
  
-   Ein Ausdruck für die Hidden-Eigenschaft eines Datenbereichs enthält einen Fehler: Der Objektverweis ist nicht auf eine Objektinstanz festgelegt.  
  
-   Ein Ausdruck hat einen ungültigen Funktionsaufruf oder einen Syntaxfehler enthalten.  
  
## <a name="user-action"></a>Benutzeraktion  
  
### <a name="finding-more-information"></a>Weitere Informationsquellen  
 Führen Sie eine oder mehrere der folgenden Aktionen aus:  
  
-   Wenn Sie den Bericht auf dem Berichtsserver anzeigen oder wenn Sie den Bericht als Abonnement anzeigen, beachten Sie den gesamten Text der Fehlermeldung. Zusätzliche Informationen werden im erweiterten Text angezeigt.  
  
-   Wenn Sie einen Bericht im Berichts-Designer erstellen und dieser Fehler angezeigt wird, während Sie eine Vorschau des Berichts anzeigen oder ihn veröffentlichen, werden im Fenster Fehlerliste zusätzliche Informationen bereitgestellt.  
  
-   Wenn Sie den Bericht in der Vorschau des Berichts-Designers erstellen, beachten Sie den gesamten Text der Fehlermeldung. Zusätzliche Informationen werden im erweiterten Text angezeigt.  
  
-   Wenn Sie einen Bericht auf dem Berichtsserver anzeigen und wenn Sie auf dem Berichtsserver als lokaler Administrator fungieren, können Sie die Aufrufliste anzeigen, wenn Sie mit der rechten Maustaste auf die Seite klicken und **Quelltext anzeigen**auswählen. Zusätzliche Informationen werden in der Aufrufliste angezeigt.  
  
-   Wenn Sie des Berichtsserver als lokaler Administrator ausführen, suchen Sie in der Protokolldatei nach `ReportProcessingException`. Weitere Informationen sind in den Protokolleinträgen enthalten. Die Berichtsserver-Protokolldatei befindet sich gewöhnlich unter \<*Laufwerk*>:\Programme\Microsoft SQL Server\MSRS12.MSSQLSERVER\Reporting Services\LogFiles\ReportServerService__*datetimestamp*.log. Weitere Informationen finden Sie unter [Reporting Services-Protokolldateien und Quellen](../../reporting-services/report-server/reporting-services-log-files-and-sources.md).  
  
### <a name="failed-to-load-expression-host-assembly"></a>Fehler beim Laden der Ausdruckshostassembly  
 Benutzerdefinierte Assemblys müssen über starke Namenssignaturen verfügen, und das Attribut „AllowPartiallyTrustedCallers“ muss für die Assembly festgelegt sein. Weitere Informationen finden Sie unter [Using Custom Assemblies with Reports](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md) und [Understanding Security Policies](../../reporting-services/extensions/secure-development/understanding-security-policies.md).  
  
### <a name="a-built-in-global-name-does-not-exist"></a>Ein integrierter globaler Name ist nicht vorhanden  
 Überprüfen Sie die Rechtschreibung in Ausdrücken. Bei integrierten globalen Namen, Parametern und Feldnamen wird nach Groß-/Kleinschreibung unterschieden. Überprüfen Sie in dem Ausdruck, der den Fehler verursacht, ob der Name im Bericht tatsächlich vorhanden ist und richtig geschrieben wurde. Weitere Informationen finden Sie unter [Integrierte Sammlungen in Ausdrücken &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/built-in-collections-in-expressions-report-builder.md).  
  
### <a name="parameter-properties-and-null"></a>Parametereigenschaften und Null  
 Ein mehrwertiger Parameter darf nicht NULL sein. Weitere Informationen finden Sie unter [Berichtsparameter &#40;Berichts-Generator und Berichts-Designer&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)" basiert.  
  
### <a name="main-report-with-subreport-could-not-be-processed"></a>Hauptbericht mit Unterbericht konnte nicht verarbeitet werden  
 Ein Bericht mit Unterberichten muss von der gleichen Version des [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Berichtsprozessors verarbeitet werden. Beim Aktualisieren von Berichten auf die aktuelle Version des Berichtsdefinitionsschemas werden der Hauptbericht und die Unterberichte möglicherweise nicht gleichzeitig aktualisiert. Wenn die Version zwischen einem Bericht und dessen Unterberichten nicht kompatibel ist, wird die folgende Meldung angezeigt: "Der Unterbericht 'x' konnte nicht verarbeitet werden."  
  
 Sie müssen den Hauptbericht oder die Unterberichte ändern, sodass alle Berichte von der gleichen Version des Berichtsprozessors verarbeitet werden. Informationen zu Fehlern beim Upgrade eines Berichts finden Sie unter [Aktualisieren von Berichten](../../reporting-services/install-windows/upgrade-reports.md).  
  
### <a name="verify-function-calls-are-visual-basic-and-not-sql"></a>Stellen Sie sicher, dass Funktionsaufrufe Visual Basic und nicht SQL entsprechen.  
 Sie können SQL-Funktionen in Abfragetext für eine relationale Datenbank verwenden. Sie können die [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] -Funktionen nicht im Abfragetext verwenden.  
  
 In [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]können für Ausdrücke [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] -Funktionen, System.Math-Funktionen oder System.String-Funktionen, vollqualifizierte [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] -Funktionen oder benutzerdefinierte Funktionen verwendet werden, die Sie in benutzerdefiniertem Code oder in einer benutzerdefinierten Assembly bereitstellen. In einem Ausdruck können keine SQL-Funktionen verwendet werden.  
  
 Stellen Sie sicher, dass die in der Abfrage und in den Ausdrücken vorgenommenen Funktionsaufrufe gültig sind.  
  
### <a name="cannot-compare-data-types-for-a-filter"></a>Datentypen für einen Filter können nicht verglichen werden  
 In einer Filtergleichung müssen der Filterausdruck, mit dem die zu filternden Elemente definiert werden, und der Filterwert den gleichen Datentyp aufweisen, damit sie verglichen werden können. Wenn einer der folgenden Fehler angezeigt wird, ändern Sie den Filterausdruck oder den Filterwert, sodass die Datentypen übereinstimmen:  
  
-   Die Verarbeitung von *\<Berichtselementtyp>* kann für *\<Berichtselementname>* nicht ausgeführt werden. Daten der Typen *\<Typ>* und *\<Typ>* können nicht verglichen werden. Überprüfen Sie den von *\<Berichtselementname>* zurückgegebenen Datentyp.  
  
-   Fehler beim Auswerten von *\<Eigenschaftenname>*.  
  
-   Fehler beim Auswerten von *\<Eigenschaftenname>*. Es wird auf ein Datasetfeld verwiesen, das einen Fehler aufweist: *\<Fehlerzeichenfolge>*.  
  
 Weitere Informationen finden Sie unter [Filtern, Gruppieren und Sortieren von Daten &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md).  
  
### <a name="invalid-or-conflicting-scope-specification-in-an-aggregate-function-call"></a>Ungültige oder konfliktverursachende Bereichsspezifikation in einem Aggregatfunktionsaufruf  
 Wenn Sie Aggregatfunktionsaufrufe in einen Ausdruck in einer Tablix-Zelle aufnehmen, wertet der Berichtsprozessor den Ausdruck im Bereich der innersten Gruppen aus, zu denen die Zelle gehört.  
  
 Sie können auch den Namen eines bestimmten Bereichs an eine Aggregatfunktion übergeben. Bereich bezieht sich auf den Namen eines Datasets, eines Datenbereichs oder auf den Namen eine Bereichs, der sich weiter oben in der Datenhierarchie befindet. Dies gilt für die folgenden Meldungen:  
  
-   Der *\<Berichtselementtyp>* „*\<Berichtselementname>*“ weist einen ungültigen Bereich „*\<Bereichsname>*“ auf. Der Bereich muss der aktuelle Bereich sein oder im aktuellen Bereich enthalten sein.  
  
-   Der *\<Eigenschaftenname>*-Ausdruck für *\<Berichtselementtyp>* „*\<Berichtselementname>*“ weist einen Bereichsparameter auf, der für eine Aggregatfunktion nicht gültig ist. Der Bereichsparameter muss auf eine Zeichenfolgenkonstante festgelegt sein, die einem der folgenden Werte entspricht: dem Namen einer enthaltenden Gruppe, dem Namen eines enthaltenden Datenbereichs oder dem Namen eines Datasets.  
  
 Für Aggregatfunktionen, die laufende Summen berechnen (**Previous**, **RunningValue**oder **RowNumber**), können Sie einen Bereichsparameter angeben, bei dem es sich entweder um einen Zeilengruppennamen oder einen Spaltengruppennamen handelt. Beides ist nicht möglich. Dies gilt für die folgende Fehlermeldung:  
  
-   Die **Previous**-, **RunningValue**- oder **RowNumber**-Aggregatfunktionen, die in den Datenzellen von *\<Berichtselementtyps>* „*\<Berichtselementname>*“ verwendet wurden, verweisen auf Gruppierungsbereiche in den Spalten und Zeilen von *\<Berichtselementtyp>*. Die Bereichsparameter aller **Previous**-, **RunningValue**- und **RowNumber**-Aggregatfunktionen in einem *\<Berichtselementtyp>* können nur auf Zeilen- oder Datenspaltengruppierungen, aber nicht auf beide Gruppierungen verweisen.  
  
 Weitere Informationen finden Sie unter [Ausdrucksbereich für Gesamtwerte, Aggregate und integrierte Sammlungen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md) und [Integrierte Sammlungen in Ausdrücken &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/built-in-collections-in-expressions-report-builder.md).  
  
### <a name="default-dataset-scope-for-a-top-level-text-box"></a>Standardmäßiger Datasetbereich für ein Textfeld der obersten Ebene  
 Verwenden Sie keinen Standardbereich für ein Textfeld, das der Berichtsentwurfsoberfläche hinzugefügt wurde, wenn der Bericht über mehr als ein Dataset verfügt. Verwenden Sie einen Ausdruck, der den Namen des Datasets als Bereich enthält, und eine Aggregatfunktion. Beispiel: `=First(Fields!FieldName.Value, "DataSet2")`.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Ausdrücke &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)   
 [Aggregatfunktionsreferenz &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md)   
 [Beispiele für Ausdrücke &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Berichtsdatasets &#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)   
 [Häufig verwendete Filter (Berichts-Generator und SSRS)](../../reporting-services/report-design/commonly-used-filters-report-builder-and-ssrs.md)   
 [Datasetfeld-Sammlung &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)   
 [Benutzerdefinierter Code und Assemblyverweise in Ausdrücken in Berichts-Designer (SSRS)](../../reporting-services/report-design/custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md)   
 [Verweise auf Parameters-Sammlungen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/built-in-collections-parameters-collection-references-report-builder.md)  
  
  
