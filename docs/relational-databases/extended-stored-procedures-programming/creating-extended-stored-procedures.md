---
title: Erstellen erweiterter gespeicherter Prozeduren | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: extended-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- warnings [SQL Server]
- extended stored procedures [SQL Server], debugging
- extended stored procedures [SQL Server], creating
- messages [SQL Server], extended stored procedures
ms.assetid: 9f7c0cdb-6d88-44c0-b049-29953ae75717
caps.latest.revision: "38"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 66111dcdc5c69df0edbda0f57143873c89e12ac1
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="creating-extended-stored-procedures"></a>Erstellen erweiterter gespeicherter Prozeduren
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Verwenden Sie stattdessen die CLR-Integration.  
  
 Eine erweiterte gespeicherte Prozedur ist eine Funktion mit einem Prototyp:  
  
 SRVRETCODE *Xp_extendedProcName* **(**SRVPROC  **\*);**  
  
 Die Verwendung des Präfix xp_ ist optional. Bei den Namen erweiterter gespeicherter Prozeduren wird die Groß-/Kleinschreibung beachtet, wenn in [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen auf sie verwiesen wird, und zwar unabhängig von der auf dem Server installierten Codepage/Sortierreihenfolge. Wenn Sie eine DLL erstellen:  
  
-   Wenn ein Einstiegspunkt erforderlich ist, schreiben Sie eine DllMain-Funktion.  
  
     Diese Funktion ist optional; wenn Sie sie nicht im Quellcode angeben, erstellt der Compiler einen Link zu seiner eigenen Version, die keine Aktionen ausführt, außer TRUE zurückzugeben. Wenn Sie eine DllMain-Funktion bereitstellen, ruft das Betriebssystem diese Funktion auf, wenn ein Thread oder ein Prozess mit der DLL verbunden oder von ihr getrennt wird.  
  
-   Alle von außerhalb der DLL aufgerufenen Funktionen (alle e-Funktionen einer erweiterten gespeicherten Prozedur) müssen exportiert werden.  
  
     Sie können eine Funktion exportieren, indem Sie seinen Namen im Abschnitt EXPORTS einer DEF-Datei auflisten, oder Sie können den Funktionsnamen im Quellcode __declspec(dllexport), eine Microsoft-compilererweiterung Präfix (Beachten Sie, dass \__declspec() mit zwei unterstrichen beginnt).  
  
 Diese Dateien sind zum Erstellen einer DLL einer erweiterten gespeicherten Prozedur erforderlich.  
  
|File|Description|  
|----------|-----------------|  
|Srv.h|API-Headerdatei für erweiterte gespeicherte Prozeduren|  
|Opends60.lib|Importbibliothek für Opends60.dll|  
  
 Um eine DLL für eine erweiterte gespeicherte Prozedur zu erstellen, erstellen Sie ein Projekt des Typs Dynamic Link Library. Weitere Informationen über das Erstellen einer DLL finden Sie in der Dokumentation zur Entwicklungsumgebung.  
  
 Es wird empfohlen, dass alle DLLs für erweiterte gespeicherte Prozeduren die folgende Funktion implementieren und exportieren:  
  
```  
__declspec(dllexport) ULONG __GetXpVersion()  
{  
   return ODS_VERSION;  
}  
```  
  
> [!NOTE]  
>  __declspec (dllexport) ist eine Microsoft-spezifische Compilererweiterung. Wenn Ihr Compiler diese Direktive nicht unterstützt, sollten Sie diese Funktion in Ihre DEF-Datei im Abschnitt EXPORTS exportieren.  
  
 Wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wird gestartet, mit dem Ablaufverfolgungsflag kennzeichnen - T260 oder wenn ein Benutzer mit Systemadministratorprivilegien DBCC TRACEON (260) durchführt und wenn die erweiterte gespeicherte Prozeduren __GetXpVersion() nicht unterstützt, eine Warnmeldung (Fehler 8131: Erweiterte gespeicherte Prozedur DLL '% s' exportiert keine \__GetXpVersion().) wird im Fehlerprotokoll ausgegeben. (Beachten Sie, dass \__GetXpVersion() mit zwei unterstrichen beginnt.)  
  
 Wenn die DLL für die erweiterte gespeicherte Prozedur __GetXpVersion() exportiert, die von der Funktion zurückgegebene Version jedoch niedriger ist als die vom Server benötigte Version, wird eine Warnmeldung ausgegeben. Diese gibt die von der Funktion zurückgegebene Version und die vom Server benötigte Version im Fehlerprotokoll an. Wenn Sie diese Meldung erhalten, die Sie einen falschen Wert von Rückgabe \__GetXpVersion(), oder Sie sind mit einer älteren Version von srv.h kompilieren.  
  
> [!NOTE]  
>  SetErrorMode, eine [!INCLUDE[msCoName](../../includes/msconame-md.md)] Win32 Funktion, sollte in erweiterten gespeicherten Prozeduren nicht aufgerufen werden.  
  
 Es wird empfohlen, dass eine erweiterte gespeicherte Prozedur mit langer Ausführungszeit in regelmäßigen Abständen srv_got_attention aufruft, damit die Prozedur sich selbst beenden kann, falls die Verbindung unterbrochen oder der Batch abgebrochen wird.  
  
 Wenn Sie eine DLL für eine erweiterte gespeicherte Prozedur debuggen möchten, kopieren Sie sie in das Verzeichnis [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\Binn. Um die ausführbare Datei für die Debugsitzung angeben möchten, geben Sie den Pfad und Dateiname der dem [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausführbare Datei (beispielsweise C:\Program Files\Microsoft SQL Server\MSSQL13. MSSQLSERVER\MSSQL\Binn\Sqlservr.exe). Weitere Informationen zu Sqlservr-Argumenten finden Sie unter [sqlservr (Anwendung)](../../tools/sqlservr-application.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Srv_got_attention &#40; Erweiterte gespeicherte Prozedur API &#41;](../../relational-databases/extended-stored-procedures-reference/srv-got-attention-extended-stored-procedure-api.md)  
  
  
