---
title: "srv_setcollen (API für erweiterte gespeicherte Prozeduren) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname: srv_setcollen
apilocation: opends60.dll
apitype: DLLExport
dev_langs: C++
helpviewer_keywords: srv_setcollen
ms.assetid: 3c60f1c3-4562-463a-a259-12df172788bd
caps.latest.revision: "30"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0ab0ed5352dbc77f6a78f5a4ed59a5d8ee8d33d5
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="srvsetcollen-extended-stored-procedure-api"></a>srv_setcollen (API für erweiterte gespeicherte Prozeduren)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Verwenden Sie stattdessen die CLR-Integration.  
  
 Gibt die aktuelle Datenlänge in Byte einer Spalte mit variabler Länge oder einer Spalte an, die NULL-Werte zulässt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
int srv_setcollen (  
SRV_PROC *  
srvproc  
,  
int   
column  
,  
int  
len   
);  
```  
  
## <a name="arguments"></a>Argumente  
 *srvproc*  
 Ein Zeiger auf die SRV_PROC-Struktur, die das Handle für eine bestimmte Clientverbindung ist. Die Struktur enthält Informationen, mit der die API-Bibliothek für erweiterte gespeicherte Prozeduren die Kommunikation und Daten zwischen der Anwendung und dem Client verwaltet.  
  
 *column*  
 Gibt die Nummer der Spalte an, für die die Datenlänge angegeben wird. Die Spalten sind fortlaufend nummeriert, beginnend mit 1.  
  
 *len*  
 Gibt die Länge der Spaltendaten in Byte an. Eine Länge von 0 bedeutet, dass der Spaltendatenwert NULL ist.  
  
## <a name="returns"></a>Rückgabewert  
 SUCCEED oder FAIL.  
  
## <a name="remarks"></a>Hinweise  
 Jede Spalte der Zeile muss zuerst mit **srv_describe** definiert werden. Die Spaltendatenlänge wird vom letzten Aufruf von **srv_describe** oder **srv_setcollen** festgelegt. Wenn Daten mit variabler Länge (NULL-terminierte Daten) für eine Zeile geändert werden, muss diese mit **srv_setcollen** auf die neue Länge festgelegt werden, bevor **srv_sendrow** aufgerufen wird. Für eine Spalte, die NULL-Werte zulässt, muss **srv_describe** mit einem auf einen Datentyp festgelegten *desttype*-Wert aufgerufen worden sein, der NULL-Werte zulässt (wie SRVINTN), und NULL-Daten werden durch Aufrufen von **srv_setcollen** angegeben, wobei *len* auf 0 festgelegt ist. Daten der Länge 0 (NULL) können nicht mit der API für erweiterte gespeicherte Prozeduren angegeben werden.  
  
 Wenn der Datentyp der Spalte von variabler Länge ist, ist *len* nicht aktiviert. Diese Funktion gibt FAIL zurück, wenn sie für eine Spalte mit fester Länge aufgerufen wird.  
  
> [!IMPORTANT]  
>  Sie sollten den Quellcode der erweiterten gespeicherten Prozeduren sorgfältig prüfen, und Sie sollten die kompilierten DLL-Dateien testen, bevor Sie sie auf einem Produktionsserver installieren. Weitere Informationen zum Überprüfen und Testen der Sicherheit finden Sie auf dieser [Microsoft-Website](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/).  
  
## <a name="see-also"></a>Siehe auch  
 [srv_describe (API für erweiterte gespeicherte Prozeduren)](../../relational-databases/extended-stored-procedures-reference/srv-describe-extended-stored-procedure-api.md)  
  
  
