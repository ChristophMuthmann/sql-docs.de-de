---
title: "srv_pfieldex (API für erweiterte gespeicherte Prozeduren) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/16/2017
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
- srv_pfieldex
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_pfieldex
ms.assetid: d4e9a34b-b3a3-434f-8556-768bd20d145a
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 70f36511846d7435cc940ea65f871c462130958d
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
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
  
  
