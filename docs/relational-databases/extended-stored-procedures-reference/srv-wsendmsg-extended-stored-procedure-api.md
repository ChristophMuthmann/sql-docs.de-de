---
title: „srv_wsendmsg“ (API für die erweiterte gespeicherte Prozedur) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: extended-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- srv_wsendmsg
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_wsendmsg
ms.assetid: f2153076-32c9-4a52-8e1b-fc9618153543
caps.latest.revision: 32
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 728d4e69531e05608db80d9ca64e435efe162f5b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="srvwsendmsg-extended-stored-procedure-api"></a>srv_wsendmsg (API für erweiterte gespeicherte Prozeduren)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Verwenden Sie stattdessen die CLR-Integration.  
  
 Sendet eine Unicode-Meldung an den Client.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
int srv_wsendmsg(SRV_PROC *   
srvproc  
, int   
msgnum  
, int   
severity  
, WCHAR *   
message  
, int   
msglen  
);  
```  
  
## <a name="arguments"></a>Argumente  
 *srvproc*   
 Ein Zeiger auf die SRV_PROC-Struktur, die das Handle für eine bestimmte Clientverbindung ist. Die Struktur enthält Informationen, mit der die API-Bibliothek für erweiterte gespeicherte Prozeduren die Kommunikation und Daten zwischen der Anwendung und dem Client verwaltet.  
  
 *Msgnum*  
 Eine 4-Byte-Meldungsnummer.  
  
 *Severity*  
 Gibt den Schweregrad des Fehlers an. Ein Schweregrad kleiner oder gleich 10 wird als Informationsmeldung betrachtet, bei einem höheren Wert handelt es sich um einen Fehler.  
  
 *Nachricht*  
 Ein Zeiger auf die an den Client zu sendende Unicode-Zeichenfolge.  
  
 *msglen*  
 Gibt die Länge von *message*in Zeichen an.  
  
## <a name="returns"></a>Rückgabewert  
 SUCCEED oder FAIL.  
  
## <a name="remarks"></a>Remarks  
 Verwenden Sie diese Funktion, um Meldungen in Unicode zu senden. Sie ähnelt **srv_sendmsg**, jedoch handelt es sich bei der gesendeten Meldung um eine WCHAR-Zeichenfolge und nicht um eine Zeichenfolge des Typs DBCHAR. Beachten Sie, dass die Länge der Meldung in Zeichen und nicht in Byte angegeben wird und dass *msglen* niemals SRV_NULLTERM entspricht.  
  
 In folgenden Fällen gibt die Funktion FAIL zurück:  
  
-   *msglen* befindet sich nicht im Bereich zwischen 0 und 32242.  
  
-   *msglen* entspricht 0, der Meldungszeiger ist jedoch NULL.  
  
-   Beim Versenden der Fehlermeldung über das Netzwerk tritt ein Fehler auf.  
  
> [!IMPORTANT]  
>  Sie sollten den Quellcode der erweiterten gespeicherten Prozeduren sorgfältig prüfen, und Sie sollten die kompilierten DLL-Dateien testen, bevor Sie sie auf einem Produktionsserver installieren. Weitere Informationen zum Überprüfen und Testen der Sicherheit finden Sie auf dieser [Microsoft-Website](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [srv_sendmsg (API für die erweiterte gespeicherte Prozedur)](../../relational-databases/extended-stored-procedures-reference/srv-sendmsg-extended-stored-procedure-api.md)  
  
  
