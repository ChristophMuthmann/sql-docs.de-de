---
title: "srv_setutype (API für erweiterte gespeicherte Prozeduren) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
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
apiname:
- srv_setutype
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_setutype
ms.assetid: 6160f15d-1b68-411e-ab6d-491ec288f264
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9dc2615a5e44a404f3bf78939392b16e8cdd394b
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="srvsetutype-extended-stored-procedure-api"></a>srv_setutype (API für erweiterte gespeicherte Prozeduren)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Verwenden Sie stattdessen die CLR-Integration.  
  
 Legt den benutzerdefinierten Datentyp für eine Spalte in einer Zeile fest.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
int srv_setutype (  
SRV_PROC *  
srvproc  
,  
int   
column  
,   
DBINT  
user_type   
);  
```  
  
## <a name="arguments"></a>Argumente  
 *srvproc*   
 Ein Zeiger auf die SRV_PROC-Struktur, die das Handle für eine bestimmte Clientverbindung ist. Die Struktur enthält Informationen, mit der die API-Bibliothek für erweiterte gespeicherte Prozeduren die Kommunikation und Daten zwischen der Anwendung und dem Client verwaltet.  
  
 *column*  
 Gibt an, welche Spalte festgelegt werden soll. Die Spalten sind fortlaufend nummeriert, beginnend mit 1.  
  
 *user_type*  
 Gibt den benutzerdefinierten Datentypcode an.  
  
## <a name="returns"></a>Rückgabewert  
 SUCCEED oder FAIL. Wenn die Spalte nicht vorhanden ist, wird FAIL zurückgegeben.  
  
## <a name="remarks"></a>Hinweise  
 Eine Spalte verfügt über zwei Datentypen: ihren tatsächlichen Datentyp und ihren benutzerdefinierten Datentyp. Der benutzerdefinierte Datentyp wird von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet, um, falls vorhanden, den tatsächlichen benutzerdefinierten Datentyp der Spalte sowie Spaltenbeschreibungsinformationen wie NULL-Zulässigkeit und Aktualisierbarkeit der Spalte zu speichern.  
  
 Die **srv_setutype** -Funktion kann jedes Mal aufgerufen werden, wenn *column* mit **srv_describe** definiert ist, und bevor die letzte Zeile gesendet wurde.  
  
> [!IMPORTANT]  
>  Sie sollten den Quellcode der erweiterten gespeicherten Prozeduren sorgfältig prüfen, und Sie sollten die kompilierten DLL-Dateien testen, bevor Sie sie auf einem Produktionsserver installieren. Weitere Informationen zum Überprüfen und Testen der Sicherheit finden Sie auf dieser [Microsoft-Website](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/).  
  
## <a name="see-also"></a>Siehe auch  
 [srv_describe (API für erweiterte gespeicherte Prozeduren)](../../relational-databases/extended-stored-procedures-reference/srv-describe-extended-stored-procedure-api.md)  
  
  
