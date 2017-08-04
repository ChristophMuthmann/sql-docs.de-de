---
title: Administration Tool Befehlszeilenoptionen (Distributed Replay Utility) | Microsoft Docs
ms.custom: 
ms.date: 08/12/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c01b0ed3-67e4-4561-92d2-a8fbb086aca8
caps.latest.revision: 35
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 652600de9d777f13332509fcaae3985daf9c26fc
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="administration-tool-command-line-options-distributed-replay-utility"></a>Befehlszeilenoptionen für das Verwaltungstool (Distributed Replay Utility)
  Das Verwaltungstool [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay ( **DReplay.exe**) ist ein Befehlszeilentool für die Kommunikation mit dem Distributed Replay-Controller. Mit dem Verwaltungstool können Sie Vorgänge auf dem Controller initiieren, überwachen und abbrechen.  
  
 ![Symbol für Themenlink](../../database-engine/configure-windows/media/topic-link.gif "Thema Linksymbol") Weitere Informationen zu den Syntaxkonventionen, die für das Verwaltungstool verwendet werden, finden Sie unter [Transact-SQL-Syntaxkonventionen &#40; Transact-SQL &#41; ](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
## <a name="syntax"></a>Syntax  
  
```  
  
dreplay {preprocess|replay|status|cancel} [options] [-?]}  
  
Usage:  
  
  dreplay preprocess [-m controller] -i input_trace_file  
    -d controller_working_dir [-c config_file] [-f status_interval]  
  
  dreplay replay [-m controller] -d controller_working_dir [-o]  
    [-s target_server] -w clients [-c config_file]  
    [-f status_interval]  
  
  dreplay status [-m controller] [-f status_interval]  
  
  dreplay cancel [-m controller] [-q]   
```  
  
## <a name="remarks"></a>Hinweise  
 Sie können mit **DReplay.exe**die folgenden Befehlszeilenoptionen ausgeben:  
  
 **preprocess**  
 Initiiert die Vorverarbeitungsphase. Der Controller bereitet die Eingabedaten der Ablaufverfolgung, die Sie aus der Produktionsumgebung aufgezeichnet haben, für die Wiedergabe anhand des Zielservers vor.  
  
 **Wiedergabe (replay)**  
 Initiiert die Ereigniswiedergabephase. Der Controller leitet Wiedergabedaten an die angegebenen Clients weiter, startet die verteilte Wiedergabe und synchronisiert die Clients. Optional zeichnet jeder ausgewählte Client die Wiedergabeaktivität auf und speichert Ergebnisdateien der Ablaufverfolgung lokal.  
  
 **status**  
 Fragt den Controller ab und zeigt den aktuellen Status an.  
  
 **cancel**  
 Bricht den Vorgang ab, der derzeit auf dem Controller ausgeführt wird.  
  
 Ausführliche Informationen zur Syntax, einschließlich Befehlsargumenten und Beispielen, finden Sie in den folgenden Themen:  
  
-   [Vorverarbeiten Sie Option &#40; Verwaltungstool "Distributed Replay" &#41;](../../tools/distributed-replay/preprocess-option-distributed-replay-administration-tool.md)  
  
-   [Wiedergabeoption &#40; Verwaltungstool "Distributed Replay" &#41;](../../tools/distributed-replay/replay-option-distributed-replay-administration-tool.md)  
  
-   [Statusoption &#40; Verwaltungstool "Distributed Replay" &#41;](../../tools/distributed-replay/status-option-distributed-replay-administration-tool.md)  
  
-   [Option "Abbrechen" &#40; Verwaltungstool "Distributed Replay" &#41;](../../tools/distributed-replay/cancel-option-distributed-replay-administration-tool.md)  
  
 RPCs werden als RPCs wiedergegeben und nicht als Sprachereignisse.  
  
## <a name="permissions"></a>Berechtigungen  
 Sie müssen das Verwaltungstool als interaktiver Benutzer mit einem lokalen Benutzerkonto oder Domänenbenutzerkonto ausführen. Um ein lokales Benutzerkonto zu verwenden, müssen das Verwaltungstool und der Controller auf demselben Computer ausgeführt werden.  
  
 Weitere Informationen finden Sie unter [Distributed Replay Security](../../tools/distributed-replay/distributed-replay-security.md).  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md)  
  
  

