---
title: srv_paramsetoutput (API für erweiterte gespeicherte Prozeduren) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/04/2017
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
- srv_paramsetoutput
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_paramsetoutput
ms.assetid: f2810e19-e513-458b-8925-5756b6ee1313
caps.latest.revision: 29
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 4808537e659adb1d840925ba2be0985063c4e3bc
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="srvparamsetoutput-extended-stored-procedure-api"></a>srv_paramsetoutput (API für erweiterte gespeicherte Prozeduren)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Verwenden Sie stattdessen die CLR-Integration.  
  
 Legt den Wert eines Rückgabeparameters fest. Diese Funktion setzt die **srv_paramset** -Funktion außer Kraft.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
int srv_paramsetoutput (  
SRV_PROC *  
srvproc  
,  
int  
n  
,  
BYTE *  
pbData  
,  
ULONG   
cbLen  
,  
BOOL  
fNull   
);  
```  
  
## <a name="arguments"></a>Argumente  
 *srvproc*   
 Ein Handle für eine Clientverbindung.  
  
 *n*  
 Die Ordnungszahl des festzulegenden Parameters. Der erste Parameter ist 1.  
  
 *pbData*  
 Ein Verweis auf den Datenwert, der als ein Prozedurrückgabeparameter an den Client zurückgesendet werden soll.  
  
 *cbLen*  
 Die tatsächliche Länge der zurückzugebenden Daten. Wenn der Datentyp des Parameters Werte einer konstanten Länge angibt und keine NULL-Werte zulässt (z. B. *srvbit* oder *srvint1*), wird *cbLen* ignoriert. Der Wert 0 gibt Daten der Länge 0 (null) an, wenn *fNull* FALSE ist.  
  
 *fNull*  
 Ein Flag, der angibt, ob der Wert des Rückgabeparameters NULL ist. Legen Sie dieses Flag auf TRUE fest, wenn der Parameter auf NULL gesetzt werden soll. Der Standardwert ist FALSE. Wenn *fNull* auf TRUE gesetzt ist, sollte *cbLen* auf 0 gesetzt werden, anderenfalls schlägt die Funktion fehl.  
  
## <a name="returns"></a>Rückgabewert  
 Wenn die Parameterinformationen erfolgreich festgelegt wurden, wird SUCCEED zurückgegeben, andernfalls FAIL. FAIL wird in den folgenden Fällen zurückgegeben:  
  
-   Der Parameter ist kein Rückgabeparameter.  
  
-   Das *cbLen* -Argument ist ungültig.  
  
## <a name="remarks"></a>Remarks  
 **Sicherheitshinweis** Sie sollten den Quellcode der erweiterten gespeicherten Prozeduren gründlich überprüfen. Außerdem sollten Sie die kompilierten DLLs vor der Installation auf einem Produktionsserver testen. Weitere Informationen zum Überprüfen und Testen der Sicherheit finden Sie auf dieser [Microsoft-Website](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/).  
  
  
