---
title: Datenquellen (Assistentenbildschirm 3) (Odbcdriver for SQLServer) | Microsoft Docs
ms.custom: ''
ms.date: 09/27/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 76326eeb-1144-4b9f-85db-50524c655d30
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cbac8f1b778dfa01e417b76b3f8044368a0bb9a7
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="data-source-wizard-screen-3"></a>Assistent Datenquellenbildschirm 3

Geben Sie die Standarddatenbank, verschiedene ANSI-Optionen, die vom Treiber verwendet werden sollen, und den Namen eines Spiegelservers an.

## <a name="options"></a>enthalten

### <a name="change-the-default-database-to"></a>Ändern Sie die Standarddatenbank auf

Gibt den Namen der Standarddatenbank für jede mit dieser Datenquelle hergestellte Verbindung an. Wenn dieses Kästchen deaktiviert ist, verwenden Verbindungen die für die Anmelde-ID auf dem Server definierte Standarddatenbank. Wenn dieses Kästchen aktiviert ist, überschreibt die in dem Kästchen bezeichnete Datenbank die für die Anmelde-ID definierte Standarddatenbank. Wenn die **Datenbank-Dateinamen anfügen** Feld hat den Namen einer primären Datei, die durch die primäre Datei beschriebene Datenbank als Datenbank anhand des Datenbanknamens, der im angegebenen angefügt ist die **die Standarddatenbank ändern, um**Feld.

Es ist effizienter, die Standarddatenbank für die Anmelde-ID zu verwenden, als eine Standarddatenbank in der ODBC-Datenquelle anzugeben.

### <a name="mirror-server"></a>Spiegelserver

Gibt den Namen des Failoverpartners der zu spiegelnden Datenbank an. Wenn Sie ein Datenbanknamen in nicht angezeigt wird die **die Standarddatenbank ändern auf** Feld oder der angezeigte Name ist die Standarddatenbank **Spiegelserver** abgeblendet.

Optional können Sie einen Serverprinzipalnamen (SPN) für den Spiegelserver angeben. Der SPN für den Spiegelserver wird zur gegenseitigen Authentifizierung zwischen Client und Server verwendet.

### <a name="attach-database-filename"></a>Datenbank-Dateinamen anfügen

Gibt den Namen der primären Datei für eine anfügbare Datenbank an. Diese Datenbank wird angefügt und als Standarddatenbank für die Datenquelle verwendet. Geben Sie den vollständigen Pfad und den Dateinamen für die primäre Datei an. Der Datenbankname angegeben, der **die Standarddatenbank ändern auf** als Namen für die angefügte Datenbank verwendet.

### <a name="use-ansi-quoted-identifiers"></a>Verwenden Sie ANSI-Bezeichner in Anführungszeichen

Gibt an, dass QUOTED_IDENTIFIERS auf festgelegt werden, wenn der ODBC-Treiber für SQL Server eine Verbindung herstellt. Wenn dieses Kontrollkästchen aktiviert ist, erzwingt SQL Server ANSI-Regeln für Anführungszeichen. Doppelte Anführungszeichen können nur für Bezeichner verwendet werden, z. B. Spalten- und Tabellennamen. Zeichenfolgen müssen in einfache Anführungszeichen eingeschlossen werden:

```
SELECT "LastName"
FROM "Person.Contact"
WHERE "LastName" = 'O''Brien'
```

Wenn dieses Kontrollkästchen deaktiviert wird, treten bei Anwendungen, die Bezeichner verwenden, wie z. B. das Abfragehilfsprogramm von Microsoft, das mit Microsoft Excel geliefert wird, Fehler beim Generieren von SQL-Anweisungen mit Bezeichnern in Anführungsstrichen auf.

### <a name="use-ansi-nulls-paddings-and-warnings"></a>ANSI-Nullen,-Auffüllungen und-Warnungen verwenden

Gibt an, dass die Optionen ANSI_NULLS, ANSI_WARNINGS und ANSI_PADDINGS auf festgelegt werden, wenn der ODBC-Treiber für SQL Server eine Verbindung herstellt.

Wenn ANSI_NULLS auf ON festgelegt ist, erzwingt der Server ANSI-Regeln beim Vergleichen von Spalten für NULL. Die ANSI-Syntax „IS NULL“ oder „IS NOT NULL“ muss für alle NULL-Vergleiche verwendet werden. Die Transact-SQL-Syntax „= NULL“ wird nicht unterstützt.

Legen Sie für ANSI_WARNINGS auf On gibt SQL Server Warnmeldungen für Bedingungen, die gegen ANSI-Regeln, aber die Regeln von Transact-SQL nicht verletzt werden. Beispiele für solche Fehler sind das Abschneiden von Daten bei der Ausführung einer INSERT- oder UPDATE-Anweisung oder das Stoßen auf einen Nullwert während einer Aggregatfunktion. 

ANSI_PADDING festgelegt, nachfolgende Leerzeichen nach **Varchar** -Werten und nachfolgende Nullen auf **Varbinary** Werte werden nicht automatisch gekürzt.

### <a name="application-intent"></a>Anwendungsabsicht

Deklariert den Arbeitsauslastungstyp der Anwendung beim Herstellen einer Verbindung mit einem Server. Mögliche Werte sind **ReadOnly** und **ReadWrite**.

### <a name="multi-subnet-failover"></a>Multisubnetz-Failover.

Wenn Ihre Anwendung eine hohe Verfügbarkeit und Disaster Recovery (AlwaysOn-Verfügbarkeitsgruppen) verfügbarkeitsgruppe (AG) in verschiedenen Subnetzen eine Verbindung herstellt, aktiviert **-multisubnetz-Failovercluster.** konfiguriert die ODBC-Treiber für SQL Server, um die schnellere Erkennung und Verbindung mit dem (gerade) aktiven Server bereitzustellen.

### <a name="transparent-network-ip-resolution"></a>Transparentes Netzwerk-IP-Auflösung.

Ändert das Verhalten des **multisubnetzfailover** um schnellere wiederverbindung während des Failovers zu ermöglichen. Finden Sie unter [mithilfe transparenten Netzwerk IP-Auflösung](../../../connect/odbc/using-transparent-network-ip-resolution.md) für Weitere Informationen.

### <a name="column-encryption"></a>Column Encryption.

Ermöglicht die automatische Entschlüsselung und Verschlüsselung von Datenübertragungen von und von mit verschlüsselten Spalten der [Always Encrypted](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md) Feature in SQL Server 2016 und höher verfügbar.

### <a name="use-fmtonly-metadata-discovery"></a>Verwenden Sie FMTONLY metadatenermittlung:

Verwenden Sie die ältere SET FMTONLY Metadaten-Ermittlungsmethode, beim Herstellen einer Verbindung mit SQL Server 2012 oder höher. Aktivieren Sie diese Option nur bei Verwendung von nicht unterstützten Abfragen [Sp_describe_first_result_set](../../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md), z. B. solche, die temporäre Tabellen enthält. 

### <a name="next"></a>Weiter

Fährt mit dem nächsten Bildschirm des Assistenten.

### <a name="back"></a>Zurück

Zurück zum vorherigen Bildschirm des Assistenten.

## <a name="next-steps"></a>Nächste Schritte

[Data Source-Assistent (Bildschirm 2)](../../../connect/odbc/windows/dsn-wizard-2.md)

[Data Source-Assistent (Bildschirm 4)](../../../connect/odbc/windows/dsn-wizard-4.md)
