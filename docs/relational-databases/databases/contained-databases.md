---
title: "Eigenständige Datenbanken | Microsoft-Dokumentation"
ms.custom: 
ms.date: 08/24/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: databases
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- contained database
- database_uncontained_usage event
- partially contained database
- contained database, understanding
ms.assetid: 36af59d7-ce96-4a02-8598-ffdd78cdc948
caps.latest.revision: "37"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: a0569381edb5d6ff8142818fb5d1382f28e7ad09
ms.sourcegitcommit: d28d9e3413b6fab26599966112117d45ec2c7045
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/11/2018
---
# <a name="contained-databases"></a>Eigenständige Datenbanken
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Eine *eigenständige Datenbank* ist eine Datenbank, die von anderen Datenbanken und der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , der die Datenbank hostet, isoliert ist.  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] hilft Benutzern dabei, ihre Datenbank von der Instanz auf vier Arten zu isolieren.  
  
-   Eine Menge der Metadaten, die eine Datenbank beschreiben, wird in der Datenbank verwaltet. (Zusätzlich zur oder anstelle der Verwaltung von Metadaten in der master-Datenbank.)  
  
-   Alle Metadaten werden definiert über die gleiche Sortierung.  
  
-   Die Benutzerauthentifizierung kann von der Datenbank ausgeführt werden, wodurch die Abhängigkeit der Datenbanken beim Anmelden der Instanz auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]reduziert wird.  
  
-   Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Umgebung (DMVs, XEvents usw.) berichtet und kann auf Kapselungsinformationen reagieren.  
  
 Einige Funktionen von teilweise eigenständigen Datenbanken, beispielsweise das Speichern von Metadaten in der Datenbank, gelten für alle [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] -Datenbanken. Einige Vorteile der teilweise eigenständigen Datenbanken, beispielsweise Authentifizierung auf Datenbankebene und Katalogsortierung, müssen erst aktiviert werden, damit sie verfügbar sind. Die partielle Eigenständigkeit wird mithilfe der Anweisungen **CREATE DATABASE** und **ALTER DATABASE** oder mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]aktiviert. Weitere Informationen zum Aktivieren der Sortierung teilweiser Datenbanken finden Sie unter [Migrate to a Partially Contained Database](../../relational-databases/databases/migrate-to-a-partially-contained-database.md).  
  
##  <a name="Concepts"></a> Konzepte zur teilweise eigenständigen Datenbank  
 Eine vollständig eigenständige Datenbank schließt alle erforderlichen Datenbankeinstellungen und Metadaten zum Definieren der Datenbank ein, und ihre Konfiguration ist nicht von der [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] -Instanz abhängig, in der die Datenbank installiert ist. In früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]konnte das Trennen einer Datenbank von der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eine zeitraubende Angelegenheit sein, und es erforderte ein fundiertes Wissen der Beziehung zwischen den Datenbanken und der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Die teilweise eigenständigen Datenbanken erleichtern das Trennen einer Datenbank von der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und anderen Datenbanken.  
  
 In der eigenständigen Datenbank werden Funktionen entsprechend der Kapselung erkannt. Jede benutzerdefinierte Entität, die sich ausschließlich auf Funktionen stützt, die in der Datenbank enthalten sind, wird als vollständig enthalten angesehen. Jede benutzerdefinierte Entität, die sich ausschließlich auf Funktionen stützt, die sich außerhalb der Datenbank befinden, wird als nicht enthalten angesehen. (Weitere Informationen finden Sie im Abschnitt [Eigenständigkeit](#containment) in diesem Thema.)  
  
 Die folgenden Begriffe beziehen sich auf das enthaltene Datenbankmodell.  
  
 Datenbankbegrenzung  
 Die Grenze zwischen einer Datenbank und der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Die Grenze zwischen einer Datenbank und anderen Datenbanken.  
  
 Enthalten  
 Ein Element, das vollständig innerhalb der Datenbankbegrenzung vorhanden ist.  
  
 Nicht enthalten  
 Ein Element, das die Datenbankbegrenzung überschreitet.  
  
 Nicht enthaltene Datenbank  
 Eine Datenbank, deren Eigenständigkeit auf **NONE**festgelegt ist. Alle Datenbanken in Versionen vor [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] sind nicht enthalten. Die Kapselung aller Datenbanken von [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] und höher ist standardmäßig auf **NONE**festgelegt.  
  
 Teilweise enthaltene Datenbank  
 Eine teilweise eigenständige Datenbank ist eine eigenständige Datenbank, die einige Funktionen zulassen kann, die die Datenbankbegrenzung überschreiten. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] enthält die Fähigkeit ein zu bestimmen, wann die Kapselungsbegrenzung überschritten wird.  
  
 Enthaltener Benutzer  
 Es gibt zwei Typen von Benutzern für enthaltene Datenbanken.  
  
-   **Benutzer einer enthaltenen Datenbank mit Kennwort**  
  
     Benutzer von enthaltenen Datenbanken mit Kennwort werden von der Datenbank authentifiziert. Weitere Informationen finden Sie unter [Eigenständige Datenbankbenutzer - machen Sie Ihre Datenbank portabel](../../relational-databases/security/contained-database-users-making-your-database-portable.md).  
  
-   **Windows-Prinzipale**  
  
     Autorisierte Windows-Benutzer und Mitglieder autorisierter Windows-Gruppen können direkt eine Verbindung mit der Datenbank herstellen, wobei keine Anmeldung in der **master** -Datenbank benötigt wird. Die Datenbank vertraut der Authentifizierung von Windows.  
  
 Benutzern kann auf Basis der Anmeldungen in der **master** -Datenbank Zugriff auf eine eigenständige Datenbank gewährt werden. Dies würde jedoch eine Abhängigkeit auf der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz zur Folge haben. Daher sollten Sie beim Erstellen von Benutzern auf Basis von Anmeldungen den Kommentar für teilweise eigenständige Datenbanken durchlesen.  
  
> [!IMPORTANT]  
>  Das Aktivieren von teilweise eigenständigen Datenbanken delegiert die Steuerung über den Zugriff auf die Instanz der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] an die Besitzer der Datenbank. Weitere Informationen finden Sie unter [Security Best Practices with Contained Databases](../../relational-databases/databases/security-best-practices-with-contained-databases.md).  
  
 Datenbankbegrenzung  
 Da teilweise eigenständige Datenbanken Datenbankfunktionen von den Funktionen der Instanz trennen, besteht eine eindeutig definierte Trennlinie zwischen diesen beiden Elementen. Diese wird als *Datenbankbegrenzung*bezeichnet.  
  
 Innerhalb der Datenbankbegrenzung befindet sich das *Datenbankmodell*, in dem die Datenbanken entwickelt und verwaltet werden. Beispiele für Entitäten, die sich innerhalb der Datenbank befinden, sind Systemtabellen (z.B. **sys.tables**), eigenständige Datenbankbenutzer mit Kennwörtern sowie Benutzertabellen in der aktuellen Datenbank, auf die mit einem zweiteiligen Namen verwiesen wird.  
  
 Außerhalb der Datenbankbegrenzung befindet sich das *Verwaltungsmodell*, das sich auf Funktionen auf Instanzebene und auf die Verwaltung bezieht. Beispiele für Entitäten, die sich außerhalb der Datenbankbegrenzung befinden, sind Systemtabellen wie **sys.endpoints**, zu Anmeldungen zugeordnete Benutzer und Benutzertabellen in einer anderen Datenbank, auf die mit einem dreiteiligen Namen verwiesen wird.  
  
##  <a name="containment"></a> Eigenständigkeit  
 Benutzerentitäten, die sich vollständig innerhalb der Datenbank befinden, werden als *enthalten*angesehen. Alle Benutzerentitäten, die sich außerhalb der Datenbank befinden oder sich auf die Interaktion mit Funktionen außerhalb der Datenbank stützen, werden als *nicht enthalten*angesehen.  
  
 Im Allgemeinen sind Benutzerentitäten folgenden Kapselungskategorien zuzuordnen:  
  
-   Vollständig eigenständige Benutzerentitäten (Entitäten, die nie die Datenbankbegrenzung überschreiten), z.B. „sys.indexes“. Jeglicher Code, in dem diese Funktionen oder Objekte verwendet werden, die nur auf diese Entitäten verweisen, ist ebenfalls vollständig enthalten.  
  
-   Nicht eigenständige Benutzerentitäten (Entitäten, die die Datenbankbegrenzung überschreiten), z.B. „sys.server_principals“ oder ein Serverprinzipal (eine Anmeldung) selbst. Jeglicher Code, in dem diese Entitäten oder Funktionen verwendet werden, die auf diese Entitäten verweisen, ist nicht enthalten.  
  
###  <a name="partial"></a> Partially Contained Database  
 Die Funktion der enthaltenen Datenbank ist derzeit nur in einem teilweise enthaltenen Status verfügbar. Eine teilweise enthaltene Datenbank ist eine enthaltene Datenbank, die die Verwendung nicht enthaltener Funktionen zulässt.  
  
 Geben Sie Informationen zu nicht eigenständigen Objekten und Funktionen mithilfe von [sys.dm_db_uncontained_entities](../../relational-databases/system-dynamic-management-views/sys-dm-db-uncontained-entities-transact-sql.md) und [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md) zurück. Durch Bestimmen des Kapselungsstatus der Elemente von Datenbanken können Sie ermitteln, welche Objekte und Funktionen ersetzt oder geändert werden müssen, um eine Kapselung zu erzielen.  
  
> [!IMPORTANT]  
>  Da bestimmte Objekte bei der Eigenständigkeit die Standardeinstellung **NONE**aufweisen, werden von dieser Sicht möglicherweise falsch positive Ergebnisse zurückgegeben.  
  
 Das Verhalten teilweise eigenständiger Datenbanken unterscheidet sich von dem abhängiger Datenbanken am deutlichsten hinsichtlich der Sortierung. Weitere Informationen zu Sortierungsaspekten finden Sie unter [Contained Database Collations](../../relational-databases/databases/contained-database-collations.md).  
  
##  <a name="benefits"></a> Vorteile des Verwendens von teilweise enthaltenen Datenbanken  
 Im Zusammenhang mit abhängigen Datenbanken treten Probleme und Schwierigkeiten auf, die mithilfe einer teilweise eigenständigen Datenbank behoben werden können.  
  
### <a name="database-movement"></a>Verschiebung von Datenbanken  
 Eines der Probleme, das beim Verschieben von Datenbanken auftritt, besteht darin, dass einige wichtige Informationen beim Verschieben der Datenbank von einer Instanz zu einer anderen möglicherweise nicht verfügbar ist. Beispielsweise werden Anmeldeinformationen innerhalb der Instanz gespeichert und nicht in der Datenbank. Wenn Sie eine abhängige Datenbank von einer Instanz in eine andere [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz verschieben, bleiben diese Daten zurück. Sie müssen die fehlenden Daten bestimmen und zusammen mit der Datenbank in die neue [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz verschieben. Dieser Vorgang kann schwierig und zeitaufwendig sein.  
  
 Die teilweise eigenständige Datenbank kann wichtige Daten in der Datenbank speichern. Demnach verfügt die Datenbank auch nach dem Verschieben weiterhin über die Daten.  
  
> [!NOTE]  
>  Eine teilweise eigenständige Datenbank ermöglicht die Dokumentation, womit jene Funktionen beschrieben werden, die von der Datenbank verwendet und nicht von der Instanz getrennt werden können. Hierzu zählen eine Liste anderer Datenbanken, von denen die Datenbank abhängt, Systemeinstellungen, die für die Datenbank erforderlich sind, jedoch nicht enthalten sein können usw.  
  
### <a name="benefit-of-contained-database-users-with-always-on"></a>Vorteil Benutzern von eigenständigen Datenbanken mit Always On  
 Durch die Reduzierung der Verknüpfungen in Bezug auf die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]können teilweise eigenständige Datenbanken bei einem Failover nützlich sein, wenn Sie [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]verwenden.  
  
 Durch die Erstellung von enthaltenen Benutzern kann der Benutzer direkt eine Verbindung mit der enthaltenen Datenbank herstellen. Dies ist eine sehr bedeutende Funktion in Szenarien mit Hochverfügbarkeit und Notfallwiederherstellung, z.B. in einer Always On-Lösung. Wenn die Benutzer enthaltene Benutzer sind, können bei einem Failover Verbindungen zur sekundären Komponente hergestellt werden, ohne dass Anmeldungen bei der Instanz erforderlich sind, die die sekundäre Komponente hostet. Dies bietet einen unmittelbaren Vorteil. Weitere Informationen finden Sie unter [Übersicht über Always On-Verfügbarkeitsgruppen (SQL Server)](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md) und [Voraussetzungen, Einschränkungen und Empfehlungen für Always On-Verfügbarkeitsgruppen (SQL Server)](../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md).  
  
### <a name="initial-database-development"></a>Anfängliche Datenbankentwicklung  
 Da einem Entwickler möglicherweise nicht bekannt ist, wo eine neue Datenbank bereitgestellt wird, verringern sich durch das Beschränken der Auswirkungen der Bereitstellungsumgebung der Arbeitsaufwand und die Probleme für den Entwickler. Im nicht enthaltenen Modell muss der Entwickler beim Programmieren mögliche Umgebungsauswirkungen auf die neue Datenbank berücksichtigen. Mit teilweise eigenständigen Datenbanken können Entwickler jedoch Auswirkungen auf Instanzebene auf die Datenbank und Aspekte auf Instanzebene für den Entwickler erkennen.  
  
### <a name="database-administration"></a>Datenbankverwaltung  
 Durch das Beibehalten der Datenbankeinstellungen in der Datenbank (im Gegensatz zur master-Datenbank) erhält jeder Datenbankbesitzer mehr Kontrolle über seine Datenbank, und zwar ohne die Datenbankbesitzer-Berechtigung **sysadmin** zu erteilen.  
  
##  <a name="Limitations"></a> Einschränkungen  
 Für teilweise eigenständige Datenbanken sind die folgenden Funktionen nicht zulässig.  
  
-   Teilweise Enthaltene Datenbanken unterstützen weder die Replikation, noch das Aufzeichnen oder das Nachverfolgen von Änderungsdaten.  
  
-   Nummerierte Prozeduren  
  
-   Schemagebundene Objekte, die von integrierten Funktionen mit Sortierungsänderungen abhängen.  
  
-   Bindungsänderungen, die sich aus Sortierungsänderungen ergeben, einschließlich von Verweisen auf Objekte, Spalten, Symbole oder Typen.  
  
-   Replikation, Change Data Capture und Änderungsnachverfolgung  
  
> [!WARNING]  
>  Temporär gespeicherte Prozeduren sind derzeit zulässig. Da temporär gespeicherte Prozeduren die Kapselung verletzen, ist nicht davon auszugehen, dass sie in künftigen Versionen der eigenständigen Datenbank unterstützt werden.  
  
##  <a name="Identifying"></a> Identifizieren der Datenbankkapselung  
 Es sind zwei Tools verfügbar, mit denen der Einschlussstatus der Datenbank bestimmt werden kann. [sys.dm_db_uncontained_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-uncontained-entities-transact-sql.md) ist eine Sicht, in der alle möglicherweise nicht eigenständigen Entitäten in der Datenbank angezeigt werden. Das database_uncontained_usage-Ereignis wird ausgelöst, wenn eine tatsächliche nicht enthaltene Entität zur Laufzeit bestimmt wird.  
  
### <a name="sysdmdbuncontainedentities"></a>sys.dm_db_uncontained_entities  
 In dieser Sicht werden alle Entitäten in der Datenbank angezeigt, bei denen es sich um nicht enthaltene Entitäten handeln könnte, weil sie beispielsweise die Datenbankbegrenzung überschreiten. Hierzu zählen die Benutzerentitäten, die Objekte außerhalb des Datenbankmodells verwenden können. Da die Kapselung einiger Entitäten (z. B. der Entitäten mit dynamischem SQL) jedoch erst zur Laufzeit bestimmt werden kann, werden in der Sicht möglicherweise einige Entitäten angezeigt, die eigentlich keine nicht enthaltenen Entitäten sind. Weitere Informationen finden Sie unter [sys.dm_db_uncontained_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-uncontained-entities-transact-sql.md).  
  
### <a name="databaseuncontainedusage-event"></a>database_uncontained_usage-Ereignis  
 Dieses XEvent wird ausgelöst, wenn nicht enthaltene Entität zur Laufzeit bestimmt wird. Dies schließt in Clientcode ausgelöste Entitäten ein. Dieses Xevent wird nur für tatsächliche nicht enthaltene Entitäten ausgelöst. Das Ereignis wird jedoch nur zur Laufzeit ausgelöst. Daher werden alle nicht enthaltenen Benutzerentitäten, die nicht ausgeführt wurden, von diesem XEvent nicht identifiziert.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Geänderte Funktionen &#40;Enthaltene Datenbank&#41;](../../relational-databases/databases/modified-features-contained-database.md)   
 [Contained Database Collations](../../relational-databases/databases/contained-database-collations.md)   
 [Security Best Practices with Contained Databases](../../relational-databases/databases/security-best-practices-with-contained-databases.md)   
 [Migrate to a Partially Contained Database](../../relational-databases/databases/migrate-to-a-partially-contained-database.md)   
 [Eigenständige Datenbankbenutzer - machen Sie Ihre Datenbank portabel](../../relational-databases/security/contained-database-users-making-your-database-portable.md)  
  
  
