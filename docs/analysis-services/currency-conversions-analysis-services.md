---
title: Währungsumrechnungen (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- multiple currency conversions
- monetary data [SQL Server]
- currency [Analysis Services]
- converting currency
- one-to-many currency conversions
- many-to-many currency conversions [Analysis Services]
- many-to-one currency conversions [Analysis Services]
ms.assetid: e03f491c-7df8-46a0-ade9-f2e55b68db85
caps.latest.revision: 18
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 3137e7f42cd910de81af821f4e63d95943a4ff06
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="currency-conversions-analysis-services"></a>Währungsumrechnungen (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas-aas](../includes/ssas-appliesto-sqlas-aas.md)]

  [!INCLUDE[applies](../includes/applies-md.md)] Nur Multidimensional  
  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] verwendet eine Kombination von Funktionen, die durch MDX-Skripts (Multidimensional Expressions) bestimmt werden, um für Cubes, die mehrere Währungen unterstützen, Währungsumrechnungen bereitzustellen.  
  
## <a name="currency-conversion-terminology"></a>Terminologie zur Währungsumrechung  
 Die folgende Terminologie wird in [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] verwendet, um die Funktionen zur Währungsumrechnung zu beschreiben:  
  
 Pivotwährung  
 Die Währung, für die Wechselkurse in die Wechselkurs-Measuregruppe eingegeben werden.  
  
 Lokale Währung  
 Die Währung, in der Transaktionen gespeichert werden, auf denen die umzurechnenden Measures basieren.  
  
 Die lokale Währung kann durch Folgendes identifiziert werden:  
  
-   Ein Währungsbezeichner in der Faktentabelle, die mit der Transaktion gespeichert wurde. Dies ist häufig bei Bankanwendungen der Fall, bei denen die Transaktion selbst die für die Transaktion verwendete Währung identifiziert.  
  
-   Ein Währungsbezeichner, der mit einem Attribut in einer Dimensionstabelle verbunden ist, das wiederum mit einer Transaktion in der Faktentabelle verbunden ist. Dies ist häufig bei Finanzanwendungen der Fall, wenn ein Ort oder ein anderer Bezeichner, wie eine Niederlassung, die für die verbundene Transaktion verwendete Währung identifiziert.  
  
 Berichtswährung  
 Die Währung, in die Transaktionen von der Pivotwährung umgerechnet werden.  
  
> [!NOTE]  
>  Bei m:1-Währungsumrechnungen sind die Pivotwährung und die Berichtswährung identisch.  
  
 Währungsdimension  
 Eine Datenbankdimension, die durch die folgenden Einstellungen definiert ist:  
  
-   Die **Type** -Eigenschaft der Dimension wird auf Currency festgelegt.  
  
-   Die **Type** -Eigenschaft von einem Attribut der Dimension wird auf CurrencyName festgelegt.  
  
    > [!IMPORTANT]  
    >  Die Werte dieses Attributs müssen in allen Spalten verwendet werden, die einen Währungsbezeichner enthalten sollen.  
  
 Wechselkurs-Measuregruppe  
 Eine Measuregruppe in einem Cube, die durch die folgenden Einstellungen definiert wird:  
  
-   Zwischen einer Währungsdimension und der Wechselkurs-Measuregruppe besteht eine reguläre Dimensionsbeziehung.  
  
-   Zwischen einer Zeitdimension und der Wechselkurs-Measuregruppe besteht eine reguläre Dimensionsbeziehung.  
  
-   Wahlweise wird die **Type** -Eigenschaft auf ExchangeRate festgelegt. Während der Business Intelligence-Assistent die Beziehungen mit den Währungs- und Zeitdimensionen zum Identifizieren der wahrscheinlichen Wechselkurs-Measuregruppe verwendet, können Clientanwendungen die Wechselkurs-Measuregruppen leichter identifizieren, wenn die **Type** -Eigenschaft auf ExchangeRate festgelegt wurde.  
  
-   Mindestens ein Measure, der die Wechselkurse darstellt, die in der Wechselkurs-Measuregruppe enthalten sind.  
  
 Berichtswährungsdimension  
 Die Dimension, die vom Business Intelligence-Assistenten nach dem Definieren einer Währungsumrechnung definiert wird, und die die Berichtswährungen für diese Währungsumrechnung enthält. Die Berichtswährungsdimension basiert auf einer benannten Abfrage aus der Dimensionshaupttabelle der Währungsdimension. Diese Abfrage ist in der Datenquellensicht definiert, auf der die zur Wechselkurs-Measuregruppe zugeordnete Währungsdimension basiert. Die Dimension wird durch die folgenden Einstellungen definiert:  
  
-   Die **Type** -Eigenschaft der Dimension wird auf Currency festgelegt.  
  
-   Die **Type** -Eigenschaft des Schlüsselattributs der Dimension wird auf CurrencyName festgelegt.  
  
-   Die **Type** -Eigenschaft von einem Attribut innerhalb der Dimension wird auf CurrencyDestination festgelegt, und die Spalte, die an das Attribut gebunden ist, enthält den Währungsbezeichner, der die Berichtswährung für die Währungsumrechnung darstellt.  
  
## <a name="defining-currency-conversions"></a>Definieren von Währungsumrechnungen  
 Sie können mit dem Business Intelligence-Assistenten die Funktionen der Währungsumrechnung für einen Cube definieren, oder Sie können Währungsumrechnungen mithilfe von MDX-Skripts manuell definieren.  
  
### <a name="prerequisites"></a>Erforderliche Komponenten  
 Bevor Sie eine Währungsumrechnung in einem Cube mithilfe des Business Intelligence-Assistenten definieren können, müssen Sie zunächst mindestens eine Währungsdimension, eine Zeitdimension und eine Wechselkurs-Measuregruppe definieren. Aus diesen Objekten kann der Business Intelligence-Assistent die Daten und Metadaten abrufen, mit deren Hilfe die notwendige Berichtswährungsdimension und das notwendige MDX-Skript zum Bereitstellen der Währungsumrechnungsfunktionen erstellt werden.  
  
### <a name="decisions"></a>Entscheidungen  
 Sie müssen die folgenden Entscheidungen treffen, bevor der Business Intelligence-Assistent die notwendige Berichtswährungsdimension und das notwendige MDX-Skript zum Bereitstellen der Währungsumrechnungsfunktionen erstellen kann:  
  
-   Wechselkursrichtung  
  
-   Umgerechnete Elemente  
  
-   Umrechnungstyp  
  
-   Lokale Währungen  
  
-   Berichtswährungen  
  
### <a name="exchange-rate-directions"></a>Wechselkursrichtungen  
 Die Wechselkurs-Measuregruppe enthält Measures, die Wechselkurse zwischen lokalen Währungen und Pivotwährungen (die häufig als Firmenwährungen bezeichnet werden) darstellen. Die Kombination aus Wechselkursrichtung und Umrechnungstyp bestimmt den Vorgang, die für die Measures ausgeführt wird, die von dem vom Business Intelligence-Assistenten erstellten MDX-Skript umgerechnet werden sollen. Die folgende Tabelle beschreibt die, abhängig vom Wechselkurs und Umrechnungstyp ausgeführten Vorgänge, die auf den im Business Intelligence-Assistenten verfügbaren Optionen für die Wechselkursrichtung und die Umrechnungsrichtungen basieren.  
  
|||||  
|-|-|-|-|  
|Wechselkursrichtung|**n:1**|**1:n**|**m:n**|  
|**n Pivotwährung zu 1 Beispielwährung**|Multiplizieren Sie das umzurechnende Measure mit dem Wechselkursmeasure für die lokale Währung, um das Measure in die Pivotwährung umzurechnen.|Dividieren Sie das umzurechnende Measure durch das Wechselkursmeasure für die Berichtswährung, um das Measure in die Berichtswährung umzurechnen.|Multiplizieren Sie das umzurechnende Measure mit dem Wechselkursmeasure für die lokale Währung, um das Measure in die Pivotwährung umzurechnen. Dividieren Sie anschließend das umgerechnete Measure durch das Wechselkursmeasure für die Berichtswährung, um das Measure in die Berichtswährung umzurechnen.|  
|**n Beispielwährung zu 1 Pivotwährung**|Dividieren Sie das umzurechnende Measure durch das Wechselkursmeasure für die lokale Währung, um das Measure in die Pivotwährung umzurechnen.|Multiplizieren Sie das umzurechnende Measure mit dem Wechselkursmeasure für die Berichtswährung, um das Measure in die Berichtswährung umzurechnen.|Dividieren Sie das umzurechnende Measure durch das Wechselkursmeasure für die lokale Währung, um das Measure in die Pivotwährung umzurechnen. Multiplizieren Sie anschließend das umgerechnete Measure mit dem Wechselkursmeasure für die Berichtswährung, um das Measure in die Berichtswährung umzurechnen.|  
  
 Wählen Sie die Wechselkursrichtung im Business Intelligence-Assistenten auf der Seite **Optionen für die Währungsumrechnung festlegen** aus. Weitere Informationen zum Festlegen der Umrechnungsrichtung finden Sie unter [Optionen für die Währungsumrechnung festlegen &#40;Business Intelligence-Assistent&#41;](http://msdn.microsoft.com/library/a49d4e1f-bdda-4a83-ab4f-ce8c500e1d6d).  
  
### <a name="converted-members"></a>Umgerechnete Elemente  
 Sie können mit dem Business Intelligence-Assistenten angeben, mit welchen Measures aus der Wechselkurs-Measuregruppen für folgende Elemente Werte umgerechnet werden:  
  
-   Measures in anderen Measuregruppen.  
  
-   Elemente einer Attributhierarchie für ein Kontoattribut in einer Datenbankdimension.  
  
-   Kontotypen, die von Elementen einer Attributhierarchie für ein Kontoattribut in einer Datenbankdimension verwendet werden.  
  
 Der Business Intelligence-Assistent verwendet diese Informationen innerhalb des MDX-Skripts, das vom Assistenten generiert wurde, um den Umfang der Währungsumrechnung zu bestimmen. Weitere Informationen zum Angeben von Elementen für die Währungsumrechnung finden Sie unter [Member auswählen &#40;Business Intelligence-Assistent&#41;](http://msdn.microsoft.com/library/1a147461-d594-41e7-a41d-09d2d003e1e0).  
  
### <a name="conversion-types"></a>Umrechnungstypen  
 Der Business Intelligence-Assistent unterstützt drei verschiedene Währungsumrechnungstypen:  
  
-   **1:n**  
  
     Transaktionen, die in der Faktentabelle in der Pivotwährung gespeichert sind und dann in mindestens eine Berichtswährung umgerechnet werden.  
  
     Die Pivotwährung kann z.&#160;B. auf US-Dollar (USD) festgelegt werden, und die Transaktionen werden in der Faktentabelle in USD gespeichert. Dieser Umrechnungstyp rechnet diese Transaktionen von der Pivotwährung in die angegebenen Berichtswährungen um. Daraus resultiert, dass die Transaktionen in der angegebenen Pivotwährung gespeichert und entweder in der Pivotwährung oder in einer der Berichtswährungen, die in der für die Währungsumrechnung definierten Berichtswährungsdimension angegeben wurden, angezeigt werden.  
  
-   **n:1**  
  
     Transaktionen, die in der Faktentabelle in der lokalen Währung gespeichert werden und anschließend in die Pivotwährung umgerechnet werden. Die Pivotwährung dient als die einzige angegebene Berichtswährung in der Berichtswährungsdimension.  
  
     Die Pivotwährung kann z. B. auf US-Dollar (USD) festgelegt werden, während in der Faktentabelle die Transaktionen in Euro (EUR), Australischen Dollar (AUD) und Mexikanischen Pesos (MXN) gespeichert werden. Dieser Umrechnungstyp rechnet diese Transaktionen von ihren angegebenen lokalen Währungen in die Pivotwährung um. Daraus resultiert, dass die Transaktionen in den angegebenen lokalen Währungen gespeichert und in der Pivotwährung, die in der für die Währungsumrechnung definierten Berichtswährungsdimension angegeben wurde, angezeigt werden.  
  
-   **m:n**  
  
     Transaktionen, die in der Faktentabelle in den lokalen Währungen gespeichert werden. Die Funktionen der Währungsumrechnung rechnen solche Transaktionen in die Pivotwährung und anschließend in mindestens eine Berichtswährung um.  
  
     Die Pivotwährung kann z. B. auf US-Dollar (USD) festgelegt werden, während in der Faktentabelle die Transaktionen in Euro (EUR), Australischen Dollar (AUD) und Mexikanischen Pesos (MXN) gespeichert werden. Bei diesem Umrechnungstyp werden diese Transaktionen aus ihren angegebenen lokalen Währungen in die Pivotwährung umgerechnet und anschließend werden die Transaktionen erneut aus der Pivotwährung in die angegebenen Berichtswährung umgerechnet. Daraus resultiert, dass die Transaktionen in den angegebenen lokalen Währungen gespeichert und entweder in der angegebenen Pivotwährung oder in einer der Berichtswährungen, die in der für die Währungsumrechnung definierten Berichtswährungsdimension angegeben wurden, angezeigt werden.  
  
 Durch das Angeben des Umrechnungstyps kann der Business Intelligence-Assistent die benannte Abfrage und die Dimensionsstruktur der Berichtswährungsdimension sowie die Struktur des für die Währungsumrechnung definierten MDX-Skripts definieren.  
  
### <a name="local-currencies"></a>Lokale Währungen  
 Wenn Sie einen m:n- oder m:1-Umrechnungstyp für die Währungsumrechnung auswählen, müssen Sie angeben, wie die lokalen Währungen identifiziert werden sollen, aus denen das MDX-Skript vom Business Intelligence-Assistenten generiert wird, das die Berechnungen für die Währungsumrechnung ausführt. Die lokale Währung einer Transaktion kann in der Faktentabelle auf zweierlei Art identifiziert werden:  
  
-   Die Measuregruppe enthält eine reguläre Dimensionsbeziehung zur Currency-Dimension. In der [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)] -Beispieldatenbank [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] verfügt die Internet Sales-Measuregruppe über eine reguläre Dimensionsbeziehung mit der Currency-Dimension. Die Faktentabelle für diese Measuregruppe enthält eine Fremdschlüsselspalte, die auf die Währungsbezeichner in der Dimensionstabelle für diese Dimension verweist. In diesem Fall können Sie das Attribut aus der Währungsdimension auswählen, auf die von der Measuregruppe zum Identifizieren der lokalen Währung für die Transaktionen in der Faktentabelle für diese Measuregruppe verweist. Diese Situation tritt sehr häufig in Bankanwendungen auf, bei denen die Transaktion selbst die Währung innerhalb der Transaktion bestimmt.  
  
-   Die Measuregruppe enthält eine referenzierte Dimensionsbeziehung zur Währungsdimension über eine andere Dimension, die direkt auf die Currency-Dimension verweist. In der [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)] -Beispieldatenbank [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] enthält die Financial Reporting-Measuregruppe beispielsweise eine Dimensionsbeziehung zur Currency-Dimension, auf die durch die Organization-Dimension verwiesen wird. Die Faktentabelle für diese Measuregruppe enthält eine Fremdschlüsselspalte, die auf Elemente in der Dimensionstabelle für die Dimension Organization verweist. Die Dimensionstabelle für die Organisationsdimension wiederum enthält eine Fremdschlüsselspalte, die auf die Währungsbezeichner in der Dimensionstabelle für die Währungsdimension verweist. Diese Situation tritt besonders häufig bei Finanzberichtsanwendungen auf, wenn der Ort oder die Niederlassung, in der eine Transaktion stattgefunden hat, die Währung für diese Transaktion bestimmt. In diesem Fall können Sie das Attribut auswählen, dass auf die Currency-Dimension von der Dimension der Geschäftseinheit verweist.  
  
### <a name="reporting-currencies"></a>Berichtswährungen  
 Wenn Sie einen m:n- oder 1:n-Umrechnungstyp für die Währungsumrechnung auswählen, müssen Sie die Berichtswährungen angeben, für die das vom Business Intelligence-Assistenten generiert MDX-Skript die Berechnungen für die Währungsumrechnung ausführt. Sie können entweder alle Elemente der Currency-Dimension, die zur Wechselkurs-Measuregruppe gehören, angeben, oder Sie können einzelne Elemente aus der Dimension auswählen.  
  
 Der Business Intelligence-Assistent erstellt eine Berichtswährungsdimension, die auf einer benannten Abfrage basiert, die aus der Dimensionstabelle für die Währungsdimension mithilfe der ausgewählten Berichtswährungen erstellt wurde.  
  
> [!NOTE]  
>  Wenn Sie den 1:n-Umrechnungstyp auswählen, wird auch eine Berichtswährungsdimension erstellt. Die Dimension enthält nur ein Element, das die Pivotwährung darstellt, weil die Pivotwährung auch als Berichtswährung bei einer 1:n-Währungsumrechnung verwendet wird.  
  
 Eine separate Currency-Dmension wird für jede in einem Cube definierte Währungsumrechnung definiert. Sie können den Namen der Berichtswährungsdimensionen nach dem Erstellen ändern. In dem Fall müssen Sie jedoch auch das für die Währungsumrechnung generierte MDX-Skript aktualisieren, um sicherzustellen, dass der richtige Name vom Skriptbefehl beim Verweisen auf die Berichtswährungsdimension verwendet wird.  
  
## <a name="defining-multiple-currency-conversions"></a>Definieren mehrfacher Währungsumrechnungen  
 Mit dem Business Intelligence-Assistenten können Sie so viele Währungsumrechnungen definieren, wie Sie für Ihre Business Intelligence-Projektmappe benötigen. Sie können entweder eine vorhandene Währungsumrechnung überschreiben oder eine neue Währungsumrechnung an das MDX-Skript für einen Cube anfügen. Mehrfache Währungsumrechnungen, die in einem einzelnen Cube definiert sind, sorgen für mehr Flexibilität in Business Intelligence-Anwendungen, die komplexe Berichtsanforderungen stellen, z.& ;B. Finanzberichtsanwendungen, die mehrere separate Umrechnungsanforderungen für internationale Berichte unterstützen.  
  
### <a name="identifying-currency-conversions"></a>Identifizieren von Währungsumrechnungen  
 Der Business Intelligence-Assistent identifiziert jede Währungsumrechnung durch Einbinden der Skriptbefehle für die Währungsumrechnungen in die folgenden Kommentare:  
  
 `//<Currency conversion>`  
  
 `...`  
  
 `[MDX statements for the currency conversion]`  
  
 `...`  
  
 `//</Currency conversion>`  
  
 Wenn Sie diese Kommentare ändern oder entfernen, ist der Business Intelligence-Assistent nicht mehr in der Lage, die Währungsumrechnung zu erkennen. Deshalb sollten Sie diese Kommentare nicht ändern.  
  
 Der Assistent speichert außerdem Metadaten in Kommentaren innerhalb dieser Kommentare, einschließlich dem Erstellungsdatum und der -zeit, dem Benutzer und dem Umrechnungstyp. Diese Kommentare sollten auch nicht geändert werden, weil der Business Intelligence-Assistent diese Metadaten verwendet, wenn vorhandene Währungsumwandlungen angezeigt werden.  
  
 Sie können die Skriptbefehle in einer Währungsumrechnung nach Bedarf ändern. Wenn Sie die Währungsumwandlung jedoch überschreiben, gehen Ihre Änderungen jedoch verloren.  
  
## <a name="see-also"></a>Siehe auch  
 [Globalisierungsszenarien für Analysis Services](../analysis-services/globalization-scenarios-for-analysis-services.md)  
  
  
