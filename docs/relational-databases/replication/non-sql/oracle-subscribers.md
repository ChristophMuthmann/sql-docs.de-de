---
title: Oracle-Abonnenten | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data types [SQL Server replication], non-SQL Server Subscribers
- Oracle Subscribers [SQL Server replication]
- non-SQL Server Subscribers, Oracle
- heterogeneous Subscribers, Oracle
- mapping data types [SQL Server replication]
ms.assetid: 591c0313-82ce-4689-9fc1-73752ff122cf
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 35360f2cfd76745e0222845f3bac0dd868283657
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/08/2018
---
# <a name="oracle-subscribers"></a>Oracle-Abonnenten
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Ab [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]unterstützt [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Oracle-Pushabonnements über den von Oracle bereitgestellten Oracle OLE DB-Anbieter.  
  
## <a name="configuring-an-oracle-subscriber"></a>Konfigurieren eines Oracle-Abonnenten  
 Führen Sie zum Konfigurieren eines Oracle-Abonnenten folgende Schritte aus:  
  
1.  Installieren und konfigurieren Sie die Oracle-Clientnetzwerksoftware sowie den Oracle OLE DB-Anbieter auf dem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Verteiler, damit dieser die Verbindung mit dem Oracle-Abonnenten herstellen kann. Sie sollten dazu die aktuellste verfügbare Version der Oracle-Clientnetzwerksoftware verwenden. Oracle empfiehlt Benutzern, die aktuellste Version der Clientsoftware zu installieren. Dabei ist die Clientsoftware häufig aktueller als die Datenbanksoftware. Am einfachsten lässt sich die Software mithilfe des Oracle Universal Installer von der Oracle-Client-CD installieren. Im Oracle Universal Installer müssen Sie folgende Informationen angeben:  
  
    |Information|Description|  
    |-----------------|-----------------|  
    |Oracle-Homeverzeichnis|Der Pfad zum Installationsverzeichnis für die Oracle-Software. Übernehmen Sie die Standardeinstellung (C:\oracle\ora90 oder Ähnliches), oder geben Sie einen anderen Pfad ein. Weitere Informationen zum Oracle-Homeverzeichnis finden Sie im Abschnitt zu Überlegungen zum Oracle-Homeverzeichnis weiter unten in diesem Thema.|  
    |Oracle-Homeverzeichnisname|Alias für den Pfad zum Oracle-Homeverzeichnis.|  
    |Installationstyp|Wählen Sie in Oracle 10g die Installationsoption **Runtime** oder **Administrator** aus.|  
  
2.  Erstellen Sie einen TNS-Namen für den Abonnenten. TNS (Transparent Network Substrate) ist eine von Oracle-Datenbanken verwendete Kommunikationsschicht. Der TNS-Dienstname ist der Name, unter dem eine Oracle-Datenbankinstanz im jeweiligen Netzwerk geführt wird. Den TNS-Dienstnamen können Sie beim Konfigurieren der Konnektivität mit der Oracle-Datenbank zuweisen. Die Replikation verwendet den TNS-Dienstnamen zum Identifizieren des Abonnenten und zum Einrichten der Verbindungen.  
  
     Wenn der Oracle Universal Installer abgeschlossen ist, konfigurieren Sie die Netzwerkkonnektivität mit Net Configuration Assistant. Zur Konfiguration der Netzwerkkonnektivität müssen Sie vier Informationen eingeben. Der Oracle-Datenbankadministrator, der die Netzwerkkonfiguration beim Einrichten der Datenbank und der Überwachung (Listener) konfiguriert, kann Ihnen diese Informationen geben, falls Sie sie nicht selbst besitzen. Führen Sie folgende Schritte aus:  
  
    |Aktion|Description|  
    |------------|-----------------|  
    |Identifizieren Sie die Datenbank.|Es gibt zwei Methoden, mit denen Sie die Datenbank identifizieren können. Die erste Methode besteht darin, die Oracle SID (System Identifier) zu verwenden. Die SID ist in jeder Oracle-Version verfügbar. Die zweite Methode besteht darin, den Dienstnamen zu verwenden, der ab Oracle Version 8.0 verfügbar ist. Beide Methoden basieren auf einem Wert, der beim Erstellen der Datenbank konfiguriert wird. Wichtig ist dabei, dass Sie bei der Clientnetzwerkkonfiguration dieselbe Benennungsmethode verwenden wie der Administrator beim Konfigurieren des Listeners der Datenbank.|  
    |Identifizieren Sie den Datenbankalias.|Für den Zugriff auf die Oracle-Datenbank müssen Sie einen Netzwerkalias angeben. Der Netzwerkalias ist im Wesentlichen ein Zeiger auf die während der Erstellung der Datenbank konfigurierte Remote-SID bzw. den Service Name. In manchen Oracle-Versionen und -Produkten wird er u. a. auch als "Net Service Name" oder "TNS Alias" bezeichnet. SQL*Plus fordert bei der Anmeldung zur Eingabe dieses Netzwerkalias als Parameter "Host String" auf.|  
    |Wählen Sie ein Netzwerkprotokoll aus.|Wählen Sie die Netzwerkprotokolle aus, die unterstützt werden sollen. Die meisten Anwendungen verwenden TCP.|  
    |Geben Sie die Hostinformationen zur Identifikation des Datenbanklisteners an.|Der Host ist der Name oder DNS-Alias des Computers, auf dem der Oracle-Listener ausgeführt wird, d. h. normalerweise der Computer, auf dem sich die Datenbank befindet. Für bestimmte Protokolle müssen Sie zusätzliche Informationen angeben. Wenn Sie TCP ausgewählt haben, müssen Sie beispielsweise auch den Port angeben, an dem der Listener Verbindungsanforderungen zur Zieldatenbank überwachen soll. Standardmäßig verwendet die TCP-Konfiguration Port 1521.|  
  
3.  Erstellen Sie eine Momentaufnahme- oder Transaktionsveröffentlichung, aktivieren Sie sie für Nicht-[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Abonnenten, und erstellen Sie dann ein Pushabonnement für den Abonnenten. Weitere Informationen finden Sie unter [Erstellen eines Abonnements für einen Nicht-SQL Server-Abonnenten](../../../relational-databases/replication/create-a-subscription-for-a-non-sql-server-subscriber.md).  
  
### <a name="setting-directory-permissions"></a>Festlegen von Verzeichnisberechtigungen  
 Dem Konto, unter dem der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Dienst auf dem Verteiler ausgeführt wird, müssen Lese- und Ausführungsberechtigungen für das Verzeichnis (und alle Unterverzeichnisse) erteilt sein, in dem die Oracle-Clientnetzwerksoftware installiert ist.  
  
### <a name="testing-connectivity-between-the-sql-server-distributor-and-the-oracle-publisher"></a>Testen der Konnektivität zwischen SQL Server-Verteiler und Oracle-Verleger  
 Gegen Ende von Net Configuration Assistant steht möglicherweise eine Option zum Testen der Verbindung mit dem Oracle-Abonnenten zur Verfügung. Stellen Sie sicher, dass die Oracle-Datenbankinstanz online ist und der Oracle-Listener ausgeführt wird, bevor Sie die Verbindung testen. Wenn der Test nicht erfolgreich ist, wenden Sie sich an den Administrator der Oracle-Datenbank, zu der Sie die Verbindung herstellen möchten.  
  
 Wenn die Verbindung mit dem Oracle-Abonnenten erfolgreich hergestellt wurde, melden Sie sich bei der Datenbank an, indem Sie das Konto und Kennwort eingeben, die Sie für den Verteilungs-Agenten des Abonnements konfiguriert haben:  
  
1.  Klicken Sie im **Startmenü**auf **Ausführen**.  
  
2.  Geben Sie `cmd` ein und klicken Sie dann auf **OK**.  
  
3.  Geben Sie an der Eingabeaufforderung Folgendes ein:  
  
     `sqlplus <UserSchemaLogin>/<UserSchemaPassword>@<NetServiceName>`  
  
     Beispiel: `sqlplus replication/$tr0ngPasswerd@Oracle90Server`  
  
4.  Wenn die Netzwerkkonfiguration erfolgreich war, werden Sie jetzt angemeldet und sehen folgende `SQL` -Eingabeaufforderung.  
  
### <a name="considerations-for-oracle-home"></a>Überlegungen zum Oracle-Homeverzeichnis  
 Oracle unterstützt die parallele Installation von Anwendungsbinärdateien; die Replikation kann jedoch nur einen Binärdateisatz gleichzeitig verwenden. Jeder Binärdateisatz ist einem Oracle-Homeverzeichnis zugeordnet; die Binärdateien befinden sich im Verzeichnis %ORACLE_HOME%\bin. Stellen Sie sicher, dass die richtigen Binärdateisätze (insbesondere die neueste Version der Clientnetzwerksoftware) verwendet werden, wenn die Replikation Verbindungen zum Oracle-Abonnenten herstellt.  
  
 Melden Sie sich mit den vom [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Dienst und dem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Agentdienst verwendeten Konten beim Verteiler an, und legen Sie die entsprechenden Umgebungsvariablen fest. Die %ORACLE_HOME%-Variable muss auf den Installationspunkt verweisen, den Sie beim Installieren der Clientnetzwerksoftware angegeben haben. Der %PATH% muss das %ORACLE_HOME% \bin-Verzeichnis als ersten Oracle-Eintrag beinhalten. Informationen zum Festlegen von Umgebungsvariablen finden Sie in der Windows-Dokumentation.  
  
> [!NOTE]  
>  Wenn Sie mehr als ein Oracle-Homeverzeichnis auf dem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Verteiler einrichten, stellen Sie sicher, dass der Verteilungs-Agent den neuesten Oracle OLE DB-Anbieter verwendet. In manchen Fällen aktualisiert Oracle den OLE DB-Anbieter beim Update von Clientkomponenten auf dem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Verteiler nicht standardmäßig. Deinstallieren Sie den OLE DB-Anbieter, und installieren Sie den neuesten OLE DB-Anbieter. Weitere Informationen zum Installieren und Deinstallieren des Anbieters finden Sie in der Oracle-Dokumentation.  
  
## <a name="considerations-for-oracle-subscribers"></a>Überlegungen zu Oracle-Abonnenten  
 Abgesehen von den unter dem Thema [Non-SQL Server Subscribers](../../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)angestellten Überlegungen sollten Sie bei der Replikation auf Oracle-Abonnenten folgende Aspekte berücksichtigen:  
  
-   Oracle behandelt sowohl leere Zeichenfolgen als auch NULL-Werte als NULL. Dies ist wichtig, wenn Sie eine [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Spalte als NOT NULL definieren und auf einen Oracle-Abonnenten replizieren. Um Fehler beim Anwenden von Änderungen auf dem Oracle-Abonnenten zu vermeiden, führen Sie einen der folgenden Schritte aus:  
  
    -   Stellen Sie sicher, dass keine leeren Zeichenfolgen als Spaltenwerte in die veröffentlichte Tabelle eingefügt werden.  
  
    -   Verwenden Sie für den Verteilungs-Agent den **–SkipErrors** -Parameter, wenn eine Fehlerbenachrichtigung im Verlaufsprotokoll des Verteilungs-Agents genügt und die Verarbeitung ansonsten fortgesetzt werden kann. Geben Sie den Oracle-Fehlercode 1400 (**-SkipErrors1400**) an.  
  
    -   Entfernen Sie das NOT NULL-Attribut aus allen Zeichenspalten, denen eventuell leere Zeichenfolgen zugeordnet werden können, aus dem generierten CREATE TABLE-Skript, und geben Sie das geänderte Skript mithilfe des @creation_script -Parameters von [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)als benutzerdefiniertes Skript für den Artikel an.  
  
-   Oracle-Abonnenten unterstützen eine Schemaoption von 0x4071. Weitere Informationen zu den Schemaoptionen finden Sie unter [sp_addarticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md).  
  
## <a name="mapping-data-types-from-sql-server-to-oracle"></a>Zuordnen von SQL Server-Datentypen zu Oracle-Datentypen  
 Die folgende Tabelle zeigt die bei der Replikation von Daten auf einem Oracle-Abonnenten verwendeten Datentypzuordnungen.  
  
|SQL Server-Datentyp|Oracle-Datentyp|  
|--------------------------|----------------------|  
|**bigint**|NUMBER(19,0)|  
|**Binary(1-2000)**|RAW(1-2000)|  
|**Binary(2001-8000)**|BLOB|  
|**bit**|NUMBER(1)|  
|**char(1-2000)**|CHAR(1-2000)|  
|**Char(2001-4000)**|VARCHAR2(2001-4000)|  
|**Char(4001-8000)**|CLOB|  
|**date**|DATE|  
|**datetime**|DATE|  
|**DATETIME2(0-7)**|TIMESTAMP(7) für Oracle 9 und Oracle 10; VARCHAR(27) für Oracle 8|  
|**DATETIMEOFFSET(0-7)**|TIMESTAMP(7) WITH TIME ZONE für Oracle 9 und Oracle 10; VARCHAR(34) für Oracle 8|  
|**decimal(1-38, 0-38)**|NUMBER(1-38, 0-38)|  
|**float(53)**|GLEITKOMMAZAHL|  
|**float**|GLEITKOMMAZAHL|  
|**geography**|BLOB|  
|**Geometrie**|BLOB|  
|**hierarchyid**|BLOB|  
|**image**|BLOB|  
|**int**|NUMBER(10,0)|  
|**money**|NUMBER(19,4)|  
|**NCHAR(1-1000)**|CHAR(1-1000)|  
|**NCHAR(1001-4000)**|NCLOB|  
|**ntext**|NCLOB|  
|**NUMERIC(1-38, 0-38)**|NUMBER(1-38, 0-38)|  
|**NCHAR(1-1000)**|VARCHAR2(1-2000)|  
|**NCHAR(1001-4000)**|NCLOB|  
|**nvarchar(max)**|NCLOB|  
|**real**|real|  
|**smalldatetime**|DATE|  
|**smallint**|NUMBER(5,0)|  
|**smallmoney**|NUMBER(10,4)|  
|**sql_variant**|–|  
|**sysname**|VARCHAR2(128)|  
|**text**|CLOB|  
|**TIME(0-7)**|VARCHAR(16)|  
|**timestamp**|RAW(8)|  
|**tinyint**|NUMBER(3,0)|  
|**uniqueidentifier**|CHAR(38)|  
|**varbinary(1-2000)**|RAW(1-2000)|  
|**varbinary(2001-8000)**|BLOB|  
|**VARCHAR(1-4000)**|VARCHAR2(1-4000)|  
|**VARCHAR(4001-8000)**|CLOB|  
|**varbinary(max)**|BLOB|  
|**varchar(max)**|CLOB|  
|**xml**|NCLOB|  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Non-SQL Server Subscribers](../../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)   
 [Subscribe to Publications](../../../relational-databases/replication/subscribe-to-publications.md)  
  
  
