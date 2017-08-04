---
title: CREATE KPI-Anweisung (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE KPI
- KPI
- CREATE_KPI
- CREATE
helpviewer_keywords:
- CREATE KPI statement
- key performance indicators [MDX]
ms.assetid: 87618fef-95e5-4dd0-a650-aeb60ccbddcb
caps.latest.revision: 18
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 8796fefabf3dc44ef03f7084e164a559e6c17d18
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="mdx-data-definition---create-kpi"></a>MDX-Datendefinition - KPI erstellen
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Erstellt einen Key Performance Indicator (KPI). Ein KPI ist eine Auflistung von Berechnungen, die einer Measuregruppe in einem Cube zugeordnet sind und zur Auswertung der Geschäfts- oder Szenarioerfolge verwendet werden.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
CREATE KPI CURRENTCUBE | <Cube Name>.KPI_Name AS KPI_Value  
   [,Property_Name = Property_Value, ...n]  
```  
  
## <a name="arguments"></a>Argumente  
 *KPI_Name*  
 Eine gültige Zeichenfolge, die einen KPI-Namen bereitstellt.  
  
 *KPI_Value*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der einen numerischen Wert zurückgibt.  
  
 *Eigenschaftsname*  
 Eine gültige Zeichenfolge, die den Namen einer KPI-Eigenschaft bereitstellt.  
  
 *Property_Value*  
 Ein gültiger Skalarausdruck, der den Wert der KPI-Eigenschaft definiert.  
  
## <a name="remarks"></a>Hinweise  
 Die Angabe eines anderen als des aktuell verbundenen Cubes verursacht einen Fehler. Daher sollten Sie den aktuellen Cube mithilfe von CURRENTCUBE statt mit dem Cubenamen angeben.  
  
## <a name="kpi-properties"></a>KPI-Eigenschaften  
 In der folgenden Tabelle werden alle KPI-Eigenschaften aufgeführt. Keine dieser Eigenschaften weist einen Standardwert auf. Daher geben Abfragen dieser Eigenschaften einen NULL-Wert zurück, bis einer KPI-Eigenschaft ein bestimmter Wert zugeordnet wird.  
  
|Eigenschaftsbezeichner|Bedeutung|  
|-------------------------|-------------|  
|GOAL|Ein gültiger MDX-Ausdruck, der einen numerischen Wert zurückgibt.|  
|STATUS|Ein gültiger MDX-Ausdruck, der einen numerischen Wert zurückgibt.|  
|STATUS_GRAPHIC|Eine Zeichenfolge, die eine Gruppe von Grafiken definiert, die von der Clientanwendung verwendet werden.|  
|TREND|Ein gültiger MDX-Ausdruck, der einen numerischen Wert zurückgibt.|  
|TREND_GRAPHIC|Eine Zeichenfolge, die eine Gruppe von Grafiken definiert, die von der Clientanwendung verwendet werden.|  
|WEIGHT|Ein gültiger MDX-Ausdruck, der einen numerischen Wert zurückgibt.|  
|CURRENT_TIME_MEMBER|Ein gültiger MDX-Ausdruck, der ein Element in der Zeitdimension zurückgibt. CURRENT_TIME_MEMBER legt den Bezugspunkt für alle relativen Zeitfunktionen fest.|  
|PARENT_KPI|Eine Zeichenfolge, die den Namen für den übergeordneten KPI bereitstellt.|  
|CAPTION|Eine Zeichenfolge, die von der Clientanwendung als Beschriftung für den KPI verwendet wird.|  
|DISPLAY_FOLDER|Eine Zeichenfolge, die den Pfad des Anzeigeordners angibt, in dem der KPI von der Clientanwendung angezeigt wird. Das Trennzeichen für Ordnerebenen wird von der Clientanwendung definiert. Zu den Tools und Clients, die vom [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], den umgekehrten Schrägstrich (\\) ebenentrennzeichen ist. Um mehrere Anzeigeordner für ein definiertes Element bereitzustellen, verwenden Sie ein Semikolon (;), um die Ordner zu trennen|  
|ASSOCIATED_MEASURE_GROUP|Eine Zeichenfolge, die den Namen der Measuregruppe angibt, auf die alle MDX-Berechnungen verweisen sollen.|  
  
 Die Werte für die Eigenschaften GOAL, STATUS und TREND sind MDX-Ausdrücke, die zu einem Wert zwischen -1 und 1 ausgewertet werden sollen. Allerdings wird der tatsächliche Wertebereich für die Eigenschaften von der Clientanwendung definiert. Bei Verwendung von Tools und Clients, die vom [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] zum Durchsuchen von KPIs Werte kleiner als-1 wie-1 behandelt werden, und Werte größer als 1 wie 1 behandelt.  
  
 Sowohl STATUS_GRAPHIC als auch TREND_GRAPHIC sind Zeichenfolgenwerte, mit denen die Clientanwendung die korrekte Gruppe der anzuzeigenden Bilder identifiziert. Diese Zeichenfolgen definieren auch das Verhalten der Anzeigefunktion. Dieses Verhalten umfasst die Anzahl von anzuzeigenden Status (normalerweise eine ungerade Anzahl) sowie die für jeden einzelnen Status zu verwendenden Bilder.  
  
### <a name="kpi-graphics-in-sql-server-data-tools"></a>KPI-Grafiken in SQL Server-Datentools  
 In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] können KPI-Grafiken entweder über drei oder fünf Status verfügen. In der folgenden Tabelle werden die Werte für jeden einzelnen Status definiert.  
  
|Anzahl von Status für KPI-Grafik|Wert dieser Status|  
|--------------------------------------|---------------------------|  
|3|Ungültig = -1 bis -0,5<br /><br /> OK =-0,4999 bis 0.4999<br /><br /> Gut = 0,50 bis 1|  
|5|Ungültig = -1 bis -0,75<br /><br /> Risiko = -0,7499 bis -0,25<br /><br /> OK = -0,2499 bis 0,2499<br /><br /> Steigend = 0,25 bis 0,7499<br /><br /> Gut = 0,75 bis 1|  
  
> [!NOTE]  
>  Für einige Grafiken, z. B. der umgekehrte Maßstab oder umgekehrte Statuspfeil, wird der Bereich umgekehrt. Das heißt, -1 ist gut, und 1 ist schlecht.  
  
 In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] wird anhand des Namens der KPI-Grafik bestimmt, ob die Grafik über drei oder fünf Status verfügt. Die folgende Tabelle enthält die Verwendung, Name und die Anzahl der gibt an, dass [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] ordnet den KPI-Grafiken.  
  
|Verwendung der Grafik|Name der KPI-Grafik|Anzahl von Status|  
|--------------------|-------------------------|----------------------|  
|Status|Formen|3|  
|Status|Verkehrsampel|3|  
|Status|Straßenschilder|3|  
|Status|Messgerät|3|  
|Status|Umgekehrter Maßstab|5|  
|Status|Thermometer|3|  
|Status|Zylinder|3|  
|Status|Gesichter|3|  
|Status|Varianzpfeil|3|  
|Trend|Standardpfeil|3|  
|Trend|Statuspfeil|3|  
|Trend|Umgekehrter Statuspfeil|5|  
|Trend|Gesichter|3|  
  
## <a name="see-also"></a>Siehe auch  
 [DROP KPI-Anweisung &#40; MDX &#41;](../mdx/mdx-data-definition-drop-kpi.md)   
 [MDX-Datendefinitionsanweisungen &#40; MDX &#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  

