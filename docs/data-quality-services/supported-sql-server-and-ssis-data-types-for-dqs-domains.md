---
title: "Unterstützte SQL Server- und SSIS-Datentypen für DQS-Domänen | Microsoft-Dokumentation"
ms.custom: 
ms.date: 11/08/2011
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- data-quality-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4931143a-b84d-478b-9b45-174128d36ed3
caps.latest.revision: 7
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: ec7d426fd60890eb6b61da4441e9f497e4d58162
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="supported-sql-server-and-ssis-data-types-for-dqs-domains"></a>Unterstützte SQL Server- und SSIS-Datentypen für DQS-Domänen
  In SQL Server und SQL Server Integration Services (SSIS) sind zahlreiche Datentypen vorhanden, darunter jedoch nur vier für DQS-Domänen: Date, Decimal, Integer und String. Nicht alle SQL Server- und SSIS-Datentypen werden in DQS unterstützt. Sie können die Quelldaten zum Durchführen der Datenbereinigung einer DQS-Domäne nur zuordnen, wenn der Quelldatentyp in DQS unterstützt wird und mit dem DQS-Domänendatentyp übereinstimmt. Dieses Thema enthält Informationen zu den SQL Server- und SSIS-Datentypen, die unterstützt werden und jedem der vier Domänendatentypen in DQS zugeordnet werden können.  
  
> [!NOTE]  
>  Der Datentyp der Quellspalte wird in XLSX- und XLS-Dateien vom häufigsten Datentyp in den ersten acht Zeilen bestimmt. Wenn eine Zelle diesem Datentyp nicht entspricht, erhält sie einen NULL-Wert. Entsprechend wird auch in CSV-Dateien der Datentyp der Quellspalte vom häufigsten Datentyp in den ersten acht Zeilen bestimmt.  
  
##  <a name="SQLServer"></a> Unterstützte SQL Server-Datentypen  
 Die folgende Tabelle enthält Informationen zu den für jeden DQS-Domänendatentyp unterstützten SQL Server-Datentypen:  
  
|DQS-Domänendatentyp|Unterstützte SQL Server-Datentypen|  
|--------------------------|------------------------------------|  
|Datum|Datum|  
|Decimal|Decimal<br /><br /> float<br /><br /> money<br /><br /> numeric<br /><br /> real<br /><br /> smallmoney|  
|Integer|bigint<br /><br /> int<br /><br /> smallint<br /><br /> tinyint|  
|String|char<br /><br /> nchar<br /><br /> nvarchar<br /><br /> varchar|  
  
 Die restlichen SQL Server-Datentypen werden in DQS nicht unterstützt. Informationen zu allen unterstützten SQL Server-Datentypen finden Sie unter[Data Types &#40;Transact-SQL&#41; (Datentypen &#40;Transact-SQL&#41;)](../t-sql/data-types/data-types-transact-sql.md).  
  
##  <a name="SSIS"></a> Unterstützte SSIS-Datentypen  
 Die folgende Tabelle enthält Informationen zu den für jeden DQS-Domänendatentyp unterstützten SSIS-Datentypen:  
  
|DQS-Domänendatentyp|Unterstützter SSIS-Datentyp|  
|--------------------------|------------------------------|  
|Datum|DT_DATE|  
|Decimal|DT_DECIMAL<br /><br /> DT_NUMERIC<br /><br /> DT_R4<br /><br /> DT_R8|  
|Integer|DT_I1<br /><br /> DT_I2<br /><br /> DT_I4<br /><br /> DT_I8<br /><br /> DT_U1<br /><br /> DT_U2<br /><br /> DT_U4<br /><br /> DT_U8|  
|String|DT_STR<br /><br /> DT_WSTR|  
  
 Die restlichen SSIS-Datentypen werden in DQS nicht unterstützt. Informationen zu allen SSIS-Datentypen finden Sie unter [Integration Services Data Types](../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Verwalten einer Domäne](../data-quality-services/managing-a-domain.md)  
  
  

