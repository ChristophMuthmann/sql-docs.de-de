---
title: Erstellen Sie die ROUTE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE_ROUTE_TSQL
- ROUTE
- CREATE ROUTE
- ROUTE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- lifetimes [Service Broker]
- routes [Service Broker], creating
- forwarding brokers [SQL Server]
- service names [Service Broker]
- database mirroring [SQL Server], routing
- expired routes [SQL Server]
- activating routes
- CREATE ROUTE statement
ms.assetid: 7e695364-1a98-4cfd-8ebd-137ac5a425b3
caps.latest.revision: 42
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b7268b5c9b43505d3c66fb6573a9a41c3cd62e3a
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="create-route-transact-sql"></a>CREATE ROUTE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Fügt der Routingtabelle der aktuellen Datenbank eine neue Route hinzu. Bei ausgehenden Nachrichten bestimmt [!INCLUDE[ssSB](../../includes/sssb-md.md)] das Routing durch eine Prüfung der Routingtabelle in der lokalen Datenbank. Nachrichten in Konversationen, die in einer anderen Instanz stammen, darunter Nachrichten weitergeleitet werden, [!INCLUDE[ssSB](../../includes/sssb-md.md)] überprüft die Routen **Msdb**.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
CREATE ROUTE route_name  
[ AUTHORIZATION owner_name ]  
WITH    
   [ SERVICE_NAME = 'service_name', ]  
   [ BROKER_INSTANCE = 'broker_instance_identifier' , ]  
   [ LIFETIME = route_lifetime , ]  
   ADDRESS =  'next_hop_address'  
   [ , MIRROR_ADDRESS = 'next_hop_mirror_address' ]  
[ ; ]  
```  
  
## <a name="arguments"></a>Argumente  
 *route_name*  
 Der Name der zu erstellenden Route. Eine neue Route wird in der aktuellen Datenbank erstellt. Ihr Besitzer ist der in der AUTHORIZATION-Klausel angegebene Prinzipal. Server-, Datenbank- und Schemaname können nicht angegeben werden. Die *Route_name* muss ein gültiger **Sysname**.  
  
 Autorisierung *Owner_name*  
 Legt den Benutzer oder die Rolle der angegebenen Datenbank als Besitzer der Route fest. Die *Owner_name* kann der Name eines beliebigen gültigen Benutzers oder einer Rolle sein, wenn der aktuelle Benutzer ein Mitglied ist die **Db_owner** festen Datenbankrolle oder der **Sysadmin** festen Serverrolle "". Andernfalls *Owner_name* kann den Namen des aktuellen Benutzers, den Namen eines Benutzers, der der aktuelle Benutzer IMPERSONATE-Berechtigungen verfügt oder der Name einer Rolle, zu der der aktuelle Benutzer gehört. Wird diese Klausel weggelassen, gehört die Route dem aktuellen Benutzer.  
  
 mit  
 Führt die Klauseln ein, über die die zurzeit erstellte Route definiert wird.  
  
 SERVICE_NAME = **"***Service_name***"**  
 Gibt den Namen des Remotediensts an, auf den diese Route zeigt. Die *Service_name* müssen genau übereinstimmen, die den Namen der Remotedienst verwendet. [!INCLUDE[ssSB](../../includes/sssb-md.md)]Führt einen Byte-pro-Byte-Vergleich mit der *Service_name*. Anders ausgedrückt: Bei dem Vergleich wird die Groß-/Kleinschreibung beachtet, die aktuelle Sortierung hingegen wird nicht berücksichtigt. Wenn SERVICE_NAME weggelassen wird, stimmt die Route mit jedem Dienstnamen überein, weist jedoch eine niedrigere Übereinstimmungspriorität als eine Route auf, die SERVICE_NAME angibt. Eine Route mit dem Dienstnamen **' SQL/ServiceBroker/BrokerConfiguration'** ist eine Route zu einem Broker-Konfigurationsdienst. Eine Route zu diesem Dienst kann keine Broker-Instanz angeben.  
  
 BROKER_INSTANCE = **"***Broker_instance_identifier***"**  
 Gibt die Datenbank an, auf der sich der Zieldienst befindet. Die *Broker_instance_identifier* Parameter muss den Broker-Instanzbezeichner für die Remotedatenbank an, die durch Ausführen der folgenden Abfrage in der ausgewählten Datenbank abgerufen werden kann:  
  
```  
SELECT service_broker_guid  
FROM sys.databases  
WHERE database_id = DB_ID()  
```  
  
 Wenn die BROKER_INSTANCE-Klausel weggelassen wird, stimmt diese Route mit jeder Broker-Instanz überein. Eine Route, die mit jeder Broker-Instanz übereinstimmt, weist eine höhere Übereinstimmungspriorität auf als Routen mit einer expliziten Broker-Instanz, wenn die Konversation keine Broker-Instanz angibt. Bei Konversationen, in denen eine Broker-Instanz angegeben wird, weist eine Route mit einer Broker-Instanz eine höhere Priorität auf als eine Route, die mit jeder Broker-Instanz übereinstimmt.  
  
 Lebensdauer  **=**  *Route_lifetime*  
 Gibt die Zeitspanne in Sekunden an, die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die Route in der Routingtabelle aufbewahrt. Am Ende ihrer Lebensdauer läuft die Route ab, und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] berücksichtigt die Route nicht bei der Auswahl einer Route für eine neue Konversation. Wenn diese Klausel weggelassen wird, die *Route_lifetime* NULL ist und die Route läuft nie ab.  
  
 Adresse **= "***Next_hop_address***"**  
 Gibt die Netzwerkadresse für diese Route an. Die *Next_hop_address* gibt eine TCP/IP-Adresse in folgendem Format an:  
  
 **TCP: / /**{ *Dns_name* | *Netbios_name* | *Ip_address* } **:**  *Portnummer*  
  
 Das angegebene *Port_number* übereinstimmen, dass die Portnummer für die [!INCLUDE[ssSB](../../includes/sssb-md.md)] Endpunkt einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf dem angegebenen Computer. Dieser kann durch Ausführen der folgenden Abfrage in der ausgewählten Datenbank abgerufen werden:  
  
```  
SELECT tcpe.port  
FROM sys.tcp_endpoints AS tcpe  
INNER JOIN sys.service_broker_endpoints AS ssbe  
   ON ssbe.endpoint_id = tcpe.endpoint_id  
WHERE ssbe.name = N'MyServiceBrokerEndpoint';  
```  
  
 Wenn eine gespiegelte Datenbank für den Dienst als Host dient, müssen Sie MIRROR_ADDRESS auch für die andere Instanz angeben, für die eine gespiegelte Datenbank als Host dient. Andernfalls führt die Route kein Failover zum Spiegel durch.  
  
 Gibt eine Route **'LOCAL'** für die *Next_hop_address*, übermittelt die Nachricht an einen Dienst innerhalb der aktuellen Instanz der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Gibt eine Route **'TRANSPORT'** für die *Next_hop_address*, die Netzwerkadresse wird basierend auf der der Netzwerkadresse des Diensts bestimmt. Eine Route, der angibt, **'TRANSPORT'** eine Dienst oder eine Broker-Instanz möglicherweise nicht angeben.  
  
 MIRROR_ADDRESS **= "***Next_hop_mirror_address***"**  
 Gibt die Netzwerkadresse für eine gespiegelte Datenbank mit einer gespiegelten Datenbank gehostet wird, auf die *Next_hop_address*. Die *Next_hop_mirror_address* gibt eine TCP/IP-Adresse in folgendem Format an:  
  
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
  
## <a name="remarks"></a>Hinweise  
 Die Routingtabelle, die Routen gespeichert, ist eine Metadatentabelle, die gelesen werden kann, durch die **sys.routes** -Katalogsicht angezeigt. Diese Katalogsicht kann nur durch CREATE ROUTE-, ALTER ROUTE- und DROP ROUTE-Anweisungen aktualisiert werden.  
  
 Standardmäßig enthält die Routingtabelle in jeder Benutzerdatenbank eine Route. Diese Route heißt **AutoCreatedLocal**. Gibt die Route **'LOCAL'** für die *Next_hop_address* und alle Service Broker Namen und die Instanz-ID übereinstimmt.  
  
 Gibt eine Route **'TRANSPORT'** für die *Next_hop_address*, die Netzwerkadresse wird basierend auf den Namen des Diensts bestimmt. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]kann erfolgreich Dienstnamen, die mit einer Netzwerkadresse in einem Format beginnen, die für gültig ist Verarbeiten einer *Next_hop_address*.  
  
 Die Routingtabelle kann eine beliebige Anzahl von Routen enthalten, die den gleichen Dienst, die gleiche Netzwerkadresse und Broker-Instanz-ID angeben. In diesem Fall wählt [!INCLUDE[ssSB](../../includes/sssb-md.md)] eine Route mithilfe einer Prozedur aus, die darauf ausgerichtet ist, eine möglichst genaue Übereinstimmung zwischen den in der Konversation angegebenen Informationen und den Informationen in der Routingtabelle festzustellen.  
  
 Abgelaufene Routen werden von [!INCLUDE[ssSB](../../includes/sssb-md.md)]nicht aus der Routingtabelle entfernt. Mit der ALTER ROUTE-Anweisung kann eine abgelaufene Route aktiviert werden.  
  
 Eine Route kann kein temporäres Objekt sein. Routennamen, die mit beginnt  **#**  zulässig sind, sind jedoch dauerhafte Objekte.  
  
## <a name="permissions"></a>Berechtigungen  
 Die Berechtigung zum Erstellen einer Route verfügen standardmäßig Mitglieder der der **Db_ddladmin** oder **Db_owner** festen Datenbankrollen und die **Sysadmin** festen Serverrolle "".  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-creating-a-tcpip-route-by-using-a-dns-name"></a>A. Erstellen einer TCP/IP-Route anhand eines DNS-Namens  
 Im folgenden Beispiel wird eine Route zum Dienst `//Adventure-Works.com/Expenses` erstellt. Über die Route wird angegeben, dass Nachrichten an diesen Dienst über TCP an Port `1234` auf dem Host übertragen werden, der durch den DNS-Namen `www.Adventure-Works.com` identifiziert wird. Der Zielserver leitet die Nachrichten bei ihrem Eingang an die Broker-Instanz weiter, die durch den eindeutigen Bezeichner `D8D4D268-00A3-4C62-8F91-634B89C1E315` identifiziert wird.  
  
```  
CREATE ROUTE ExpenseRoute  
    WITH  
    SERVICE_NAME = '//Adventure-Works.com/Expenses',  
    BROKER_INSTANCE = 'D8D4D268-00A3-4C62-8F91-634B89C1E315',  
    ADDRESS = 'TCP://www.Adventure-Works.com:1234' ;  
```  
  
### <a name="b-creating-a-tcpip-route-by-using-a-netbios-name"></a>B. Erstellen einer TCP/IP-Route anhand eines NetBIOS-Namens  
 Im folgenden Beispiel wird eine Route zum Dienst `//Adventure-Works.com/Expenses` erstellt. Über die Route wird angegeben, dass Nachrichten an diesen Dienst über TCP an Port `1234` auf dem Host übertragen werden, der durch den NetBIOS-Namen `SERVER02` identifiziert wird. Beim Eintreffen leitet der Zielserver mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die Nachricht an die Datenbankinstanz weiter, die durch den eindeutigen Bezeichner `D8D4D268-00A3-4C62-8F91-634B89C1E315` identifiziert wird.  
  
```  
CREATE ROUTE ExpenseRoute  
    WITH   
    SERVICE_NAME = '//Adventure-Works.com/Expenses',  
    BROKER_INSTANCE = 'D8D4D268-00A3-4C62-8F91-634B89C1E315',  
    ADDRESS = 'TCP://SERVER02:1234' ;  
```  
  
### <a name="c-creating-a-tcpip-route-by-using-an-ip-address"></a>C. Erstellen einer TCP/IP-Route anhand einer IP-Adresse  
 Im folgenden Beispiel wird eine Route zum Dienst `//Adventure-Works.com/Expenses` erstellt. Über die Route wird angegeben, dass Nachrichten an diesen Dienst über TCP an Port `1234` auf dem Host mit der IP-Adresse `192.168.10.2` übertragen werden. Beim Eintreffen leitet der Zielserver mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die Nachricht an die Broker-Instanz weiter, die durch den eindeutigen Bezeichner `D8D4D268-00A3-4C62-8F91-634B89C1E315` identifiziert wird.  
  
```  
CREATE ROUTE ExpenseRoute  
    WITH  
    SERVICE_NAME = '//Adventure-Works.com/Expenses',  
    BROKER_INSTANCE = 'D8D4D268-00A3-4C62-8F91-634B89C1E315',  
    ADDRESS = 'TCP://192.168.10.2:1234' ;  
```  
  
### <a name="d-creating-a-route-to-a-forwarding-broker"></a>D. Erstellen einer Route zu einem Weiterleitungsbroker  
 Im folgenden Beispiel wird eine Route zum Weiterleitungsbroker auf dem Server `dispatch.Adventure-Works.com` erstellt. Da weder der Dienstname noch die Broker-Instanz-ID angegeben sind, verwendet [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] diese Route für Dienste, für die keine andere Route definiert ist.  
  
```  
CREATE ROUTE ExpenseRoute  
    WITH  
    ADDRESS = 'TCP://dispatch.Adventure-Works.com' ;   
```  
  
### <a name="e-creating-a-route-to-a-local-service"></a>E. Erstellen einer Route zu einem lokalen Dienst  
 Im folgenden Beispiel wird eine Route zum Dienst `//Adventure-Works.com/LogRequests` in der gleichen Instanz wie die Route erstellt.  
  
```  
CREATE ROUTE LogRequests  
    WITH  
    SERVICE_NAME = '//Adventure-Works.com/LogRequests',  
    ADDRESS = 'LOCAL' ;  
```  
  
### <a name="f-creating-a-route-with-a-specified-lifetime"></a>F. Erstellen einer Route mit einer angegebenen Lebensdauer  
 Im folgenden Beispiel wird eine Route zum Dienst `//Adventure-Works.com/Expenses` erstellt. Die Lebensdauer der Route beträgt `259200` Sekunden. Dies entspricht 72 Stunden.  
  
```  
CREATE ROUTE ExpenseRoute  
    WITH  
    SERVICE_NAME = '//Adventure-Works.com/Expenses',  
    LIFETIME = 259200,  
    ADDRESS = 'TCP://services.Adventure-Works.com:1234' ;  
```  
  
### <a name="g-creating-a-route-to-a-mirrored-database"></a>G. Erstellen einer Route zu einer gespiegelten Datenbank  
 Im folgenden Beispiel wird eine Route zum Dienst `//Adventure-Works.com/Expenses` erstellt. Für den Dienst dient eine Datenbank als Host, die gespiegelt wird. Eine der gespiegelten Datenbanken besitzt die Adresse `services.Adventure-Works.com:1234`, und die andere Datenbank besitzt die Adresse `services-mirror.Adventure-Works.com:1234`.  
  
```  
CREATE ROUTE ExpenseRoute  
    WITH  
    SERVICE_NAME = '//Adventure-Works.com/Expenses',  
    BROKER_INSTANCE = '69fcc80c-2239-4700-8437-1001ecddf933',  
    ADDRESS = 'TCP://services.Adventure-Works.com:1234',   
    MIRROR_ADDRESS = 'TCP://services-mirror.Adventure-Works.com:1234' ;  
```  
  
### <a name="h-creating-a-route-that-uses-the-service-name-for-routing"></a>H. Erstellen einer Route, die für Routing den Dienstnamen verwendet  
 Im folgenden Beispiel wird eine Route erstellt, die den Dienstnamen verwendet, um die Netzwerkadresse zu bestimmen, an die die Nachricht gesendet wird. Beachten Sie, dass eine Route, die `'TRANSPORT'` als Netzwerkadresse angibt, eine niedrigere Priorität für Übereinstimmungen aufweist als andere Routen.  
  
```  
CREATE ROUTE TransportRoute  
    WITH ADDRESS = 'TRANSPORT' ;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [ALTER ROUTE &#40; Transact-SQL &#41;](../../t-sql/statements/alter-route-transact-sql.md)   
 [DROP ROUTE &#40; Transact-SQL &#41;](../../t-sql/statements/drop-route-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  

