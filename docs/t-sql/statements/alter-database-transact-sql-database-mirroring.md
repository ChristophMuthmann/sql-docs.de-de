---
title: ALTER DATABASE Database Mirroring (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/17/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- witness [SQL Server], establishing
- manual failover [SQL Server]
- ALTER DATABASE statement, database mirroring
- database mirroring [SQL Server], Transact-SQL
ms.assetid: 27a032ef-1cf6-4959-8e67-03d28c4b3465
caps.latest.revision: "22"
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 54396925abb0e8eb2d6006ffdd4048551792d6db
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="alter-database-transact-sql-database-mirroring"></a>ALTER DATABASE (Transact-SQL) Database Mirroring 
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

    
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Verwendung [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] stattdessen.  
  
 Steuert die Datenbankspiegelung für eine Datenbank. Werte, die mit den Optionen für die Datenbankspiegelung angegeben werden, gelten für Kopien der Datenbank sowie für die gesamte Sitzung zur Datenbankspiegelung. Nur ein \<Database_mirroring_option > pro ALTER DATABASE-Anweisung zulässig ist.  
  
> [!NOTE]  
>  Es wird empfohlen, dass die Konfiguration der datenbankspiegelung Spitzenzeiten, da die Konfiguration die Leistung auswirken kann.  
  
 ALTER DATABASE-Optionen finden Sie unter [ALTER DATABASE &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-database-transact-sql.md). ALTER DATABASE SET-Optionen finden Sie unter [ALTER DATABASE SET-Optionen &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-database-transact-sql-set-options.md).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
ALTER DATABASE database_name   
SET { <partner_option> | <witness_option> }  
  <partner_option> ::=  
    PARTNER { = 'partner_server'   
            | FAILOVER   
            | FORCE_SERVICE_ALLOW_DATA_LOSS  
            | OFF  
            | RESUME   
            | SAFETY { FULL | OFF }  
            | SUSPEND   
            | TIMEOUT integer  
            }  
  <witness_option> ::=  
    WITNESS { = 'witness_server'   
            | OFF   
            }  
  
```  
  
## <a name="arguments"></a>Argumente  
  
> [!IMPORTANT]  
>  Ein SET PARTNER- oder SET WITNESS-Befehl kann nach der Eingabe erfolgreich abgeschlossen werden und dennoch später einen Fehler generieren.  
  
> [!NOTE]  
>  Die Optionen der ALTER DATABASE-Datenbankspiegelung sind für enthaltene Datenbanken nicht verfügbar.  
  
 *database_name*  
 Der Name der Datenbank, die geändert werden soll.  
  
 PARTNER \<partner_option>  
 Steuert die Datenbankeigenschaften, die die Failoverpartner einer Datenbank-Spiegelungssitzung und deren Verhalten definieren. Einige Optionen von SET PARTNER können auf einem beliebigen der Partner festgelegt werden, andere sind auf den Prinzipal- oder den Spiegelserver beschränkt. Weitere Informationen finden Sie unter den jeweiligen Optionen von PARTNER weiter unten. Eine SET PARTNER-Klausel wirkt sich auf beide Kopien der Datenbank aus, unabhängig davon, für welchen Partner sie angegeben ist.  
  
 Zum Ausführen der SET PARTNER-Anweisung muss die Option STATE der Endpunkte beider Partner auf STARTED festgelegt sein. Außerdem muss ROLE für den Datenbank-Spiegelungsendpunkt jeder Partnerserverinstanz auf PARTNER oder ALL festgelegt sein. Weitere Informationen dazu, wie einen Endpunkt angegeben wird, finden Sie unter [Erstellen eines Datenbankspiegelungs-Endpunkt für Windows-Authentifizierung &#40; Transact-SQL &#41; ](../../database-engine/database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md). Verwenden Sie folgende [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung, um die Rolle und den Status des Datenbank-Spiegelungsendpunkts einer Serverinstanz zu erfahren:  
  
```  
SELECT role_desc, state_desc FROM sys.database_mirroring_endpoints  
```  
  
 **\<partner_option> ::=**  
  
> [!NOTE]  
>  Nur ein \<Partner_option > pro SET PARTNER-Klausel zulässig ist.  
  
 **'** *partner_server* **'**  
 Gibt die Server-Netzwerkadresse einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] an, die als Failoverpartner in einer neuen Datenbank-Spiegelungssitzung agiert. Jede Sitzung erfordert zwei Partner, von denen einer als Prinzipalserver, der andere als Spiegelserver beginnt. Die beiden Partner sollten sich auf unterschiedlichen Computern befinden.  
  
 Diese Option wird einmal pro Sitzung für jeden Partner angegeben. Initiieren eine Datenbank-spiegelungssitzung erfordert zwei ALTER DATABASE *Datenbank* SET PARTNER **= "***Partner_server***"** Anweisungen. Ihre Reihenfolge ist wichtig. Zunächst Herstellen einer Verbindung mit dem Spiegelserver, und geben Sie die Prinzipalserverinstanz als *Partner_server* (SET PARTNER **= "***Principal_server***"**). Zweitens, Herstellen einer Verbindung mit dem Prinzipalserver her, und geben Sie die Spiegelserverinstanz als *Partner_server* (SET PARTNER **= "***Mirror_server***"**); Dadurch wird eine Datenbank gestartet. spiegelungssitzung zwischen diesen beiden Partnern. Weitere Informationen finden Sie weiter unten in diesem Thema unter [Einrichten der Datenbankspiegelung &#40;SQL Server&#41;](../../database-engine/database-mirroring/setting-up-database-mirroring-sql-server.md).  
  
 Der Wert der *Partner_server* ist eine Server-Netzwerkadresse. Diese hat folgende Syntax:  
  
 TCP **://***\<Systemadresse >***: ***\<Port >*  
  
 Dabei gilt:  
  
-   *\<System-Address >* ist eine Zeichenfolge, z. B. ein Systemname, einen vollqualifizierten Domänennamen oder eine IP-Adresse, die das Zielsystem für den Computer eindeutig identifiziert.  
  
-   *\<Port >* ist eine Portnummer, die dem Spiegelungsendpunkt der Partnerserverinstanz zugeordnet ist.  
  
 Weitere Informationen finden Sie unter [Angeben einer Servernetzwerkadresse &#40;Datenbankspiegelung&#41;](../../database-engine/database-mirroring/specify-a-server-network-address-database-mirroring.md).  
  
 Das folgende Beispiel veranschaulicht die SET PARTNER **= "***Partner_server***"** Klausel:  
  
```  
'TCP://MYSERVER.mydomain.Adventure-Works.com:7777'  
```  
  
> [!IMPORTANT]  
>  Wird eine Sitzung mithilfe der ALTER DATABASE-Anweisung statt mit [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] eingerichtet, wird die Sitzung standardmäßig auf vollständige Transaktionssicherheit festgelegt (SAFETY wird auf FULL festgelegt) und im Modus für hohe Sicherheit ohne automatisches Failover ausgeführt. Konfigurieren Sie einen Zeugen, um automatisches Failover zuzulassen. Für die Ausführung im Modus für hohe Leistung deaktivieren Sie die Transaktionssicherheit (SAFETY OFF).  
  
 FAILOVER  
 Führt ein manuelles Failover vom Prinzipalserver zum Spiegelserver aus. Sie können FAILOVER nur auf dem Prinzipalserver angeben. Diese Option ist nur dann gültig, wenn die Einstellung SAFETY auf FULL (Standard) festgelegt ist.  
  
 Die Option FAILOVER erfordert **master** als Datenbankkontext.  
  
 FORCE_SERVICE_ALLOW_DATA_LOSS  
 Erzwingt ein Failover des Datenbankdiensts auf die Spiegeldatenbank, wenn auf dem Prinzipalserver ein Fehler auftritt, wobei sich die Datenbank im nicht synchronisierten Zustand oder im synchronisierten Zustand ohne automatisches Failover befindet.  
  
 Es wird dringend empfohlen, den Dienst nur dann zu erzwingen, wenn der Prinzipalserver nicht mehr ausgeführt wird. Ansonsten können einige Clients weiter versuchen, auf die ursprüngliche Prinzipaldatenbank zuzugreifen statt auf die neue Prinzipaldatenbank.  
  
 FORCE_SERVICE_ALLOW_DATA_LOSS ist nur auf dem Spiegelserver verfügbar und nur unter allen folgenden Bedingungen:  
  
-   Der Prinzipalserver ist ausgefallen.  
  
-   WITNESS ist auf OFF festgelegt, oder der Zeuge ist mit dem Spiegelserver verbunden.  
  
 Sie sollten den Dienst nur erzwingen, wenn Sie bereit sind, Datenverluste in Kauf zu nehmen, um den Dienst für die Datenbank unverzüglich wiederherzustellen.  
  
 Durch das Erzwingen des Diensts wird die Sitzung ausgesetzt, und alle Daten werden vorübergehend in der ursprünglichen Prinzipaldatenbank beibehalten. Sobald der ursprüngliche Prinzipalserver in Betrieb und zur Kommunikation mit dem neuen Prinzipalserver in der Lage ist, kann der Datenbankadministrator den Dienst fortsetzen. Wenn die Sitzung fortgesetzt wird, gehen alle nicht gesendeten Protokolldatensätze sowie die entsprechenden Updates verloren.  
  
 OFF  
 Entfernt eine Datenbank-Spiegelungssitzung und entfernt die Spiegelung von der Datenbank. Sie können OFF auf beiden Partnern festlegen. Informationen finden Sie über die Auswirkungen des Entfernens der Spiegelung, finden Sie unter [Entfernen der Datenbankspiegelung &#40; SQLServer &#41; ](../../database-engine/database-mirroring/removing-database-mirroring-sql-server.md).  
  
 RESUME  
 Setzt eine ausgesetzte Datenbank-Spiegelungssitzung fort. Sie können RESUME nur auf dem Hauptserver angeben.  
  
 SAFETY { FULL | OFF }  
 Legt die Sicherheitsstufe für Transaktionen fest. Sie können SAFETY nur auf dem Hauptserver angeben.  
  
 Der Standardwert ist FULL. Mit der vollständigen Sicherheit, die von Datenbank-spiegelungssitzung synchron ausgeführt werden (in *Hochsicherheitsmodus*). Wenn SAFETY auf OFF festgelegt ist, führt den Datenbank-spiegelungssitzung asynchron (im *Modus für hohe Leistung*).  
  
 Das Verhalten des Modus für hohe Sicherheit hängt teilweise folgendermaßen vom Zeugen ab:  
  
-   Wenn die Sicherheit auf FULL und ein Zeuge für die Sitzung festgelegt wurde, wird die Sitzung im Modus für hohe Sicherheit mit automatischem Failover ausgeführt. Wenn der Prinzipalserver ausfällt, findet automatisch ein Failover der Sitzung statt, sofern die Datenbank synchronisiert ist und die Spiegelserverinstanz und der Zeuge noch miteinander verbunden sind (das heißt, sie verfügen über ein Quorum). Weitere Informationen finden Sie unter [Quorum: Auswirkungen eines Zeugen auf die Datenbankverfügbarkeit &#40;Datenbankspiegelung&#41;](../../database-engine/database-mirroring/quorum-how-a-witness-affects-database-availability-database-mirroring.md).  
  
     Wenn ein Zeuge für die Sitzung festgelegt wurde, der zurzeit nicht verbunden ist, bewirkt der Verlust des Spiegelservers, dass der Prinzipalserver ausfällt  
  
-   Wenn die Sicherheit auf FULL und der Zeuge auf OFF festgelegt wurde, wird die Sitzung im Modus für hohe Sicherheit ohne automatisches Failover ausgeführt. Wenn die Spiegelserverinstanz ausfällt, hat dies keine Auswirkungen auf die Prinzipalserverinstanz. Wenn der Prinzipalserver ausfällt, können Sie den Dienst (mit möglichem Datenverlust) auf dem Spiegelserver erzwingen.  
  
 Ist SAFETY auf OFF festgelegt, wird die Sitzung im Modus für hohe Leistung ausgeführt, und weder automatisches noch manuelles Failover werden unterstützt. Probleme auf dem Spiegelserver wirken sich jedoch nicht auf den Prinzipalserver aus. Wenn die Prinzipalserverinstanz ausfällt, können Sie ggf. das Failover des Diensts (mit möglichem Datenverlust) auf die Spiegelserverinstanz erzwingen – wenn WITNESS auf OFF festgelegt wurde oder der Zeuge aktuell mit dem Spiegelserver verbunden ist. Weitere Informationen zum Erzwingen des Diensts finden Sie unter FORCE_SERVICE_ALLOW_DATA_LOSS weiter oben in diesem Abschnitt.  
  
> [!IMPORTANT]  
>  Der Modus für hohe Leistung ist nicht für die Verwendung eines Zeugen konzipiert. Beim Festlegen von SAFETY auf OFF sollte unbedingt sichergestellt werden, dass WITNESS ebenfalls auf OFF festgelegt ist.  
  
 SUSPEND  
 Hält eine Datenbank-Spiegelungssitzung an.  
  
 Sie können SUSPEND auf beiden Partnern angeben.  
  
 TIMEOUT *ganze Zahl*  
 Gibt den Timeoutzeitraum in Sekunden an. Der Timeoutzeitraum ist die Zeit, die eine Serverinstanz maximal auf den Empfang einer PING-Nachricht von einer anderen Instanz in der Spiegelungssitzung wartet, bevor davon ausgegangen wird, dass die Verbindung der anderen Instanz getrennt wurde.  
  
 Sie können die Option TIMEOUT nur auf dem Prinzipalserver angeben. Wenn Sie die Option nicht angeben, beträgt der Timeoutzeitraum standardmäßig 10 Sekunden. Wenn Sie 5 oder höher angeben, wird der Timeoutzeitraum auf die angegebene Anzahl von Sekunden festgelegt. Wenn Sie einen Timeoutzeitwert von 0 bis 4 Sekunden angeben, wird der Timeoutzeitraum automatisch auf 5 Sekunden festgelegt.  
  
> [!IMPORTANT]  
>  Es wird empfohlen, einen Timeoutzeitraum von 10 Sekunden oder mehr zu wählen. Wenn Sie diesen Wert auf weniger als 10 Sekunden festlegen, verpasst ein stark ausgelastetes System möglicherweise PINGs und meldet einen falschen Fehler.  
  
 Weitere Informationen finden Sie unter [Possible Failures During Database Mirroring](../../database-engine/database-mirroring/possible-failures-during-database-mirroring.md).  
  
 WITNESS \<witness_option>  
 Steuert die Datenbankeigenschaften, die einen Datenbank-Spiegelungszeugen definieren. Eine SET WITNESS-Klausel wirkt sich auf beide Kopien der Datenbank aus, Sie können SET WITNESS jedoch nur auf dem Prinzipalserver angeben. Wenn für eine Sitzung ein Zeuge festgelegt ist, ist die Datenbank, unabhängig von der SAFETY-Einstellung ein Quorum erforderlich; Weitere Informationen finden Sie unter [Quorum: Auswirkungen eines Zeugen Datenbankverfügbarkeit &#40; Datenbankspiegelung &#41;](../../database-engine/database-mirroring/quorum-how-a-witness-affects-database-availability-database-mirroring.md).  
  
 Zeuge und Failoverpartner sollten sich auf separaten Computern befinden. Informationen zum Zeugen finden Sie unter [Database Mirroring Witness](../../database-engine/database-mirroring/database-mirroring-witness.md).  
  
 Für die Endpunkte von Prinzipal- und Zeugenserverinstanz muss STATE auf STARTED festgelegt werden, um eine SET WITNESS-Anweisung auszuführen. Außerdem muss ROLE für den Datenbank-Spiegelungsendpunkt einer Zeugenserverinstanz auf WITNESS oder ALL festgelegt sein. Informationen zum Angeben eines Endpunkts finden Sie unter [der Datenbankspiegelungs-Endpunkt &#40; SQLServer &#41; ](../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md).  
  
 Verwenden Sie folgende [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung, um die Rolle und den Status des Datenbank-Spiegelungsendpunkts einer Serverinstanz zu erfahren:  
  
```  
SELECT role_desc, state_desc FROM sys.database_mirroring_endpoints  
```  
  
> [!NOTE]  
>  Auf dem Zeugen können keine Datenbankeigenschaften festgelegt werden.  
  
 **\<witness_option> ::=**  
  
> [!NOTE]  
>  Nur ein \<Witness_option > pro SET WITNESS-Klausel zulässig ist.  
  
 **'** *witness_server* **'**  
 Gibt eine Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] an, die als Zeugenserver für die Datenbank-Spiegelungssitzung agiert. Sie können SET WITNESS-Anweisungen nur auf dem Prinzipalserver angeben.  
  
 In einer SET WITNESS **= "***Witness_server***"** -Anweisung ist die Syntax von *Witness_server* ist identisch mit der Syntax der *Partner_server*.  
  
 OFF  
 Entfernt den Zeugen aus einer Datenbank-Spiegelungssitzung. Durch das Festlegen des Zeugen auf OFF wird das automatische Failover deaktiviert. Ist die Datenbank auf FULL SAFETY festgelegt und der Zeuge auf OFF, führt ein Fehler auf dem Spiegelserver dazu, dass der Prinzipalserver die Datenbank nicht verfügbar macht.  
  
## <a name="remarks"></a>Hinweise  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-creating-a-database-mirroring-session-with-a-witness"></a>A. Erstellen einer Datenbank-Spiegelungssitzung mit einem Zeugen  
 Das Einrichten einer Datenbankspiegelung mit einem Zeugen erfordert das Konfigurieren von Sicherheit und Vorbereiten der Spiegeldatenbank sowie das Verwenden von ALTER DATABASE zum Festlegen der Partner. Ein Beispiel des vollständigen Setupprozesses finden Sie unter [Einrichten der Datenbankspiegelung &#40; SQLServer &#41; ](../../database-engine/database-mirroring/setting-up-database-mirroring-sql-server.md).  
  
### <a name="b-manually-failing-over-a-database-mirroring-session"></a>B. Manuelles Ausführen eines Failovers für eine Datenbank-Spiegelungssitzung  
 Ein manuelles Failover kann von beiden Datenbank-Spiegelungspartnern initiiert werden. Vor dem Failover sollten Sie sicherstellen, dass es sich bei dem aktuellen Prinzipalserver auch tatsächlich um den Prinzipalserver handelt. Führen Sie z. B. für die [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]-Datenbank auf der Serverinstanz, die Sie für den aktuellen Prinzipalserver halten, die folgende Abfrage aus:  
  
```  
SELECT db.name, m.mirroring_role_desc   
FROM sys.database_mirroring m   
JOIN sys.databases db  
ON db.database_id = m.database_id  
WHERE db.name = N'AdventureWorks2012';   
GO  
```  
  
 Handelt es sich bei der Serverinstanz tatsächlich um den Prinzipalserver, hat `mirroring_role_desc` den Wert `Principal`. Handelt es sich bei der Serverinstanz aber um den Spiegelserver, gibt die `SELECT`-Anweisung `Mirror` zurück.  
  
 Im folgenden Beispiel wird vorausgesetzt, dass es sich bei dem Server um den aktuellen Prinzipalserver handelt.  
  
1.  Manuelles Failover an den Datenbank-Spiegelungspartner:  
  
    ```  
    ALTER DATABASE AdventureWorks2012 SET PARTNER FAILOVER;  
    GO  
    ```  
  
2.  Führen Sie die folgende Abfrage aus, um die Ergebnisse des Failovers auf dem neuen Spiegelserver zu überprüfen:  
  
    ```  
    SELECT db.name, m.mirroring_role_desc   
    FROM sys.database_mirroring m   
    JOIN sys.databases db  
    ON db.database_id = m.database_id  
    WHERE db.name = N'AdventureWorks2012';   
    GO  
    ```  
  
     Der aktuelle Wert von `mirroring_role_desc` ist jetzt `Mirror`.  
  
## <a name="see-also"></a>Siehe auch  
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [DATABASEPROPERTYEX &#40;Transact-SQL&#41;](../../t-sql/functions/databasepropertyex-transact-sql.md)   
 [sys.database_mirroring_witnesses &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/database-mirroring-witness-catalog-views-sys-database-mirroring-witnesses.md)  
  
  
