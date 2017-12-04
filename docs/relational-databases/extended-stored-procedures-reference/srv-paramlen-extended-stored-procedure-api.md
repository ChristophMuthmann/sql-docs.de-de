---
title: "srv_paramlen (API für erweiterte gespeicherte Prozeduren) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: extended-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname: srv_paramlen
apilocation: opends60.dll
apitype: DLLExport
dev_langs: C++
helpviewer_keywords: srv_paramlen
ms.assetid: d1fe92ff-cad6-4396-8216-125e5642e81e
caps.latest.revision: "32"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9f3f7a3a3b8f0cae6813cbc571ad038f1e673a41
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="srvparamlen-extended-stored-procedure-api"></a>srv_paramlen (API für erweiterte gespeicherte Prozeduren)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Verwenden Sie stattdessen die CLR-Integration.  
  
 Gibt die Datenlänge des Aufrufparameters für eine remote gespeicherte Prozedur zurück. Diese Funktion wurde durch die **srv_paraminfo**-Funktion ersetzt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
int srv_paramlen (  
SRV_PROC *  
srvproc  
,  
int  
n   
);  
```  
  
## <a name="arguments"></a>Argumente  
 *srvproc*   
 Ist ein Zeiger auf die SRV_PROC-Struktur, die das Handle für eine bestimmte Clientverbindung ist (in diesem Fall das Handle, das den Aufruf der remote gespeicherten Prozedur erhalten hat). Die Struktur enthält Informationen, mit der die API-Bibliothek für erweiterte gespeicherte Prozeduren die Kommunikation und Daten zwischen der Anwendung und dem Client verwaltet.  
  
 *n*  
 Gibt die Anzahl der Parameter an. Der erste Parameter ist 1.  
  
## <a name="returns"></a>Rückgabewert  
 Die tatsächliche Länge der Parameterdaten in Byte. Wenn es keinen *n*-ten Parameter gibt, oder wenn es keine remote gespeicherte Prozedur gibt, wird –1 zurückgegeben. Wenn der *n*-te Parameter NULL ist, wird 0 (null) zurückgegeben.  
  
 Diese Funktion gibt die folgenden Werte zurück, wenn der Parameter einem der folgenden Systemdatentypen von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] entspricht.  
  
|Neue Datentypen|Länge der Eingabedaten|  
|--------------------|-----------------------|  
|**BITN**|**NULL**: 1<br /><br /> **ZERO**: 1<br /><br /> **>=255:** NICHT ZUTREFFEND<br /><br /> **<255:** NICHT ZUTREFFEND|  
|**BIGVARCHAR**|**NULL**: 0<br /><br /> **ZERO**: 1<br /><br /> **>=255:** 255<br /><br /> **<255:** tatsächlicher *len*-Wert|  
|**BIGCHAR**|**NULL**: 0<br /><br /> **ZERO:** 255<br /><br /> **>=255:** 255<br /><br /> **<255:** 255|  
|**BIGBINARY**|**NULL**: 0<br /><br /> **ZERO:** 255<br /><br /> **>=255:** 255<br /><br /> **<255:** 255|  
|**BIGVARBINARY**|**NULL**: 0<br /><br /> **ZERO**: 1<br /><br /> **>=255:** 255<br /><br /> **<255:** tatsächlicher *len*-Wert|  
|**NCHAR**|**NULL**: 0<br /><br /> **ZERO:** 255<br /><br /> **>=255:** 255<br /><br /> **<255:** 255|  
|**NVARCHAR**|**NULL**: 0<br /><br /> **ZERO**: 1<br /><br /> **>=255:** 255<br /><br /> **<255:** tatsächlicher *len*-Wert|  
|**NTEXT**|**NULL:** –1<br /><br /> **ZERO:** –1<br /><br /> **>=255:** –1<br /><br /> **\<255:** –1|  
  
 \* tatsächlicher *len*-Wert = Länge von Mehrbyte-Zeichenfolgen (cch)  
  
## <a name="remarks"></a>Hinweise  
 Parameter einer remote gespeicherten Prozedur haben eine tatsächliche und eine maximale Datenlänge. Bei Standarddatentypen fester Länge, die keine Nullwerte zulassen, ist die tatsächliche Länge mit der maximalen Länge identisch. Bei Datentypen variabler Länge können die Längen unterschiedlich sein. Ein als **varchar(30)** deklarierter Parameter kann beispielsweise über Daten verfügen, die nur 10 Byte lang sind. Die tatsächliche Länge des Parameters ist 10, die maximale Länge jedoch 30. Die **srv_paramlen**-Funktion ruft die tatsächliche Datenlänge einer remote gespeicherten Prozedur in Byte ab. Zum Abrufen der maximalen Datenlänge eines Parameters verwenden Sie **srv_parammaxlen**.  
  
 Wenn eine remote gespeicherte Prozedur mit Parametern aufgerufen wird, werden die Parameter entweder mit ihrem Namen oder mit ihrer Position übergeben (unbenannt). Werden beim Aufruf einer remote gespeicherten Prozedur einige Parameter über ihren Namen und andere über ihre Position übergeben, so tritt ein Fehler auf. Der SRV_RPC-Handler wird trotzdem aufgerufen, doch es sind scheinbar keine Parameter vorhanden, und **srv_rpcparams** gibt 0 zurück.  
  
> [!IMPORTANT]  
>  Sie sollten den Quellcode der erweiterten gespeicherten Prozeduren sorgfältig prüfen, und Sie sollten die kompilierten DLL-Dateien testen, bevor Sie sie auf einem Produktionsserver installieren. Weitere Informationen zum Überprüfen und Testen der Sicherheit finden Sie auf dieser [Microsoft-Website](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/).  
  
## <a name="see-also"></a>Siehe auch  
 [srv_paraminfo (API für erweiterte gespeicherte Prozeduren)](../../relational-databases/extended-stored-procedures-reference/srv-paraminfo-extended-stored-procedure-api.md)   
 [srv_rpcparams (API für erweiterte gespeicherte Prozeduren)](../../relational-databases/extended-stored-procedures-reference/srv-rpcparams-extended-stored-procedure-api.md)  
  
  
