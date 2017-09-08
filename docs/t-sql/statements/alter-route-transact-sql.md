---
title: ALTER ROUTE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_ROUTE_TSQL
- ALTER ROUTE
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER ROUTE statement
- dropping routes
- modifying routes
- removing routes
- routes [Service Broker], modifying
ms.assetid: 8dfb7b16-3dac-4e1e-8c97-adf2aad07830
caps.latest.revision: 33
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 39e39b8688e2350d27e664b4a1517584c11df941
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="alter-route-transact-sql"></a>ALTER ROUTE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Verändert die Routeninformationen für eine vorhandene Route in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
ALTER ROUTE route_name  
WITH    
  [ SERVICE_NAME = 'service_name' [ , ] ]  
  [ BROKER_INSTANCE = 'broker_instance' [ , ] ]  
  [ LIFETIME = route_lifetime [ , ] ]  
  [ ADDRESS =  'next_hop_address' [ , ] ]  
  [ MIRROR_ADDRESS = 'next_hop_mirror_address' ]  
[ ; ]  
  
```  
  
## <a name="arguments"></a>Argumente  
 *route_name*  
 Der Name der zu ändernden Route. Server-, Datenbank- und Schemaname können nicht angegeben werden.  
  
 mit  
 Führt die Klauseln ein, die die Route definieren, die gerade geändert wird.  
  
 SERVICE_NAME **= "***Service_name***"**  
 Gibt den Namen des Remotediensts an, auf den diese Route zeigt. Die *Service_name* müssen genau übereinstimmen, die den Namen der Remotedienst verwendet. [!INCLUDE[ssSB](../../includes/sssb-md.md)]Führt einen Byte-pro-Byte-Vergleich mit der *Service_name*. Anders ausgedrückt: Bei dem Vergleich wird die Groß-/Kleinschreibung beachtet, die aktuelle Sortierung hingegen wird nicht berücksichtigt. Eine Route mit dem Dienstnamen **' SQL/ServiceBroker/BrokerConfiguration'** ist eine Route zu einem Broker-Konfigurationsdienst. Eine Route zu diesem Dienst kann keine Broker-Instanz angeben.  
  
 Wird die SERVICE_NAME-Klausel weggelassen, ändert sich der Dienstname für die Route nicht.  
  
 BROKER_INSTANCE **= "***Broker_instance***"**  
 Gibt die Datenbank an, auf der sich der Zieldienst befindet. Die *Broker_instance* Parameter muss den Broker-Instanzbezeichner für die Remotedatenbank an, die durch Ausführen der folgenden Abfrage in der ausgewählten Datenbank abgerufen werden kann:  
  
```  
SELECT service_broker_guid  
FROM sys.databases  
WHERE database_id = DB_ID();  
```  
  
 Wird die BROKER_INSTANCE-Klausel weggelassen, ändert sich die Broker-Instanz für die Route nicht.  
  
> [!NOTE]  
>  Diese Option ist in einer enthaltenen Datenbank nicht verfügbar.  
  
 Lebensdauer  **=**  *Route_lifetime*  
 Gibt die Zeitspanne in Sekunden an, die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die Route in der Routingtabelle aufbewahrt. Am Ende ihrer Lebensdauer läuft die Route ab, und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] berücksichtigt die Route nicht bei der Auswahl einer Route für eine neue Konversation. Wird die Klausel weggelassen, bleibt die Lebensdauer der Route unverändert.  
  
 Adresse **= "***Next_hop_address'*  
 Gibt die Netzwerkadresse für diese Route an. Die *Next_hop_address* gibt eine TCP/IP-Adresse in folgendem Format an:  
  
 **TCP: / /** { *Dns_name* | *Netbios_name* |*Ip_address* } **:**  *Portnummer*  
  
 Das angegebene *Port_number* übereinstimmen, dass die Portnummer für die [!INCLUDE[ssSB](../../includes/sssb-md.md)] Endpunkt einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf dem angegebenen Computer. Dieser kann durch Ausführen der folgenden Abfrage in der ausgewählten Datenbank abgerufen werden:  
  
```  
SELECT tcpe.port  
FROM sys.tcp_endpoints AS tcpe  
INNER JOIN sys.service_broker_endpoints AS ssbe  
   ON ssbe.endpoint_id = tcpe.endpoint_id  
WHERE ssbe.name = N'MyServiceBrokerEndpoint';  
```  
  
 Gibt eine Route **'LOCAL'** für die *Next_hop_address*, übermittelt die Nachricht an einen Dienst innerhalb der aktuellen Instanz der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Gibt eine Route **'TRANSPORT'** für die *Next_hop_address*, die Netzwerkadresse wird basierend auf der der Netzwerkadresse des Diensts bestimmt. Eine Route, der angibt, **'TRANSPORT'** können eine Dienst oder eine Broker-Instanz angeben.  
  
 Wenn die *Next_hop_address* der Prinzipalserver für eine gespiegelte Datenbank müssen Sie auch MIRROR_ADDRESS für den Spiegelserver angeben. Andernfalls führt diese Route kein automatisches Failover zum Spiegelserver durch.  
  
> [!NOTE]  
>  Diese Option ist in einer enthaltenen Datenbank nicht verfügbar.  
  
 MIRROR_ADDRESS **= "***Next_hop_mirror_address***"**  
 Gibt die Netzwerkadresse für den Spiegelserver eines gespiegelten Paars, dessen Prinzipalserver, die *Next_hop_address*. Die *Next_hop_mirror_address* gibt eine TCP/IP-Adresse in folgendem Format an:  
  
 **TCP: / /**{ *Dns_name* | *Netbios_name* | *Ip_address* } **:**  *Portnummer*  
  
 Das angegebene *Port_number* übereinstimmen, dass die Portnummer für die [!INCLUDE[ssSB](../../includes/sssb-md.md)] Endpunkt einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf dem angegebenen Computer. Dieser kann durch Ausführen der folgenden Abfrage in der ausgewählten Datenbank abgerufen werden:  
  
```  
SELECT tcpe.port  
FROM sys.tcp_endpoints AS tcpe  
INNER JOIN sys.service_broker_endpoints AS ssbe  
   ON ssbe.endpoint_id = tcpe.endpoint_id  
WHERE ssbe.name = N'MyServiceBrokerEndpoint';  
```  
  
 Wird MIRROR_ADDRESS angegeben, muss die Route die SERVICE_NAME-Klausel und die BROKER_INSTANCE-Klausel angeben. Eine Route, der angibt, **'LOCAL'** oder **'TRANSPORT'** für die *Next_hop_address* möglicherweise keine spiegeladresse.  
  
> [!NOTE]  
>  Diese Option ist in einer enthaltenen Datenbank nicht verfügbar.  
  
## <a name="remarks"></a>Hinweise  
 Die Routingtabelle, die Routen gespeichert, ist eine Metadatentabelle, die gelesen werden kann, durch die **sys.routes** -Katalogsicht angezeigt. Die Routingtabelle kann nur mit der CREATE ROUTE-, ALTER ROUTE- und DROP ROUTE-Anweisung aktualisiert werden.  
  
 Klauseln, die im ALTER ROUTE-Befehl nicht angegeben werden, bleiben unverändert. Deshalb ist es nicht möglich, über ALTER festzulegen, dass für die Route kein Timeout gilt, dass die Route mit jedem Dienstnamen übereinstimmt oder dass die Route mit jeder Broker-Instanz übereinstimmt. Wenn Sie diese Merkmale einer Route ändern möchten, müssen Sie die vorhandene Route löschen und eine neue Route mit den neuen Informationen erstellen.  
  
 Gibt eine Route **'TRANSPORT'** für die *Next_hop_address*, die Netzwerkadresse wird basierend auf den Namen des Diensts bestimmt. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]kann erfolgreich Dienstnamen, die mit einer Netzwerkadresse in einem Format beginnen, die für gültig ist Verarbeiten einer *Next_hop_address*. Für Dienste mit Namen, die gültige Netzwerkadressen enthalten, erfolgt das Routing an die Netzwerkadresse im Dienstnamen.  
  
 Die Routingtabelle kann eine beliebige Anzahl von Routen enthalten, die den gleichen Dienst, die gleiche Netzwerkadresse und/oder Broker-Instanz-ID angeben. In diesem Fall wählt [!INCLUDE[ssSB](../../includes/sssb-md.md)] eine Route mithilfe einer Prozedur aus, die darauf ausgerichtet ist, eine möglichst genaue Übereinstimmung zwischen den in der Konversation angegebenen Informationen und den Informationen in der Routingtabelle festzustellen.  
  
 Verwenden Sie die ALTER AUTHORIZATION-Anweisung, wenn Sie AUTHORIZATION für einen Dienst ändern möchten.  
  
## <a name="permissions"></a>Berechtigungen  
 Berechtigung zum Ändern einer Route erhalten standardmäßig Besitzer der Route, Mitglieder der der **Db_ddladmin** oder **Db_owner** festen Datenbankrollen und Mitglieder der **Sysadmin** behoben Serverrolle.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-changing-the-service-for-a-route"></a>A. Ändern des Diensts für eine Route  
 Im folgenden Beispiel wird die Route `ExpenseRoute` so geändert, dass sie auf den Remotedienst `//Adventure-Works.com/Expenses` zeigt.  
  
```  
ALTER ROUTE ExpenseRoute  
   WITH   
     SERVICE_NAME = '//Adventure-Works.com/Expenses';  
```  
  
### <a name="b-changing-the-target-database-for-a-route"></a>B. Ändern der Zieldatenbank für eine Route  
 Im folgenden Beispiel wird die Zieldatenank für die Route `ExpenseRoute` in die Datenbank geändert, die durch folgenden eindeutigen Bezeichner angegeben wird: `D8D4D268-00A3-4C62-8F91-634B89B1E317.`  
  
```  
ALTER ROUTE ExpenseRoute  
   WITH   
     BROKER_INSTANCE = 'D8D4D268-00A3-4C62-8F91-634B89B1E317';  
```  
  
### <a name="c-changing-the-address-for-a-route"></a>C. Ändern der Adresse für eine Route  
 Im folgenden Beispiel wird die Netzwerkadresse für die Route `ExpenseRoute` in den TCP-Port `1234` auf dem Host mit der IP-Adresse `10.2.19.72` geändert.  
  
```  
ALTER ROUTE ExpenseRoute   
   WITH   
     ADDRESS = 'TCP://10.2.19.72:1234';  
```  
  
### <a name="d-changing-the-database-and-address-for-a-route"></a>D. Ändern der Datenbank und Adresse für eine Route  
 Im folgenden Beispiel wird die Netzwerkadresse für die Route `ExpenseRoute` in den TCP-Port `1234` auf dem Host mit dem DNS-Namen `www.Adventure-Works.com` geändert. Zudem wird die Zieldatenbank in die durch den eindeutigen Bezeichner `D8D4D268-00A3-4C62-8F91-634B89B1E317` identifizierte Datenbank geändert.  
  
```  
ALTER ROUTE ExpenseRoute  
   WITH   
     BROKER_INSTANCE = 'D8D4D268-00A3-4C62-8F91-634B89B1E317',  
     ADDRESS = 'TCP://www.Adventure-Works.com:1234';  
```  
  
## <a name="see-also"></a>Siehe auch  
 [CREATE ROUTE &#40;Transact-SQL&#41;](../../t-sql/statements/create-route-transact-sql.md)   
 [DROP ROUTE &#40; Transact-SQL &#41;](../../t-sql/statements/drop-route-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
