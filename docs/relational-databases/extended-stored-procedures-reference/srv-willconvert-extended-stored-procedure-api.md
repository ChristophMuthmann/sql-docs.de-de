---
title: srv_willconvert (API für erweiterte gespeicherte Prozeduren) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: extended-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- srv_willconvert
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_willconvert
ms.assetid: 6f4db5fd-215a-461c-95e4-17697852733e
caps.latest.revision: 29
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: e22955b073e17802be37e95ddf41659766da0662
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="srvwillconvert-extended-stored-procedure-api"></a>srv_willconvert (API für erweiterte gespeicherte Prozeduren)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Verwenden Sie stattdessen die CLR-Integration.  
  
 Bestimmt, ob eine bestimmte Datentypkonvertierung innerhalb der ODS-Bibliothek verfügbar ist.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
BOOL srv_willconvert (  
int  
srctype  
,  
int  
desttype   
);  
```  
  
## <a name="arguments"></a>Argumente  
 *srctype*  
 Gibt den Datentyp der zu konvertierenden Daten an. Dieser Parameter kann ein beliebiger in der API für erweiterte gespeicherte Prozeduren verfügbarer Datentyp sein.  
  
 *desttype*  
 Gibt den Datentyp an, in den die Quelldaten konvertiert werden. Dieser Parameter kann ein beliebiger in der API für erweiterte gespeicherte Prozeduren verfügbarer Datentyp sein.  
  
## <a name="returns"></a>Rückgabewert  
 TRUE, wenn die Datentypkonvertierung unterstützt wird; FALSE, wenn die Datentypkonvertierung nicht unterstützt wird.  
  
## <a name="remarks"></a>Remarks  
 Eine Beschreibung der einzelnen Datentypen finden Sie in [Data Types (Extended Stored Procedure API) (Datentypen (API für erweiterte gespeicherte Prozeduren))](../../relational-databases/extended-stored-procedures-reference/data-types-extended-stored-procedure-api.md).  
  
> [!IMPORTANT]  
>  Sie sollten den Quellcode der erweiterten gespeicherten Prozeduren sorgfältig prüfen, und Sie sollten die kompilierten DLL-Dateien testen, bevor Sie sie auf einem Produktionsserver installieren. Weitere Informationen zum Überprüfen und Testen der Sicherheit finden Sie auf dieser [Microsoft-Website](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [srv_convert (API für erweiterte gespeicherte Prozeduren)](../../relational-databases/extended-stored-procedures-reference/srv-convert-extended-stored-procedure-api.md)  
  
  
