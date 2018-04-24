---
title: ALTER DATABASE SET HADR (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: sql-database
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- SET HADR
- SET_HADR_TSQL
- HADR_TSQL
- HADR
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER DATABASE statement, AlwaysOn Availability Group
- ALTER DATABASE statement, SET HADR options
- Availability Groups [SQL Server], configuring
- Availability Groups [SQL Server], Transact-SQL statements
- Availability Groups [SQL Server], databases
ms.assetid: 20e6e803-d6d5-48d5-b626-d1e0a73d174c
caps.latest.revision: 44
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 33222606ec1930a5a53cd91aeea96bb0328288f7
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="alter-database-transact-sql-set-hadr"></a>ALTER DATABASE (Transact-SQL) SET HADR 
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Dieses Thema enthält die ALTER DATABASE-Syntax zum Festlegen von [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]-Optionen in einer sekundären Datenbank. Pro ALTER DATABASE-Anweisung ist nur eine SET HADR-Option erlaubt. Diese Optionen werden nur auf sekundären Replikaten unterstützt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
ALTER DATABASE database_name  
   SET HADR   
   {  
        { AVAILABILITY GROUP = group_name | OFF }  
   | { SUSPEND | RESUME }  
   }  
[;]  
```  
  
## <a name="arguments"></a>Argumente  
 *database_name*  
 Der Name der sekundären Datenbank, die geändert werden soll.  
  
 SET HADR  
 Führt den angegebenen Befehl [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]-Befehl in der angegebenen Datenbank aus.  
  
 { AVAILABILITY GROUP **=***group_name* | OFF }  
 Verknüpft die Verfügbarkeitsdatenbank mit der angegebenen Verfügbarkeitsgruppe oder entfernt sie hieraus.  
  
 *group_name*  
 Verknüpft die angegebene Datenbank auf dem sekundären Replikat, das von der Serverinstanz gehostet wird, auf der Sie den Befehl ausführen, mit der durch group_name angegebenen Verfügbarkeitsgruppe.  
  
 Für diesen Vorgang müssen folgende Voraussetzungen gegeben sein:  
  
-   Die Datenbank muss der Verfügbarkeitsgruppe auf dem primären Replikat bereits hinzugefügt worden sein.  
  
-   Das primäre Replikat muss aktiv sein. Informationen zur Problembehandlung für ein inaktives primäres Replikat finden Sie unter [Problembehandlung für die Always On-Verfügbarkeitsgruppenkonfiguration (SQL Server)](http://go.microsoft.com/fwlink/?LinkId=225834).  
  
-   Das primäre Replikat muss online sein, und das sekundäre Replikat muss mit dem primären Replikat verbunden sein.  
  
-   Die sekundäre Datenbank muss mit WITH NORECOVERY aus einer aktuellen Datenbank und Protokollsicherungen der primären Datenbank wiederhergestellt werden und mit einer Protokollsicherung enden, die so aktuell ist, dass die sekundäre Datenbank den gleichen Stand hat wie die primäre Datenbank.  
  
    > [!NOTE]  
    >  Um der Verfügbarkeitsgruppe eine Datenbank hinzuzufügen, stellen Sie eine Verbindung mit der Serverinstanz her, die das primäre Replikat hostet, und verwenden Sie dann die Anweisung [ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md)*group_name* ADD DATABASE *database_name*.  
  
 Weitere Informationen finden Sie unter [Verknüpfen einer sekundären Datenbank mit einer Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/join-a-secondary-database-to-an-availability-group-sql-server.md)aktiviert sind, eine Always On-Verfügbarkeitsgruppe zu erstellen.  
  
 OFF  
 Entfernt die angegebene sekundäre Datenbank aus der Verfügbarkeitsgruppe.  
  
 Das Entfernen einer sekundären Datenbank ist sinnvoll, wenn diese gegenüber der primären Datenbank stark veraltet ist und Sie nicht warten möchten, bis die sekundäre Datenbank wieder auf dem Stand der primären Datenbank ist. Sie können die sekundäre Datenbank auch nach dem Entfernen aktualisieren, indem Sie eine Sequenz von Sicherungen wiederherstellen, die mit einer aktuellen Protokollsicherung enden (mittels RESTORE … WITH NORECOVERY).  
  
> [!IMPORTANT]  
>  Um eine Verfügbarkeitsdatenbank vollständig aus einer Verfügbarkeitsgruppe zu entfernen, stellen Sie eine Verbindung mit der Serverinstanz her, die das primäre Replikat hostet, und verwenden Sie die Anweisung [ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md)*group_name* REMOVE DATABASE *availability_database_name*. Weitere Informationen finden Sie unter [Entfernen einer primären Datenbank aus einer Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/remove-a-primary-database-from-an-availability-group-sql-server.md).  
  
 SUSPEND  
 Hält das Verschieben von Daten in einer sekundären Datenbank an. Ein SUSPEND-Befehl gibt einen Wert zurück, sobald es vom Replikat akzeptiert wurde, das die Zieldatenbank hostet. Das Anhalten der Datenbank ist jedoch dadurch asynchron.  
  
 Der Umfang der Auswirkungen hängt davon ab, wo Sie die ALTER DATABASE-Anweisung ausführen:  
  
-   Wenn Sie eine sekundäre Datenbank auf einem sekundären Replikat anhalten, wird nur die lokale sekundäre Datenbank angehalten. Vorhandene Verbindungen mit dem lesbaren sekundären Replikat können weiter verwendet werden. Neue Verbindungen mit der angehaltenen Datenbank auf dem lesbaren sekundären Replikat werden erst zugelassen, wenn Datenverschiebung fortgesetzt wird.  
  
-   Wenn Sie eine Datenbank auf dem primären Replikat anhalten, wird die Datenverschiebung in die entsprechenden sekundären Datenbanken auf jedem sekundären Replikat angehalten. Vorhandene Verbindungen in einem sekundären Replikat bleiben verwendbar, und neue Verbindungen für beabsichtigte Lesevorgänge stellen keine Verbindung mit den lesbaren sekundären Replikaten her.  
  
-   Wenn die Datenverschiebung aufgrund eines erzwungenen manuellen Failovers angehalten wird, werden Verbindungen mit dem neuen sekundären Replikat nicht zugelassen, solange die Datenverschiebung angehalten ist.  
  
 Wenn eine Datenbank auf einem sekundären Replikat angehalten ist, werden die Datenbank und das Replikat nicht mehr synchronisiert und als NOT SYNCHRONIZED markiert.  
  
> [!IMPORTANT]  
>  Während eine sekundäre Datenbank angehalten ist, sammelt die Sendewarteschlange der entsprechenden primären Datenbank nicht gesendete Transaktionsprotokoll-Datensätze. Verbindungen mit dem sekundären Replikat geben Daten zurück, die verfügbar waren, als die Datenverschiebung angehalten wurde.  
  
> [!NOTE]  
>  Das Anhalten und Fortsetzen einer sekundären Always On-Datenbank wirkt sich nicht direkt auf die Verfügbarkeit der primären Datenbank aus, das Anhalten einer sekundären Datenbank kann sich jedoch auf Redundanz- und Failoverfunktionen für die primäre Datenbank auswirken, bis die angehaltene sekundären Datenbank fortgesetzt wird. Dies steht im Gegensatz zur Datenbankspiegelung, bei der der Spiegelungsstatus sowohl in der Spiegeldatenbank als auch in der Prinzipaldatenbank angehalten wird, bis die Spiegelung fortgesetzt wird. Durch Anhalten einer primären AlwaysOn-Datenbank wird die Datenverschiebung auf allen entsprechenden sekundären Datenbanken angehalten, und Redundanz- und Failoverfunktionen für diese Datenbank werden deaktiviert, bis die primäre Datenbank fortgesetzt wird.  
  
 Weitere Informationen finden Sie weiter unten in diesem Thema unter [Anhalten einer Verfügbarkeitsdatenbank &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/suspend-an-availability-database-sql-server.md).  
  
 RESUME  
 Nimmt eine angehaltene Datenverschiebung in die angegebene sekundäre Datenbank wieder auf. Ein RESUME-Befehl gibt einen Wert zurück, sobald es vom Replikat akzeptiert wurde, das die Zieldatenbank hostet. Das Fortsetzen der Datenbank ist jedoch dadurch asynchron.  
  
 Der Umfang der Auswirkungen hängt davon ab, wo Sie die ALTER DATABASE-Anweisung ausführen:  
  
-   Wenn Sie eine sekundäre Datenbank auf einem sekundären Replikat wieder aufnehmen, wird nur die lokale sekundäre Datenbank wieder aufgenommen. Die Datenverschiebung wird fortgesetzt, außer die Datenbank wurde auch auf dem primären Replikat angehalten.  
  
-   Wenn Sie eine Datenbank auf dem primären Replikat wieder aufnehmen, wird Datenverschiebung auf alle sekundären Replikate fortgesetzt, auf denen die entsprechende sekundäre Datenbank nicht ebenfalls lokal angehalten wurde. Um eine sekundäre Datenbank fortzusetzen, die einzeln auf einem sekundären Replikat angehalten wurde, stellen Sie eine Verbindung mit der Serverinstanz her, die das sekundäre Replikat hostet, und setzen Sie die Datenbank dort fort.  
  
     Im Modus für synchrone Commits ändert sich der Datenbankstatus in SYNCHRONIZING. Wenn zurzeit keine andere Datenbank angehalten ist, ändert sich der Replikatstatus ebenfalls in SYNCHRONIZING.  
  
     Weitere Informationen finden Sie weiter unten in diesem Thema unter [Fortsetzen einer Verfügbarkeitsdatenbank &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/resume-an-availability-database-sql-server.md)anhalten.  
  
## <a name="database-states"></a>Datenbankstatus  
 Wenn eine sekundäre Datenbank mit einer Verfügbarkeitsgruppe verbunden wird, ändert das lokale sekundäre Replikat den Status dieser sekundären Datenbank von RESTORING in ONLINE. Wenn eine sekundäre Datenbank aus der Verfügbarkeitsgruppe entfernt wird, wird sie vom lokalen sekundären Replikat auf den Status RESTORING zurückgesetzt. Dies ermöglicht Ihnen, nachfolgende Protokollsicherungen aus der primären Datenbank auf diese sekundäre Datenbank anzuwenden.  
  
## <a name="restrictions"></a>Restrictions  
 Führen Sie ALTER DATABASE-Anweisungen außerhalb von Transaktionen und Batches aus.  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>Berechtigungen  
 Erfordert die ALTER-Berechtigung für die Datenbank. Das Verknüpfen einer Datenbank mit einer Verfügbarkeitsgruppe erfordert die Mitgliedschaft in der festen **db_owner**-Datenbankrolle.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird die sekundäre Datenbank `AccountsDb1` mit dem lokalen sekundären Replikat der `AccountsAG`-Verfügbarkeitsgruppe verknüpft.  
  
```  
ALTER DATABASE AccountsDb1 SET HADR AVAILABILITY GROUP = AccountsAG;  
```  
  
> [!NOTE]  
>  Unter [Erstellen einer Verfügbarkeitsgruppe &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/create-an-availability-group-transact-sql.md) können Sie die Verwendung dieser [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung im Kontext sehen.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-availability-group-transact-sql.md)   
 [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-availability-group-transact-sql.md)   
 [Übersicht über Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md) [Problembehandlung für die Always On-Verfügbarkeitsgruppenkonfiguration &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/troubleshoot-always-on-availability-groups-configuration-sql-server.md) 
  
  
