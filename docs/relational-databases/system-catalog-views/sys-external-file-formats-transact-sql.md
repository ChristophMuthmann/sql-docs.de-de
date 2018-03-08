---
title: Sys.external_file_formats (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: a89efb2c-0a3a-4b64-9284-6e93263e29ac
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 08318355eebbff784da00fc27303af1abbf17a31
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="sysexternalfileformats-transact-sql"></a>Sys.external_file_formats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  Enthält eine Zeile für jeden externen Dateiformats in der aktuellen Datenbank für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[ssSDS](../../includes/sssds-md.md)], und [!INCLUDE[ssSDW](../../includes/sssdw-md.md)].  
  
 Enthält eine Zeile für jeden externen Dateiformats auf dem Server für [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
|Spaltenname|Datentyp|Description|Bereich|  
|-----------------|---------------|-----------------|-----------|  
|file_format_id|**int**|Objekt-ID für das externe Dateiformat.||  
|name|**sysname**|Der Name des Dateiformats ab. in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und [!INCLUDE[ssSDW](../../includes/sssdw-md.md)], dies ist für die Datenbank eindeutig. In [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], dies ist für den Server eindeutig.||  
|format_type|**tinyint**|Der Typ des Datei-Format.|DELIMITEDTEXT, RCFILE, ORC, PARQUET|  
|Feldabschlusszeichen|**nvarchar(10)**|Für die Format_type = DELIMITEDTEXT, dies ist das Feldabschlusszeichen.||  
|string_delimiter|**nvarchar(10)**|Für die Format_type = DELIMITEDTEXT, dies ist das Trennzeichen für Zeichenfolgen.||  
|date_format|**nvarchar(50)**|Für die Format_type = DELIMITEDTEXT, dies ist das benutzerdefinierte Datums- und Zeitformat.||  
|use_type_default|**bit**|Für die Format_type = TEXT als TRENNZEICHEN, gibt an, wie fehlende Werte behandelt wird, wenn PolyBase Daten aus Textdateien in HDFS importiert [!INCLUDE[ssSDW](../../includes/sssdw-md.md)].|0 – speichern fehlende Werte als die Zeichenfolge 'NULL'.<br /><br /> 1 – Speichern von fehlenden Werten als der Standardwert der Spalte.|  
|serde_method|**nvarchar(255)**|Für die Format_type = RCFILE, dies ist die Methode für die Serialisierung/Deserialisierung.||  
|row_terminator|**nvarchar(10)**|Für die Format_type = DELIMITEDTEXT, dies ist die Zeichenfolge, die jede Zeile in der externen Hadoop-Datei wird beendet.|Always '\n'.|  
|Codierung|**nvarchar(10)**|Für die Format_type = DELIMITEDTEXT, dies ist die Codierungsmethode für die externe Hadoop-Datei.|Immer 'UTF8'.|  
|data_compression|**nvarchar(255)**|Die datenkomprimierungsmethode für die externen Daten.|Für die Format_type = DELIMITEDTEXT:<br /><br /> -   'org.apache.hadoop.io.compress.DefaultCodec'<br />-   'org.apache.hadoop.io.compress.GzipCodec'<br /><br /> Für die Format_type = RCFILE:<br /><br /> -   'org.apache.hadoop.io.compress.DefaultCodec'<br /><br /> Für die Format_type = ORC:<br /><br /> -   'org.apache.hadoop.io.compress.DefaultCodec'<br />-   'org.apache.hadoop.io.compress.SnappyCodec'<br /><br /> Für die Format_type = PARQUET:<br /><br /> -   'org.apache.hadoop.io.compress.GzipCodec'<br />-   'org.apache.hadoop.io.compress.SnappyCodec'|  
  
## <a name="permissions"></a>Berechtigungen  
 Die Sichtbarkeit der Metadaten in Katalogsichten ist auf sicherungsfähige Elemente eingeschränkt, bei denen der Benutzer entweder der Besitzer ist oder für die dem Benutzer eine Berechtigung erteilt wurde. Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Siehe auch  
 [sys.external_data_sources &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-external-data-sources-transact-sql.md)   
 [sys.external_tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-external-tables-transact-sql.md)   
 [CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)  
  
  
