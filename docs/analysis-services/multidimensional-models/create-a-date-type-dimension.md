---
title: "Erstellen einer Datumstypdimension | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Zeitdimensionen [Analysis Services]"
  - "Dimensionen [Analysis Services], Zeit"
  - "Hinzufügen von Zeitintelligenz"
  - "Serverzeitdimensionen [Analysis Services]"
  - "Kalender [Analysis Services]"
  - "Zeitintelligenz [Analysis Services]"
ms.assetid: 6d692856-4b01-4dca-a650-f97ac220c114
caps.latest.revision: 38
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Erstellen einer Datumstypdimension
  In [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]ist eine Zeitdimension ein Dimensionstyp, dessen Attribute Zeiträume darstellen, z. B. Jahre, Semester, Quartale, Monate und Tage. Die in einer Zeitdimension enthaltenen Zeiträume stellen zeitbasierte Granularitätsebenen für Analysen und Berichte bereit. Die Attribute sind in Hierarchien organisiert, und die Granularität der Zeitdimension wird weitgehend durch die Anforderungen des Geschäfts und des Berichtswesens an historische Daten bestimmt. So verwenden beispielsweise die meisten Finanz- und Verkaufsdaten in Business Intelligence-Anwendungen eine monatliche oder quartalsweise Granularität.  
  
 In der Regel beeinhalten Cubes in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] eine Zeitdimension in irgendeiner Form. Ein Cube kann mehrere Zeitdimensionen oder mehrere Hierarchien derselben Zeitdimension enthalten. Diese hängen von der Granularität der Daten und den Berichtsanforderungen ab. Es benötigen jedoch nicht alle Cubes eine Zeitdimension. Manche OLAP-Anwendungen, wie z. B. eine aktivitätsbasierte Kostenrechnung, benötigen keine Zeitdimension, weil die Kostenrechnung in einer aktivitätsbasierten Dimension auf einer Aktivität und nicht auf Zeit basiert.  
  
## Dimensionsstruktur  
 Die Dimensionsstruktur für eine Zeitdimension hängt davon ab, wie die zugrunde liegende Datenquelle die Zeitraumangaben speichert. Aus diesem Unterschied beim Speichern ergeben sich zwei Basistypen von Zeitdimensionen:  
  
 Zeitdimension  
 Zeitdimensionen sind mit anderen Dimensionen vergleichbar, da die Dimensionstabelle die Attribute für die Dimension liefert. Jede Spalte der Dimensionshaupttabelle definiert ein Attribut für einen bestimmten Zeitraum.  
  
 Wie bei anderen Dimensionen hat die Faktentabelle eine Fremdschlüsselbeziehung mit der Dimensionstabelle für die Zeitdimension. Das Schlüsselattribut für eine Zeitdimension basiert entweder auf einem Ganzzahlschlüssel, oder auf der niedrigsten Detailebene, wie dem Datum, das in der Dimensionshaupttabelle enthalten ist.  
  
 Serverzeitdimension  
 Wenn Sie über keine Dimensionstabelle verfügen, um zeitgestützte Attribute daran zu binden, können Sie durch [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] eine auf Zeiträumen basierende Serverzeitdimension definieren lassen. Um die von einer Serverzeitdimension dargestellten Hierarchien, Ebenen und Elemente zu definieren, wählen Sie beim Erstellen der Dimension Standardzeiträume aus.  
  
 Attribute in einer Serverzeitdimension verfügen über bestimmte Zeitattributbindungen. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] verwendet die zu Daten gehörigen Attributtypen, z. B. Jahr, Monat oder Tag, um Elemente von Attributen in einer Zeitdimension zu definieren.  
  
 Nachdem Sie die Serverzeitdimension in einen Cube aufgenommen haben, legen Sie die Beziehung zwischen der Measuregruppe und der Serverzeitdimension fest, indem Sie die Beziehung auf der Seite **Dimensionsverwendung definieren** des Cube-Assistenten angeben.  
  
### Kalender  
 In einer Zeitdimension oder einer Serverzeitdimension werden die Zeitraumattribute in Hierarchien miteinander gruppiert. Diese Hierarchien werden im Allgemeinen als Kalender bezeichnet.  
  
 Business Intelligence-Anwendungen benötigen oft mehrere Kalenderdefinitionen. Eine Personalabteilung verwaltet die Mitarbeiter z.B. mit einem *Standard*-Kalender – einem auf zwölf Monaten basierenden gregorianischen Kalender, der am 1. Januar beginnt und am 31. Dezember endet. Dieselbe Personalabteilung kann Ausgaben aber über einen *Geschäfts*-Kalender verfolgen – einen zwölfmonatigen Kalender, der das vom Unternehmen verwendete Geschäftsjahr definiert.  
  
 Diese verschiedenen Kalender können Sie manuell im Dimensions-Designer erstellen. Der Dimensions-Assistent stellt jedoch verschiedene Hierarchievorlagen bereit, mit denen Sie automatisch verschiedene Kalendertypen generieren können, wenn Sie eine Zeitdimension oder eine Serverzeitdimension erstellen. Die folgende Tabelle beschreibt die verschiedenen Kalender, die mit dem Dimensions-Assistenten generiert werden können.  
  
|Kalender|Description|  
|--------------|-----------------|  
|Standardkalender|Ein zwölfmonatiger gregorianischer Kalender, der am 1. Januar beginnt und am 31. Dezember endet.<br /><br /> Unabhängig davon, ob Sie mit dem Dimensions-Assistenten eine Zeitdimension oder eine Serverzeitdimension erstellen, generiert der Assistent eine Hierarchie für einen Standardkalender, nachdem Sie die Attribute definiert haben, die die Zeiträume der Dimension darstellen. Wenn Sie mit dem Dimensions-Assistenten eine Serverzeitdimension erstellen, können Sie das Anfangsdatum des Standardkalenders auf einen anderen Tag als den 1. Januar legen.|  
|Geschäftskalender|Ein zwölfmonatiger Geschäftskalender. Wenn Sie diesen Kalender auswählen, müssen Sie den Anfangstag des vom Unternehmen verwendeten Geschäftsjahres angeben.<br /><br /> Hinweis: Dieser Kalender ist nur verfügbar, wenn Sie mit dem Dimensions-Assistenten eine Serverzeitdimension erstellen.|  
|Berichtskalender (oder Marketingkalender)|Ein zwölfmonatiger Berichtskalender, der in einem dreimonatigen (quartalsweisen) Muster zwei Monate mit vier und einen Monat mit fünf Wochen enthält. Wenn Sie diesen Kalender auswählen, müssen Sie den Anfangstag und den Anfangsmonat des Dreimonatsmusters mit 4-4-5, 4-5-4 oder 5-4-4 Wochen angeben, wobei diese Zahlen die in einem Monat enthaltenen Wochen darstellen.<br /><br /> Hinweis: Dieser Kalender ist nur verfügbar, wenn Sie mit dem Dimensions-Assistenten eine Serverzeitdimension erstellen.|  
|Produktionskalender|Ein Kalender, der 13 aus vier Wochen bestehende Perioden verwendet, die in drei Quartale mit drei Perioden und ein Quartal mit vier Perioden unterteilt sind. Wenn Sie diesen Kalender auswählen, müssen Sie die Anfangswoche (zwischen 1 und 4) und den Anfangsmonat des von Ihrem Unternehmen verwendeten Produktionsjahres angeben und festlegen, welches Quartal vier Perioden enthält.<br /><br /> Hinweis: Dieser Kalender ist nur verfügbar, wenn Sie mit dem Dimensions-Assistenten eine Serverzeitdimension erstellen.|  
|ISO 8601-Kalender|Der Standardkalender für die Daten- und Zeitdarstellung (8601) der Internationalen Organisation für Normung (International Organization for Standardization, ISO). Dieser Kalender besitzt eine integrale Anzahl von 7-Tage-Wochen. Das neue Jahr kann mehrere Wochen vor oder nach dem Beginn des neuen Jahres auf der Basis des gregorianischen Kalenders anfangen. Die erste Woche dieses Kalenders wird durch die erste Woche des gregorianischen Kalenders bestimmt, die einen Donnerstag enthält. Aus diesem Grund kann es sein, dass der erste Tag dieser Woche – der Sonntag – noch im Vorjahr liegt.<br /><br /> Hinweis: Dieser Kalender ist nur verfügbar, wenn Sie mit dem Dimensions-Assistenten eine Serverzeitdimension erstellen.|  
  
 Wenn Sie eine Serverzeitdimension erstellen und die Zeiträume und Kalender angeben, die in der Dimension verwendet werden sollen, fügt der Dimensions-Assistent die jeweils für die angegebenen Kalender geeigneten Attribute hinzu. Wenn Sie z. B. eine Serverzeitdimension erstellen, die als Zeitraum "Jahre" verwendet und sowohl Geschäfts- als auch Berichtskalender enthält, fügt der Assistent dann der Dimension die Attribute FiscalYear und ReportingYear sowie das Standardattribut Years hinzu. Eine Serverzeitdimension besitzt außerdem Attribute für Kombinationen ausgewählter Zeiträume, wie das Attribut DayOfWeek für eine Dimension, die Days und Weeks enthält. Der Dimensions-Assistent erstellt eine Kalenderhierarchie, indem er Attribute kombiniert, die zu einem einzelnen Kalendertyp gehören. Eine Finanzkalenderhierarchie kann die folgenden Ebenen enthalten: Geschäftsjahr, Geschäftshalbjahr, Geschäftsquartal, Geschäftsmonat und Geschäftstag.  
  
## Hinzufügen von Zeitintelligenz mit dem Business Intelligence-Assistenten  
 Nachdem Sie eine Zeitdimension definiert und diese Dimension einem Cube hinzugefügt haben, können Sie mit dem Business Intelligence-Assistenten eine Zeitintelligenzfunktion hinzufügen, wie Vergleiche zwischen Zeitraum und Datum, Zeitraum und Zeitraum und Measures für einen gleitenden Durchschnitt. Weitere Informationen finden Sie unter [Definieren von Zeitintelligenzberechnungen mithilfe des Business Intelligence-Assistenten](../../analysis-services/multidimensional-models/define-time-intelligence-calculations-using-the-business-intelligence-wizard.md).  
  
> [!NOTE]  
>  Mit dem Business Intelligence-Assistenten können Sie keine Zeitintelligenz zu Serverzeitdimensionen hinzufügen. Der Business Intelligence-Assistent fügt eine Hierarchie für die Unterstützung der Zeitintelligenz hinzu. Diese Hierarchie muss mit einer Spalte der Zeitdimensionstabelle verbunden werden. Serverzeitdimensionen besitzen keine zugehörige Zeitdimensionstabelle und können diese zusätzliche Hierarchie daher nicht unterstützen.  
  
## Siehe auch  
 [Erstellen einer Zeitdimension durch Generieren einer Zeittabelle](../../analysis-services/multidimensional-models/create-a-time-dimension-by-generating-a-time-table.md)   
 [Business Intelligence-Assistent (F1-Hilfe)](../Topic/Business%20Intelligence%20Wizard%20F1%20Help.md)   
 [Dimensionstypen](../Topic/Dimension%20Types.md)  
  
  