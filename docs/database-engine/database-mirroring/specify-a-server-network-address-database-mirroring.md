---
title: "Angeben einer Servernetzwerkadresse (Datenbankspiegelung) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Datenbankspiegelung [SQL Server], Bereitstellung"
  - "Datenbankspiegelung [SQL Server], Endpunkt"
  - "Endpunkte [SQL Server], Datenbankspiegelung"
  - "Servernetzwerkadressen [SQL Server]"
ms.assetid: a64d4b6b-9016-4f1e-a310-b1df181dd0c6
caps.latest.revision: 60
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 59
---
# Angeben einer Servernetzwerkadresse (Datenbankspiegelung)
  Beim Einrichten einer Datenbank-Spiegelungssitzung ist für jede Serverinstanz eine Server-Netzwerkadresse erforderlich. Die Server-Netzwerkadresse der Serverinstanz muss die Instanz eindeutig identifizieren, indem sie eine Systemadresse und die Nummer des Ports angibt, den die Instanz überwacht.  
  
 Bevor Sie einen Port in einer Server-Netzwerkadresse angeben können, muss der Endpunkt der Datenbankspiegelung auf der Serverinstanz vorhanden sein. Weitere Informationen finden Sie unter [Erstellen eines Endpunkts der Datenbankspiegelung für Windows-Authentifizierung &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md).  
  
 **In diesem Thema:**  
  
-   [Syntax für eine Server-Netzwerkadresse](#Syntax)  
  
-   [Ermitteln des vollqualifizierten Domänennamens](#FindFqDn)  
  
-   [Beispiele](#Examples)  
  
-   [Verwandte Aufgaben](#RelatedTasks)  
  
##  <a name="Syntax"></a> Syntax für eine Server-Netzwerkadresse  
 Die Syntax für eine Server-Netzwerkadresse lautet:  
  
 TCP**://***<Systemadresse>***:***\<Port>*  
  
 Dabei gilt:  
  
-   *<Systemadresse>* ist eine Zeichenfolge, die das Zielcomputersystem eindeutig identifiziert. In der Regel handelt es sich bei der Serveradresse um einen Systemnamen (wenn sich die Systeme in derselben Domäne befinden), einen vollqualifizierten Domänennamen oder eine IP-Adresse:  
  
    -   Befinden sich die Systeme in derselben Domäne, können Sie den Namen des Computersystems verwenden, z. B. `SYSTEM46`.  
  
    -   Wenn Sie eine IP-Adresse verwenden möchten, muss diese in Ihrer Umgebung eindeutig sein. Wir empfehlen die Verwendung einer IP-Adresse nur, wenn diese statisch ist. Die IP-Adresse kann im IPv4-Format (IP Version 4) oder im IPv6-Format (IP Version) vorliegen. Eine IPv6-Adresse muss in eckige Klammern gesetzt werden, z.B. **[***\<IPv6-Adresse>***]**.  
  
         Um die IP-Adresse eines Systems zu ermitteln, geben Sie an der Windows-Eingabeaufforderung den Befehl **ipconfig** ein.  
  
    -   Der vollqualifizierte Domänenname funktioniert auf alle Fälle. Hierbei handelt es sich um eine lokal definierte Adresszeichenfolge, die an unterschiedlichen Stellen unterschiedliche Formen annimmt. Häufig, jedoch nicht immer, ist ein vollqualifizierter Domänenname ein zusammengesetzter Name, der den Computernamen und eine Reihe von Domänensegmenten enthält, die durch Punkte voneinander getrennt sind, z. B.:  
  
         *Computername* **.** *Domänensegment*[...**.***Domänensegment*]  
  
         Dabei steht *Computername* für den Netzwerknamen des Computers, auf dem die Serverinstanz ausgeführt wird, und *Domänensegment*[...**.***Domänensegment*] für die übrigen Domäneninformationen des Servers. Beispiel: `localinfo.corp.Adventure-Works.com`.  
  
         Inhalt und Anzahl von Domänenelementen werden innerhalb des Unternehmens oder der Organisation bestimmt. Wenn Sie den vollqualifizierten Domänennamen des Servers nicht kennen, wenden Sie sich an den Systemadministrator.  
  
        > [!NOTE]  
        >  Informationen zum Ermitteln eines vollqualifizierten Domänennamens finden Sie nachfolgend in diesem Thema unter "Ermitteln des vollqualifizierten Domänennamens".  
  
-   *\<Port>* ist die Portnummer, die vom Spiegelungsendpunkt der Partnerserverinstanz verwendet wird. Weitere Informationen zum Angeben eines Endpunkts finden Sie unter [Erstellen eines Endpunkts der Datenbankspiegelung für Windows-Authentifizierung &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md).  
  
     Ein Datenbankspiegelungs-Endpunkt kann jeden verfügbaren Port im Computersystem verwenden. Jede Portnummer in einem Computersystem darf nur einem Endpunkt zugeordnet werden, und jeder Endpunkt ist einer einzelnen Serverinstanz zugeordnet. Daher lauschen unterschiedliche Serverinstanzen auf dem gleichen Server an unterschiedliche Endpunkten mit unterschiedlichen Ports. Aus diesem Grund leitet der Port, den Sie beim Einrichten einer Datenbank-Spiegelungssitzung in der Server-Netzwerkadresse angeben, die Sitzung immer an die Serverinstanz weiter, deren Endpunkt dem jeweiligen Port zugeordnet ist.  
  
     In der Server-Netzwerkadresse einer Serverinstanz unterscheidet nur die Nummer des Ports, die ihrem Spiegelungsendpunkt zugeordnet ist, diese Instanz von anderen Instanzen auf dem Computer. Die folgende Abbildung veranschaulicht die Server-Netzwerkadresse von zwei Serverinstanzen auf einem Computer. In der Standardinstanz wird Port `7022` verwendet, und in der benannten Instanz wird Port `7033`verwendet. Die Server-Netzwerkadressen für diese beiden Serverinstanzen lauten `TCP://MYSYSTEM.Adventure-works.MyDomain.com:7022` bzw. `TCP://MYSYSTEM.Adventure-works.MyDomain.com:7033`. Beachten Sie, dass die Adresse nicht den Namen der Serverinstanz enthält.  
  
     ![Servernetzwerkadressen einer Standardinstanz](../../database-engine/availability-groups/windows/media/dbm-2-instances-ports-1-system.gif "Servernetzwerkadressen einer Standardinstanz")  
  
     Verwenden Sie die folgende [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung, um den Port zu identifizieren, der derzeit dem Endpunkt der Datenbankspiegelung einer Serverinstanz zugeordnet ist:  
  
    ```  
    SELECT type_desc, port FROM sys.tcp_endpoints  
    ```  
  
     Suchen Sie die Zeile, deren **type_desc**-Wert „DATABASE_MIRRORING“ lautet, und verwenden Sie die entsprechende Portnummer.  
  
### Beispiele  
  
#### A. Verwenden eines Systemnamens  
 Die folgende Server-Netzwerkadresse gibt den Systemnamen `SYSTEM46`und Port `7022`an.  
  
```  
ALTER DATABASE AdventureWorks SET PARTNER ='tcp://SYSTEM46:7022';  
```  
  
#### B. Verwenden eines vollqualifizierten Domänennamens  
 Die folgende Server-Netzwerkadresse gibt den vollqualifizierten Domänennamen `DBSERVER8.manufacturing.Adventure-Works.com`und Port `7024`an.  
  
```  
ALTER DATABASE AdventureWorks SET PARTNER ='tcp://DBSERVER8.manufacturing.Adventure-Works.com:7024';  
```  
  
#### C. Verwenden von IPv4  
 Die folgende Server-Netzwerkadresse gibt die IPv4-Adresse `10.193.9.134`und Port `7023`an.  
  
```  
ALTER DATABASE AdventureWorks SET PARTNER ='tcp://10.193.9.134:7023';  
```  
  
#### D. Verwenden von IPv6  
 Die folgende Server-Netzwerkadresse gibt die IPv6-Adresse `2001:4898:23:1002:20f:1fff:feff:b3a3`und Port `7022`an.  
  
```  
ALTER DATABASE AdventureWorks SET PARTNER ='tcp://[2001:4898:23:1002:20f:1fff:feff:b3a3]:7022';  
```  
  
## Ermitteln des vollqualifizierten Domänennamens  
 Um den vollqualifizierten Domänennamen eines Systems zu ermitteln, geben Sie an der Windows-Eingabeaufforderung des Systems den folgenden Befehl ein:  
  
 **IPCONFIG /ALL**  
  
 Um den vollqualifizierten Domänennamen zu bilden, verketten Sie die Werte von *<Hostname>* und *\<Primäres_DNS-Suffix>* wie folgt:  
  
 *<Hostname>* **.** *<Primary_Dns_Suffix>*  
  
 Beispielsweise entspricht die IP-Konfiguration  
  
 `Host Name  .  .  .  .  .  .  : MYSERVER`  
  
 `Primary Dns Suffix  .  .  .  : mydomain.Adventure-Works.com`  
  
 dem folgenden vollqualifizierten Domänennamen:  
  
 `MYSERVER.mydomain.Adventure-Works.com`  
  
##  <a name="Examples"></a> Beispiele  
 Im folgenden Beispiel wird die Server-Netzwerkadresse für eine Serverinstanz auf einem Computersystem namens `REMOTESYSTEM3` in einer anderen Domäne dargestellt. Die Domäneninformationen lauten `NORTHWEST.ADVENTURE-WORKS.COM`, und der Port des Datenbank-Spiegelungsendpunkts ist `7025`. Auf der Grundlage dieser Beispielkomponenten lautet die Server-Netzwerkadresse:  
  
 `TCP://REMOTESYSTEM3.NORTHWEST.ADVENTURE-WORKS.COM:7025`  
  
 Im folgenden Beispiel wird die Server-Netzwerkadresse für eine Serverinstanz auf einem Computersystem namens `DBSERVER1`dargestellt. Dieses System befindet sich in der lokalen Domäne und wird durch seinen Systemnamen eindeutig identifiziert. Der Port des Datenbank-Spiegelungsendpunkts ist `7022`.  
  
 `TCP://DBSERVER1:7022`  
  
##  <a name="RelatedTasks"></a> Verwandte Aufgaben  
  
-   [Erstellen eines Endpunkts der Datenbankspiegelung für Windows-Authentifizierung &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)  
  
## Siehe auch  
 [Datenbankspiegelung &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [Der Datenbankspiegelungs-Endpunkt &#40;SQL Server&#41;](../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)  
  
  