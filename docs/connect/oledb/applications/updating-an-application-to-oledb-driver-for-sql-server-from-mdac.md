---
title: Aktualisieren von einer Anwendung auf OLE DB-Treiber für SQLServer von MDAC | Microsoft Docs
description: Aktualisieren von einer Anwendung auf OLE DB-Treiber für SQL Server von MDAC
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb|applications
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- MDAC [SQL Server]
- MSOLEDBSQL, vs. MDAC
- OLE DB Driver for SQL Server, vs. MDAC
- data access [OLE DB Driver for SQL Server], vs. MDAC
- OLE DB Driver for SQL Server, updating applications
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 61056a6951176b4257856b114a512f6f81dfc33e
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2018
---
# <a name="updating-an-application-to-ole-db-driver-for-sql-server-from-mdac"></a>Aktualisieren von einer Anwendung auf OLE DB-Treiber für SQLServer von MDAC
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Es gibt eine Reihe von Unterschieden zwischen OLE DB-Treiber für SQL Server und Microsoft Data Access Components (MDAC); ab Windows Vista, werden die Datenzugriffskomponenten jetzt Windows Data Access Components (oder Windows DAC) bezeichnet. Obwohl beide bieten die systemeigenen Datenzugriff auf [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Datenbanken, OLE DB-Treiber für SQL Server speziell entworfen wurde, um die neuen Funktionen von verfügbar zu machen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], während gleichzeitig Abwärtskompatibilität mit früheren Versionen zu verwalten.   

 Darüber hinaus Obwohl MDAC Komponenten zur Verwendung von OLE DB, ODBC und ActiveX Data Objects (ADO) enthält, implementiert OLE DB-Treiber für SQL Server nur OLE DB (obwohl ADO die Funktionalität des OLE DB-Treiber für SQL Server zugreifen kann).  

 OLE DB-Treiber für SQL Server und MDAC unterscheiden sich in folgenden Bereichen:  

-   Benutzer, die ADO verwenden, um einen OLE DB-Treiber für SQL Server zugreifen können möglicherweise weniger Filterfunktionen zur Verfügung als wenn sie einen SQL OLE DB-Anbieter zugegriffen.  

-   Wenn eine ADO-Anwendung OLE DB-Treiber für SQL Server verwendet und versucht, eine berechnete Spalte zu aktualisieren, wird ein Fehler gemeldet werden. Mit MDAC wurde das Update akzeptiert, jedoch ignoriert.  

-   OLE DB-Treiber für SQL Server ist eine einzelne, eigenständige dynamic Link Library (DLL)-Datei. Die öffentlich verfügbaren Schnittstellen wurden auf ein Minimum reduziert, um sowohl die Verteilung zu erleichtern als auch die Sicherheitsrisiken einzuschränken.  

-   Es werden nur OLE DB-Schnittstellen unterstützt.  

-   Der OLE DB-Treiber für SQL Server-Namen unterscheiden sich von den mit MDAC verwendeten.  

-   Benutzer zugänglichen von MDAC-Komponenten bereitgestellte Funktionalität ist bei Verwendung von OLE DB-Treiber für SQL Server verfügbar. Dazu gehören u. a.: Verbindungspooling, ADO-Unterstützung und Clientcursorunterstützung. Wenn eine dieser Funktionen verwendet wird, stellt OLE DB-Treiber für SQL Server nur Datenbankkonnektivität bereit. MDAC stellt Funktionen wie Ablaufverfolgung, Verwaltungssteuerelemente und Leistungsindikatoren bereit.  

-   Anwendungen können OLE DB-Basisdienste mit OLE DB-Treiber für SQL Server verwenden, aber wenn der OLE DB-Cursormoduls verwenden zu können, sollten sie die Datentyp-Kompatibilitätsoption verwenden, um potenzielle Probleme zu vermeiden, die auftreten können, da das Cursormodul nicht der neuen kennt [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] -Datentypen.  

-   OLE DB-Treiber für SQL Server unterstützt den Zugriff auf frühere [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Datenbanken.  

-   OLE DB-Treiber für SQL Server enthält keine XML-Integration. OLE DB-Treiber für SQL Server unterstützt SELECT... FÜR XML-Abfragen, aber andere XML-Funktionen nicht unterstützt. OLE DB-Treiber für SQL Server unterstützt jedoch die **Xml** -Datentyp in eingeführte [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  

-   OLE DB-Treiber für SQL Server unterstützt das Konfigurieren von clientseitigen Netzwerkbibliotheken nur Verbindungszeichenfolgen-Attribute verwenden. Wenn Sie eine umfassendere Netzwerkbibliothekskonfiguration benötigen, müssen Sie [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Konfigurations-Manager verwenden.  

-   OLE DB-Treiber für SQL Server ist nicht kompatibel mit odbcbcp.dll. Anwendungen müssen neu erstellt werden, um mit msoledbsql.lib verknüpfen, um die OLE DB-Treiber für SQL Server verwenden.    

-   MDAC-Verbindungszeichenfolgen ermöglichen einen booleschen Wert (**"true"**) für die **Trusted_Connection** Schlüsselwort. Verwenden Sie einen OLE DB-Treiber für SQL Server-Verbindungszeichenfolge muss **Ja** oder **keine**.  

-   An Warnungen und Fehlern wurden geringfügige Änderungen vorgenommen. Warnungen und Fehler, die vom Server zurückgegebenen behalten den gleichen Schweregrad bei OLE DB-Treiber für SQL Server an. Sie sollten sicherstellen, dass die Anwendung gründlich getestet wurde, wenn Sie auf das Abfangen bestimmter Warnungen und Fehler angewiesen sind.  

-   OLE DB-Treiber für SQL Server hat die strengere fehlerprüfung als MDAC, dies bedeutet, dass einige Anwendungen, die nicht unbedingt den OLE DB-Spezifikationen entsprechen sich anders verhalten. Z. B. der SQLOLEDB-Anbieter die Regel, die Parameternamen mit beginnen müssen nicht erzwingen "@" für Ergebnis Parameter, aber der OLE DB-Treiber für SQL Server verfügt.  

-   OLE DB-Treiber für SQL Server Verhalten sich anders als MDAC in Bezug auf fehlgeschlagene Verbindungen. MDAC gibt beispielsweise zwischengespeicherte Eigenschaftswerte für eine Verbindung, die Fehler aufgetreten ist, zurück, während die OLE DB-Treiber für SQL Server einen Fehler an die aufrufende Anwendung meldet.  

-   OLE DB-Treiber für SQL Server generiert keine Visual Studio Analyzer-Ereignisse, sondern stattdessen Windows-Ablaufverfolgungsereignisse.  

-   OLE DB-Treiber für SQL Server kann nicht mit Perfmon verwendet werden. Perfmon ist ein Windows-Tool, das nur mit DSNs verwendet werden kann, die den im Lieferumfang von Windows enthaltenen MDAC SQLODBC-Treiber verwenden.  

-   Wenn OLE DB-Treiber für SQL Server verbunden ist, um [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] und höheren Versionen wird Serverfehler 16947 als SQL_ERROR zurückgegeben zurückgegeben. Dieser Fehler tritt auf, wenn ein positioniertes Update oder Löschen eine Zeile nicht aktualisieren oder löschen kann. Mit MDAC wird beim Herstellen einer Verbindung mit einer Version von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] der Serverfehler 16947 als Warnung (SQL_SUCCESS_WITH_INFO) zurückgegeben.  

-   OLE DB-Treiber für SQL Server implementiert die **IDBDataSourceAdmin** Schnittstelle. Hierbei handelt es sich um eine optionale OLE DB-Schnittstelle, die nicht zuvor implementiert, jedoch nur die **CreateDataSource** -Methode dieses Es ist eine optionale Schnittstelle implementiert. [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  

-   Der OLE DB-Treiber für SQL Server gibt Synonyme in den Tabellen und TABLE_INFO zurück, wobei der Wert TABLE_TYPE auf SYNONYM gesetzt-Schemarowsets.  

-   Rückgabewerte vom Datentyp **varchar(max)**, **nvarchar(max)**, **varbinary(max)**, **Xml**, **Udt**, oder andere LOB-Typen können nicht zurückgegeben werden, um Clientversionen vor [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. Wenn Sie diese Typen als Rückgabewerte verwenden möchten, müssen Sie den OLE DB-Treiber für SQL Server verwenden.  

-   MDAC lässt die folgenden Anweisungen am Anfang des manueller und impliziter Transaktionen ausgeführt werden, OLE DB-Treiber für SQL Server jedoch nicht. Die Anweisungen müssen im Autocommitmodus ausgeführt werden.  

    -   Alle Volltextvorgänge (Index- und Katalog-DDL)  

    -   Alle Datenbankvorgänge (CREATE DATABASE, ALTER DATABASE, DROP DATABASE)  

    -   Neukonfigurieren  

    -   Shutdown  

    -   Kill  

    -   Sicherung  

-   Wenn MDAC-Anwendungen eine Verbindung mit [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] herstellen, werden die in [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] eingeführten Datentypen als [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)]-kompatible Datentypen angezeigt, wie in der folgenden Tabelle dargestellt.  

    |SQL Server 2005-Typ|SQL Server 2000|  
    |--------------------------|--------------------------|  
    |**varchar(max)**|**text**|  
    |**nvarchar(max)**|**ntext**|  
    |**varbinary(max)**|**image**|  
    |**udt**|**varbinary**|  
    |**xml**|**ntext**|  

     Diese Typzuordnung beeinflusst die für Spaltenmetadaten zurückgegebenen Werte. Z. B. eine **Text** Spalte hat eine maximale Größe von 2.147.483.647, aber OLE DB-Treiber für SQL Server gibt die maximale Größe der **varchar(max)** Spalten als 2.147.483.647 oder -1, je nach Plattform.  

-   OLE DB-Treiber für SQL Server ermöglicht Mehrdeutigkeit in Verbindungszeichenfolgen (z. B. einige Schlüsselwörter können mehr als einmal angegeben werden, und konfliktverursachende Schlüsselwörter können mit einer Auflösung basierend auf der Position oder Rangfolge zugelassen werden) aus Gründen der Abwärtskompatibilität. Zukünftige Versionen von OLE DB-Treiber für SQL Server u. u. nicht Mehrdeutigkeit in Verbindungszeichenfolgen zu. Es wird empfohlen, beim Ändern von Anwendungen, OLE DB-Treiber für SQL Server zu verwenden, um eine Abhängigkeit von Mehrdeutigkeit von Verbindungszeichenfolgen zu vermeiden.  

-   Wenn Sie einen OLE DB-Aufruf zum Starten von Transaktionen verwenden, besteht ein Unterschied im Verhalten zwischen OLE DB-Treiber für SQL Server und MDAC; Transaktionen beginnt sofort mit OLE DB-Treiber für SQL Server, jedoch Transaktionen beginnt, nachdem der Zugriff auf die erste Datenbank MDAC verwenden. Dies kann das Verhalten von gespeicherten Prozeduren und Batches auswirken, da [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] @ erfordert@TRANCOUNT identisch sein, nach einem Batch oder einer gespeicherten Prozedur Beenden der Ausführung des Batches oder gespeicherte Prozedur gestartet wurde.  

-   Mit OLE DB-Treiber für SQL Server wird ITransactionLocal::BeginTransaction dazu führen, dass eine Transaktion sofort gestartet werden soll. Mit MDAC wurde der Transaktionsstart verzögert, bis die Anwendung eine Anweisung ausgeführt hat, die eine Transaktion im impliziten Transaktionsmodus erforderte. Weitere Informationen finden Sie unter [SET IMPLICIT_TRANSACTIONS &#40;Transact-SQL&#41;](../../../t-sql/statements/set-implicit-transactions-transact-sql.md).  


 Beide OLE DB-Treiber für SQL Server auch MDAC unterstützen lesen committed-Transaktionsisolation mit zeilenversionsverwaltung, aber nur OLE DB-Treiber für SQL Server unterstützt die Momentaufnahmen-Transaktionsisolation. (Programmiertechnisch ausgedrückt bedeutet dies, dass die Read Committed-Transaktionsisolation mit Zeilenversionsverwaltung gleichbedeutend mit einer Read Committed-Transaktion ist.)  

## <a name="see-also"></a>Siehe auch  
 [Erstellen von Anwendungen mit dem OLE DB-Treiber für SQL Server](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
