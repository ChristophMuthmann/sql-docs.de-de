---
title: Sp_trace_create (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_trace_create_TSQL
- sp_trace_create
dev_langs: TSQL
helpviewer_keywords: sp_trace_create
ms.assetid: f3a43597-4c5a-4520-bcab-becdbbf81d2e
caps.latest.revision: "38"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: ca00a949b0fe0122f6aba9b8fecfa072374e96f3
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sptracecreate-transact-sql"></a>sp_trace_create (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Erstellt eine Ablaufverfolgungsdefinition. Die neue Ablaufverfolgung weist einen beendeten Status auf.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Verwenden Sie stattdessen erweiterte Ereignisse.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_trace_create [ @traceid = ] trace_id OUTPUT   
          , [ @options = ] option_value   
          , [ @tracefile = ] 'trace_file'   
     [ , [ @maxfilesize = ] max_file_size ]  
     [ , [ @stoptime = ] 'stop_time' ]  
     [ , [ @filecount = ] 'max_rollover_files' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@traceid=** ] *Trace_id*  
 Ist die Nummer des vom zugewiesenen [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in die neue Ablaufverfolgung. Benutzereingaben werden ignoriert. *Trace_id* ist **Int**, hat den Standardwert NULL. Der Benutzer verwendet die *Trace_id* zu identifizieren, ändern und Steuern der Ablaufverfolgung, die von dieser gespeicherten Prozedur definierten Wert.  
  
 [  **@options=** ] *Option_value*  
 Gibt die für die Ablaufverfolgung festgelegten Optionen an. *Option_value* ist **Int**, hat keinen Standardwert. Benutzer können eine Kombination dieser Optionen wählen, indem sie den Summenwert der gewünschten Optionen angeben. Um die Optionen TRACE_FILE_ROLLOVER und SHUTDOWN_ON_ERROR zu aktivieren, geben Sie z. B. **6** für *Option_value*.  
  
 In der folgenden Tabelle werden die Optionen, Beschreibungen und die zugehörigen Werte aufgeführt.  
  
|Optionsname|Optionswert|Description|  
|-----------------|------------------|-----------------|  
|TRACE_FILE_ROLLOVER|**2**|Gibt an, dass die *Max_file_size* erreicht ist, wird die aktuelle Ablaufverfolgungsdatei geschlossen wird und eine neue Datei erstellt wird. Alle neuen Datensätze werden in die neue Datei geschrieben. Die neue Datei hat den gleichen Namen wie die vorige, aber eine ganze Zahl zur Angabe der Abfolge angefügt. Ist z. B. der Name der ursprünglichen Ablaufverfolgungsdatei filename.trc, so wird die nächste Datei mit filename_1.trc benannt, dann folgt filename_2.trc usw.<br /><br /> Wenn weitere Ablaufverfolgungs-Rolloverdateien erstellt werden, erhöht sich der an die Dateinamen angefügte ganzzahlige Wert sequenziell.<br /><br /> SQL Server verwendet den Standardwert des *Max_file_size* (5 MB), wenn diese Option angegeben wird, ohne Angabe eines Werts für *Max_file_size*.|  
|SHUTDOWN_ON_ERROR|**4**|Gibt an, dass SQL Server heruntergefahren wird, wenn die Ablaufverfolgung nicht in die Datei geschrieben werden kann, unabhängig vom Grund. Diese Option ist beim Ausführen von Ablaufverfolgungen zur Sicherheitsüberwachung hilfreich.|  
|TRACE_PRODUCE_BLACKBOX|**8**|Gibt an, dass eine Aufzeichnung der letzten 5 MB der Ablaufverfolgungsinformationen, die vom Server erzeugt wurden, von diesem Server gespeichert werden. TRACE_PRODUCE_BLACKBOX ist mit keiner der anderen Optionen kompatibel.|  
  
 [  **@tracefile=** ] *"**Trace_file**"*  
 Gibt den Speicherort und den Dateinamen zum Schreiben der Ablaufverfolgung an. *Ablaufverfolgungs_Datei* ist **nvarchar(245)** hat keinen Standardwert. *Ablaufverfolgungs_Datei* kann entweder ein lokales Verzeichnis (z. B. N 'C:\MSSQL\Trace\trace.trc') oder ein UNC-Angabe für eine Freigabe oder einen Pfad (N'\\\\*Servername*\\*Sharename* \\ *Directory*\trace.trc').  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Fügt eine **trc** Erweiterung für alle Namen von Ablaufverfolgungsdateien. Wenn die Option TRACE_FILE_ROLLOVER und ein *Max_file_size* angegeben sind, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eine neue Ablaufverfolgungsdatei erstellt, wenn die maximale Größe die ursprünglichen Ablaufverfolgungsdatei vergrößert wird. Die neue Datei hat den gleichen Namen wie die ursprüngliche Datei, aber _ *n*  wird angehängt, um die Angabe der Abfolge, beginnend mit **1**. Wenn die erste Ablaufverfolgungsdatei heißt beispielsweise **filename.trc**, die zweite Datei heißt **filename_1.trc**.  
  
 Wenn Sie die Option TRACE_FILE_ROLLOVER verwenden, sollten im ursprünglichen Dateinamen keine Unterstriche enthalten sein. Bei Verwendung von Unterstrichen tritt Folgendes auf:  
  
-   [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]erfasst nicht automatisch laden, oder Sie werden aufgefordert, die Rolloverdateien (sofern eine dieser dateirolloveroptionen konfiguriert sind).  
  
-   Die Fn_trace_gettable-Funktion lädt keine Rolloverdateien (wenn mithilfe des Parameters der *Number_files* Argument), in dem der ursprüngliche Dateiname endet mit einem Unterstrich und einem numerischen Wert. (Dies gilt nicht für den Unterstrich und die Zahl, die beim Rollover automatisch angehängt werden.)  
  
> [!NOTE]  
>  Um diese beiden Probleme zu umgehen, können Sie die Dateien umbenennen und die Unterstriche im ursprünglichen Dateinamen entfernen. Wenn die ursprüngliche Datei heißt beispielsweise **my_trace.trc**, und die Rolloverdatei heißt **my_trace_1.trc**, können Sie die Dateien umbenennen **mytrace.trc** und **mytrace_1.trc** vor dem Öffnen von Dateien in [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].  
  
 *Ablaufverfolgungs_Datei* kann nicht angegeben werden, wenn die Option TRACE_PRODUCE_BLACKBOX verwendet wird.  
  
 [  **@maxfilesize=** ] *Max_file_size*  
 Gibt die Maximalgröße in Megabyte (MB) an, auf die eine Ablaufverfolgungsdatei vergrößert werden kann. *Wert für Max_file_size* ist **"bigint"**, hat den Standardwert des **5**.  
  
 Wenn dieser Parameter ohne die Option TRACE_FILE_ROLLOVER angegeben wird, beendet die Ablaufverfolgung Aufzeichnung in der Datei an, wenn der verwendete Speicherplatz auf den angegebenen Betrag überschreitet *Max_file_size*.  
  
 [  **@stoptime=** ] **"***Stop_time***"**  
 Gibt das Datum und die Uhrzeit an, zu denen die Ablaufverfolgung beendet wird. *Stop_time* ist **"DateTime"**, hat den Standardwert NULL. Beim Wert NULL wird die Ablaufverfolgung so lange ausgeführt, bis sie manuell beendet oder der Server heruntergefahren wird.  
  
 Wenn beide *Stop_time* und *Max_file_size* angegeben sind, TRACE_FILE_ROLLOVER ist nicht angegeben, die Ablaufverfolgung beendet wird, wenn die angegebene Beendigungszeit oder die maximale Dateigröße erreicht wird. Wenn *Stop_time*, *Max_file_size*, und TRACE_FILE_ROLLOVER angegeben werden, wird die Ablaufverfolgung beendet wird am angegebenen Beendigungszeit, vorausgesetzt die Ablaufverfolgung Auffüllen nicht auf dem Laufwerk.  
  
 [  **@filecount=** ] **"***Max_rollover_files***"**  
 Gibt die maximale Anzahl von Ablaufverfolgungsdateien an, die mit dem gleichen Basisdateinamen verwaltet werden sollen. *MAX_ROLLOVER_FILES* ist **Int**, größer als 1. Dieser Parameter ist nur dann gültig, wenn die Option TRACE_FILE_ROLLOVER angegeben wird. Wenn *Max_rollover_files* angegeben wird, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versucht, die keine verwalten mehr als *Max_rollover_files* Ablaufverfolgungsdateien, indem die älteste Ablaufverfolgungsdatei gelöscht, bevor Sie eine neue Ablaufverfolgungsdatei öffnen. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wird das Alter von Ablaufverfolgungsdateien durch das Anfügen einer Nummer an den Basisdateinamen nachverfolgt.  
  
 Beispielsweise, wenn die *Ablaufverfolgungs_Datei* -Parameter angegeben wird als "c:\mytrace", eine Datei mit dem Namen "c:\mytrace_123.trc" älter als eine Datei mit dem Namen "c:\mytrace_124.trc". Wenn *Max_rollover_files* SQL Server die Datei "c:\mytrace_123.trc" löscht vor dem Erstellen der Ablaufverfolgungsdatei "c:\mytrace_125.trc" ist auf 2 festgelegt.  
  
 Beachten Sie, dass in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] jede Datei nur einmal zu löschen versucht wird und eine Datei nicht gelöscht werden kann, wenn diese von einem anderen Prozess verwendet wird. Wenn in einer anderen Anwendung Ablaufverfolgungsdateien verwendet werden, während die Ablaufverfolgung ausgeführt wird, werden diese Ablaufverfolgungsdateien daher möglicherweise von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] im Dateisystem belassen.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 In der folgenden Tabelle werden die Codewerte beschrieben, die die Benutzer nach Abschluss der gespeicherten Prozedur möglicherweise erhalten.  
  
|Rückgabecode|Beschreibung|  
|-----------------|-----------------|  
|0|Kein Fehler.|  
|1|Unbekannter Fehler.|  
|10|Ungültige Optionen. Wird zurückgegeben, wenn angegebene Optionen inkompatibel sind.|  
|12|Datei nicht erstellt.|  
|13|Nicht genügend Arbeitsspeicher. Wird zurückgegeben, wenn nicht genügend Arbeitsspeicher zum Ausführen der angegebenen Aktion verfügbar ist.|  
|14|Ungültige Beendigungszeit. Wird zurückgegeben, wenn die angegebene Beendigungszeit bereits verstrichen ist.|  
|15|Ungültige Parameter. Wird zurückgegeben, wenn der Benutzer inkompatible Parameter angegeben hat.|  
  
## <a name="remarks"></a>Hinweise  
 **Sp_trace_create** ist ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gespeicherten Prozedur, die viele der zuvor von ausgeführten Aktionen ausführt, **Xp_trace_\***  erweiterte gespeicherte Prozeduren, die in früheren Versionen von SQL Server verfügbar. Verwendung **Sp_trace_create** anstelle von:  
  
-   **xp_trace_addnewqueue**  
  
-   **xp_trace_setqueuecreateinfo**  
  
-   **xp_trace_setqueuedestination**  
  
 **Sp_trace_create** erstellt nur eine Ablaufverfolgungsdefinition. Diese gespeicherte Prozedur kann nicht verwendet werden, um eine Ablaufverfolgung zu starten oder zu ändern.  
  
 Parameter aller gespeicherten Prozeduren der SQL-Ablaufverfolgung (**sp_trace_xx**) haben eine strikte Typbindung. Wenn diese Parameter nicht mit den richtigen Datentypen für Eingabeparameter aufgerufen werden, wie in der Argumentbeschreibung angegeben, gibt die gespeicherte Prozedur einen Fehler zurück.  
  
 Für **Sp_trace_create**, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienstkonto muss über die Schreibberechtigung auf den Ordner der Ablaufverfolgungsdatei verfügen. Wenn das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Dienstkonto kein Administrator auf dem Computer ist, auf dem die Ablaufverfolgungsdatei gespeichert ist, müssen Sie dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Dienstkonto explizit die Schreibberechtigung erteilen.  
  
> [!NOTE]  
>  Sie können mit erstellte Ablaufverfolgungsdatei automatisch laden **Sp_trace_create** in eine Tabelle mit den **Fn_trace_gettable** -Systemfunktion. Informationen zur Verwendung dieser Systemfunktion finden Sie unter [Sys. fn_trace_gettable &#40; Transact-SQL &#41; ](../../relational-databases/system-functions/sys-fn-trace-gettable-transact-sql.md).  
  
 Ein Beispiel zum Verwenden gespeicherter Prozeduren der Ablaufverfolgung finden Sie unter [Erstellen einer Ablaufverfolgung &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/create-a-trace-transact-sql.md).  
  
 **TRACE_PRODUCE_BLACKBOX** weist folgende Merkmale auf:  
  
-   Es handelt sich um eine Rollover-Ablaufverfolgung. Die Standardeinstellung *File_count* 2 können jedoch überschrieben werden vom Benutzer mit *Filecount* Option.  
  
-   Die Standardeinstellung *File_size* wie bei anderen ablaufverfolgungen 5 MB beträgt und geändert werden kann.  
  
-   Es kann kein Dateiname angegeben werden. Die Datei wird als gespeichert werden: **N'%SQLDIR%\MSSQL\DATA\blackbox.trc "**  
  
-   Nur die folgenden Ereignisse und deren Spalten sind in der Ablaufverfolgung enthalten:  
  
    -   **RPC starten**  
  
    -   **BatchStarting**  
  
    -   **Ausnahme**  
  
    -   **Aufmerksamkeit**  
  
-   Für diese Ablaufverfolgung können Ereignisse oder Spalten nicht hinzugefügt oder entfernt werden.  
  
-   Filter können für diese Ablaufverfolgung nicht angegeben werden.  
  
## <a name="permissions"></a>Berechtigungen  
 Benutzer müssen über die ALTER TRACE-Berechtigung verfügen.  
  
## <a name="see-also"></a>Siehe auch  
 ["sp_trace_generateevent" &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-trace-generateevent-transact-sql.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [sp_trace_setfilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql.md)   
 [sp_trace_setstatus &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql.md)   
 [SQL-Ablaufverfolgung](../../relational-databases/sql-trace/sql-trace.md)  
  
  
