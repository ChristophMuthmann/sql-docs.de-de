---
title: Sys. numbered_procedure_parameters (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- numbered_procedure_parameters_TSQL
- sys.numbered_procedure_parameters_TSQL
- numbered_procedure_parameters
- sys.numbered_procedure_parameters
dev_langs: TSQL
helpviewer_keywords: sys.numbered_procedure_parameters catalog view
ms.assetid: a441d46d-1f30-41c2-8d94-e9442f59786e
caps.latest.revision: "20"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8d2eee8a375dc7b2705b69b93a99f6ce2d8eae4b
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="sysnumberedprocedureparameters-transact-sql"></a>sys.numbered_procedure_parameters (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Enthält eine Zeile für jeden Parameter einer nummerierten Prozedur. Beim Erstellen einer nummerierten gespeicherten Prozedur erhält die Basisprozedur die Nummer 1. Nachfolgende Prozeduren erhalten die Nummern 2, 3 usw. **sys.numbered_procedure_parameters** enthält die Parameterdefinitionen für alle nachfolgenden Prozeduren ab der Nummer 2 aufwärts. Diese Sicht zeigt keine Parameter für die gespeicherte Basisprozedur (Nummer 1). Die gespeicherte Basisprozedur ist mit einer nicht nummerierten gespeicherten Prozedur vergleichbar. Aus diesem Grund werden die Parameter dargestellt [sys.parameters (Transact-SQL)](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md).  
  
> [!IMPORTANT]  
>  Nummerierte Prozeduren sind als veraltet markiert. Von der Verwendung nummerierter Prozeduren wird abgeraten. Ein DEPRECATION_ANNOUNCEMENT-Ereignis wird ausgelöst, wenn eine Abfrage kompiliert wird, die diese Katalogsicht verwendet.  
  
> [!NOTE]  
>  XML- und CLR-Parameter werden für nummerierte Prozeduren nicht unterstützt.  
  
||  
|-|  
|**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis zur [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|Die ID des Objekts, zu dem dieser Parameter gehört.|  
|**procedure_number**|**smallint**|Die Nummer dieser Prozedur innerhalb des Objekts, d. h. 2 oder größer.|  
|**name**|**sysname**|Der Name des Parameters. Ist innerhalb von **procedure_number**eindeutig.|  
|**parameter_id**|**int**|ID des Parameters. Ist innerhalb von **procedure_number**eindeutig.|  
|**system_type_id**|**tinyint**|Die Systemtyp-ID des Parameters.|  
|**user_type_id**|**int**|Die ID des Parametertyps gemäß der Definition seitens des Benutzers.|  
|**max_length**|**smallint**|Die maximale Länge des Parameters in Byte.<br /><br /> -1 = Spaltendaten sind vom Datentyp varchar(max), nvarchar(max) oder varbinary(max).|  
|**Genauigkeit**|**tinyint**|Genauigkeit des Parameters, wenn dieser numerisch ist. Andernfalls ist der Wert 0.|  
|**Skalierung**|**tinyint**|Dezimalstellen des Parameters, wenn dieser numerisch ist. Andernfalls ist der Wert 0.|  
|**is_output**|**bit**|1 = Der Parameter ist ein Ausgabe- oder Rückgabewert; andernfalls 0.|  
|**is_cursor_ref**|**bit**|1 = Der Parameter ist ein Cursorverweis.|  
  
> [!NOTE]  
>  XML- und CLR-Parameter werden für nummerierte Prozeduren nicht unterstützt.  
  
## <a name="permissions"></a>Berechtigungen  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Katalogsichten für Objekte &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
