---
title: Konfigurieren eines Oracle-Verlegers | Microsoft-Dokumentation
ms.custom: 
ms.date: 09/05/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Oracle publishing [SQL Server replication], configuring
ms.assetid: 240c8416-c8e5-4346-8433-07e0f779099f
caps.latest.revision: "60"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 57b1971bbd25071242b35f32b25ffebbaf4fe6f5
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="configure-an-oracle-publisher"></a>Konfigurieren eines Oracle-Verlegers
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Veröffentlichungen von Oracle-Verlegern werden auf dieselbe Weise erstellt wie gängige Momentaufnahmen- und Transaktionsveröffentlichungen. Vor der Erstellung einer Veröffentlichung eines Oracle-Verlegers müssen jedoch folgende Schritte ausgeführt werden (die Schritte eins, drei und vier werden in diesem Thema ausführlich beschrieben):  
  
1.  Erstellen Sie innerhalb der Oracle-Datenbank mit dem angegebenen Skript einen administrativen Replikationsbenutzer.  
  
2.  Erteilen Sie dem in Schritt 1 erstellten administrativen Oracle-Benutzer für die Tabellen, die Sie veröffentlichen möchten, direkt für die jeweilige Tabelle (nicht über eine Rolle) eine SELECT-Berechtigung.  
  
3.  Installieren Sie die Oracle-Clientsoftware und den OLE DB-Anbieter auf dem [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Verteiler, und starten Sie den Server der Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] anschließend neu. Wenn der Verteiler auf einer 64-Bit-Plattform ausgeführt wird, müssen Sie die 64-Bit-Version des Oracle OLE DB-Anbieters verwenden.  
  
4.  Konfigurieren Sie die Oracle-Datenbank auf dem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Verteiler als Verleger.  

[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] unterstützt die folgenden heterogenen Szenarien für die Transaktions- und Momentaufnahmereplikation:  
  
-   Veröffentlichen von Daten aus [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] an Nicht-[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Abonnenten.  

-   Beim Veröffentlichen von Daten an und von Oracle bestehen folgende Einschränkungen:  
  | |2016 oder früher |2017 oder höher |
  |-------|-------|--------|
  |Replikation von Oracle |Wird nur für Oracle 10g oder früher unterstützt |Wird nur für Oracle 10g oder früher unterstützt |
  |Replikation zu Oracle |Bis Oracle 12c |Nicht unterstützt |

 Die heterogene Replikation an Nicht-SQL Server-Abonnenten ist veraltet. Das Veröffentlichen mit Oracle ist veraltet. Um Daten zu verschieben, erstellen Sie Lösungen mit Change Data Capture und [!INCLUDE[ssIS](../../../includes/ssis-md.md)].  


 Eine Liste der Objekte, die aus der Oracle-Datenbank repliziert werden können, finden Sie unter [Überlegungen zum Entwurf und Einschränkungen für Oracle-Verleger](../../../relational-databases/replication/non-sql/design-considerations-and-limitations-for-oracle-publishers.md).  
  
> [!NOTE]  
>  Sie müssen ein Mitglied der festen Serverrolle **sysadmin** sein, um einen Verleger oder Verteiler zu aktivieren und um eine Oracle-Veröffentlichung bzw. ein Abonnement einer Oracle-Veröffentlichung erstellen zu können.  
  
## <a name="creating-the-replication-administrative-user-schema-within-the-oracle-database"></a>Erstellen des Schemas für den administrativen Replikationsbenutzer innerhalb der Oracle-Datenbank  
 Replikations-Agents stellen eine Verbindung mit der Oracle-Datenbank her und führen Operationen im Kontext eines Benutzerschemas aus, das Sie erstellen müssen. Diesem Schema müssen mehrere Berechtigungen erteilt werden, die im nächsten Abschnitt aufgeführt werden. Dieses Schema besitzt mit Ausnahme des öffentlichen Synonyms [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] replication process on the Oracle Publisher, with the exception of a public synonym, **MSSQLSERVERDISTRIBUTOR**. Weitere Informationen zu den in der Oracle-Datenbank erstellten Objekten finden Sie unter [Objects Created on the Oracle Publisher](../../../relational-databases/replication/non-sql/objects-created-on-the-oracle-publisher.md).  
  
> [!NOTE]  
>  Beim Löschen des öffentlichen Synonyms **MSSQLSERVERDISTRIBUTOR** und des konfigurierten Oracle-Replikationsbenutzers mit der **CASCADE** -Option werden alle Replikationsobjekte vom Oracle-Verleger entfernt.  
  
 Es wurde ein Beispielskript angegeben, um das Setup des Schemas für den Oracle-Replikationsbenutzer zu erleichtern. Nach dem Installieren von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ist das Skript im folgenden Verzeichnis verfügbar: *\<Laufwerk>*:\\\Programme\Microsoft SQL Server\\*\<Instanzname>*\MSSQL\Install\oracleadmin.sql. Es ist auch im Thema [Script to Grant Oracle Permissions](../../../relational-databases/replication/non-sql/script-to-grant-oracle-permissions.md)enthalten.  
  
 Stellen Sie mithilfe eines Kontos mit DBA-Berechtigungen eine Verbindung mit der Oracle-Datenbank her, und führen Sie das Skript aus. Dieses Skript fordert zur Eingabe des Benutzernamens und des Kennworts für das Schema des administrativen Replikationsbenutzers sowie der Standardtabellenbereich, in der die Objekte erstellt werden sollen (der Tabellenbereich muss in der Oracle-Datenbank bereits vorhanden sein), auf. Informationen zum Angeben anderer Tabellenbereiche für Objekte finden Sie unter [Verwalten von Oracle-Tabellenbereichen](../../../relational-databases/replication/non-sql/manage-oracle-tablespaces.md). Wählen Sie einen beliebigen Benutzernamen und ein sicheres Kennwort aus. Notieren Sie sich jedoch beides, da Sie diese Informationen später beim Konfigurieren der Oracle-Datenbank als Verleger erneut bereitstellen müssen. Es empfiehlt sich, das Schema nur für Objekte zu verwenden, die für die Replikation erforderlich sind. Erstellen Sie keine Tabellen, die in diesem Schema veröffentlicht werden sollen.  
  
### <a name="creating-the-user-schema-manually"></a>Manuelles Erstellen des Benutzerschemas  
 Wenn Sie das Schema für den administrativen Replikationsbenutzer erstellen, müssen Sie dem Schema entweder direkt oder über eine Datenbankrolle folgende Berechtigungen erteilen:  
  
-   CREATE PUBLIC SYNONYM und DROP PUBLIC SYNONYM  
  
-   CREATE PROCEDURE  
  
-   CREATE SEQUENCE  
  
-   CREATE SESSION  
  
 Zudem müssen Sie dem Benutzer folgende Berechtigungen direkt (nicht über eine Rolle) erteilen:  
  
-   CREATE ANY TRIGGER Dies ist sowohl bei der Momentaufnahme- als auch bei der Transaktionsreplikation erforderlich.  
  
-   CREATE TABLE  
  
-   CREATE VIEW  
  
## <a name="installing-and-configuring-oracle-client-networking-software-on-the-sql-server-distributor"></a>Installieren und Konfigurieren der Oracle-Clientnetzwerksoftware auf dem SQL Server-Verteiler  
 Sie müssen die Oracle-Clientnetzwerksoftware und den Oracle OLE DB-Anbieter auf dem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Verteiler installieren, sodass der Verteiler Verbindungen mit dem Oracle-Verleger herstellen kann. Nach dem Installieren der Software legen Sie die entsprechenden Berechtigungen in den Ordnern fest, in denen die Software installiert wurde, und starten Sie dann die Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] neu, um sicherzustellen, dass alle Einstellungen aktualisiert werden (Berechtigungen werden unten im Abschnitt zum Festlegen von Verzeichnisberechtigungen beschrieben).  
  
> [!NOTE]  
>  Die Oracle-Clientnetzwerksoftware muss die neueste verfügbare Version aufweisen. Oracle empfiehlt Benutzern, die aktuellste Version der Clientsoftware zu installieren. Dabei ist die Clientsoftware häufig aktueller als die Datenbanksoftware.  
  
 Die einfachste Methode zum Installieren und Konfigurieren der Clientnetzwerksoftware ist das Verwenden von Oracle Universal Installer und des Net-Konfigurationsassistenten auf dem Datenträger des Oracle-Clients.  
  
 Im Oracle Universal Installer müssen Sie folgende Informationen angeben:  
  
|Informationen|Beschreibung|  
|-----------------|-----------------|  
|Oracle-Homeverzeichnis|Der Pfad zum Installationsverzeichnis für die Oracle-Software. Übernehmen Sie die Standardeinstellung (C:\oracle\ora90 oder Ähnliches), oder geben Sie einen anderen Pfad ein. Weitere Informationen zum Oracle-Homeverzeichnis finden Sie im Abschnitt zu Überlegungen zum Oracle-Homeverzeichnis weiter unten in diesem Thema.|  
|Oracle-Homeverzeichnisname|Alias für den Pfad zum Oracle-Homeverzeichnis.|  
|Installationstyp|Wählen Sie in Oracle 10g die Installationsoption **Administrator** aus.|  
  
 Wenn der Oracle Universal Installer abgeschlossen ist, konfigurieren Sie die Netzwerkkonnektivität mit Net Configuration Assistant. Zur Konfiguration der Netzwerkkonnektivität müssen Sie vier Informationen eingeben. Der Oracle-Datenbankadministrator, der die Netzwerkkonfiguration beim Einrichten der Datenbank und der Überwachung (Listener) konfiguriert, kann Ihnen diese Informationen geben, falls Sie sie nicht selbst besitzen. Führen Sie folgende Schritte aus:  
  
|Aktion|Beschreibung|  
|------------|-----------------|  
|Identifizieren Sie die Datenbank.|Es gibt zwei Methoden, mit denen Sie die Datenbank identifizieren können. Die erste Methode besteht darin, die Oracle SID (System Identifier) zu verwenden. Die SID ist in jeder Oracle-Version verfügbar. Die zweite Methode besteht darin, den Dienstnamen zu verwenden, der ab Oracle Version 8.0 verfügbar ist. Beide Methoden basieren auf einem Wert, der beim Erstellen der Datenbank konfiguriert wird. Wichtig ist dabei, dass Sie bei der Clientnetzwerkkonfiguration dieselbe Benennungsmethode verwenden wie der Administrator beim Konfigurieren des Listeners der Datenbank.|  
|Identifizieren Sie den Datenbankalias.|Für den Zugriff auf die Oracle-Datenbank müssen Sie einen Netzwerkalias angeben. Dieser Alias muss auch angegeben werden, wenn Sie die Oracle-Datenbank auf dem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Verteiler als Verleger identifizieren. Der Netzwerkalias ist im Wesentlichen ein Zeiger auf die während der Erstellung der Datenbank konfigurierte Remote-SID bzw. den Service Name. In manchen Oracle-Versionen und -Produkten wird er u. a. auch als "Net Service Name" oder "TNS Alias" bezeichnet. SQL*Plus fordert bei der Anmeldung zur Eingabe dieses Netzwerkalias als Parameter "Host String" auf.|  
|Wählen Sie ein Netzwerkprotokoll aus.|Wählen Sie die Netzwerkprotokolle aus, die unterstützt werden sollen. Die meisten Anwendungen verwenden TCP.|  
|Geben Sie die Hostinformationen zur Identifikation des Datenbanklisteners an.|Der Host ist der Name oder DNS-Alias des Computers, auf dem der Oracle-Listener ausgeführt wird, d. h. normalerweise der Computer, auf dem sich die Datenbank befindet. Für bestimmte Protokolle müssen Sie zusätzliche Informationen angeben. Wenn Sie TCP ausgewählt haben, müssen Sie beispielsweise auch den Port angeben, an dem der Listener Verbindungsanforderungen zur Zieldatenbank überwachen soll. Standardmäßig verwendet die TCP-Konfiguration Port 1521.|  
  
### <a name="setting-directory-permissions"></a>Festlegen von Verzeichnisberechtigungen  
 Dem Konto, unter dem der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Dienst auf dem Verteiler ausgeführt wird, müssen Lese- und Ausführungsberechtigungen für das Verzeichnis (und alle Unterverzeichnisse) erteilt sein, in dem die Oracle-Clientnetzwerksoftware installiert ist.  
  
### <a name="testing-connectivity-between-the-sql-server-distributor-and-the-oracle-publisher"></a>Testen der Konnektivität zwischen dem SQL Server-Verteiler und dem Oracle-Verleger  
 Gegen Ende des Net Configuration Assistant sollte eine Option zum Testen der Verbindung mit dem Oracle-Verleger verfügbar sein. Stellen Sie sicher, dass die Oracle-Datenbankinstanz online ist und der Oracle-Listener ausgeführt wird, bevor Sie die Verbindung testen. Wenn der Test nicht erfolgreich ist, wenden Sie sich an den Administrator der Oracle-Datenbank, zu der Sie die Verbindung herstellen möchten.  
  
 Wenn Sie eine Verbindung mit dem Oracle-Verleger herstellen konnten, versuchen Sie, sich mit dem Konto und dem Kennwort bei der Datenbank anzumelden, die dem erstellten Schema für den administrativen Replikationsbenutzer zugeordnet sind. Beim Ausführen unter demselben Windows-Konto, das der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Dienst verwendet, muss Folgendes ausgeführt werden:  
  
1.  Klicken Sie im **Startmenü**auf **Ausführen**.  
  
2.  Geben Sie `cmd` ein und klicken Sie dann auf **OK**.  
  
3.  Geben Sie an der Eingabeaufforderung Folgendes ein:  
  
     `sqlplus <UserSchemaLogin>/<UserSchemaPassword>@<NetServiceName>`  
  
     Beispiel: `sqlplus replication/$tr0ngPasswerd@Oracle90Server`  
  
4.  Wenn die Netzwerkkonfiguration erfolgreich war, werden Sie jetzt angemeldet und sehen folgende `SQL`-Eingabeaufforderung.  
  
5.  Wenn Sie Probleme haben, eine Verbindung mit der Oracle-Datenbank herzustellen, finden Sie entsprechende Informationen in dem Abschnitt in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , der sich mit Verbindungsproblemen zwischen dem [ssNoVersion](../../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md).  
  
### <a name="considerations-for-oracle-home"></a>Überlegungen zum Oracle-Homeverzeichnis  
 Oracle unterstützt die parallele Installation von Anwendungsbinärdateien; die Replikation kann jedoch nur einen Binärdateisatz gleichzeitig verwenden. Jeder Binärdateisatz ist einem Oracle-Homeverzeichnis zugeordnet; die Binärdateien befinden sich im Verzeichnis %ORACLE_HOME%\bin. Sie müssen sicherstellen, dass das richtige Set von Binärdateien (insbesondere die neueste Version der Clientnetzwerksoftware) verwendet wird, wenn die Replikation Verbindungen mit dem Oracle-Verleger herstellt.  
  
 Melden Sie sich mit den vom [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Dienst und dem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Agentdienst verwendeten Konten beim Verteiler an, und legen Sie die entsprechenden Umgebungsvariablen fest. Die %ORACLE_HOME%-Variable muss auf den Installationspunkt verweisen, den Sie beim Installieren der Clientnetzwerksoftware angegeben haben. Der %PATH% muss das %ORACLE_HOME% \bin-Verzeichnis als ersten Oracle-Eintrag beinhalten. Informationen zum Festlegen von Umgebungsvariablen finden Sie in der Windows-Dokumentation.  
  
## <a name="configuring-the-oracle-database-as-a-publisher-at-the-sql-server-distributor"></a>Konfigurieren der Oracle-Datenbank als Verleger auf dem SQL Server-Verteiler  
 Oracle-Verleger verwenden immer einen Remoteverteiler. Sie müssen eine Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] konfigurieren, die als Verteiler für den Oracle-Verleger fungieren soll (ein Oracle-Verleger kann nur einen Verteiler verwenden, ein Verteiler kann jedoch mehrere Oracle-Verleger bedienen). Nach dem Konfigurieren eines Verteilers identifizieren Sie über [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , Transact-SQL oder Replikationsverwaltungsobjekte (RMO) die Oracle-Datenbankinstanzen auf dem [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]-Verteiler, die als Verleger fungieren sollen. Weitere Informationen zum Konfigurieren eines Verteilers finden Sie unter [Konfigurieren der Verteilung](../../../relational-databases/replication/configure-distribution.md).  
  
> [!NOTE]  
>  Ein Oracle-Verleger darf nicht denselben Namen aufweisen wie der zugehörige [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Verteiler oder wie ein anderer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Verleger, der denselben Verteiler verwendet.  
  
 Wenn Sie die Oracle-Datenbank als Verleger identifizieren, müssen Sie eine Oracle-Veröffentlichungsoption auswählen: Vollständig oder Oracle-Gateway. Nachdem ein Verleger identifiziert wurde, kann diese Option nicht mehr geändert werden, ohne dass der Verleger gelöscht und neu konfiguriert wird. Bei Verwendung der Option Vollständig werden Momentaufnahme- und Transaktionsveröffentlichungen mit dem vollständigen Satz der unterstützten Funktionen für das Veröffentlichen mit Oracle bereitgestellt. Die Oracle-Gateway-Option bietet spezifische Entwurfsoptimierungen für die Verbesserung der Leistung für den Fall, dass die Replikation als Gateway zwischen Systemen fungiert.  
  
 Nachdem der Oracle-Verleger auf dem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Verteiler identifiziert wurde, erstellt die Replikation einen Verbindungsserver mit dem Namen des TNS-Dienstes der Oracle-Datenbank. Dieser Verbindungsserver kann ausschließlich von der Replikation verwendet werden. Wenn Sie über eine Verbindungsserververbindung eine Verbindung mit dem Oracle-Verleger herstellen müssen, erstellen Sie einen anderen TNS-Dienstnamen, und verwenden Sie dann diesen Namen für den Aufruf von [p_addlinkedserver &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md).  
  
 Informationen zum Konfigurieren eines Oracle-Verlegers und zum Erstellen einer Veröffentlichung finden Sie unter [Create a Publication from an Oracle Database](../../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Überlegungen zu administrativen Aufgaben bei Oracle-Verlegern](../../../relational-databases/replication/non-sql/administrative-considerations-for-oracle-publishers.md)   
 [Datentypzuordnung für Oracle-Verleger](../../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md)   
 [Begriffe im Zusammenhang mit dem Veröffentlichen von Oracle-Daten](../../../relational-databases/replication/non-sql/glossary-of-terms-for-oracle-publishing.md)   
 [Oracle Publishing Overview](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md)  
  
  
