---
title: Befehlszeilenoptionen für das Verwaltungstool (Distributed Replay-Hilfsprogramm) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 08/12/2016
ms.prod: sql
ms.prod_service: sql-tools
ms.component: distributed-replay
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: c01b0ed3-67e4-4561-92d2-a8fbb086aca8
caps.latest.revision: 35
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f939ad0cc8f8711b69a7e67401954c20690e7b7d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MTE
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="administration-tool-command-line-options-distributed-replay-utility"></a>Befehlszeilenoptionen für das Verwaltungstool (Distributed Replay Utility)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Das Verwaltungstool [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay ( **DReplay.exe**) ist ein Befehlszeilentool für die Kommunikation mit dem Distributed Replay-Controller. Mit dem Verwaltungstool können Sie Vorgänge auf dem Controller initiieren, überwachen und abbrechen.  
  
 ![Artikellinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") Weitere Informationen zu den Syntaxkonventionen für das Verwaltungstool finden Sie unter [Transact-SQL-Syntaxkonventionen &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
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
  
## <a name="remarks"></a>Remarks  
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
  
-   [Vorverarbeitungsoption &#40;Verwaltungstool „Distributed Replay“&#41;](../../tools/distributed-replay/preprocess-option-distributed-replay-administration-tool.md)  
  
-   [Wiedergabeoption &#40;Verwaltungstool „Distributed Replay“&#41;](../../tools/distributed-replay/replay-option-distributed-replay-administration-tool.md)  
  
-   [Statusoption &#40;Verwaltungstool „Distributed Replay“&#41;](../../tools/distributed-replay/status-option-distributed-replay-administration-tool.md)  
  
-   [Option zum Abbrechen &#40;Verwaltungstool „Distributed Replay“&#41;](../../tools/distributed-replay/cancel-option-distributed-replay-administration-tool.md)  
  
 RPCs werden als RPCs wiedergegeben und nicht als Sprachereignisse.  
  
## <a name="permissions"></a>Berechtigungen  
 Sie müssen das Verwaltungstool als interaktiver Benutzer mit einem lokalen Benutzerkonto oder Domänenbenutzerkonto ausführen. Um ein lokales Benutzerkonto zu verwenden, müssen das Verwaltungstool und der Controller auf demselben Computer ausgeführt werden.  
  
 Weitere Informationen finden Sie unter [Distributed Replay Security](../../tools/distributed-replay/distributed-replay-security.md).  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md)  
  
  
