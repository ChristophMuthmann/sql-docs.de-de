---
title: SQL Server AlwaysOn Availability Group-Bereitstellungsmuster | Microsoft Docs
ms.custom: 
ms.date: 10/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: linux
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: edd75f68-dc62-4479-a596-57ce8ad632e5
caps.latest.revision: "34"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: cacdf2de6c6e85c8afd0723f4dae21feab0c71cf
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="high-availability-and-data-protection-for-availability-group-configurations"></a>Hohe Verfügbarkeit und Datenschutz für verfügbarkeitsgruppenkonfigurationen

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

Dieser Artikel zeigt unterstützte Bereitstellungskonfigurationen für SQL Server Always On-Verfügbarkeitsgruppen für Linux-Servern. Eine verfügbarkeitsgruppe unterstützt hohe Verfügbarkeit und Schutz von Daten. Automatische fehlererkennung, automatisches Failover und transparente wiederverbindung nach einem Failover bereitstellen hohen Verfügbarkeit. Synchronisierte Replikate bereitzustellen Datenschutz. 

Auf einem Windows Server Failover Cluster (WSFC) verwendet eine gemeinsame Konfiguration für hohe Verfügbarkeit, zwei Replikate mit synchronem und einen dritten Server oder die Dateifreigabe wird, um Quorum zu ermöglichen. Der Dateifreigabenzeugen überprüft die verfügbarkeitsgruppenkonfiguration - Status der Synchronisierung und die Rolle des Replikats, zum Beispiel. Diese Konfiguration wird sichergestellt, dass das sekundäre Replikat als Ziel für das Failover die neuesten Daten und alle Änderungen an der Konfiguration von Availability-Gruppe ausgewählt. 

Der WSFC synchronisiert Konfigurationsmetadaten für die Failover-Vermittlung zwischen Replikate der verfügbarkeitsgruppe und die Dateifreigabenzeugen. Wenn eine verfügbarkeitsgruppe nicht für einen wsfc-Cluster ist, speichern die SQL Server-Instanzen Konfigurationsmetadaten in der master-Datenbank.

Z. B. eine verfügbarkeitsgruppe auf einem Linux-Cluster verfügt `CLUSTER_TYPE = EXTERNAL`. Es gibt keine WSFC Failover vermitteln konnte. In diesem Fall wird die Konfigurationsmetadaten verwaltet und von SQL Server-Instanzen verwaltet. Da in diesem Cluster ohne Zeugenserver vorhanden ist, ist eine dritte Instanz von SQL Server zum Speichern von Status Konfigurationsmetadaten erforderlich. Alle drei SQL Server-Instanzen bereitstellen zusammen verteilte Metadaten-Speicher für den Cluster. 

Der Cluster-Manager kann Abfragen von SQL Server-Instanzen in der verfügbarkeitsgruppe und orchestriert Failover aus, um hohe Verfügbarkeit sicherzustellen. In einem Linux-Cluster ist Schrittmacher der Cluster-Manager. 

SQL Server 2017 CU 1 ermöglicht hohe Verfügbarkeit für eine verfügbarkeitsgruppe mit `CLUSTER_TYPE = EXTERNAL` für zwei synchrone Replikate plus eines Replikats Konfiguration. Das einzige Replikat der Konfiguration kann auf eine beliebige Edition von SQL Server 2017 CU1 oder höher - einschließlich SQL Server Express Edition gehostet werden. Das einzige Replikat von Configuration Konfigurationsinformationen zur verfügbarkeitsgruppe in der master-Datenbank verwaltet, jedoch keine Benutzerdatenbanken in der verfügbarkeitsgruppe. 

## <a name="how-the-configuration-affects-default-resource-settings"></a>Auswirkungen von Standardeinstellungen für die Ressource in die Konfiguration

SQL Server-2017 führt die `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` -clusterressourceneinstellung. Diese Einstellung garantiert der angegebenen Anzahl von sekundären Replikaten Schreiben der Transaktionsdaten anmelden, bevor das primäre Replikat jeder Transaktion ein Commit ausgeführt wird. Wenn Sie einen externen Cluster-Manager verwenden, wirkt sich diese Einstellung auf hohe Verfügbarkeit und Schutz von Daten aus. Der Standardwert für die Einstellung hängen von der Architektur, die zum Zeitpunkt der Clusterressource erstellt wird. Bei der Installation des SQL Server-Ressource-Agents - `mssql-server-ha` - und erstellen Sie eine Clusterressource für die verfügbarkeitsgruppe, wird der Cluster-Manager erkennt die Verfügbarkeit gruppieren, Konfiguration und legt `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` entsprechend. 

Wenn von der Konfiguration die Ressource Agentparameter unterstützt `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` festgelegt ist, auf den Wert an, die hohe Verfügbarkeit und Datenschutz bietet. Weitere Informationen finden Sie unter [verstehen von SQL Server-Ressource-Agent für Schrittmacher](#pacemakerNotify).

In den folgenden Abschnitten wird das Standardverhalten für die Clusterressource erläutert. 

Wählen Sie einen Verfügbarkeit Entwurf entsprechend den geschäftlichen Anforderungen für hohe Verfügbarkeit sowie von Datenschutz- und Skalieren von Lesevorgängen erfüllen.

Die folgenden Konfigurationen werden den Entwurfsmustern für die Verfügbarkeit-Gruppe und die Funktionen der einzelnen Muster beschrieben. Diese Entwurfsmuster anwenden, um Verfügbarkeitsgruppen mit `CLUSTER_TYPE = EXTERNAL` für Lösungen mit hoher Verfügbarkeit. 

- **Drei synchroner Replikate**
- **Zwei synchrone Replikate**
- **Zwei synchrone Replikate und eines Replikats Konfiguration**

<a name="threeSynch"></a>

## <a name="three-synchronous-replicas"></a>Drei synchroner Replikate

Diese Konfiguration umfasst drei synchroner Replikate. Standardmäßig wird die hohe Verfügbarkeit und Datenschutz. Es kann auch Skalieren von Lesevorgängen bereitstellen.

![Drei Replikate][3]

Eine verfügbarkeitsgruppe mit drei synchroner Replikate bieten Skalieren von Lesevorgängen, hohe Verfügbarkeit und Schutz von Daten. In der folgenden Tabelle wird die Verfügbarkeit Verhalten beschrieben. 

| |Skalieren von Lesevorgängen|Hohe Verfügbarkeit & </br> Datenschutz | Schutz von Daten
|:---|---|---|---
|`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT=`|0 |1<sup>*</sup>|2
|Ausfall des primären Replikats | Manuelles Failover. Möglicherweise kommt es zu Datenverlusten. Neue primäre ist R / w. |Automatisches Failover. Neue primäre ist R / w. |Automatisches Failover. Neue primäre ist nicht verfügbar für Benutzertransaktionen, bis vorherigen primären wiederhergestellt und als sekundäre verfügbarkeitsgruppe verknüpft. 
|Ausfall eines sekundären Replikats  | Ein Primärschlüssel ist R / w. Kein automatisches Failover, wenn das primäre schlägt fehl. |Ein Primärschlüssel ist R / w. Kein automatisches Failover, wenn das primäre schlägt auch fehl. | Primäre ist nicht verfügbar für Benutzertransaktionen. 
<sup>*</sup>Standardwert

<a name="twoSynch"></a>

## <a name="two-synchronous-replicas"></a>Zwei synchrone Replikate

Mit dieser Konfiguration können den Datenschutz. Wie die anderen verfügbarkeitsgruppenkonfigurationen können sie Skalieren von Lesevorgängen aktivieren. Die Konfiguration von zwei synchronen Replikaten bietet keine automatische hohen Verfügbarkeit. 

![Zwei synchrone Replikate][1]

Eine verfügbarkeitsgruppe mit zwei synchronen Replikaten bietet Skalieren von Lesevorgängen und den Datenschutz. In der folgenden Tabelle wird die Verfügbarkeit Verhalten beschrieben. 

| |Skalieren von Lesevorgängen |Schutz von Daten
|:---|---|---
|`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT=`|0 <sup>*</sup>|1
|Ausfall des primären Replikats | Manuelles Failover. Möglicherweise kommt es zu Datenverlusten. Neue primäre ist R / w.| Automatisches Failover. Neue primäre ist nicht verfügbar für Benutzertransaktionen, bis vorherigen primären wiederhergestellt und als sekundäre verfügbarkeitsgruppe verknüpft.
|Ausfall eines sekundären Replikats  |Primäre ist R/W, läuft Sie ungeschützt zu Datenverlusten. |Primäre steht nicht für Benutzertransaktionen bis sekundären wiederhergestellt.
<sup>*</sup>Standardwert

>[!NOTE]
>Die oben beschriebene Szenario ist das Verhalten vor SQL Server 2017 CU-1. 

<a name = "configOnly"></a>

## <a name="two-synchronous-replicas-and-a-configuration-only-replica"></a>Zwei synchrone Replikate und eines Replikats Konfiguration

Eine verfügbarkeitsgruppe mit zwei (oder mehr) synchrone Replikate und eines Replikats Konfiguration bietet Schutz der Daten und möglicherweise auch hohen Verfügbarkeit. Das folgende Diagramm zeigt diese Architektur:

![Konfiguration nur verfügbarkeitsgruppe.][2]

1. Synchrone Replikation von Benutzerdaten auf dem sekundären Replikat. Darüber hinaus verfügbarkeitsgruppenmetadaten Konfiguration.
2. Synchrone Replikation der Konfiguration der verfügbarkeitsgruppenmetadaten. Es umfasst nicht die Benutzerdaten.

Im Diagramm Gruppe Verfügbarkeit schiebt ein primäres Replikat Konfigurationsdaten als einziges Replikat der Konfiguration und das sekundäre Replikat. Das sekundäre Replikat empfängt auch Benutzerdaten. Das einzige Configuration-Replikat empfängt keine Benutzerdaten. Das sekundäre Replikat ist im Verfügbarkeitsmodus für synchrone. Das einzige Replikat der Konfiguration enthält keine Datenbanken in der verfügbarkeitsgruppe – nur Metadaten zur verfügbarkeitsgruppe. Konfigurationsdaten für die Konfiguration nur Replikat sind synchron ein Commit ausgeführt wurde.

>[!NOTE]
>Eine Availabilility-Verwaltungsgruppe mit der Konfiguration nur Replikat ist für SQL Server 2017 CU1 neu. Alle Instanzen von SQL Server in der verfügbarkeitsgruppe muss SQL Server 2017 CU1 oder höher. 

Der Standardwert für `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` ist 0. In der folgenden Tabelle wird die Verfügbarkeit Verhalten beschrieben. 

| |Hohe Verfügbarkeit & </br> Datenschutz | Schutz von Daten
|:---|---|---
|`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT=`|0 <sup>*</sup>|1
|Ausfall des primären Replikats | Automatisches Failover. Neue primäre ist R / w. | Automatisches Failover. Neue primäre ist nicht verfügbar für Benutzertransaktionen. 
|Ausfall des sekundären Replikats | Primäre ist R/W, läuft Sie ungeschützt zu Datenverlusten (falls der primäre schlägt fehl, und kann nicht wiederhergestellt werden). Kein automatisches Failover, wenn das primäre schlägt auch fehl. | Primäre ist nicht verfügbar für Benutzertransaktionen. Kein Replikat für ein Failover, wenn das primäre schlägt auch fehl. 
|Konfiguration nur Replikat Ausfall | Ein Primärschlüssel ist R / w. Kein automatisches Failover, wenn das primäre schlägt auch fehl. | Ein Primärschlüssel ist R / w. Kein automatisches Failover, wenn das primäre schlägt auch fehl. 
|Synchrone sekundäre + -Konfiguration nur Replikat Ausfall| Primäre ist nicht verfügbar für Benutzertransaktionen. Kein automatisches Failover. | Primäre ist nicht verfügbar für Benutzertransaktionen. Kein Replikat für ein Failover aus, wenn auch primäre ein Fehler auftritt. 
<sup>*</sup>Standardwert

>[!NOTE]
>Die Instanz von SQL Server, die die Konfiguration nur Replikat hostet, kann auch andere Datenbanken hosten. Sie können auch als eine einzige Konfigurationsdatenbank für mehr als eine verfügbarkeitsgruppe teilnehmen. 

## <a name="requirements"></a>Anforderungen

* Alle Replikate in einer verfügbarkeitsgruppe mit einem einzigen Configuration-Replikat müssen SQL Server 2017 CU 1 oder höher sein.
* Eine beliebige Edition von SQL Server kann eine einzige Replikat Konfiguration, einschließlich SQL Server Express hosten. 
* Die verfügbarkeitsgruppe benötigt mindestens ein sekundäres Replikat – zusätzlich zu das primäre Replikat.
* Nur Replikate Konfiguration zählen nicht für die maximale Anzahl der Replikate pro Instanz von SQL Server. SQL Server standard Edition kann bis zu drei Replikate, SQL Server Enterprise Edition können bis zu 9.

## <a name="considerations"></a>Weitere Überlegungen

* Einzige Replikat, das nicht mehr als eine Konfiguration pro verfügbarkeitsgruppe. 
* Ein einzige Replikat, das Konfiguration darf nicht über ein primäres Replikat sein.
* Den Verfügbarkeitsmodus des Replikats eine Konfiguration kann nicht geändert werden. Um auf ein sekundäres Replikat für synchrone oder asynchrone von eines Replikats Konfiguration zu ändern, entfernen Sie das einzige Replikat der Konfiguration und Hinzufügen eines sekundären Replikats mit den erforderlichen Verfügbarkeitsmodus. 
* Ein einzige Konfiguration-Replikat ist synchron mit der Metadaten der verfügbarkeitsgruppe. Es sind keine Benutzerdaten. 
* Eine verfügbarkeitsgruppe mit einem primären Replikat und einzige Replikat, das eine Konfiguration, aber kein sekundäres Replikat ist ungültig. 
* Das Erstellen einer verfügbarkeitsgruppe auf einer Instanz von SQL Server Express Edition ist nicht möglich. 

<a name="pacemakerNotify"></a>

## <a name="understand-sql-server-resource-agent-for-pacemaker"></a>SQL Server-Agent-Ressource für Schrittmacher verstehen

SQL Server 2017 CTP 1.4 hinzugefügt `sequence_number` auf `sys.availability_groups` ermöglichen Schrittmacher wie auf dem neuesten Stand sekundäre identifizieren Replikate, die mit dem primären Replikat sind. `sequence_number`ist eine monoton ansteigende "bigint", die Aktualität des lokalen verfügbarkeitsgruppenreplikats darstellt. Schrittmacher Updates der `sequence_number` mit jeder Availability Group-konfigurationsänderung. Beispiele für Änderungen an der Konfiguration sind Failover, Replikat hinzufügen oder entfernen. Die Anzahl der primären Datenbank aktualisiert, dann auf sekundäre Replikate repliziert. Daher hat ein sekundäres Replikat, das der aktuellen Konfiguration verfügt wie die primäre Datenbank die gleichen Sequenznummer. 

Wenn Schrittmacher entscheidet, die ein Replikat zur primären höher stufen, sendet er zuerst eine *vorab heraufstufen* Benachrichtigung an alle Replikate. Die Replikate zurück, die Sequenznummer. Als Nächstes Schrittmacher tatsächlich versucht, ein Replikat zur primären höher stufen, stuft das Replikat nur selbst wenn die Sequenznummer der höchsten die Sequenznummern ist. Wenn eine eigene Sequenznummer nicht mit die höchste Sequenznummer übereinstimmt, lehnt das Replikat den Promote-Vorgang ab. Auf diese Weise kann nur das Replikat mit der höchsten Sequenznummer zu einem primären heraufgestuft werden, sodass es nicht zu Datenverlust kommt. 

Dieser Prozess erfordert mindestens ein Replikat verfügbar, für die heraufstufung mit der gleichen Sequenznummer wie die frühere primäre Datenbank. Der Agent Schrittmacher Ressourcensätze `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` so, dass mindestens ein sekundäres Replikat wird, auf dem neuesten Stand und für das Ziel in der Standardeinstellung ein automatisches Failover verfügbar. Mit jeder Überwachung Aktion, den Wert des `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` berechnet (und bei Bedarf aktualisiert). Die `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` Wert ist "Anzahl der synchronen Replikate" geteilt durch 2. Zum Zeitpunkt der Failover der Ressourcen-Agent benötigt (`total number of replicas`  -  `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` Replikate) So reagieren Sie auf die Benachrichtigung vorab heraufstufen. Das Replikat mit der höchsten `sequence_number` primäre heraufgestuft wird. 

Z. B. eine verfügbarkeitsgruppe mit drei synchronen Replikaten - ein primäres Replikat und zwei synchrone sekundäre Replikate.

- `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT`ist 1. (3 / 2-1 >).

- Die erforderliche Anzahl von Replikaten zu reagieren, um eine Aktion vorab zu erzielen, ist 2. (3: 1 = 2). 

In diesem Szenario haben zwei Replikate für die Reaktion für das Failover ausgelöst werden soll. Für das erfolgreiche automatische Failover nach einem Ausfall des primären Replikats, beide sekundäre Replikate müssen auf dem neuesten Stand und reagieren auf die Benachrichtigung vorab heraufstufen. Wenn sie online und synchron sind, haben sie die gleichen Sequenznummer. Die verfügbarkeitsgruppe stuft eine davon. Wenn nur eines der sekundären Replikate auf reagiert der vorab heraufstufen Aktion, der Resource-Agent kann nicht garantieren, dass die sekundäre Datenbank, die geantwortet hat die höchste Sequence_number hat und ein Failover wird nicht ausgelöst.

>[!IMPORTANT]
>Wenn `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` 0 (null) entspricht, besteht das Risiko von Datenverlust. Bei einem Ausfall primäre Replikat wird der Agent für die Ressource nicht automatisch einen Failover ausgelöst. Sie können entweder warten, vom primären zum Wiederherstellen oder manuell ein Failover mit `FORCE_FAILOVER_ALLOW_DATA_LOSS`.

Sie können auswählen, um das Standardverhalten überschreiben und verhindern, dass die verfügbarkeitsgruppenressource Einstellung `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` automatisch.

Das folgende Skript legt `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` auf 0 für eine verfügbarkeitsgruppe mit dem Namen `<**ag1**>`. Vor dem Ausführen von Replace `<**ag1**>` mit dem Namen der verfügbarkeitsgruppe.

```bash
sudo pcs resource update <**ag1**> required_synchronized_secondaries_to_commit=0
```

Wieder in den Standardwert, basierend auf der Konfiguration der verfügbarkeitsgruppe ausführen:

```bash
sudo pcs resource update <**ag1**> required_synchronized_secondaries_to_commit=
```

>[!NOTE]
>Wenn Sie die vorherigen Befehle ausführen, wird das primäre vorübergehend zum sekundären herabgestuft anschließend erneut heraufgestuft. Das Update der Ressource bewirkt, dass alle Replikate beenden und neu starten. Der neue Wert für`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` wird nur festgelegt werden, sobald die Replikate neu gestartet werden, nicht sofort.

## <a name="see-also"></a>Siehe auch

[Verfügbarkeitsgruppen unter Linux](sql-server-linux-availability-group-overview.md)

<!--Image references-->
[1]: ./media/sql-server-linux-availability-group-ha/1-read-scale-out.png
[2]: ./media/sql-server-linux-availability-group-ha/2-configuration-only.png
[3]: ./media/sql-server-linux-availability-group-ha/3-three-replica.png
[4]: ./media/sql-server-linux-availability-group-ha/configuration-only-example.png
