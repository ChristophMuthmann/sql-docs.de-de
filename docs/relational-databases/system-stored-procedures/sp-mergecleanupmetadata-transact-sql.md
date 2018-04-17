---
title: Sp_mergecleanupmetadata (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_mergecleanupmetadata_TSQL
- sp_mergecleanupmetadata
helpviewer_keywords:
- sp_mergecleanupmetadata
ms.assetid: 892f8628-4cbe-4cc3-b959-ed45ffc24064
caps.latest.revision: 17
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1f4d2e6e866cff9c4c48e874871f7cfdf113a0d3
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="spmergecleanupmetadata-transact-sql"></a>sp_mergecleanupmetadata (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Sollte verwendet werden, nur in Replikationstopologien mit Servern mit Versionen von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vor [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] Service Pack 1. **Sp_mergecleanupmetadata** können Administratoren ein Cleanup der Metadaten in die **MSmerge_genhistory**, **MSmerge_contents** und **MSmerge_tombstone** Systemtabellen. Diese gespeicherte Prozedur wird auf dem Verleger für die Veröffentlichungsdatenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_mergecleanupmetadata [ [ @publication = ] 'publication' ]  
    [ , [ @reinitialize_subscriber = ] 'reinitialize_subscriber' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@publication =** ] **'***publication***'**  
 Der Name der Veröffentlichung. *Veröffentlichung* ist **Sysname**, hat den Standardwert **%**, die Metadaten für alle Veröffentlichungen bereinigt. Die Veröffentlichung muss bereits vorhanden sein, wenn sie explizit angegeben wird.  
  
 [  **@reinitialize_subscriber =** ] **"***Abonnenten***"**  
 Gibt an, ob der Abonnent erneut zu initialisieren ist. *Abonnenten* ist **nvarchar(5)**, kann **"true"** oder **"false"**, hat den Standardwert **"true"**. Wenn **"true"**, Abonnements für die erneute Initialisierung gekennzeichnet. Wenn **"false"**, die Abonnements werden nicht für die erneute Initialisierung markiert.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_mergecleanupmetadata** sollte verwendet werden, nur in Replikationstopologien mit Servern mit Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vor [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] Service Pack 1. Topologien mit ausschließlich [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] Service Pack 1 oder höher sollten eine auf Metadatencleanup basierende automatische Beibehaltung verwenden. Beim Ausführen dieser gespeicherten Prozedur müssen Sie beachten, dass die Protokolldatei auf dem Computer, auf dem die gespeicherte Prozedur ausgeführt wird, stark anwachsen kann.  
  
> [!CAUTION]  
>  Nach dem **Sp_mergecleanupmetadata** ausgeführt wird, wird standardmäßig alle Abonnements auf den Abonnenten von Veröffentlichungen, die in gespeicherten Metadaten haben **MSmerge_genhistory**, **MSmerge_contents**  und **MSmerge_tombstone** markiert sind für die erneute Initialisierung, alle ausstehenden Änderungen auf dem Abonnenten verloren und die aktuelle Momentaufnahme als veraltet markiert ist.  
  
> [!NOTE]  
>  Wenn mehrere Veröffentlichungen in einer Datenbank vorhanden sind, und eine für diese Veröffentlichungen eine unbegrenzte Aufbewahrungsdauer für Veröffentlichungen verwendet (**@retention**=**0**) ausführen  **Sp_mergecleanupmetadata** keinen Cleanup der Merge Replication Metadaten zur änderungsnachverfolgung für die Datenbank. Aus diesem Grund sollten Sie die unbegrenzte Aufbewahrungsdauer für Veröffentlichungen mit Vorsicht verwenden.  
  
 Beim Ausführen dieser gespeicherten Prozedur können Sie auswählen, ob durch Festlegen von Abonnenten erneut initialisieren der **@reinitialize_subscriber** Parameter **"true"** (Standard) oder **"false"**. Wenn **Sp_mergecleanupmetadata** ausgeführt wird, mit der **@reinitialize_subscriber** Parametersatz auf **"true"**, eine Momentaufnahme wird erneut auf dem Abonnenten angewendet, selbst wenn das Abonnement wurde erstellt, ohne dass eine anfangsmomentaufnahme (beispielsweise, wenn die momentaufnahmedaten und das Schema wurden manuell angewendet oder auf dem Abonnenten bereits vorhandenen Zeichenfolgenform). Festlegen des Parameters auf **"false"** sollte mit Vorsicht, verwendet werden, da die Veröffentlichung ist nicht erneut initialisiert werden, Sie sicherstellen müssen, dass Daten auf dem Verleger und Abonnent synchronisiert werden.  
  
 Unabhängig vom Wert der **@reinitialize_subscriber**, **Sp_mergecleanupmetadata** schlägt fehl, wenn vorhanden sind Mergeprozesse, die versuchen, Änderungen an einen Verleger oder einen Wiederveröffentlichungsabonnenten am hochgeladen werden. der Zeitpunkt, zu die gespeicherte Prozedur aufgerufen wird.  
  
 **Ausführen von Sp_mergecleanupmetadata mit @reinitialize_subscriber = "true":**  
  
1.  Es ist nicht vorgeschrieben, wird jedoch empfohlen, alle Updates der Veröffentlichungs- und Abonnementdatenbanken zu beenden. Falls Updates fortgesetzt werden, gehen alle seit der letzten Zusammenführung beim Abonnenten vorgenommenen Updates beim erneuten Initialisieren der Veröffentlichung verloren. Die Datenkonvergenz bleibt jedoch erhalten.  
  
2.  Ausführen eines Mergeprozesses durch Ausführen des Merge-Agents. Wir empfehlen die Verwendung der **– Validate** Befehlszeilenoption Agent auf den einzelnen Abonnenten, wenn Sie den Merge-Agent ausführen. Wenn Sie Mergeprozesse im fortlaufenden Modus ausgeführt werden, finden Sie unter *spezielle Überlegungen zu Mergeprozessen im fortlaufenden Modus* weiter unten in diesem Abschnitt.  
  
3.  Nachdem alle Mergeprozesse abgeschlossen wurden, führen Sie **Sp_mergecleanupmetadata**.  
  
4.  Führen Sie **Sp_reinitmergepullsubscription** auf allen Abonnenten benannte oder anonyme Pullabonnements zum Sicherstellen der Datenkonvergenz verwenden.  
  
5.  Wenn Sie Mergeprozesse im fortlaufenden Modus ausgeführt werden, finden Sie unter *spezielle Überlegungen zu Mergeprozessen im fortlaufenden Modus* weiter unten in diesem Abschnitt.  
  
6.  Generieren Sie Snaphotdateien für alle beteiligten Mergeveröffentlichungen auf allen Ebenen erneut. Wenn Sie das Zusammenführen versuchen, ohne die Momentaufnahme zuvor erneut zu generieren, wird eine Eingabeaufforderung angezeigt, die Sie dazu auffordert, die Momentaufnahme erneut zu generieren.  
  
7.  Sichern Sie die Veröffentlichungsdatenbank. Wenn dies versäumt wird, kann es zu einem Mergefehler führen, nachdem die Veröffentlichungsdatenbank wiederhergestellt wurde.  
  
 **Ausführen von Sp_mergecleanupmetadata mit @reinitialize_subscriber = "false":**  
  
1.  Beenden Sie **alle** Updates der Veröffentlichungs- und Abonnementdatenbanken.  
  
2.  Ausführen eines Mergeprozesses durch Ausführen des Merge-Agents. Wir empfehlen die Verwendung der **– Validate** Befehlszeilenoption Agent auf den einzelnen Abonnenten, wenn Sie den Merge-Agent ausführen. Wenn Sie Mergeprozesse im fortlaufenden Modus ausgeführt werden, finden Sie unter *spezielle Überlegungen zu Mergeprozessen im fortlaufenden Modus* weiter unten in diesem Abschnitt.  
  
3.  Nachdem alle Mergeprozesse abgeschlossen wurden, führen Sie **Sp_mergecleanupmetadata**.  
  
4.  Wenn Sie Mergeprozesse im fortlaufenden Modus ausgeführt werden, finden Sie unter *spezielle Überlegungen zu Mergeprozessen im fortlaufenden Modus* weiter unten in diesem Abschnitt.  
  
5.  Generieren Sie Snaphotdateien für alle beteiligten Mergeveröffentlichungen auf allen Ebenen erneut. Wenn Sie das Zusammenführen versuchen, ohne die Momentaufnahme zuvor erneut zu generieren, wird eine Eingabeaufforderung angezeigt, die Sie dazu auffordert, die Momentaufnahme erneut zu generieren.  
  
6.  Sichern Sie die Veröffentlichungsdatenbank. Wenn dies versäumt wird, kann es zu einem Mergefehler führen, nachdem die Veröffentlichungsdatenbank wiederhergestellt wurde.  
  
 **Besonderheiten bei der Mergeprozesse im fortlaufenden Modus**  
  
 Wenn Sie Mergeprozesse im fortlaufenden Modus ausführen, müssen Sie einen der folgenden Schritte ausführen:  
  
-   Beenden Sie den Merge-Agent, und führen Sie dann einen weiteren Mergeprozess ohne die **-Continuous** Parameter wurde angegeben.  
  
-   Deaktivieren Sie die Veröffentlichung mit **Sp_changemergepublication** um sicherzustellen, dass alle im fortlaufenden Modus Mergeprozesse, die den Veröffentlichungsstatus abrufen fehlschlagen.  
  
    ```  
    EXEC central..sp_changemergepublication @publication = 'dynpart_pubn', @property = 'status', @value = 'inactive'  
    ```  
  
 Nach Abschluss von Schritt 3 der Ausführung **Sp_mergecleanupmetadata**, Mergeprozesse im fortlaufenden Modus, die basierend auf der Sie sie gestoppt fortsetzen. Führen Sie einen der folgenden Schritte aus:  
  
-   Hinzufügen der **– Continuous** -Parameter für den Merge-Agent zurück.  
  
-   Reaktivieren Sie die Veröffentlichung mit **Sp_changemergepublication.**  
  
    ```  
    EXEC central..sp_changemergepublication @publication = 'dynpart_pubn', @property = 'status', @value = 'active'  
    ```  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der der **Sysadmin** feste Serverrolle oder **Db_owner** feste Datenbankrolle können ausführen **Sp_mergecleanupmetadata**.  
  
 Zum Verwenden dieser gespeicherten Prozedur muss der Verleger [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] ausführen. Die Abonnenten müssen ausgeführt werden, entweder [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] oder [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0, Service Pack 2.  
  
## <a name="see-also"></a>Siehe auch  
 [MSmerge_genhistory &#40;Transact-SQL&#41;](../../relational-databases/system-tables/msmerge-genhistory-transact-sql.md)   
 [MSmerge_contents &#40;Transact-SQL&#41;](../../relational-databases/system-tables/msmerge-contents-transact-sql.md)   
 [MSmerge_tombstone &#40;Transact-SQL&#41;](../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md)  
  
  
