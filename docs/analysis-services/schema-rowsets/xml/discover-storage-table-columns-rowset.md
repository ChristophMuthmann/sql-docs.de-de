---
title: DISCOVER_STORAGE_TABLE_COLUMNS-Rowset | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
ms.assetid: 24abb88e-33a9-4ae2-829d-cdef0ff22ec1
caps.latest.revision: "14"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 8a0fec3423b126a425206441543fd50679712c2f
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="discoverstoragetablecolumns-rowset"></a>DISCOVER_STORAGE_TABLE_COLUMNS-Rowset
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Stellt Informationen auf Spaltenebene zu Speichertabellen, die von einer im SharePoint- oder tabellarischen Modus ausgeführten Analysis Services-Datenbank verwendet.  
  
 **Gilt für:** tabellarische Modelle  
  
## <a name="rowset-columns"></a>Rowsetspalten  
 Die **DISCOVER_STORAGE_TABLE_COLUMNS** Rowset enthält die folgenden Spalten.  
  
|**Spaltenname**|**Typindikator**|**Einschränkung**|**Beschreibung**|  
|---------------------|------------------------|---------------------|---------------------|  
|**DATENBANKNAME**|**DBTYPE_WSTR**|ja|Gibt den Namen der Datenbank an, die die Tabellen enthält. Bei Auslassung wird die aktuelle Datenbank verwendet.<br /><br /> Die **DISCOVER_STORAGE_TABLE_COLUMNS** Rowset kann mithilfe dieser Spalte eingeschränkt werden.|  
|**CUBE_NAME**|**DBTYPE_WSTR**|ja|Gibt den Cube oder das Modell an, das die Tabellen enthält.<br /><br /> Das **DISCOVER_STORAGE_TABLES** -Rowset kann mithilfe dieser Spalte eingeschränkt werden.|  
|**MEASURE_GROUP_NAME**|**DBTYPE_WSTR**|ja|Der Name der Measuregruppe.|  
|**DIMENSION_NAME**|**DBTYPE_WSTR**||Der Name der Dimension.|  
|**ATTRIBUTNAME**|**DBTYPE_WSTR**||Der Name des Attributs.|  
|**TABLE_ID**|**DBTYPE_WSTR**||Die ID der Tabelle.|  
|**COLUMN_ID**|**DBTYPE_ WSTR**||Die ID der Spalte. Die Spalten-ID ist für das xVelocity-Modul für Datenanalyse im Arbeitsspeicher (VertiPaq) intern und wird nur zu Informationszwecken verwendet.|  
|**COLUMN_TYPE**|**DBTYPE_WSTR**||Der Typ der Spalte. Der Spaltentyp ist für das xVelocity-Modul für Datenanalyse im Arbeitsspeicher (VertiPaq) intern und wird nur zu Informationszwecken verwendet.<br /><br /> BASIC_DATA<br /><br /> HIERARCHY_DATAID_TO_POSITION<br /><br /> HIERARCHY_POSITION_TO_DATAID<br /><br /> RELATIONSHIP|  
|**COLUMN_ENCODING**|**DBTYPE_UI8**||Eine ganze Zahl, die den für Spaltendaten verwendeten Codierungstyp darstellt.<br /><br /> **0**verwendet mit **COLUMN_TYPE**: HIERARCHY_DATAID_TO_POSITION, HIERARCHY_POSITION_TO_DATAID,-Beziehung<br /><br /> **1**verwendet mit **COLUMN_TYPE**: BASIC_DATA<br /><br /> **2**verwendet mit **COLUMN_TYPE**: BASIC_DATA|  
|**DATENTYP**|**DBTYPE_WSTR**||Der Datentyp der Spalte. Verfügt über folgende Werte möglich:<br /><br /> DBTYPE_BOOL<br /><br /> DBTYPE_CY<br /><br /> DBTYPE_DATE<br /><br /> DBTYPE_I4<br /><br /> DBTYPE_I8<br /><br /> DBTYPE_R8<br /><br /> DBTYPE_WSTR<br /><br /> –|  
|**ISKEY**|**DBTYPE_BOOL**||**"True"** ist die Spalte als Primär- oder Fremdschlüssel Schlüssel andernfalls **"false"**.|  
|**ISUNIQUE**|**DBTYPE_BOOL**||**"True"** , wenn die Werte in der Spalte eindeutig, und andernfalls sind **"false"**.|  
|**ISNULLABLE**|**DBTYPE_BOOL**||**"True"** ist die Spalte NULL-Werte zulässt, andernfalls **"false"**.|  
|**ISROWNUMBER**|**DBTYPE_BOOL**||**"True"** , wenn die Spalte eine Zeilennummernspalte ist. Zeilennummernspalten zur internen Verwendung durch das xVelocity-Modul für Datenanalyse im Arbeitsspeicher.|  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>Verwenden von ADOMD.NET zum Zurückgeben des Rowsets  
 Wenn Sie Metadaten mithilfe von ADOMD.NET und des Schemarowsets abrufen, können Sie entweder die GUID verwenden oder eine Referenz für ein Schemarowsetobjekt in der GetSchemaDataSet-Methode herstellen. Weitere Informationen finden Sie unter [Working with Schema Rowsets in ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets.md).  
  
 Die folgende Tabelle enthält die GUID und die Zeichenfolgenwerte, die dieses Rowset identifizieren.  
  
|Argument|value|  
|--------------|-----------|  
|GUID|a07ccd44-8148-11D0-87bb-00c04fc33942|  
|ADOMDNAME|StorageTableColumns|  
  
## <a name="example"></a>Beispiel  
 Das folgende Codebeispiel gibt das Resultset mithilfe einer DMV-Abfrage zurück.  
  
```  
SELECT *  
FROM $System.DISCOVER_STORAGE_TABLE_COLUMNS  
ORDER BY TABLE_ID DESC  
  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Analysis Services-Schemarowsets](../../../analysis-services/schema-rowsets/analysis-services-schema-rowsets.md)  
  
  
