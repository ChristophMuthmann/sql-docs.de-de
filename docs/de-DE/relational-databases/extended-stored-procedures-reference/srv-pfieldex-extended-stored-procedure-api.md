---
title: srv_pfieldex (API für erweiterte gespeicherte Prozeduren) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/16/2017
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
- srv_pfieldex
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_pfieldex
ms.assetid: d4e9a34b-b3a3-434f-8556-768bd20d145a
caps.latest.revision: 30
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 76e8d3991b4154e929b6b05a96e1b3f816c61b3f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="srvpfieldex-extended-stored-procedure-api"></a>srv_pfieldex (API für erweiterte gespeicherte Prozeduren)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Verwenden Sie stattdessen die CLR-Integration.  
  
 Gibt einen Zeiger auf Daten zurück, die das angeforderte SRV_PROC-Feld enthalten.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
void *srv_pfieldex(SRV_PROC *   
srvproc  
, int   
field  
, int *   
len  
);  
```  
  
## <a name="arguments"></a>Argumente  
 *srvproc*   
 Ein Zeiger auf die SRV_PROC-Struktur, die das Handle für eine bestimmte Clientverbindung ist. Die Struktur enthält Informationen, mit der die API-Bibliothek für erweiterte gespeicherte Prozeduren die Kommunikation und Daten zwischen der Anwendung und dem Client verwaltet.  
  
 *field*  
 Gibt das zurückzugebende *srvproc*-Feld an  
  
|Feld|Description|Rückgabetyp|  
|-----------|-----------------|------------------|  
|SRV_MSGLCID|Aktuelle Sitzungsmeldung-LCID|ULONG*|  
|SRV_INSTANCENAME|Instanzname (wenn genannt); gibt andernfalls NULL zurück|WCHAR*|  
  
 *len*  
 Ein Zeiger auf eine **int**-Variable, die die Länge des zurückgegebenen *field*-Werts in Byte enthält. Wenn *len* NULL ist, wird die Länge nicht zurückgegeben. Wenn NULL zurückgegeben wird, wird **len* auf 0 (null) festgelegt.  
  
## <a name="returns"></a>Rückgabewert  
 Ein Zeiger auf Daten, deren Typ von *field* abhängt. NULL wird zurückgegeben, wenn *len* oder *srvproc* NULL ist. Ist *field* unbekannt, wird NULL zurückgegeben. Wenn NULL zurückgegeben wird, wird **len* auf 0 (null) festgelegt.  
  
> [!IMPORTANT]  
>  Der vom Server zurückgegebene Puffer sollte schreibgeschützt sein. Andernfalls ist der Serverstatus möglicherweise beschädigt.  
  
## <a name="remarks"></a>Remarks  
 **Sicherheitshinweis** Sie sollten den Quellcode der erweiterten gespeicherten Prozeduren gründlich überprüfen. Außerdem sollten Sie die kompilierten DLLs vor der Installation auf einem Produktionsserver testen. Weitere Informationen zum Überprüfen und Testen der Sicherheit finden Sie auf dieser [Microsoft-Website](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/).  
  
  
