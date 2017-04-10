---
title: "Lektion 3: Umbenennen von Spalten | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: 5fc8ba1a-2b30-4775-9b3b-c09dee711b3e
caps.latest.revision: 22
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
robots: noindex,nofollow
---
# Lektion 3: Umbenennen von Spalten
In dieser Lektion benennen Sie viele der Spalten in jeder importierten Tabelle um. Durch das Umbenennen von Spalten sind diese leichter identifizierbar und navigierbar sowohl im Modell-Designer als auch in einer Clientanwendung bei der Auswahl von Feldern durch Benutzer. Weitere Informationen finden Sie unter [Umbenennen einer Tabelle oder Spalte &#40;SSAS – tabellarisch&#41;](../analysis-services/tabular-models/rename-a-table-or-column-ssas-tabular.md).  
  
> [!IMPORTANT]  
> Das Umbenennen von Spalten ist zum Abschluss dieses Lernprogramms nicht notwendig. Übrige Lektionen, insbesondere diejenigen über die Erstellung von Beziehungen und berechneten Spalten und Measures mit DAX-Formeln, verweisen auf die in dieser Lektion beschriebenen Spaltenanzeigenamen. Wenn Sie Spalten umbenennen möchten, sind die DAX-Formeln in den Lektionen 5, 6 und 7 zu bearbeiten, um die ursprünglichen in dieser Lektion bereitgestellten Namen der Quellspalten zu verwenden.  
  
Geschätzte Zeit zum Bearbeiten dieser Lektion: **20 Minuten**  
  
## Erforderliche Komponenten  
Dieses Thema ist Teil eines Lernprogramms zur Tabellenmodellierung, das in der entsprechenden Reihenfolge bearbeitet werden sollte. Sie sollten vor dem Ausführen der Tasks in dieser Lektion die vorherige Lektion abgeschlossen haben: [Lektion 2: Hinzufügen von Daten](../analysis-services/lesson-2-add-data.md).  
  
## Umbenennen von Spalten  
  
#### So benennen Sie Spalten um  
  
1.  Klicken Sie im Modell-Designer auf die Tabelle (Registerkarte) **Customer**.  
  
    Wenn Sie auf eine Registerkarte klicken, wird diese Tabelle im Modell-Designer-Fenster aktiv.  
  
2.  Doppelklicken Sie auf den Spaltennamen **CustomerKey**, geben Sie **Customer Id** ein, und drücken Sie die EINGABETASTE.  
  
    > [!TIP]  
    > Sie können auch in der Eigenschaft **Spaltenname** im Fenster **Eigenschaften** oder in der Diagrammsicht eine Spalte umbenennen.  
  
3.  Benennen Sie die verbleibenden Spalten in der Tabelle **Customer** sowie die Spalten in den verbleibenden Tabellen um. Ersetzen Sie dabei den Quellnamen durch den entsprechenden Anzeigenamen:  
  
    **Customer-Tabelle**  
  
    |Quellname|Anzeigename|  
    |---------------|-----------------|  
    |GeographyKey|Geography Id|  
    |CustomerAlternateKey|Customer Alternate ID|  
    |FirstName|First Name|  
    |MiddleName|Middle Name|  
    |LastName|Last Name|  
    |NameStyle|Name Style|  
    |BirthDate|Birth Date|  
    |MaritalStatus|Marital Status|  
    |EmailAddress|Email Address|  
    |YearlyIncome|Yearly Income|  
    |TotalChildren|Total Children|  
    |NumberChildrenAtHome|Number of Children At Home|  
    |EnglishEducation|Education|  
    |EnglishOccupation|Occupation|  
    |HouseOwnerFlag|Owns House|  
    |NumberCarsOwned|Number of Cars Owned|  
    |AddressLine1|Adresszeile 1|  
    |AddressLine2|Address Line 2|  
    |Phone|Phone Number|  
    |DateFirstPurchase|Date of First Purchase|  
    |CommuteDistance|Commute Distance|  
  
    **Datum**  
  
    |Quellname|Anzeigename|  
    |---------------|-----------------|  
    |FullDateAlternateKey|Datum|  
    |DayNumberOfWeek|Day Number of Week|  
    |EnglishDayNameOfWeek|Day Name|  
    |DayNumberOfMonth|Day of Month|  
    |DayNumberOfYear|Day of Year|  
    |WeekNumberOfYear|Week Number of Year|  
    |EnglishMonthName|Month Name|  
    |MonthNumberOfYear|Month|  
    |CalendarQuarter|Calendar Quarter|  
    |CalendarYear|Calendar Year|  
    |CalendarSemester|Calendar Semester|  
    |FiscalQuarter|Fiscal Quarter|  
    |FiscalYear|Fiscal Year|  
    |FiscalSemester|Fiscal Semester|  
  
    **Geography**  
  
    |Quellname|Anzeigename|  
    |---------------|-----------------|  
    |GeographyKey|Geography Id|  
    |Bundesland/Kanton/PLZ|State Province Code|  
    |StateProvinceName|State Province Name|  
    |CountryRegionCode|Country Region Code|  
    |EnglishCountryRegionName|Country Region Name|  
    |PostalCode|Postal Code|  
    |SalesTerritoryKey|Sales Territory Id|  
  
    **Product**  
  
    |Quellname|Anzeigename|  
    |---------------|-----------------|  
    |ProductKey|Product Id|  
    |ProductAlternateKey|Product Alternate Id|  
    |ProductSubcategoryKey|Product Subcategory Id|  
    |WeightUnitMeasureCode|Weight Unit Code|  
    |SizeUnitMeasureCode|Size Unit Code|  
    |EnglishProductName|Produktname|  
    |StandardCost|Standard Cost|  
    |FinishedGoodsFlag|Is Finished Product|  
    |SafetyStockLevel|Safety Stock Level|  
    |ReorderPoint|Reorder Point|  
    |ListPrice|List Price|  
    |SizeRange|Size Range|  
    |DaysToManufacture|Days to Manufacture|  
    |ProductLine|Product Line|  
    |Dealer Price|Dealer Price|  
    |ModelName|Model Name|  
    |LargePhoto|Large Photo|  
    |EnglishDescription|Description|  
    |StartDate|Product Start Date|  
    |EndDate|Product End Date|  
    |Status|Product Status|  
  
    **Product Category**  
  
    |Quellname|Anzeigename|  
    |---------------|-----------------|  
    |ProductCategoryKey|Product Category Id|  
    |ProductCategoryAlternateKey|Product Category Alternate Id|  
    |EnglishProductCategoryName|Product Category Name|  
  
    **Product Subcategory**  
  
    |Quellname|Anzeigename|  
    |---------------|-----------------|  
    |ProductSubcategoryKey|Product Subcategory Id|  
    |ProductSubcategoryAlternateKey|Product Subcategory Alternate Id|  
    |EnglishProductSubcategoryName|Product Subcategory Name|  
    |ProductCategoryKey|Product Category Id|  
  
    **Internet Sales**  
  
    |Quellname|Anzeigename|  
    |---------------|-----------------|  
    |ProductKey|Product Id|  
    |CustomerKey|Customer Id|  
    |PromotionKey|Promotion Id|  
    |CurrencyKey|Currency Id|  
    |SalesTerritoryKey|Sales Territory Id|  
    |SalesOrderNumber|Sales Order Number|  
    |SalesOrderLineNumber|Sales Order Line Number|  
    |RevisionNumber|Revision Number|  
    |OrderQuantity|Order Quantity|  
    |UnitPrice|Unit Price|  
    |ExtendedAmount|Extended Amount|  
    |UnitPriceDiscountPct|Unit Price Discount Pct|  
    |DiscountAmount|Discount Amount|  
    |ProductStandardCost|Product Standard Cost|  
    |TotalProductCost|Total Product Cost|  
    |SalesAmount|Sales Amount|  
    |TaxAmt|Tax Amt|  
    |CarrierTrackingNumber|Carrier Tracking Number|  
    |CustomerPONumber|Customer PO Number|  
    |OrderDate|Order Date|  
    |DueDate|Due Date|  
    |ShipDate|Ship Date|  
  
## Nächster Schritt  
Wenn Sie mit diesem Tutorial fortfahren möchten, wechseln Sie zur nächsten Lektion: [Lektion 4: Markieren als Datumstabelle](../analysis-services/lesson-4-mark-as-date-table.md).  
  
  
  
