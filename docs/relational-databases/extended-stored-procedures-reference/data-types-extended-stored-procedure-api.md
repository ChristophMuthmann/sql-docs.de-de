---
title: "Datentypen (API für die erweiterte gespeicherte Prozedur) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: extended-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], data types
- data types [SQL Server], extended stored procedures
ms.assetid: 37fb86b9-8819-4387-bcdc-9616968e15ad
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a69f167e3979a975deb506270843886142244dc4
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="data-types-extended-stored-procedure-api"></a>Datentypen (API für erweiterte gespeicherte Prozeduren)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Verwenden Sie stattdessen die CLR-Integration.  
  
 Um die API-Datentypen für erweiterte gespeicherte Prozeduren zu verwenden, schließen Sie die Headerdatei Srv.h ins Programm ein.  
  
|Datentyp|SQL Server-Datentyp|Description|  
|---------------|--------------------------|-----------------|  
|SRVBIGBINARY|**binary**|**binary**-Datentyp mit einer Länge von 0 bis 8000 Byte.|  
|SRVBIGCHAR|**char**|**character**-Datentyp mit einer Länge von 0 bis 8000 Byte.|  
|SRVBIGVARBINARY|**varbinary**|**binary**-Datentyp mit variabler Länge zwischen 0 und 8000 Byte.|  
|SRVBIGVARCHAR|**varchar**|**character**-Datentyp mit variabler Länge zwischen 0 und 8000 Byte.|  
|SRVBINARY|**binary**|**binary**-Datentyp|  
|SRVBIT|**Bit**|**bit**-Datentyp|  
|SRVBITN|**bit null**|**bit**-Datentyp, NULL-Werte sind zulässig.|  
|SRVCHAR|**char**|**character**-Datentyp|  
|SRVDATETIME|**datetime**|**datetime**-Datentyp mit einer Länge von 8 Byte|  
|SRVDATETIM4|**smalldatetime**|**smalldatetime**-Datentyp mit einer Länge von 4 Byte|  
|SRVDATETIMN|**datetime null**|**smalldatetime**- oder **datetime**-Datentyp, NULL-Werte sind zulässig.|  
|SRVDECIMAL|**decimal**|**decimal**-Datentyp|  
|SRVDECIMALN|**decimal null**|**decimal**-Datentyp, NULL-Werte sind zulässig.|  
|SRVFLT4|**real**|**real**-Datentyp mit einer Länge von 4 Byte|  
|SRVFLT8|**float**|**float**-Datentyp mit einer Länge von 8 Byte|  
|SRVFLTN|**real** &#124; **float Null**|**real**- oder **float**-Datentyp, NULL-Werte sind zulässig.|  
|SRVIMAGE|**image**|**image**-Datentyp|  
|SRVINT1|**tinyint**|**tinyint**-Datentyp mit einer Länge von einem Byte|  
|SRVINT2|**smallint**|**smallint**-Datentyp mit einer Länge von 2 Byte|  
|SRVINT4|**int**|**int**-Datentyp mit einer Länge von 4 Byte|  
|SRVINTN|**"tinyint"** &#124; **"smallint"** &#124; **Int null**|**tinyint**-, **smallint**-, oder **int**-Datentyp, NULL-Werte sind zulässig.|  
|SRVMONEY4|**smallmoney**|**smallmoney**-Datentyp mit einer Länge von 4 Byte|  
|SRVMONEY|**money**|**money**-Datentyp mit einer Länge von 8 Byte|  
|SRVMONEYN|**Money** &#124; **Smallmoney null**|**smallmoney**- oder **money**-Datentyp, NULL-Werte sind zulässig.|  
|SRVNCHAR|**nchar**|**character**-Unicode-Datentyp|  
|SRVNTEXT|**ntext**|**text**-Unicode-Datentyp|  
|SRVNUMERIC|**numeric**|**numeric**-Datentyp|  
|SRVNUMERICN|**numeric null**|**numeric**-Datentyp, NULL-Werte sind zulässig.|  
|SRVNVARCHAR|**nvarchar**|**character**-Datentyp mit Unicode-Zeichen von variabler Länge|  
|SRVTEXT|**text**|**text**-Datentyp|  
|SRVVARBINARY|**varbinary**|**binary**-Datentyp mit variabler Länge|  
|SRVVARCHAR|**varchar**|**character**-Datentyp mit variabler Länge|  
  
> [!IMPORTANT]  
>  Sie sollten den Quellcode der erweiterten gespeicherten Prozeduren sorgfältig prüfen, und Sie sollten die kompilierten DLL-Dateien testen, bevor Sie sie auf einem Produktionsserver installieren. Weitere Informationen zum Überprüfen und Testen der Sicherheit finden Sie auf dieser [Microsoft-Website](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/).  
  
  
