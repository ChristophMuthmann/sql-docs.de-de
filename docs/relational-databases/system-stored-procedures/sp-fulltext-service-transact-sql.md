---
title: Sp_fulltext_service (Transact-SQL) | Microsoft Docs
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
- sp_fulltext_service
- sp_fulltext_service_TSQL
dev_langs: TSQL
helpviewer_keywords:
- full-text search [SQL Server], properties
- sp_fulltext_service
- Full-Text Search Upgrade Option
ms.assetid: 17a91433-f9b6-4a40-88c4-8c704ec2de9f
caps.latest.revision: "79"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 433afd2d2b17f85acb75fd0b5fddba44e99d3662
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="spfulltextservice-transact-sql"></a>sp_fulltext_service (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Ändert die Servereigenschaften der Volltextsuche für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
||  
|-|  
|**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis zur [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_fulltext_service [ [@action=] 'action'   
     [ , [ @value= ] value ] ]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@action=**] **"***Aktion***"**  
 Ist die Eigenschaft, die geändert oder zurückgesetzt werden soll. *Aktion* ist **nvarchar(100),** hat keinen Standardwert. Eine Liste der einem*c*Tion Eigenschaften, deren Beschreibung und die Werte, die festgelegt werden können, finden Sie in der Tabelle unter der *Wert* Argument. Dieses Argument gibt die folgenden Eigenschaften zurück: Datentyp, aktuell zur Ausführung verwendeter Wert, Minimal- oder Maximalwert und ggf. Status zur Aktualität.  
  
 [  **@value=**] *Wert*  
 Ist der Wert der angegebenen Eigenschaft. *Wert* ist **Sql_variant**, hat den Standardwert NULL. Wenn @value ist null, **Sp_fulltext_service** gibt die aktuelle Einstellung zurück. In dieser Tabelle werden Aktionseigenschaften, zugehörige Beschreibungen und die festzulegenden Werte aufgelistet.  
  
> [!NOTE]  
>  Die folgenden Aktionen werden in einer zukünftigen Version von entfernt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **Clean_up**, **Connect_timeout**, **Data_timeout**, und **Resource_ Verwendung**. Vermeiden Sie die Verwendung dieser Aktionen bei neuen Entwicklungsarbeiten, und planen Sie die Änderung von Anwendungen, die diese Aktionen zurzeit verwenden.  
  
|Aktion|Datentyp|Description|  
|------------|---------------|-----------------|  
|**clean_up**|**int**|Wird nur aus Gründen der Abwärtskompatibilität unterstützt. Der Wert lautet stets 0.|  
|**connect_timeout**|**int**|Wird nur aus Gründen der Abwärtskompatibilität unterstützt. Der Wert lautet stets 0.|  
|**data_timeout**|**int**|Wird nur aus Gründen der Abwärtskompatibilität unterstützt. Der Wert lautet stets 0.|  
|**load_os_resources**|**int**|Gibt an, ob Wörtertrennungen, Wortstammerkennungen und Filter des Betriebssystems mit dieser Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] registriert sind und verwendet werden. Folgende Angaben sind möglich:<br /><br /> 0 = Nur spezifische Filter und Wörtertrennungen für diese Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwenden.<br /><br /> 1 = Betriebssystemfilter und Wörtertrennungen laden.<br /><br /> Standardmäßig ist diese Eigenschaft deaktiviert, damit das Verhalten durch Updates des Systems nicht versehentlich geändert wird. Aktivieren der Verwendung von Betriebssystemressourcen bietet Zugriff auf Ressourcen für Sprachen und Dokumenttypen registriert [!INCLUDE[msCoName](../../includes/msconame-md.md)] Indexdienst, denen keine instanzspezifische Ressource installiert sind. Wenn Sie das Laden von Betriebssystemressourcen aktivieren, stellen Sie sicher, dass die Betriebssystemressourcen vertrauenswürdige signierte Binärdateien sind; andernfalls, sie können nicht geladen werden, wenn **Verify_signature** (siehe unten) auf 1 festgelegt ist.|  
|**master_merge_dop**|**int**|Gibt die Anzahl der Threads an, die vom Masterzusammenführungsprozess verwendet werden soll. Dieser Wert darf die Anzahl der verfügbaren CPUs oder CPU-Kerne nicht überschreiten.<br /><br /> Wenn dieses Argument nicht angegeben wird, verwendet der Dienst den kleinsten der 4 oder die Anzahl der verfügbaren CPUs oder CPU-Kerne.|  
|**pause_indexing**|**int**|Gibt an, ob die Volltextindizierung angehalten werden soll, wenn sie ausgeführt wird, oder fortgesetzt werden soll, wenn sie angehalten wurde.<br /><br /> 0 = Setzt die Aktivitäten zur Volltextindizierung für die Serverinstanz fort.<br /><br /> 1 = Hält die Aktivitäten zur Volltextindizierung für die Serverinstanz an.|  
|**resource_usage**|**int**|Hat in [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] und höheren Versionen keine Funktion und wird ignoriert.|  
|**update_languages**|NULL|Aktualisiert die Liste der für die Volltextsuche registrierten Sprachen. Die Sprachen werden beim Konfigurieren der Indizierung und in Volltextabfragen angegeben. Filter werden verwendet, von dem filterdämonhost gehostet zum Extrahieren von Textinformationen aus entsprechenden Dateiformaten wie .docx gespeichert, in Datentypen, z. B. **Varbinary**, **varbinary(max)**, **Bild** , oder **Xml**, für die Volltextindizierung.<br /><br /> Weitere Informationen finden Sie unter [View or Change Registered Filters and Word Breakers](../../relational-databases/search/view-or-change-registered-filters-and-word-breakers.md).|  
|**upgrade_option**|**int**|Steuert, wie Volltextindizes migriert werden, wenn Sie eine Datenbank von [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] auf eine höhere Version aktualisieren. Diese Eigenschaft ist für die folgenden Aktionen gültig: Upgrade durch Anfügen einer Datenbank, Wiederherstellen einer Datenbanksicherung, Wiederherstellen einer Dateisicherung oder Kopieren der Datenbank mit dem Assistenten zum Kopieren von Datenbanken.<br /><br /> Folgende Angaben sind möglich:<br /><br /> 0 = Volltextkataloge werden mithilfe der neuen und verbesserten Worttrennmodule neu erstellt. Das Neuerstellen von Indizes kann einige Zeit dauern, und nach dem Upgrade ist ggf. eine beträchtliche Menge an CPU-Leistung und Arbeitsspeicherkapazität erforderlich.<br /><br /> 1 = Volltextkataloge werden zurückgesetzt. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Volltextkatalogdateien werden entfernt. Die Metadaten für die Volltextkataloge und die Volltextindizes bleiben jedoch erhalten. Nach der Upgrade wird die Änderungsnachverfolgung für alle Volltextindizes deaktiviert, und Durchforstungen werden nicht automatisch gestartet. Der Katalog bleibt leer, bis Sie ihn nach Beendigung des Upgrades manuell vollständig auffüllen.<br /><br /> 2 = Volltextkataloge werden importiert. Normalerweise ist der Import bedeutend schneller als eine Neuerstellung. Wenn Sie zum Beispiel nur eine CPU verwenden, läuft ein Import etwa zehnmal schneller ab als eine Neuerstellung. Ein importierter Volltextkatalog verwendet jedoch nicht die neuen und erweiterten Wörtertrennungen. Aus diesem Grund sollten Sie zu einem späteren Zeitpunkt eine Neuerstellung der Volltextkataloge durchführen.<br /><br /> Hinweis: Kann Neuerstellung im multithreadmodus ausführen, und wenn mehr als 10 CPUs verfügbar sind, neu erstellen möglicherweise schneller ausgeführt als der Import Falls Sie alle CPUs verwenden können.<br /><br /> Wenn ein Volltextkatalog nicht verfügbar ist, werden die zugehörigen Volltextindizes neu erstellt. Diese Option ist nur für [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] -Datenbanken verfügbar.<br /><br /> Informationen zum Auswählen einer Option für das Volltextupgrade finden Sie unter[Upgrade der Volltextsuche](../../relational-databases/search/upgrade-full-text-search.md).<br /><br /> Hinweis: Diese Eigenschaft festgelegt wird, [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], verwenden Sie die **Volltext Upgradeoption** Eigenschaft. Weitere Informationen finden Sie unter [Verwalten und Überwachen der Volltextsuche auf einer Serverinstanz](../../relational-databases/search/manage-and-monitor-full-text-search-for-a-server-instance.md).|  
|**verify_signature**|**int**|Gibt an, ob ausschließlich signierte Binärdateien durch das Volltextmodul geladen werden. Standardmäßig werden nur vertrauenswürdige signierte Binärdateien geladen.<br /><br /> 1 = Überprüfen, ob ausschließlich vertrauenswürdige signierte Binärdateien geladen werden (Standardeinstellung).<br /><br /> 0 = Nicht überprüfen, ob Binärdateien signiert sind.|  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 Keine  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der der **Serveradmin** feste Serverrolle oder der Systemadministrator kann ausführen **Sp_fulltext_service**.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-updating-the-list-of-registered-languages"></a>A. Aktualisieren der Liste registrierter Sprachen  
 Im folgenden Beispiel wird die Liste der für die Volltextsuche registrierten Sprachen aktualisiert.  
  
```  
EXEC sp_fulltext_service 'update_languages';  
GO  
```  
  
### <a name="b-changing-the-full-text-upgrade-option-to-reset-full-text-catalogs"></a>B. Ändern der Volltext-Upgradeoption, um Volltextkataloge zurückzusetzen  
 Im folgenden Beispiel wird die Volltext-Upgradeoption geändert, sodass Volltextkataloge zurückgesetzt werden. Damit werden die Kataloge vollständig entfernt. In diesem Beispiel werden die optionalen Schlüsselwörter `@action` und `@value` angegeben.  
  
```  
EXEC sp_fulltext_service @action='upgrade_option', @value=1;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Volltextsuche](../../relational-databases/search/full-text-search.md)   
 [FULLTEXTSERVICEPROPERTY &#40; Transact-SQL &#41;](../../t-sql/functions/fulltextserviceproperty-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
