---
title: Geben Sie-Element (DimensionAttribute) (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- Type Element (DimensionAttribute)
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- TYPE
helpviewer_keywords:
- Type element
ms.assetid: 64fce1f5-39b7-4d0a-ae60-21203a03bd0d
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 9cd0db2e914ffba09e7e2e3831b5815be8288e10
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="type-element-dimensionattribute-assl"></a>Type-Element (DimensionAttribute) (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Enthält den Typ des Attributs.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<DimensionAttribute>  
      ...  
   <Type>...</Type>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Description|  
|--------------------|-----------------|  
|Datentyp und -länge|Zeichenfolge (Enumeration)|  
|Standardwert|*Reguläre*|  
|Cardinality|0-1: Optionales Element, das nur einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnetes Element|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|  
|Untergeordnete Elemente|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Hinweise  
 Der Wert dieses Elements ist auf eine der in der folgenden Tabelle aufgelisteten Zeichenfolgen beschränkt.  
  
|value|Description|  
|-----------|-----------------|  
|*Konto*|Das Attribut stellt den Namen eines Kontos dar.|  
|*AccountNumber*|Das Attribut stellt die Nummer eines Kontos dar.|  
|*AccountType*|Das Attribut stellt den Typ eines Kontos dar.|  
|*Adresse*|Das Attribut stellt eine Adresse dar.|  
|*AddressBuilding*|Das Attribut stellt einen Gebäudebezeichner für eine Adresse dar.|  
|*AddressCity*|Das Attribut stellt einen Ort für eine Adresse dar.|  
|*AddressCountry*|Das Attribut stellt ein Land oder eine Region für eine Adresse dar.|  
|*AddressFax*|Das Attribut stellt eine Faxnummer dar.|  
|*AddressFloor*|Das Attribut stellt einen Etagenbezeichner für eine Adresse dar.|  
|*AddressHouse*|Das Attribut stellt eine Hausnummer für eine Adresse dar.|  
|*AddressPhone*|Das Attribut stellt eine Rufnummer dar.|  
|*AddressQuarter*|Das Attribut stellt einen Stadtteil für eine Adresse dar.|  
|*AddressRoom*|Das Attribut stellt einen Raumbezeichner für eine Adresse dar.|  
|*AddressStateOrProvince*|Das Attribut stellt ein Bundesland oder einen Kanton für eine Adresse dar.|  
|*AddressStreet*|Das Attribut stellt die Straße für eine Adresse dar.|  
|*AddressZip*|Das Attribut stellt eine Postleitzahl für eine Adresse dar.|  
|*BOMResource*|Das Attribut stellt eine Stücklistenressource dar.|  
|*Beschriftung*|Das Attribut stellt eine Beschriftung dar.|  
|*CaptionAbbreviation*|Das Attribut stellt eine Abkürzung dar.|  
|*CaptionDescription*|Das Attribut stellt eine Beschreibung dar.|  
|*Channel*|Das Attribut stellt einen Kanal dar.|  
|*Ort*|Das Attribut stellt einen Ort dar.|  
|*Unternehmensportal*|Das Attribut stellt eine Firma dar.|  
|*Kontinent*|Das Attribut stellt einen Kontinent dar.|  
|*Land*|Das Attribut stellt ein Land oder eine Region dar.|  
|*Ein Bundesland oder Kanton*|Das Attribut stellt ein Bundesland oder einen Kanton dar.|  
|*CurrencyDestination*|Das Attribut stellt die Zielwährung einer Währungsumrechnung dar.|  
|*CurrencyISOcode*|Das Attribut stellt den ISO-Code einer Währung dar.|  
|*CurrencName*|Das Attribut stellt den Namen einer Währung dar.|  
|*CurrencySource*|Das Attribut stellt die Ausgangswährung einer Währungsumrechnung dar.|  
|*CustomerGroup*|Das Attribut stellt eine Kundengruppe dar.|  
|*CustomerHousehold*|Das Attribut stellt einen Kundenhaushalt dar.|  
|*Kunden*|Das Attribut stellt einen Kunden dar.|  
|*Datum*|Das Attribut stellt ein Datum dar.|  
|*DateCanceled*|Das Attribut stellt ein Abbruchdatum dar.|  
|*DateDuration*|Das Attribut stellt eine Dauer dar.|  
|*DateEnded*|Das Attribut stellt ein Enddatum dar.|  
|*DateModified*|Das Attribut stellt ein Änderungsdatum dar.|  
|*DateStart*|Das Attribut stellt ein Startdatum dar.|  
|*DayOfHalfYears*|Das Attribut stellt die Ordnungszahl für einen Tag eines Halbjahres dar.|  
|*DayOfMonth*|Das Attribut stellt die Ordnungszahl für einen Tag eines Monats dar.|  
|*DayOfQuarter*|Das Attribut stellt die Ordnungszahl für einen Tag eines Quartals dar.|  
|*DayOfTrimester*|Das Attribut stellt die Ordnungszahl für einen Tag eines Trimesters dar.|  
|*DayOfWeek*|Das Attribut stellt die Ordnungszahl für einen Tag einer Woche dar.|  
|*DayOfYear*|Das Attribut stellt die Ordnungszahl für einen Tag eines Jahres dar.|  
|*Tage*|Das Attribut stellt Tage dar.|  
|*DaysOfTenDays*|Das Attribut stellt die Ordnungszahl für einen Tag innerhalb eines Zeitraums von 10 Tagen dar.|  
|*FiscalDay*|Das Attribut stellt Tage in einem Geschäftskalender dar.|  
|*FiscalDayOfHalfYears*|Das Attribut stellt die Ordnungszahl für einen Tag eines Halbjahrs in einem Geschäftskalender dar.|  
|*FiscalDayOfMonth*|Das Attribut stellt die Ordnungszahl für einen Tag eines Monats in einem Geschäftskalender dar.|  
|*FiscalDayOfQuarter*|Das Attribut stellt die Ordnungszahl für einen Tag eines Quartals in einem Geschäftskalender dar.|  
|*FiscalDayOfTrimester*|Das Attribut stellt die Ordnungszahl für einen Tag eines Trimesters in einem Geschäftskalender dar.|  
|*FiscalDayOfWeek*|Das Attribut stellt die Ordnungszahl für einen Tag einer Woche in einem Geschäftskalender dar.|  
|*FiscalDayOfYear*|Das Attribut stellt die Ordnungszahl für einen Tag eines Jahres in einem Geschäftskalender dar.|  
|*FiscalHalfYears*|Das Attribut stellt Halbjahre in einem Geschäftskalender dar.|  
|*FiscalHalfYearsOfYear*|Das Attribut stellt die Ordnungszahl für ein Halbjahr eines Jahres in einem Geschäftskalender dar.|  
|*Geschäftsmonat*|Das Attribut stellt Monate in einem Geschäftskalender dar.|  
|*FiscalMonthOfHalfYears*|Das Attribut stellt die Ordnungszahl für einen Monat eines Halbjahres in einem Geschäftskalender dar.|  
|*FiscalMonthOfQuarter*|Das Attribut stellt die Ordnungszahl für einen Monat eines Quartals in einem Geschäftskalender dar.|  
|*FiscalMonthOfTrimester*|Das Attribut stellt die Ordnungszahl für einen Monat eines Trimesters in einem Geschäftskalender dar.|  
|*FiscalMonthOfYear*|Das Attribut stellt die Ordnungszahl für einen Monat eines Jahres in einem Geschäftskalender dar.|  
|*FiscalQuarter*|Das Attribut stellt Quartale in einem Geschäftskalender dar.|  
|*FiscalQuarterOfHalfYear*|Das Attribut stellt die Ordnungszahl für ein Quartal eines Halbjahres in einem Geschäftskalender dar.|  
|*FiscalQuarterOfYear*|Das Attribut stellt die Ordnungszahl für ein Quartal eines Jahres in einem Geschäftskalender dar.|  
|*FiscalTrimester*|Das Attribut stellt Trimester in einem Geschäftskalender dar.|  
|*FiscalTrimesterOfYear*|Das Attribut stellt die Ordnungszahl für ein Trimester eines Jahres in einem Geschäftskalender dar.|  
|*FiscalWeek*|Das Attribut stellt Wochen in einem Geschäftskalender dar.|  
|*FiscalWeekOfHalfYears*|Das Attribut stellt die Ordnungszahl für eine Woche eines Halbjahres in einem Geschäftskalender dar.|  
|*FiscalWeekOfMonth*|Das Attribut stellt die Ordnungszahl für eine Woche eines Monats in einem Geschäftskalender dar.|  
|*FiscalWeekOfQuarter*|Das Attribut stellt die Ordnungszahl für eine Woche eines Quartals in einem Geschäftskalender dar.|  
|*FiscalWeekOfTrimester*|Das Attribut stellt die Ordnungszahl für eine Woche eines Trimesters in einem Geschäftskalender dar.|  
|*FiscalWeekOfYear*|Das Attribut stellt die Ordnungszahl für eine Woche eines Jahres in einem Geschäftskalender dar.|  
|*FiscalYear*|Das Attribut stellt Jahre in einem Geschäftskalender dar.|  
|*FormattingColor*|Das Attribut stellt die bei der Formatierung verwendete Farbe dar.|  
|*FormattingFont*|Das Attribut stellt die bei der Formatierung verwendete Schriftart dar.|  
|*FormattingFontEffects*|Das Attribut stellt die bei der Formatierung verwendeten Schriftarteffekte dar.|  
|*FormattingFontSize*|Das Attribut stellt den bei der Formatierung verwendeten Schriftgrad dar.|  
|*FormattingOrder*|Das Attribut stellt die bei der Formatierung verwendete Reihenfolge dar.|  
|*FormattingSubtotal*|Das Attribut stellt ein Teilergebnis dar.|  
|*GeoBoundaryBottom*|Das Attribut stellt den untersten Wert einer geographischen Begrenzung dar.|  
|*GeoBoundaryFront*|Das Attribut stellt den vordersten Wert einer geographischen Begrenzung dar|  
|*GeoBoundaryLeft*|Das Attribut stellt den äußeren linken Wert einer geographischen Begrenzung dar.|  
|*GeoBoundaryPolygon*|Das Attribut stellt die Vieleckdefinition einer geographischen Begrenzung dar.|  
|*GeoBoundaryRear*|Das Attribut stellt den hintersten Wert einer geographischen Begrenzung dar.|  
|*GeoBoundaryRight*|Das Attribut stellt den äußeren rechten Wert einer geographischen Begrenzung dar.|  
|*GeoBoundaryTop*|Das Attribut stellt den obersten Wert einer geographischen Begrenzung dar.|  
|*GeoCentroidX*|Das Attribut stellt einen X-Achsenschwerpunkt für einen geographische Bereich dar.|  
|*GeoCentroidY*|Das Attribut stellt einen Y-Achsenschwerpunkt für einen geographischen Bereich dar.|  
|*GeoCentroidZ*|Das Attribut stellt einen Z-Achsenschwerpunkt für einen geographischen Bereich dar.|  
|*HalfYears*|Das Attribut stellt Halbjahre dar.|  
|*HalfYearsOfYear*|Das Attribut stellt die Ordnungszahl für ein Halbjahr eines Jahres dar.|  
|*Stunden*|Das Attribut stellt Stunden dar.|  
|*ID*|Das Attribut stellt einen Bezeichner oder einen Schlüssel dar.|  
|*IsHoliday*|Das Attribut gibt an, ob ein Datum ein Feiertag ist.|  
|*ISO8601DayOfWeek*|Das Attribut stellt die Ordnungszahl für einen Tag einer Woche in einem ISO 8601-Kalender dar.|  
|*ISO8601DayOfYear*|Das Attribut stellt die Ordnungszahl für einen Tag eines Jahres in einem ISO 8601-Kalender dar.|  
|*ISO8601Days*|Das Attribut stellt Tage in einem ISO 8601-Kalender dar.|  
|*ISO8601Week*|Das Attribut stellt Wochen in einem ISO 8601-Kalender dar.|  
|*ISO8601WeekOfYear*|Das Attribut stellt die Ordnungszahl für eine Woche eines Jahres in einem ISO 8601-Kalender dar.|  
|*ISO8601Year*|Das Attribut stellt Jahre in einem ISO 8601-Kalender dar.|  
|*IsWeekDay*|Das Attribut gibt an, ob ein Datum ein Wochentag ist.|  
|*IsWorkingDay*|Das Attribut gibt an, ob ein Datum ein Arbeitstag ist.|  
|*ManufacturingDay*|Das Attribut stellt Tage in einem Produktionskalender dar.|  
|*ManufacturingDayOfHalfYears*|Das Attribut stellt die Ordnungszahl für einen Tag eines Halbjahres in einem Produktionskalender dar.|  
|*ManufacturingDayOfMonth*|Das Attribut stellt die Ordnungszahl für einen Tag eines Monats in einem Produktionskalender dar.|  
|*ManufacturingDayOfQuarter*|Das Attribut stellt die Ordnungszahl für einen Tag eines Quartals in einem Produktionskalender dar.|  
|*ManufacturingDayOfTrimester*|Das Attribut stellt die Ordnungszahl für einen Tag eines Trimesters in einem Produktionskalender dar.|  
|*ManufacturingDayOfWeek*|Das Attribut stellt die Ordnungszahl für einen Tag einer Woche in einem Produktionskalender dar.|  
|*ManufacturingDayOfYear*|Das Attribut stellt die Ordnungszahl für einen Tag eines Jahres in einem Produktionskalender dar.|  
|*ManufacturingHalfYears*|Das Attribut stellt Halbjahre in einem Produktionskalender dar.|  
|*ManufacturingHalfYearsOfYear*|Das Attribut stellt die Ordnungszahl für ein Halbjahr eines Jahres in einem Produktionskalender dar.|  
|*ManufacturingMonth*|Das Attribut stellt Monate in einem Produktionskalender dar.|  
|*ManufacturingMonthOfHalfYears*|Das Attribut stellt die Ordnungszahl für einen Monat eines Halbjahres in einem Produktionskalender dar.|  
|*ManufacturingMonthOfQuarter*|Das Attribut stellt die Ordnungszahl für einen Monat eines Quartals in einem Produktionskalender dar.|  
|*ManufacturingMonthOfTrimester*|Das Attribut stellt die Ordnungszahl für einen Monat eines Trimesters in einem Produktionskalender dar.|  
|*ManufacturingMonthOfYear*|Das Attribut stellt die Ordnungszahl für einen Monat eines Jahres in einem Produktionskalender dar.|  
|*ManufacturingQuarter*|Das Attribut stellt Quartale in einem Produktionskalender dar.|  
|*ManufacturingQuarterOfHalfYear*|Das Attribut stellt die Ordnungszahl für ein Quartal eines Halbjahres in einem Produktionskalender dar.|  
|*ManufacturingQuarterOfYear*|Das Attribut stellt die Ordnungszahl für ein Quartal eines Jahres in einem Produktionskalender dar.|  
|*ManufacturingTrimester*|Das Attribut stellt Trimester in einem Produktionskalender dar.|  
|*ManufacturingTrimesterOfYear*|Das Attribut stellt die Ordnungszahl für ein Trimester eines Jahres in einem Produktionskalender dar.|  
|*ManufacturingWeek*|Das Attribut stellt Wochen in einem Produktionskalender dar.|  
|*ManufacturingWeekOfHalfYears*|Das Attribut stellt die Ordnungszahl für eine Woche eines Halbjahres in einem Produktionskalender dar.|  
|*ManufacturingWeekOfMonth*|Das Attribut stellt die Ordnungszahl für eine Woche eines Monats in einem Produktionskalender dar.|  
|*ManufacturingWeekOfQuarter*|Das Attribut stellt die Ordnungszahl für eine Woche eines Quartals in einem Produktionskalender dar.|  
|*ManufacturingWeekOfTrimester*|Das Attribut stellt die Ordnungszahl für eine Woche eines Trimesters in einem Produktionskalender dar.|  
|*ManufacturingWeekOfYear*|Das Attribut stellt die Ordnungszahl für eine Woche eines Jahres in einem Produktionskalender dar.|  
|*ManufacturingYear*|Das Attribut stellt Jahre in einem Produktionskalender dar.|  
|*Minuten*|Das Attribut stellt Minuten dar.|  
|*MonthOfHalfYears*|Das Attribut stellt die Ordnungszahl für einen Monat eines Halbjahres dar.|  
|*MonthOfQuarter*|Das Attribut stellt die Ordnungszahl für einen Monat eines Quartals dar.|  
|*MonthOfTrimester*|Das Attribut stellt die Ordnungszahl für einen Monat eines Trimesters dar.|  
|*MonthOfYear*|Das Attribut stellt die Ordnungszahl für einen Monat eines Jahres dar.|  
|*Monate*|Das Attribut stellt Monate dar.|  
|*OrganizationalUnit*|Das Attribut stellt eine Organisationseinheit dar.|  
|*OrgTitle*|Das Attribut stellt einen Organisationstitel dar.|  
|*PercentOwnership*|Das Attribut stellt einen Besitzprozentwert dar.|  
|*PercentVoteRight*|Das Attribut stellt einen Prozentwert für Abstimmungsrechte dar.|  
|*Person*|Das Attribut stellt eine Person dar.|  
|*PersonContact*|Das Attribut stellt Kontaktinformationen für eine Person dar.|  
|*PersonDemographic*|Das Attribut stellt demografische Informationen für eine Person dar.|  
|*PersonFirstName*|Das Attribut stellt den Vornamen einer Person dar.|  
|*PersonFullName*|Das Attribut stellt den vollständigen Namen einer Person dar.|  
|*PersonLastName*|Das Attribut stellt den Nachnamen einer Person dar.|  
|*PersonMiddleName*|Das Attribut stellt die weiteren Vornamen einer Person dar.|  
|*PhysicalColor*|Das Attribut stellt eine Farbe dar.|  
|*PhysicalDensity*|Das Attribut stellt die Dichte dar.|  
|*PhysicalDepth*|Das Attribut stellt die Tiefe dar.|  
|*PhysicalHeight*|Das Attribut stellt die Höhe dar.|  
|*PhysicalSize*|Das Attribut stellt eine Größe dar.|  
|*PhysicalVolume*|Das Attribut stellt das Volumen dar.|  
|*PhysicalWeight*|Das Attribut stellt das Gewicht dar.|  
|*PhysicalWidth*|Das Attribut stellt die Breite dar.|  
|*Point*|Das Attribut stellt einen Punkt dar.|  
|*Postleitzahl*|Das Attribut stellt eine Postleitzahl dar.|  
|*Product*|Das Attribut stellt ein Produkt dar.|  
|*ProductBrand*|Das Attribut stellt eine Produktmarke dar.|  
|*"ProductCategory"*|Das Attribut stellt eine Produktkategorie dar.|  
|*ProductGroup*|Das Attribut stellt eine Produktgruppe dar.|  
|*ProductSKU*|Das Attribut stellt eine Produkt-SKU dar.|  
|*ProjectCode*|Das Attribut stellt einen Projektcode dar.|  
|*Projectcompletion*|Das Attribut stellt den Abschlussstatus eines Projekts dar.|  
|*ProjectEnddate*|Das Attribut stellt das Enddatum eines Projekts dar.|  
|*Projektname*|Das Attribut stellt einen Projektnamen dar.|  
|*ProjectStartDate*|Das Attribut stellt das Startdatum eines Projekts dar.|  
|*Promotion*|Das Attribut stellt eine Höherstufung dar.|  
|*QtyRangeHigh*|Das Attribut stellt den größten Wert eines Bereichs von Mengen dar.|  
|*QtyRangeLow*|Das Attribut stellt den niedrigsten Wert eines Bereichs von Mengen dar.|  
|*Quantitative*|Das Attribut stellt ein quantitatives Attribut dar.|  
|*QuarterOfHalfYear*|Das Attribut stellt die Ordnungszahl für ein Quartal eines Halbjahres dar.|  
|*QuarterOfYear*|Das Attribut stellt die Ordnungszahl für ein Quartal eines Jahres dar.|  
|*Quartale*|Das Attribut stellt Quartale dar.|  
|*Rate*|Das Attribut stellt ein Rate dar.|  
|*RateType*|Das Attribut stellt ein Ratentyp dar.|  
|*Region*|Das Attribut stellt eine kundendefinierte Region dar.|  
|*Reguläre*|Das Attribut stellt ein reguläres Attribut dar.|  
|*RelationToParent*|Das Attribut stellt eine Beziehung zu einem übergeordneten Element dar.|  
|*ReportingDay*|Das Attribut stellt Tage in einem Berichtskalender dar.|  
|*ReportingDayOfHalfYears*|Das Attribut stellt die Ordnungszahl für einen Tag eines Halbjahres in einem Berichtskalender dar.|  
|*ReportingDayOfMonth*|Das Attribut stellt die Ordnungszahl für einen Tag eines Monats in einem Berichtskalender dar.|  
|*ReportingDayOfQuarter*|Das Attribut stellt die Ordnungszahl für einen Tag eines Quartals in einem Berichtskalender dar.|  
|*ReportingDayOfTrimester*|Das Attribut stellt die Ordnungszahl für einen Tag eines Trimesters in einem Berichtskalender dar.|  
|*ReportingDayOfWeek*|Das Attribut stellt die Ordnungszahl für einen Tag einer Woche in einem Berichtskalender dar.|  
|*ReportingDayOfYear*|Das Attribut stellt die Ordnungszahl für einen Tag eines Jahres in einem Berichtskalender dar.|  
|*ReportingHalfYears*|Das Attribut stellt Halbjahre in einem Berichtskalender dar.|  
|*ReportingHalfYearsOfYear*|Das Attribut stellt die Ordnungszahl für ein Halbjahr eines Jahres in einem Berichtskalender dar.|  
|*ReportingMonth*|Das Attribut stellt Monate in einem Berichtskalender dar.|  
|*ReportingMonthOfHalfYears*|Das Attribut stellt die Ordnungszahl für einen Monat eines Halbjahres in einem Berichtskalender dar.|  
|*ReportingMonthOfQuarter*|Das Attribut stellt die Ordnungszahl für einen Monat eines Quartals in einem Berichtskalender dar.|  
|*ReportingMonthOfTrimester*|Das Attribut stellt die Ordnungszahl für einen Monat eines Trimesters in einem Berichtskalender dar.|  
|*ReportingMonthOfYear*|Das Attribut stellt die Ordnungszahl für einen Monat eines Jahres in einem Berichtskalender dar.|  
|*ReportingQuarter*|Das Attribut stellt Quartale in einem Berichtskalender dar.|  
|*ReportingQuarterOfHalfYear*|Das Attribut stellt die Ordnungszahl für ein Quartal eines Halbjahres in einem Berichtskalender dar.|  
|*ReportingQuarterOfYear*|Das Attribut stellt die Ordnungszahl für ein Quartal eines Jahres in einem Berichtskalender dar.|  
|*ReportingTrimester*|Das Attribut stellt Trimester in einem Berichtskalender dar.|  
|*ReportingTrimesterOfYear*|Das Attribut stellt die Ordnungszahl für ein Trimester eines Jahres in einem Berichtskalender dar.|  
|*ReportingWeek*|Das Attribut stellt Wochen in einem Berichtskalender dar.|  
|*ReportingWeekOfHalfYears*|Das Attribut stellt die Ordnungszahl für eine Woche eines Halbjahres in einem Berichtskalender dar.|  
|*ReportingWeekOfMonth*|Das Attribut stellt die Ordnungszahl für eine Woche eines Monats in einem Berichtskalender dar.|  
|*ReportingWeekOfQuarter*|Das Attribut stellt die Ordnungszahl für eine Woche eines Quartals in einem Berichtskalender dar.|  
|*ReportingWeekOfTrimester*|Das Attribut stellt die Ordnungszahl für eine Woche eines Trimesters in einem Berichtskalender dar.|  
|*ReportingWeekOfYear*|Das Attribut stellt die Ordnungszahl für eine Woche eines Jahres in einem Berichtskalender dar.|  
|*ReportingYear*|Das Attribut stellt Jahre in einem Berichtskalender dar.|  
|*Vertreter*|Das Attribut stellt einen Vertriebsmitarbeiter dar.|  
|*Szenario*|Das Attribut stellt ein Szenario dar.|  
|*Sekunden*|Das Attribut stellt Sekunden dar.|  
|*Sequenz*|Das Attribut stellt ein sequenzielles Attribut dar.|  
|*ShortCaption*|Das Attribut stellt einen Kurztitel dar.|  
|*StateOrProvince*|Das Attribut stellt ein Bundesland oder einen Kanton dar.|  
|*TenDayOfHalfYears*|Das Attribut stellt die Ordnungszahl für einen zehntägigen Zeitraum eines Halbjahres dar.|  
|*TenDayOfQuarter*|Das Attribut stellt die Ordnungszahl für einen zehntägigen Zeitraum eines Quartals dar.|  
|*TenDayOfTrimester*|Das Attribut stellt die Ordnungszahl für einen zehntägigen Zeitraum eines Trimesters dar.|  
|*TenDayOfYear*|Das Attribut stellt die Ordnungszahl für einen zehntägigen Zeitraum eines Jahres dar.|  
|*TenDays*|Das Attribut stellt einen zehntägigen Zeitraum dar.|  
|*TenDaysOfMonth*|Das Attribut stellt die Ordnungszahl für einen zehntägigen Zeitraum eines Monats dar.|  
|*Im Vergleich zum Vortrimester*|Das Attribut stellt Trimester dar.|  
|*TrimesterOfYear*|Das Attribut stellt die Ordnungszahl für ein Trimester eines Jahres dar.|  
|*UndefinedTime*|Das Attribut stellt einen nicht definierten Zeitraum dar.|  
|*Hilfsprogramm*|Das Attribut stellt ein Hilfsprogramm dar.|  
|*Version*|Das Attribut stellt eine Version dar.|  
|*WebHtml*|Das Attribut stellt HTML-Inhalte dar.|  
|*WebMailAlias*|Das Attribut stellt einen E-Mail-Alias dar.|  
|*WebUrl*|Das Attribut stellt eine URL-Adresse dar.|  
|*WebXmlOrXsl*|Das Attribut stellt XML- oder XSL-Inhalte dar.|  
|*WeekOfHalfYears*|Das Attribut stellt die Ordnungszahl für eine Woche eines Halbjahres dar.|  
|*WeekOfMonth*|Das Attribut stellt die Ordnungszahl für eine Woche eines Monats dar.|  
|*WeekOfQuarter*|Das Attribut stellt die Ordnungszahl für eine Woche eines Quartals dar.|  
|*WeekOfTrimester*|Das Attribut stellt die Ordnungszahl für eine Woche eines Trimesters dar.|  
|*WeekOfYear*|Das Attribut stellt die Ordnungszahl für eine Woche eines Jahres dar.|  
|*Wochen*|Das Attribut stellt Wochen dar.|  
|*Jahre*|Das Attribut stellt Jahre dar.|  
  
 Die Enumeration, die den zulässigen Werten für entspricht **Typ** im Objekt Analysis Management Objects (AMO) Modell ist <xref:Microsoft.AnalysisServices.AttributeType>.  
  
 Das Element, das das übergeordnete Element des entspricht **Typ** im Objekt Analysis Management Objects (AMO) Modell ist <xref:Microsoft.AnalysisServices.DimensionAttribute>.  
  
## <a name="see-also"></a>Siehe auch  
 [Attributes-Element &#40; ASSL &#41;](../../../analysis-services/scripting/collections/attributes-element-assl.md)   
 [Dimension-Element &#40; ASSL &#41;](../../../analysis-services/scripting/objects/dimension-element-assl.md)   
 [Datenbankeigenschaften &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
