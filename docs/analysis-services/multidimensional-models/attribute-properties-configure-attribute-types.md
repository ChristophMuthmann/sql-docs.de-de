---
title: Konfigurieren von Attributtypen | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- time dimensions [Analysis Services]
- attributes [Analysis Services], types
- slowly changing dimensions
- account dimensions [Analysis Services]
- currency dimensions [Analysis Services]
- Type property
ms.assetid: c2c6a3da-555e-4362-a83f-88da28427520
caps.latest.revision: 25
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 740d140999a182df59eb9741c5addedd9dac0aac
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="attribute-properties---configure-attribute-types"></a>Attributeigenschaften: Konfigurieren von Attributtypen
  In [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]tragen Attributtypen zur Klassifizierung eines Attributs im Hinblick auf die Geschäftsfunktionalität bei. Es gibt viele Attributtypen. Die meisten werden von Clientanwendungen verwendet, um ein Attribut anzuzeigen oder zu unterstützen. Einige Attributtypen haben jedoch auch eine besondere Bedeutung für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. So identifizieren manche Attributtypen Attribute, die in verschiedenen Kalendern für Zeitdimensionen die Zeiträume darstellen.  
  
##  <a name="setting_attibute_types"></a> Festlegen von Attributtypen  
 Der Wert der **Type** -Eigenschaft für ein Attribut bestimmt den Attributtyp des entsprechenden Attributs. Verschiedene Assistenten in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] legen die Attributtypen fest, wenn Dimensionen oder Attribute definiert werden. Diese [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Assistenten legen auch dann Attributtypen fest, wenn den Dimensionen mit den Assistenten Funktionen hinzugefügt werden. Der Business Intelligence-Assistent wendet auf Attribute in einer Dimension mehrere Attributtypen an, wenn der Assistent Kontointelligenz zur Identifizierung von Attributen hinzufügt, die die Namen, Codes, Nummern und Struktur von Konten in der Dimension enthalten. Der Business Intelligence-Assistent verarbeitet auch Attributtypen, z. B. für die Währungsumrechnung. Weitere Informationen finden Sie unter [Erstellen einer Währungstypdimension](../../analysis-services/multidimensional-models/database-dimensions-create-a-currency-type-dimension.md).  
  
 Die folgenden Tabellen enthalten eine Liste der in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]verfügbaren Attributtypen. Diese Tabellen teilen die Attributtypen in die folgenden Kategorien auf:  
  
|Begriff|Definition|  
|----------|----------------|  
|[Allgemeine Attributtypen](#general_attribute_types)|Diese Werte stehen allen Attributen zur Verfügung und sind nur vorhanden, um eine Klassifizierung der Attribute für Clientanwendungszwecke zu ermöglichen.|  
|[Attributtypen der Kontodimension](#account_dimension_attribute_types)|Diese Werte identifizieren ein Attribut, das einer Kontodimension angehört. Weitere Informationen zur Kontodimension finden Sie unter [Erstellen eines Finanzkontos des über- und untergeordneten Typs Dimension](../../analysis-services/multidimensional-models/database-dimensions-finance-account-of-parent-child-type.md).|  
|[Attributtyp der Währungsdimension](#currency_dimension_attribute_types)|Diese Werte identifizieren ein Attribut, das einer Währungsdimension angehört. Weitere Informationen zu Währungsdimensionen finden Sie unter [Erstellen einer Währungstypdimension](../../analysis-services/multidimensional-models/database-dimensions-create-a-currency-type-dimension.md).|  
|[Langsam veränderliche Dimensionsattribute](#slowly_changing_dimension_attribute_types)|Diese Werte identifizieren ein Attribut, das einer langsam veränderlichen Dimension angehört.|  
|[Attribute der Zeitdimension](#time_dimension_attribute_types)|Diese Werte identifizieren ein Attribut, das einer Zeitdimension angehört. Weitere Informationen zu Zeitdimensionen finden Sie unter [Erstellen einer Datentypdimension](../../analysis-services/multidimensional-models/database-dimensions-create-a-date-type-dimension.md).|  
  
###  <a name="general_attribute_types"></a> General Attribute Types  
  
|Wert des Attributtyps|Description|  
|--------------------------|-----------------|  
|**Adresse**|Stellt eine Adresse dar.|  
|**AddressBuilding**|Stellt einen Gebäudebezeichner für eine Adresse dar.|  
|**AddressCity**|Stellt eine Stadt für eine Adresse dar.|  
|**AddressCountry**|Stellt ein Land oder eine Region für eine Adresse dar.|  
|**AddressFax**|Stellt eine Faxnummer dar.|  
|**AddressFloor**|Stellt einen Etagenbezeichner für eine Adresse dar.|  
|**AddressHouse**|Stellt eine Hausnummer für eine Adresse dar.|  
|**AddressPhone**|Stellt eine Telefonnummer dar.|  
|**AddressQuarter**|Stellt einen Stadtteil für eine Adresse dar.|  
|**AddressRoom**|Stellt einen Raumbezeichner für eine Adresse dar.|  
|**AddressStateOrProvince**|Stellt ein Bundesland oder einen Kanton für eine Adresse dar.|  
|**AddressStreet**|Stellt die Straße für eine Adresse dar.|  
|**AddressZip**|Stellt eine Postleitzahl für eine Adresse dar.|  
|**BomResource**|Stellt eine Stücklistenressource dar.|  
|**Beschriftung**|Stellt eine Beschriftung dar.|  
|**CaptionAbbreviation**|Stellt eine Abkürzung dar.|  
|**CaptionDescription**|Stellt eine Beschreibung dar.|  
|**Channel**|Stellt einen Kanal dar.|  
|**City**|Stellt eine Stadt dar.|  
|**Company**|Stellt ein Unternehmen dar.|  
|**Continent**|Stellt einen Kontinent dar.|  
|**Country**|Stellt ein Land oder eine Region dar.|  
|**County**|Stellt einen Landkreis dar.|  
|**CustomerGroup**|Stellt eine Kundengruppe dar.|  
|**CustomerHousehold**|Stellt einen Kundenhaushalt dar.|  
|**Customers**|Stellt einen Kunden dar.|  
|**DateCanceled**|Stellt ein Abbruchdatum dar.|  
|**DateDuration**|Stellt eine Dauer dar.|  
|**DateEnded**|Stellt ein Enddatum dar.|  
|**DateModified**|Stellt ein Änderungsdatum dar.|  
|**DateStart**|Stellt ein Startdatum dar.|  
|**DeletedFlag**|Gibt an, ob ein Mitglied gelöscht wurde oder gelöscht werden sollte (im Hinblick auf die Geschäftsfunktionalität).<br /><br /> Hinweis: In [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] wird dieser Attributtyp nicht verwendet, um zu ermitteln, ob ein Mitglied gelöscht werden sollte. Stattdessen soll dieser Attributtyp von Clientanwendungen nur zu Anzeigezwecken verwendet werden.|  
|**FormattingColor**|Stellt die bei der Formatierung verwendete Farbe dar.|  
|**FormattingFont**|Stellt die bei der Formatierung verwendete Schriftart dar.|  
|**FormattingFontEffects**|Stellt die bei der Formatierung verwendeten Schriftarteffekte dar.|  
|**FormattingFontSize**|Stellt den bei der Formatierung verwendeten Schriftgrad dar.|  
|**FormattingOrder**|Stellt die bei der Formatierung verwendete Reihenfolge dar.|  
|**FormattingSubtotal**|Stellt ein Teilergebnis dar.|  
|**GeoBoundaryBottom**|Stellt den untersten Wert einer geographischen Begrenzung dar.|  
|**GeoBoundaryFront**|Stellt den vordersten Wert einer geographischen Begrenzung dar.|  
|**GeoBoundaryLeft**|Stellt den äußeren linken Wert einer geographischen Begrenzung dar.|  
|**GeoBoundaryPolygon**|Stellt die Vieleckdefinition einer geographischen Begrenzung dar.|  
|**GeoBoundaryRear**|Stellt den hintersten Wert einer geographischen Begrenzung dar.|  
|**GeoBoundaryRight**|Stellt den äußeren rechten Wert einer geographischen Begrenzung dar.|  
|**GeoBoundaryTop**|Stellt den obersten Wert einer geographischen Begrenzung dar.|  
|**GeoCentroidX**|Stellt einen X-Achsenschwerpunkt für einen geographischen Bereich dar.|  
|**GeoCentroidY**|Stellt einen Y-Achsenschwerpunkt für einen geographischen Bereich dar.|  
|**GeoCentroidZ**|Stellt einen Z-Achsenschwerpunkt für einen geographischen Bereich dar.|  
|**ID**|Stellt einen Bezeichner oder einen Schlüssel dar.|  
|**Bild**|Stellt ein Bild in einem nicht definierten Grafikformat dar.|  
|**ImageBmp**|Stellt ein Bild im Bitmap-Grafikformat dar.|  
|**ImageGif**|Stellt ein Bild im GIF-Grafikformat dar.|  
|**ImageJpg**|Stellt ein Bild im JPEG-Grafikformat dar.|  
|**ImagePng**|Stellt ein Bild im PNG-Grafikformat dar.|  
|**ImageTiff**|Stellt ein Bild im TIFF-Grafikformat dar.|  
|**OrganizationalUnit**|Stellt eine Organisationseinheit dar.|  
|**OrgTitle**|Stellt einen Organisationstitel dar.|  
|**PercentOwnership**|Stellt einen Besitzprozentwert dar.|  
|**PercentVoteRight**|Stellt einen Prozentwert für Abstimmungsrechte dar.|  
|**Person**|Stellt eine Person dar.|  
|**PersonContact**|Stellt Kontaktinformationen für eine Person dar.|  
|**PersonDemographic**|Stellt demographische Informationen für eine Person dar.|  
|**PersonFirstName**|Stellt den Vornamen einer Person dar.|  
|**PersonFullName**|Stellt den vollständigen Namen einer Person dar.|  
|**PersonLastName**|Stellt den Nachnamen einer Person dar.|  
|**PersonMiddleName**|Stellt die weiteren Vornamen einer Person dar.|  
|**PhysicalColor**|Stellt eine Farbe dar.|  
|**PhysicalDensity**|Stellt die Dichte dar.|  
|**PhysicalDepth**|Stellt die Tiefe dar.|  
|**PhysicalHeight**|Stellt die Höhe dar.|  
|**PhysicalSize**|Stellt eine Größe dar.|  
|**PhysicalVolume**|Stellt das Volumen dar.|  
|**PhysicalWeight**|Stellt die Gewichtung dar.|  
|**PhysicalWidth**|Stellt die Breite dar.|  
|**Punkt**|Stellt einen Punkt dar.|  
|**PostalCode**|Stellt eine Postleitzahl dar.|  
|**Product**|Stellt ein Produkt dar.|  
|**ProductBrand**|Stellt eine Produktmarke dar.|  
|**ProductCategory**|Stellt eine Produktkategorie dar.|  
|**ProductGroup**|Stellt eine Produktgruppe dar.|  
|**ProductSKU**|Stellt eine Produkt-SKU dar.|  
|**Projekt**|Stellt ein Projekt dar.|  
|**ProjectCode**|Stellt einen Projektcode dar.|  
|**ProjectCompletion**|Stellt den Abschlussstatus eines Projekts dar.|  
|**ProjectEndDate**|Stellt das Enddatum eines Projekts dar.|  
|**ProjectName**|Stellt einen Projektnamen dar.|  
|**ProjectStartDate**|Stellt das Startdatum eines Projekts dar.|  
|**Promotion**|Stellt eine Höherstufung dar.|  
|**QtyRangeHigh**|Stellt den größten Wert eines Bereichs von Mengen dar.|  
|**QtyRangeLow**|Stellt den niedrigsten Wert eines Bereichs von Mengen dar.|  
|**Quantitative**|Stellt ein quantitatives Attribut dar.|  
|**ZINS**|Stellt eine Rate dar.|  
|**RateType**|Stellt einen Ratentyp dar.|  
|**Region**|Stellt eine kundendefinierte Region dar.|  
|**Regulär**|Stellt ein reguläres Attribut dar.|  
|**RelationToParent**|Stellt eine Beziehung zu einem übergeordneten Element dar.|  
|**Representative**|Stellt einen Vertriebsmitarbeiter dar.|  
|**Szenario**|Stellt ein Szenario dar.|  
|**Sequenz**|Stellt ein sequenzielles Attribut dar.|  
|**ShortCaption**|Stellt einen Kurztitel dar.|  
|**StateOrProvince**|Stellt ein Bundesland oder einen Kanton dar.|  
|**Hilfsprogramm**|Stellt ein Hilfsprogramm dar.|  
|**Version**|Stellt eine Version dar.|  
|**WebHtml**|Stellt HTML-Inhalte dar.|  
|**WebMailAlias**|Stellt einen E-Mail-Alias dar.|  
|**WebUrl**|Stellt eine URL-Adresse dar.|  
|**WebXmlOrXsl**|Stellt XML- oder XSL-Inhalte dar.|  
  
###  <a name="account_dimension_attribute_types"></a> Account Dimension Attribute Types  
  
|Wert des Attributtyps|Description|  
|--------------------------|-----------------|  
|**Konto**|Stellt das übergeordnete Element eines Kontos dar. Dieser Attributtyp wird in der Regel auf das übergeordnete Attribut einer Kontodimension angewendet.|  
|**AccountName**|Stellt den Namen eines Kontos dar. Dieser Attributtyp wird in der Regel auf die Schlüsselattribute einer Kontodimension angewendet.|  
|**AccountNumber**|Stellt die Nummer eines Kontos dar.|  
|**AccountType**|Stellt den Typ eines Kontos dar. Dieser Attributtyp identifiziert die Aggregationsfunktion eines Kontomitglieds in einer Kontotypdimension der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank.|  
  
###  <a name="currency_dimension_attribute_types"></a> Attributtypen der Währungsdimension  
  
|Wert des Attributtyps|Description|  
|--------------------------|-----------------|  
|**CurrencyDestination**|Stellt die Zielwährung einer Währungsumrechnung dar. Dieser Attributtyp wird in der Regel auf das Schlüsselattribut einer Berichtsdimension zum Verwenden bei der Währungsumrechnung angewendet. Weitere Informationen zu Währungsumrechnungen finden Sie unter [Währungsumrechnungen &#40;Analysis Services&#41;](../../analysis-services/currency-conversions-analysis-services.md).|  
|**CurrencyIsoCode**|Stellt den ISO-Code einer Währung dar. Weitere Informationen zu Währungsumrechnungen finden Sie unter [Währungsumrechnungen &#40;Analysis Services&#41;](../../analysis-services/currency-conversions-analysis-services.md).|  
|**CurrencyName**|Stellt den Namen einer Währung dar. Weitere Informationen zu Währungsumrechnungen finden Sie unter [Währungsumrechnungen &#40;Analysis Services&#41;](../../analysis-services/currency-conversions-analysis-services.md).|  
|**CurrencySource**|Stellt die Ausgangswährung einer Währungsumrechnung dar. Dieser Attributtyp wird in der Regel auf das Schlüsselattribut einer Währungsdimension zum Verwenden bei der Währungsumrechnung verwendet. Weitere Informationen zu Währungsumrechnungen finden Sie unter [Währungsumrechnungen &#40;Analysis Services&#41;](../../analysis-services/currency-conversions-analysis-services.md).|  
  
###  <a name="slowly_changing_dimension_attribute_types"></a> Attributtypen für langsam veränderliche Dimension  
  
|Wert des Attributtyps|Description|  
|--------------------------|-----------------|  
|**SCDEndDate**|Stellt das effektive Enddatum für ein Element einer langsam veränderlichen Dimension dar.|  
|**SCDOriginalID**|Stellt den ursprünglichen Bezeichner für ein Element einer langsam veränderlichen Dimension dar.|  
|**SCDStartDate**|Stellt das effektive Startdatum für ein Element einer langsam veränderlichen Dimension dar.|  
|**SCDStatus**|Stellt den effektiven Status für ein Element einer langsam veränderlichen Dimension dar.|  
  
###  <a name="time_dimension_attribute_types"></a> Attributtypen der Zeitdimension  
  
|Wert des Attributtyps|Description|  
|--------------------------|-----------------|  
|**Datum**|Stellt ein Datum dar. Dieser Attributtyp wird in der Regel auf das Schlüsselattribut einer Zeitdimension oder einer Serverzeitdimension angewendet.|  
|**DayOfHalfYear**|Stellt die Ordnungszahl für einen Tag eines Halbjahres dar.|  
|**DayOfMonth**|Stellt die Ordnungszahl für einen Tag eines Monats dar.|  
|**DayOfQuarter**|Stellt die Ordnungszahl für einen Tag eines Quartals dar.|  
|**DayOfTenDays**|Stellt die Ordnungszahl für einen Tag innerhalb eines Zeitraums von 10 Tagen dar.|  
|**DayOfTrimester**|Stellt die Ordnungszahl für einen Tag eines Trimesters dar.|  
|**DayOfWeek (TagderWoche)**|Stellt die Ordnungszahl für einen Tag einer Woche dar.|  
|**Dayofyear**|Stellt die Ordnungszahl für einen Tag eines Jahres dar.|  
|**Tage**|Stellt Tage dar.|  
|**FiscalDate**|Stellt ein Datum in einem Geschäftskalender dar.|  
|**FiscalDayOfHalfYear**|Stellt die Ordnungszahl für einen Tag eines Halbjahres in einem Geschäftskalender dar.|  
|**FiscalDayOfMonth**|Stellt die Ordnungszahl für einen Tag eines Monats in einem Geschäftskalender dar.|  
|**FiscalDayOfQuarter**|Stellt die Ordnungszahl für einen Tag eines Quartals in einem Geschäftskalender dar.|  
|**FiscalDayOfTrimester**|Stellt die Ordnungszahl für einen Tag eines Trimesters in einem Geschäftskalender dar.|  
|**FiscalDayOfWeek**|Stellt die Ordnungszahl für einen Tag einer Woche in einem Geschäftskalender dar.|  
|**FiscalDayOfYear**|Stellt die Ordnungszahl für einen Tag eines Jahres in einem Geschäftskalender dar.|  
|**FiscalHalfYears**|Stellt Halbjahre in einem Geschäftskalender dar.|  
|**FiscalHalfYearOfYear**|Stellt die Ordnungszahl für ein Halbjahr eines Jahres in einem Geschäftskalender dar.|  
|**FiscalMonths**|Stellt Monate in einem Geschäftskalender dar.|  
|**FiscalMonthOfHalfYear**|Stellt die Ordnungszahl für einen Monat eines Halbjahres in einem Geschäftskalender dar.|  
|**FiscalMonthOfQuarter**|Stellt die Ordnungszahl für einen Monat eines Quartals in einem Geschäftskalender dar.|  
|**FiscalMonthOfTrimester**|Stellt die Ordnungszahl für einen Monat eines Trimesters in einem Geschäftskalender dar.|  
|**FiscalMonthOfYear**|Stellt die Ordnungszahl für einen Monat eines Jahres in einem Geschäftskalender dar.|  
|**FiscalQuarters**|Stellt Quartale in einem Geschäftskalender dar.|  
|**FiscalQuarterOfHalfYear**|Stellt die Ordnungszahl für ein Quartal eines Halbjahres in einem Geschäftskalender dar.|  
|**FiscalQuarterOfYear**|Stellt die Ordnungszahl für ein Quartal eines Jahres in einem Geschäftskalender dar.|  
|**FiscalTrimesters**|Stellt Trimester in einem Geschäftskalender dar.|  
|**FiscalTrimesterOfYear**|Stellt die Ordnungszahl für ein Trimester eines Jahres in einem Geschäftskalender dar.|  
|**FiscalWeeks**|Stellt Wochen in einem Geschäftskalender dar.|  
|**FiscalWeekOfHalfYear**|Stellt die Ordnungszahl für eine Woche eines Halbjahres in einem Geschäftskalender dar.|  
|**FiscalWeekOfMonth**|Stellt die Ordnungszahl für eine Woche eines Monats in einem Geschäftskalender dar.|  
|**FiscalWeekOfQuarter**|Stellt die Ordnungszahl für eine Woche eines Quartals in einem Geschäftskalender dar.|  
|**FiscalWeekOfTrimester**|Stellt die Ordnungszahl für eine Woche eines Trimesters in einem Geschäftskalender dar.|  
|**FiscalWeekOfYear**|Stellt die Ordnungszahl für eine Woche eines Jahres in einem Geschäftskalender dar.|  
|**FiscalYears**|Stellt Jahre in einem Geschäftskalender dar.|  
|**HalfYears**|Stellt Halbjahre dar.|  
|**HalfYearOfYear**|Stellt die Ordnungszahl für ein Halbjahr eines Jahres dar.|  
|**Stunden**|Stellt Stunden dar.|  
|**IsHoliday**|Gibt an, ob ein Datum ein Feiertag ist.|  
|**ISO8601Date**|Stellt ein Datum in einem ISO 8601-Kalender dar.|  
|**ISO8601DayOfWeek**|Stellt die Ordnungszahl für einen Tag in einem ISO 8601-Kalender dar.|  
|**ISO8601DayOfYear**|Stellt die Ordnungszahl für einen Tag eines Jahres in einem ISO 8601-Kalender dar.|  
|**ISO8601Weeks**|Stellt Wochen in einem ISO 8601-Kalender dar.|  
|**ISO8601WeekOfYear**|Stellt die Ordnungszahl für eine Woche eines Jahres in einem ISO 8601-Kalender dar.|  
|**ISO8601Years**|Stellt Jahre in einem ISO 8601-Kalender dar.|  
|**IsPeakDay**|Gibt an, ob ein Datum ein Spitzentag ist.|  
|**IsWeekDay**|Gibt an, ob ein Datum ein Arbeitstag ist.|  
|**IsWorkingDay**|Gibt an, ob ein Datum ein Arbeitstag ist.|  
|**ManufacturingDate**|Stellt ein Datum in einem Produktionskalender dar.|  
|**ManufacturingDayOfHalfYear**|Stellt die Ordnungszahl für einen Tag eines Halbjahres in einem Produktionskalender dar.|  
|**ManufacturingDayOfMonth**|Stellt die Ordnungszahl für einen Tag eines Monats in einem Produktionskalender dar.|  
|**ManufacturingDayOfQuarter**|Stellt die Ordnungszahl für einen Tag eines Quartals in einem Produktionskalender dar.|  
|**ManufacturingDayOfTrimester**|Stellt die Ordnungszahl für einen Tag eines Trimesters in einem Produktionskalender dar.|  
|**ManufacturingDayOfWeek**|Stellt die Ordnungszahl für einen Tag einer Woche in einem Produktionskalender dar.|  
|**ManufacturingDayOfYear**|Stellt die Ordnungszahl für einen Tag eines Jahres in einem Produktionskalender dar.|  
|**ManufacturingHalfYears**|Stellt Halbjahre in einem Produktionskalender dar.|  
|**ManufacturingHalfYearOfYear**|Stellt die Ordnungszahl für ein Halbjahr eines Jahres in einem Produktionskalender dar.|  
|**ManufacturingMonths**|Stellt Monate in einem Produktionskalender dar.|  
|**ManufacturingMonthOfHalfYear**|Stellt die Ordnungszahl für einen Monat eines Halbjahres in einem Produktionskalender dar.|  
|**ManufacturingMonthOfQuarter**|Stellt die Ordnungszahl für einen Monat eines Quartals in einem Produktionskalender dar.|  
|**ManufacturingMonthOfTrimester**|Stellt die Ordnungszahl für einen Monat eines Trimesters in einem Produktionskalender dar.|  
|**ManufacturingMonthOfYear**|Stellt die Ordnungszahl für einen Monat eines Jahres in einem Produktionskalender dar.|  
|**ManufacturingQuarters**|Stellt Quartale in einem Produktionskalender dar.|  
|**ManufacturingQuarterOfHalfYear**|Stellt die Ordnungszahl für ein Quartal eines Halbjahres in einem Produktionskalender dar.|  
|**ManufacturingQuarterOfYear**|Stellt die Ordnungszahl für ein Quartal eines Jahres in einem Produktionskalender dar.|  
|**ManufacturingWeeks**|Stellt Wochen in einem Produktionskalender dar.|  
|**ManufacturingWeekOfHalfYear**|Stellt die Ordnungszahl für eine Woche eines Halbjahres in einem Produktionskalender dar.|  
|**ManufacturingWeekOfMonth**|Stellt die Ordnungszahl für eine Woche eines Monats in einem Produktionskalender dar.|  
|**ManufacturingWeekOfQuarter**|Stellt die Ordnungszahl für eine Woche eines Quartals in einem Produktionskalender dar.|  
|**ManufacturingWeekOfTrimester**|Stellt die Ordnungszahl für eine Woche eines Trimesters in einem Produktionskalender dar.|  
|**ManufacturingWeekOfYear**|Stellt die Ordnungszahl für eine Woche eines Jahres in einem Produktionskalender dar.|  
|**ManufacturingYears**|Stellt Jahre in einem Produktionskalender dar.|  
|**Minuten**|Stellt Minuten dar.|  
|**Months**|Stellt Monate dar.|  
|**MonthOfHalfYear**|Represents the month ordinal of a half-year.|  
|**MonthOfQuarter**|Stellt die Ordnungszahl für einen Monat eines Quartals dar.|  
|**MonthOfTrimester**|Stellt die Ordnungszahl für einen Monat eines Trimesters dar.|  
|**MonthOfYear**|Stellt die Ordnungszahl für einen Monat eines Jahres dar.|  
|**Quarters**|Stellt Quartale dar.|  
|**QuarterOfHalfYear**|Stellt die Ordnungszahl für ein Quartal eines Halbjahres dar.|  
|**QuarterOfYear**|Stellt die Ordnungszahl für ein Quartal eines Jahres dar.|  
|**ReportingDate**|Stellt ein Datum in einem Berichtskalender dar.|  
|**ReportingDayOfHalfYear**|Stellt die Ordnungszahl für einen Tag eines Halbjahres in einem Berichtskalender dar.|  
|**ReportingDayOfMonth**|Stellt die Ordnungszahl für einen Tag eines Monats in einem Berichtskalender dar.|  
|**ReportingDayOfQuarter**|Stellt die Ordnungszahl für einen Tag eines Quartals in einem Berichtskalender dar.|  
|**ReportingDayOfTrimester**|Stellt die Ordnungszahl für einen Tag eines Trimesters in einem Berichtskalender dar.|  
|**ReportingDayOfWeek**|Stellt die Ordnungszahl für einen Tag einer Woche in einem Geschäftskalender dar.|  
|**ReportingDayOfYear**|Stellt die Ordnungszahl für einen Tag eines Jahres in einem Berichtskalender dar.|  
|**ReportingHalfYears**|Stellt Halbjahre in einem Berichtskalender dar.|  
|**ReportingHalfYearOfYear**|Stellt die Ordnungszahl für ein Halbjahr eines Jahres in einem Berichtskalender dar.|  
|**ReportingMonths**|Stellt Monate in einem Berichtskalender dar.|  
|**ReportingMonthOfHalfYear**|Stellt die Ordnungszahl für einen Monat eines Halbjahres in einem Berichtskalender dar.|  
|**ReportingMonthOfQuarter**|Stellt die Ordnungszahl für einen Monat eines Quartals in einem Berichtskalender dar.|  
|**ReportingMonthOfTrimester**|Stellt die Ordnungszahl für einen Monat eines Trimesters in einem Berichtskalender dar.|  
|**ReportingMonthOfYear**|Stellt die Ordnungszahl für einen Monat eines Jahres in einem Berichtskalender dar.|  
|**ReportingQuarters**|Stellt Quartale in einem Berichtskalender dar.|  
|**ReportingQuarterOfHalfYear**|Stellt die Ordnungszahl für ein Quartal eines Halbjahres in einem Berichtskalender dar.|  
|**ReportingQuarterOfYear**|Stellt die Ordnungszahl für ein Quartal eines Jahres in einem Berichtskalender dar.|  
|**ReportingTrimesters**|Stellt Trimester in einem Berichtskalender dar.|  
|**ReportingTrimesterOfYear**|Stellt die Ordnungszahl für ein Trimester eines Jahres in einem Berichtskalender dar.|  
|**ReportingWeeks**|Stellt Wochen in einem Berichtskalender dar.|  
|**ReportingWeekOfHalfYear**|Stellt die Ordnungszahl für eine Woche eines Halbjahres in einem Berichtskalender dar.|  
|**ReportingWeekOfMonth**|Stellt die Ordnungszahl für eine Woche eines Monats in einem Berichtskalender dar.|  
|**ReportingWeekOfQuarter**|Stellt die Ordnungszahl für eine Woche eines Quartals in einem Berichtskalender dar.|  
|**ReportingWeekOfTrimester**|Stellt die Ordnungszahl für eine Woche eines Trimesters in einem Berichtskalender dar.|  
|**ReportingWeekOfYear**|Stellt die Ordnungszahl für eine Woche eines Jahres in einem Berichtskalender dar.|  
|**ReportingYears**|Stellt Jahre in einem Berichtskalender dar.|  
|**Sekunden**|Stellt Sekunden dar.|  
|**TenDayOfHalfYear**|Stellt die Ordnungszahl für einen zehntägigen Zeitraum eines Halbjahres dar.|  
|**TenDayOfMonth**|Stellt die Ordnungszahl für einen zehntägigen Zeitraum eines Monats dar.|  
|**TenDayOfQuarter**|Stellt die Ordnungszahl für einen zehntägigen Zeitraum eines Quartals dar.|  
|**TenDayOfTrimester**|Stellt die Ordnungszahl für einen zehntägigen Zeitraum eines Trimesters dar.|  
|**TenDayOfYear**|Stellt die Ordnungszahl für einen zehntägigen Zeitraum eines Jahres dar.|  
|**TenDays**|Stellt zehntägige Zeiträume dar.|  
|**Trimesters**|Stellt Trimester dar.|  
|**TrimesterOfYear**|Stellt die Ordnungszahl für ein Trimester eines Jahres dar.|  
|**UndefinedTime**|Stellt einen nicht definierten Zeitraum dar.|  
|**WeekOfYear**|Stellt die Ordnungszahl für eine Woche eines Jahres dar.|  
|**Weeks**|Stellt Wochen dar.|  
|**WinterSummerSeason**|Gibt an, ob das Datum Teil der Winter-/Sommersaison ist.|  
|**Years**|Stellt Jahre dar.|  
  
## <a name="see-also"></a>Siehe auch  
 [Attribute und Attributhierarchien](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)   
 [Dimensionsattributeigenschaftenverweis](../../analysis-services/multidimensional-models/dimension-attribute-properties-reference.md)  
  
  

