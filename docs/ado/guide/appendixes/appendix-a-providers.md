---
title: 'Anhang A: Anbieter | Microsoft Docs'
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data providers [ADO]
- providers [ADO]
- ADO, providers
- service providers [ADO]
- service components [ADO]
ms.assetid: e2581b47-b11e-4e1e-b96c-d39c77c5b48a
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 09a9ef813f1ef093456abb62fd68a28c61cfd30d
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="appendix-a-data-and-service-providers"></a>Anhang A: Daten und Dienstanbieter
In diesem Abschnitt behandelt die drei Arten von Anbietern: Datenanbieter Dienstanbieter und Dienstkomponenten. Anbieter können zwei Kategorien zugeordnet: Bereitstellen von Daten und die Dienste bereitstellen. Ein *Datenanbieter* besitzt seine eigenen Daten und es in tabellarischer Form an Ihre Anwendung verfügbar gemacht. Ein *Dienstanbieter* kapselt einen Dienst durch erzeugen und Nutzen von Daten, die Funktionen in den ADO-Anwendungen zu erweitern. Ein Dienstanbieter kann als auch genauer definiert eine *Dienstkomponente*, die zusammen mit anderen Dienstanbietern oder Komponenten arbeiten müssen.

## <a name="data-providers"></a>Datenanbieter
 ADO ist leistungsstark und flexibel, da es mehrere unterschiedliche Daten-Anbieter herstellen und weiterhin verfügbar das gleiche Programmiermodell, unabhängig vom angegebenen Anbieter die bestimmten Funktionen machen kann.

 Allerdings da jeden Datenanbieter eindeutig ist, variieren wie Ihre Anwendung mit ADO kommuniziert geringfügig vom Datenanbieter. Die Unterschiede werden in der Regel in drei Kategorien unterteilt:

-   Verbindungsparameter in die ["ConnectionString"](../../../ado/reference/ado-api/connectionstring-property-ado.md) Eigenschaft.

-   [Befehl](../../../ado/reference/ado-api/command-object-ado.md) Nutzung-Objekt.

-   Anbieterspezifische [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) Verhalten.

 Details für jede der derzeit verfügbaren von Microsoft-Datenanbieter werden wie folgt aufgeführt.

|Bereich|Thema|
|----------|-----------|
|ODBC-Datenbanken|[Microsoft OLE DB-Anbieter für ODBC](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-odbc.md)|
|Microsoft Indexdienst|[Microsoft OLE DB-Anbieter für Microsoft Indexdienst](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-indexing-service.md)|
|Active Directory-Dienst|[Microsoft OLE DB-Anbieter für Microsoft Active Directory-Dienst](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-active-directory-service.md)|
|Microsoft Jet-Datenbanken|[OLE DB-Anbieter für Microsoft Jet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-jet.md)|
|Microsoft SQL Server|[Microsoft OLE DB-Anbieter für SQLServer](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md)|
|Oracle-Datenbanken|[Microsoft OLE DB-Anbieter für Oracle](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-oracle.md)|
|Veröffentlichen im Internet|[Microsoft OLE DB-Anbieter für Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)|
|Einfache Datenquellen|[Einfache Microsoft OLE DB-Anbieter](../../../ado/guide/appendixes/microsoft-ole-db-simple-provider.md)|

## <a name="provider-specific-dynamic-properties"></a>Anbieterspezifische dynamische Eigenschaften
 Die [Eigenschaften](../../../ado/reference/ado-api/properties-collection-ado.md) Sammlungen von der [Verbindung](../../../ado/reference/ado-api/connection-object-ado.md), [Befehl](../../../ado/reference/ado-api/command-object-ado.md), und [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) Objekten zählen die dynamische Eigenschaften, die spezifisch für die Anbieter. Diese Eigenschaften stellen Informationen zu spezifischen Funktionen bereit, an den Anbieter über das integrierten Eigenschaften, die ADO unterstützt.

 Verwenden Sie nach dem Herstellen der Verbindung, und Erstellen dieser Objekte, die [aktualisieren](../../../ado/reference/ado-api/refresh-method-ado.md) Methode für die **Eigenschaften** Auflistung des Objekts, das die anbieterspezifischen Eigenschaften zu erhalten. Finden Sie in der Dokumentation und der [OLE DB Programmer's Guide](http://msdn.microsoft.com/en-us/3c5e2dd5-35e5-4a93-ac3a-3818bb43bbf8) ausführliche Informationen über diese dynamischen Eigenschaften.

## <a name="service-providers"></a>Dienstanbieter
 Wenn einen Dienstanbieter verwenden möchten, müssen Sie ein Schlüsselwort angeben. Sie sollten auch die anbieterspezifische dynamische Eigenschaften mit jedem Dienstanbieter beachten. Anbieterspezifische Informationen sind für jeden Dienstanbieter aufgeführt, die derzeit von Microsoft verfügbar ist:

-   [Microsoft Data strukturiert werden, Dienst für OLE DB](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)

-   [Microsoft OLE DB-Persistenz-Provider](../../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md)

-   [Microsoft OLE DB-Anbieter für Remoting](../../../ado/guide/appendixes/microsoft-ole-db-remoting-provider-ado-service-provider.md)

## <a name="service-components"></a>Dienstkomponenten
 Die [Cursordiensts für OLE DB-](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) Dienstkomponente ergänzt die Cursorfunktionen der Unterstützung von Datenanbietern. Ein Schlüsselwort erfordert außerdem eine dynamische Eigenschaften hat.

 Weitere Informationen zu OLE DB-Anbietern finden Sie unter [Microsoft OLE DB-](https://msdn.microsoft.com/library/windows/desktop/ms722784.aspx).

## <a name="provider-commands"></a>Anbieterbefehle
 Für jeden Anbieter hier aufgeführt, wenn Ihre Anwendung Benutzer zur Eingabe von SQL-Anweisungen, wenn die Anbieterbefehle zuzulassen, müssen Sie immer die Benutzereingabe validieren und werden von möglichen Hackerangriffen potenziell gefährlichen SQL-Anweisungen, wie z. B. mit entsprechender `DROP TABLE t1`, im Rahmen der Benutzereingabe.

## <a name="see-also"></a>Siehe auch
 [Command-Objekt (ADO)](../../../ado/reference/ado-api/command-object-ado.md) [Verbindungsobjekt (ADO)](../../../ado/reference/ado-api/connection-object-ado.md) [Microsoft OLE DB-Anbieter für Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md) [Microsoft OLE DB-Anbieter für Microsoft Active Directory Dienst](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-active-directory-service.md) [Microsoft OLE DB-Anbieter für Microsoft Indexdienst](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-indexing-service.md) [Microsoft OLE DB-Anbieter für ODBC](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-odbc.md) [Microsoft OLE DB-Anbieter für Oracle](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-oracle.md) [Microsoft OLE DB-Anbieter für SQLServer](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md) [Microsoft OLE DB-Anbieter für Microsoft Jet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-jet.md) [Properties-Auflistung (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md) [Recordset Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md) [Refresh-Methode (RDS)](../../../ado/reference/rds-api/refresh-method-rds.md)

