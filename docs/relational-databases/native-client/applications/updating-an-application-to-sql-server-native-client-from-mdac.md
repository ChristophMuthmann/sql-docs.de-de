---
title: Aktualisieren einer Anwendung von MDAC auf SQL Server Native Client | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client|applications
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- MDAC [SQL Server]
- SQLNCLI, vs. MDAC
- SQL Server Native Client, vs. MDAC
- data access [SQL Server Native Client], vs. MDAC
- SQL Server Native Client, updating applications
ms.assetid: 2860efdd-c59a-4deb-8a0e-5124a8f4e6dd
caps.latest.revision: 81
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: b5163ef5cea7268824b8b9f5e0fe35911ab4a2f8
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="updating-an-application-to-sql-server-native-client-from-mdac"></a>Aktualisieren einer Anwendung von MDAC auf SQL Server Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  Es gibt eine Reihe von Unterschieden zwischen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client und Microsoft Data Access Components (MDAC; ab Windows Vista werden die Datenzugriffskomponenten als Windows Data Access Components oder Windows DAC bezeichnet). Durch beide Technologien wird systemeigener Datenzugriff auf [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Datenbanken bereitgestellt, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] SQL Native Client wurde jedoch speziell für die Verwendung der neuen Funktionen von [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] entwickelt und bietet gleichzeitig Abwärtskompatibilität mit früheren Versionen.  
  
 Anhand der Informationen in diesem Thema können Sie die MDAC-Anwendung (oder Windows DAC) auf die Version [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client aktualisieren, die im Lieferumfang von [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] enthalten ist. Um diese Anwendung mit der Version der aktuellen werden treffen zu können [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, der im Lieferumfang [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], finden Sie unter [Aktualisieren einer Anwendung von SQL Server 2005 Native Client](../../../relational-databases/native-client/applications/updating-an-application-from-sql-server-2005-native-client.md).  
  
 Obwohl MDAC Komponenten zur Verwendung von OLE DB, ODBC und ActiveX Data Objects (ADO) enthält, implementiert [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client nur OLE DB und ODBC (ADO hat allerdings Zugriff auf die Funktionen von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client).  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client und MDAC unterscheiden sich in anderen Bereichen wie folgt:  
  
-   Benutzern, die mit ADO auf einen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client-Anbieter zugreifen, stehen möglicherweise weniger Filterfunktionen zur Verfügung als bei Zugriff auf einen SQL OLE DB-Anbieter.  
  
-   Wenn eine ADO-Anwendung [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client verwendet und versucht, eine berechnete Spalte zu aktualisieren, wird ein Fehler gemeldet. Mit MDAC wurde das Update akzeptiert, jedoch ignoriert.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ist eine einzelne, eigenständige Dynamic Link Library-Datei (DLL). Die öffentlich verfügbaren Schnittstellen wurden auf ein Minimum reduziert, um sowohl die Verteilung zu erleichtern als auch die Sicherheitsrisiken einzuschränken.  
  
-   Es werden nur OLE DB und ODBC-Schnittstellen unterstützt.  
  
-   Die Namen des [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client-OLE DB-Anbieters und des ODBC-Treibers unterscheiden sich von den mit MDAC verwendeten Namen.  
  
-   Mit [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client sind von MDAC-Komponenten bereitgestellte Benutzerzugriffsfunktionen verfügbar. Dazu gehören u. a.: Verbindungspooling, ADO-Unterstützung und Clientcursorunterstützung. Wenn eine dieser Funktionen verwendet wird, stellt [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client nur Datenbankkonnektivität zur Verfügung. MDAC stellt Funktionen wie Ablaufverfolgung, Verwaltungssteuerelemente und Leistungsindikatoren bereit.  
  
-   Anwendungen können die OLE DB-Basisdienste mit [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client verwenden. Bei Verwendung des OLE DB-Cursormoduls sollten sie jedoch die Datentyp-Kompatibilitätsoption verwenden, um potenzielle Probleme zu vermeiden, die auftreten können, da das Cursormodul die neuen [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]-Datentypen nicht erkennt.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client unterstützt den Zugriff auf Datenbanken früherer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Versionen.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client enthält keine XML-Integration. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client unterstützt SELECT... FÜR XML-Abfragen, aber andere XML-Funktionen nicht unterstützt. Allerdings [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client unterstützt die **Xml** -Datentyp in eingeführte [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client unterstützt das Konfigurieren clientseitiger Netzwerkbibliotheken nur mithilfe von Verbindungszeichenfolgenattributen. Wenn Sie eine umfassendere Netzwerkbibliothekskonfiguration benötigen, müssen Sie [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Konfigurations-Manager verwenden.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ist nicht kompatibel mit odbcbcp.dll. Anwendungen, die beide ODBC verwenden und **Bcp** APIs müssen neu erstellt werden, um mit sqlncli11.lib verknüpft werden, um verwenden [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client wird vom Microsoft OLE DB-Anbieter für ODBC (MSDASQL) nicht unterstützt. Wenn Sie den MDAC SQLODBC-Treiber mit MSDASQL oder mit ADO verwenden, sollten Sie in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB verwenden.  
  
-   MDAC-Verbindungszeichenfolgen ermöglichen einen booleschen Wert (**"true"**) für die **Trusted_Connection** Schlüsselwort. Ein [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client-Verbindungszeichenfolge muss verwenden **Ja** oder **keine**.  
  
-   An Warnungen und Fehlern wurden geringfügige Änderungen vorgenommen. Vom Server zurückgegebene Warnungen und Fehler behalten bei Übergabe an den [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client den gleichen Schweregrad bei. Sie sollten sicherstellen, dass die Anwendung gründlich getestet wurde, wenn Sie auf das Abfangen bestimmter Warnungen und Fehler angewiesen sind.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client enthält eine strengere Fehlerprüfung als MDAC. Dies bedeutet, dass einige Anwendungen, die den ODBC- und OLE DB-Spezifikationen nicht hundertprozentig entsprechen, sich anders verhalten. Der SQLOLEDB-Anbieter hat beispielsweise die Regel, dass Parameternamen für Ergebnisparameter mit "@" beginnen müssen, nicht erzwungen; der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter hat ihn dagegen erzwungen.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client verhält sich in Bezug auf fehlgeschlagene Verbindungen anders als MDAC. MDAC gibt beispielsweise zwischengespeicherte Eigenschaftswerte für eine fehlgeschlagene Verbindung zurück, während [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client einen Fehler an die aufrufende Anwendung meldet.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client generiert keine Visual Studio Analyzer-Ereignisse, sondern stattdessen Windows-Ablaufverfolgungsereignisse.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client kann nicht mit perfmon verwendet werden. Perfmon ist ein Windows-Tool, das nur mit DSNs verwendet werden kann, die den im Lieferumfang von Windows enthaltenen MDAC SQLODBC-Treiber verwenden.  
  
-   Wenn [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client mit [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] oder höheren Versionen verbunden wird, wird Serverfehler 16947 als SQL_ERROR zurückgegeben. Dieser Fehler tritt auf, wenn ein positioniertes Update oder Löschen eine Zeile nicht aktualisieren oder löschen kann. Mit MDAC wird beim Herstellen einer Verbindung mit einer Version von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] der Serverfehler 16947 als Warnung (SQL_SUCCESS_WITH_INFO) zurückgegeben.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client implementiert den **IDBDataSourceAdmin** Schnittstelle. Hierbei handelt es sich um eine optionale OLE DB-Schnittstelle, die nicht zuvor implementiert, jedoch nur die **CreateDataSource** Methode diesem Optionaler Schnittstelle implementiert wird. [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
-   Der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter gibt Synonyme in den Schemarowsets TABLES und TABLE_INFO zurück, wobei der Wert TABLE_TYPE auf SYNONYM gesetzt ist.  
  
-   Rückgabewerte vom Datentyp **varchar(max)**, **nvarchar(max)**, **varbinary(max)**, **Xml**, **Udt**, oder andere LOB-Typen können nicht zurückgegeben werden, um Clientversionen vor [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. Wenn Sie diese Typen als Rückgabewerte verwenden möchten, müssen Sie [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client verwenden.  
  
-   MDAC lässt die Ausführung folgender Anweisungen beim Start manueller und impliziter Transaktionen zu, während [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client diese Möglichkeit nicht bietet. Die Anweisungen müssen im Autocommitmodus ausgeführt werden.  
  
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
  
     Diese Typzuordnung beeinflusst die für Spaltenmetadaten zurückgegebenen Werte. Z. B. eine **Text** Spalte hat eine maximale Größe von 2.147.483.647. jedoch [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC meldet die maximale Größe des **varchar(max)** Spalten als SQL_SS_LENGTH_UNLIMITED und [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client OLE DB gibt die maximale Größe der **varchar(max)** Spalten als 2.147.483.647 oder -1, je nach Plattform.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client lässt aus Gründen der Abwärtskompatibilität Mehrdeutigkeit in Verbindungszeichenfolgen zu (einige Schlüsselwörter können beispielsweise mehr als einmal angegeben werden, und konfliktverursachende Schlüsselwörter können mit einer Auflösung basierend auf der Position oder Rangfolge zugelassen werden). Zukünftige Versionen von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client lassen möglicherweise keine Mehrdeutigkeit in Verbindungszeichenfolgen zu. Es empfiehlt sich beim Ändern von Anwendungen, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client zu verwenden, um eine Abhängigkeit von der Mehrdeutigkeit von Verbindungszeichenfolgen zu umgehen.  
  
-   Wenn Sie einen ODBC- oder OLE DB-Aufruf zum Starten von Transaktionen verwenden, verhalten sich [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client und MDAC unterschiedlich. Mit [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client werden die Transaktionen unmittelbar gestartet, mit MDAC hingegen beginnen sie erst nach dem ersten Datenzugriff. Dies kann das Verhalten von gespeicherten Prozeduren und Batches auswirken, da [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] @ erfordert@TRANCOUNT identisch sein, nach einem Batch oder einer gespeicherten Prozedur Beenden der Ausführung des Batches oder gespeicherte Prozedur gestartet wurde.  
  
-   Mit [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ITransactionLocal::BeginTransaction führt dazu, dass eine Transaktion sofort gestartet werden soll. Mit MDAC wurde der Transaktionsstart verzögert, bis die Anwendung eine Anweisung ausgeführt hat, die eine Transaktion im impliziten Transaktionsmodus erforderte. Weitere Informationen finden Sie unter [SET IMPLICIT_TRANSACTIONS &#40;Transact-SQL&#41;](../../../t-sql/statements/set-implicit-transactions-transact-sql.md).  
  
-   Sie können Fehler auftreten, wenn [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client-Treiber mit "System.Data.ODBC" den Zugriff auf eine [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Servercomputer, die neue, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]--spezifische Datentypen oder Funktionen. "System.Data.ODBC" stellt eine generische ODBC-Implementierung und anschließend macht nicht herstellerspezifischen Funktionen oder Erweiterungen. (Der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client-Treiber wird aktualisiert, um die neuesten [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Funktionen systemeigen zu unterstützen.) Zur Umgehung dieses Problem, Sie können entweder zu MDAC zurückkehren oder Migrieren zu System.Data.SqlClient.  
  
 Sowohl [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client als auch MDAC unterstützen die Read Committed-Isolation mit Zeilenversionsverwaltung, aber nur [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client unterstützt die Momentaufnahmen-Transaktionsisolation. (Programmiertechnisch ausgedrückt bedeutet dies, dass die Read Committed-Transaktionsisolation mit Zeilenversionsverwaltung gleichbedeutend mit einer Read Committed-Transaktion ist.)  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen von Anwendungen mit SQL Server Native Client](../../../relational-databases/native-client/applications/building-applications-with-sql-server-native-client.md)  
  
  
