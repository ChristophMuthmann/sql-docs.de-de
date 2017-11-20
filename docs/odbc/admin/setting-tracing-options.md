---
title: Festlegen von Ablaufverfolgungsoptionen | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: admin
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Visual Studio Analyzer tracing [ODBC]
- ODBC data source administrator [ODBC], tracing options
- tracing options [ODBC], ODBC data source administrator
ms.assetid: 44404a79-b716-4bc1-9ffb-70cd8239d237
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b11d6337c2e0ca2853838d964842be536454c5f4
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="setting-tracing-options"></a>Festlegen von Ablaufverfolgungsoptionen
Die **Ablaufverfolgung** auf der Registerkarte die **ODBC-Datenquellenadministrator** Dialogfeld können Sie konfigurieren ODBC-Funktionsaufrufe werden nachverfolgt.  
  
## <a name="how-tracing-works"></a>Funktionsweise der Ablaufverfolgung  
 Beim Starten der Ablaufverfolgung aus der **Ablaufverfolgung** Registerkarte der Treiber-Manager werden alle ODBC-Funktionsaufrufe protokolliert, für alle anschließend Anwendungen ausgeführt werden. ODBC-Funktionsaufrufe von Anwendungen, die ausgeführt werden, bevor die Ablaufverfolgung gestartet wird, werden nicht protokolliert. ODBC-Funktionsaufrufe werden in einer Protokolldatei aufgezeichnet, die Sie angeben.  
  
 Ablaufverfolgung wird angehalten, nur, nachdem Sie auf **Ablaufverfolgung jetzt beenden**. Denken Sie daran, dass während der Ablaufverfolgung wird weiterhin die Protokolldatei erhöhen, sodass dies wirkt sich die Leistung von alle ODBC-Anwendungen auf.  
  
 Weitere Informationen zur Ablaufverfolgung finden Sie unter [Ablaufverfolgung](../../odbc/reference/develop-app/tracing.md).  
  
### <a name="changes-in-odbc-tracing"></a>Änderungen in ODBC-Protokollierung  
 ODBC-Protokollierung wurde vor dem MDAC 2.7 SP2 nur zulässig, auf einer computerweiten Basis erfolgt in der Ablaufverfolgung verfügbar gemachten Details zu allen ODBC-Anwendungen, die Identitäten unter aufzeichnet. Diese enthalten die Ablaufverfolgung für ODBC-bezogenen Aktivitäten, die für Prozesse, die erstellt oder im Auftrag von anderen lokalen Benutzerkonten und Integrierte Sicherheitsprinzipale wie z. B. die Local Service und Network Service ausgeführt auftreten können.  
  
 Standardmäßig werden ODBC-Ablaufverfolgung jetzt Einzelbenutzer-Modus verwendet. Wenn Sie ein lokaler Administrator sind, können jedoch Sie weiterhin computerweite Ablaufverfolgung aktivieren, indem mithilfe von ODBC-Datenquellen-Administrator.  
  
 So konfigurieren Sie den Ablaufverfolgungsmodus ODBC:  
  
1.  Wenn es erforderlich ist, melden Sie sich mit einem Konto an, die die Mitgliedschaft in der lokalen Administratorengruppe sein muss.  
  
2.  Öffnen Sie von der Verwaltung ODBC-Datenquellen-Administrator.  
  
3.  Klicken Sie auf die **Tracing** Registerkarte.  
  
4.  Konfigurieren Sie den Modus mit der **computerweite Ablaufverfolgung für alle Benutzeridentitäten** Kontrollkästchen:  
  
5.  Aktivieren Sie das Kontrollkästchen zum Aktivieren der Ablaufverfolgung computerweite.  
  
6.  Deaktivieren Sie das Kontrollkästchen, damit wieder der Einzelbenutzer-Ablaufverfolgung.  
  
7.  Klicken Sie auf **Anwenden**.  
  
> [!NOTE]  
>  Wenn Sie die Ablaufverfolgung bereits in einem Modus gestartet haben, müssen Sie Ablaufverfolgung zu beenden, und wechseln Sie zu anderen Modus für den Modus erfolgreich geändert werden.  
  
> [!IMPORTANT]  
>  Computerweite Ablaufverfolgung sollte nur aktiviert werden, wenn er benötigt wird; Andernfalls sollte gelassen werden deaktiviert.  
  
## <a name="visual-studio-analyzer-tracing"></a>Visual Studio Analyzer-Ablaufverfolgung  
  
> [!IMPORTANT]  
>  Unterstützung für Visual Studio Analyzer wurde entfernt ab Windows 8 (Visual Studio Analyzer wurde nur in früheren Versionen von Visual Studio enthalten.). Verwenden Sie eine Alternative zur Problembehandlung Mechanismus BID-Ablaufverfolgung.  
  
 Visual Studio® Analyzer-Ablaufverfolgung bietet, Leistung und Debuginformationen über die ODBC-Ebene. Aller ausgehenden Ereignisse werden auf der obersten Ebene Schnittstellenebene als genau ein Bild möglichst dargestellt in ODBC-Komponenten zu Verweildauer ausgelöst. Visual Studio Analyzer Tracing erfordert Ereignisquelle verwendet wurden, registrieren, wenn die Quelle eingerichtet ist. Weitere Informationen über diese Art von Ablaufverfolgung finden Sie in der Visual Studio-Dokumentation.

