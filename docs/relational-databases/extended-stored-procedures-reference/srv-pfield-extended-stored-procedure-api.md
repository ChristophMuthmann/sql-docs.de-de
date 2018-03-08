---
title: "srv_pfield (API für erweiterte gespeicherte Prozeduren) | Microsoft-Dokumentation"
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
- srv_pfield
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_pfield
ms.assetid: a61e4c1f-e65b-48ea-a7d1-3e1544af389d
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 157bf19237d3b2dcf64a1401823c746fd2849cf0
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="srvpfield-extended-stored-procedure-api"></a>srv_pfield (API für erweiterte gespeicherte Prozeduren)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Verwenden Sie stattdessen die CLR-Integration.  
  
 Gibt Informationen zur Datenbankverbindung zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
DBCHAR * srv_pfield (  
SRV_PROC *  
srvproc  
,  
int   
field  
,  
int *  
len  
);  
```  
  
## <a name="arguments"></a>Argumente  
 *srvproc*   
 Zeiger, der eine Datenbankverbindung identifiziert  
  
 *field*  
 Gibt Daten über die Verbindung zur Rückgabe an.  
  
|Wert|Rückgabewert|  
|-----------|-------------|  
|SRV_APPLNAME|Der vom Client beim Herstellen der Verbindung bereitgestellte Anwendungsname.|  
|SRV_BCPFLAG|Ein Flag, das TRUE ist, wenn sich der Client auf einen Massenkopiervorgang vorbereitet; andernfalls FALSE.|  
|SRV_CLIB|Der Name der Bibliothek, die dem Client ermöglicht, mit einem Server zu kommunizieren.|  
|SRV_CPID|Die Client-Prozess-ID auf dem Client-Quellcomputer.|  
|SRV_HOST|Der vom Client beim Herstellen der Verbindung bereitgestellte Name des Clientcomputers.|  
|SRV_LIBVERS|Die Version der Clientbibliothek.|  
|SRV_LSECURE|Ein Flag. TRUE, wenn die Verbindung integrierte Sicherheit zur Anmeldung verwendet hat.|  
|SRV_NETWORK_MODULE|Der Name der von der Verbindung verwendeten Netzwerkbibliotheks-DLL.|  
|SRV_NETWORK_VERSION|Die Version der von der Verbindung verwendeten Netzwerkbibliotheks-DLL.|  
|SRV_NETWORK_CONNECTION|Die Verbindungszeichenfolge, die an die Net-Library-DLL für die aktuelle *srvproc*-Verbindung übergeben wird.|  
|SRV_PIPEHANDLE|Zeichenfolge, die das Pipehandle eines verbundenen Client enthält, oder NULL, falls der Client mit einem Netzwerk verbunden ist, das keine Named Pipes verwendet. Um dieses Handle als gültiges Pipehandle mit [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows zu verwenden, wandeln Sie die Zeichenfolge in eine Ganzzahl um.|  
|SRV_RMTSERVER|Der Server, von dem der Clientprozess angemeldet wird. Wenn die Anmeldung von einem Client stammt, ist dieser Wert eine leere Zeichenfolge.|  
|SRV_ROWSENT|Die Anzahl von Zeilen, die bereits von *srvproc* für die aktuellen Ergebnisse gesendet wurde.|  
|SRV_SPID|Serverthread-ID von *srvproc*. Für erweiterte gespeicherte Prozeduren ist dieser Wert identisch mit der **kpid**-Spalte von **sys.sysprocesses** und kann sich im Laufe der Zeit ändern.|  
|SRV_SPROC_CODEPAGE|Codepage, die der Server verwendet, um Multibytedaten zu interpretieren.|  
|SRV_STATUS|Aktueller Status von *srvproc*: wird ausgeführt oder wurde beendet|  
|SRV_TYPE|Verbindungstyp von *srvproc*. Wenn ein Server zurückgegeben wird, ist *srvproc* von einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Wenn ein Client zurückgegeben wird, stammt *srvproc* von einer DB-Bibliothek oder einem ODBC-Client.|  
|SRV_USER|Der Benutzername der Verbindung.|  
|||  
  
 *len*  
 Zeiger auf eine **int**-Variable, die die Länge des zurückgegebenen *field*-Werts enthält. Wenn *len* NULL ist, wird die Länge der Zeichenfolge nicht zurückgegeben.  
  
## <a name="returns"></a>Rückgabewert  
 Zeiger auf eine auf NULL endende Zeichenfolge, die den aktuellen Wert für das in der SRV_PROC-Struktur angegebene Feld enthält. Wenn das Feld leer ist, wird ein gültiger Zeiger auf eine leere Zeichenfolge zurückgegeben, und *len* enthält den Wert 0. Wenn das Feld unbekannt ist, wird NULL zurückgegeben, und *len* enthält den Wert –1.  
  
> [!IMPORTANT]  
>  Sie sollten den Quellcode der erweiterten gespeicherten Prozeduren sorgfältig prüfen, und Sie sollten die kompilierten DLL-Dateien testen, bevor Sie sie auf einem Produktionsserver installieren. Weitere Informationen zum Überprüfen und Testen der Sicherheit finden Sie im [Security Developer Center](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/).  
  
  
