---
title: SQL Server AlwaysOn Availability Group-Bereitstellungsmuster | Microsoft Docs
ms.custom: 
ms.date: 06/16/2017
ms.prod: sql-linux
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: edd75f68-dc62-4479-a596-57ce8ad632e5
caps.latest.revision: 34
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 8e2d26fd9ce79fc8c47c7499313648d565ae1b97
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---

# <a name="high-availability-and-data-protection-for-availability-group-configurations"></a>Hohe Verfügbarkeit und Datenschutz für verfügbarkeitsgruppenkonfigurationen

Dieser Artikel zeigt unterstützte Bereitstellungskonfigurationen für SQL Server Always On-Verfügbarkeitsgruppen für Linux-Servern. Eine verfügbarkeitsgruppe unterstützt hohe Verfügbarkeit und Schutz von Daten. Automatische fehlererkennung, automatisches Failover und transparente wiederverbindung nach einem Failover bereitstellen hohen Verfügbarkeit. Synchronisierte Replikate bereitzustellen Datenschutz. 

>[!NOTE]
>Zusätzlich zu hohe Verfügbarkeit und Datenschutz eine verfügbarkeitsgruppe auch ermöglichen Wiederherstellung im Notfall, cross Platform Migration und mit horizontaler Skalierung zu lesen. Dieser Artikel beschreibt in erster Linie die Implementierungen für hohe Verfügbarkeit und Datenschutz. 

Mit Windows Server Failover clustering, eine gemeinsame Konfiguration für hoher Verfügbarkeit mit zwei synchrone Replikaten verwendet und eine [Dateifreigaben Zeugen](http://technet.microsoft.com/library/cc731739.aspx). Der Dateifreigabenzeugen überprüft die verfügbarkeitsgruppenkonfiguration - Status der Synchronisierung und die Rolle des Replikats, zum Beispiel. Diese Konfiguration wird sichergestellt, dass das sekundäre Replikat als Ziel für das Failover die neuesten Daten und alle Änderungen an der Konfiguration von Availability-Gruppe ausgewählt. 

Die aktuelle Lösungen mit hoher Verfügbarkeit für Linux führen Sie einen externen Zeugen wie dateifreigabezeugen in einem Windows Server-Failovercluster nicht aufnehmen. Wenn es kein Windows Server-Failovercluster ist, wird die verfügbarkeitsgruppenkonfiguration in der master-Datenbank auf beteiligten Instanzen von SQL Server gespeichert. Die verfügbarkeitsgruppe erfordert daher mindestens drei synchroner Replikate für hohe Verfügbarkeit und Datenschutz. Erstellen Sie eine Clusterressource, nach der Erstellung einer verfügbarkeitsgruppe auf Linux-Servern. Die Ressource Clustereinstellungen bestimmen die Konfiguration für hohe Verfügbarkeit.

Wählen Sie einen Entwurf Verfügbarkeit für hohe Verfügbarkeit, Datenschutz, bestimmte geschäftsanforderungen zu erfüllen, und lesen die horizontale Skalierung.

>[!IMPORTANT]
>Die folgenden Konfigurationen werden den Entwurfsmustern für die Verfügbarkeit-Gruppe und die Funktionen der einzelnen Muster beschrieben. Diese Entwurfsmuster anwenden, um Verfügbarkeitsgruppen mit `CLUSTER_TYPE = EXTERNAL` für Lösungen mit hoher Verfügbarkeit. 

Der Entwurf Patters sind zwei verfügbarkeitsgruppenkonfigurationen. Die Konfigurationen umfassen Folgendes:

- **Drei synchroner Replikate**

- **Zwei synchrone Replikate**

## <a name="how-the-configuration-affects-default-resource-settings"></a>Auswirkungen von Standardeinstellungen für die Ressource in die Konfiguration

Die Einstellung "Cluster Resource" `required_synchronized_secondaries_to_commit` wird sichergestellt, dass jede Transaktion in einer minimalen Anzahl von sekundären Replikat Protokolle geschrieben wird, vor dem Commit der Transaktion auf dem primären Replikat. Diese Einstellung kann auf hohe Verfügbarkeit und Datenschutz, abhängig von der Konfiguration beeinflussen. Bei der Installation des SQL Server-Ressource-Agents - `mssql-server-ha` - und erstellen Sie eine Clusterressource für die verfügbarkeitsgruppe, wird der Cluster-Manager erkennt die Verfügbarkeit gruppieren, Konfiguration und legt `required_synchronized_secondaries_to_commit` entsprechend. 

Wenn von der Konfiguration die Ressource Agentparameter unterstützt `required_synchronized_secondaries_to_commit` festgelegt ist, auf den Wert an, die hohe Verfügbarkeit und Datenschutz bietet. Weitere Informationen finden Sie unter [verstehen von SQL Server-Ressource-Agent für Schrittmacher](#pacemakerNotify).

In den folgenden Abschnitten wird das Standardverhalten für die Clusterressource erläutert. 

<a name="threeSynch"></a>

## <a name="three-synchronous-replicas"></a>Drei synchroner Replikate

Diese Konfiguration umfasst drei synchroner Replikate. Standardmäßig wird die hohe Verfügbarkeit und Datenschutz. Es kann auch lesen mit horizontaler Skalierung bereitstellen.

![Drei Replikate][3]

Die folgende Tabelle beschreibt die hohe Verfügbarkeit und Schutzverhalten basierend auf den Einstellungen für eine verfügbarkeitsgruppe mit drei synchronen Replikaten: 

|`required_synchronized_secondaries_to_commit`|0 |1 \*|2
| --- |:---:|:---:|:---:
|Automatisches Failover nach dem Ausfall des primären Replikats| |✔| 
|Primäre Replikat verfügbar, nachdem ein sekundäres Replikat Ausfall|✔|✔| 
|Primäre Replikat nach zwei Ausfällen der sekundäres Replikat verfügbar|✔| |
|Manuelles Failover nach Ausfall der primären Replikat - möglichem Datenverlust|✔| | 

\*Standard festlegen, wenn die verfügbarkeitsgruppe als Ressource in einem Cluster hinzugefügt wird.

<a name="twoSynch"></a>

## <a name="two-synchronous-replicas"></a>Zwei synchrone Replikate

Mit dieser Konfiguration können den Datenschutz. Wie die anderen verfügbarkeitsgruppenkonfigurationen können sie schreibgeschützte mit horizontaler Skalierung aktivieren. Die Konfiguration von zwei synchronen Replikaten bietet keine automatische hohen Verfügbarkeit. 

![Zwei synchrone Replikate][1]

Diese Konfiguration sind zwei Server erforderlich. Diese Server füllen Sie die Rolle des primären und sekundären Replikat. 

Die Konfiguration von zwei synchronen Replikaten ist optimiert für Data Protection und die lesearbeitslast für Datenbanken zu verteilen. Standardmäßig ist die Ressource für den Datenschutz konfiguriert. Diese Konfiguration bietet keine hohen Verfügbarkeit, da fällt eine Instanz von SQL Server aus, entweder die Datenbank nicht vollständig verfügbar ist oder Gefahr eines Datenverlusts besteht. 

Die folgende Tabelle beschreibt das Verhalten beim Datenschutz gemäß den möglichen Werten für eine verfügbarkeitsgruppe mit zwei synchronen Replikaten: 

|`required_synchronized_secondaries_to_commit`|0 \*|1 
| --- |:---|:---
|Automatisches Failover nach dem Ausfall des primären Replikats| |✔ \*\* | 
|Primäre Replikat verfügbar ist, nach dem Ausfall des sekundären Replikats|✔| |

\*Standard festlegen, wenn die verfügbarkeitsgruppe als Ressource in einem Cluster hinzugefügt wird.

\*\*In dieser Konfiguration nachdem der Ausfall des primären Replikats die verfügbarkeitsgruppe, die automatische erfolgt ein Failover. Anwendungen können nicht mit der verfügbarkeitsgruppe herstellen, bis das primäre Replikat, wieder auf die Zeile – jetzt als sekundäres Replikat ist. 

Die Konfiguration von zwei synchronen Replikate, möglicherweise die wirtschaftliche, daran, dass er nur zwei Instanzen von SQL Server auf zwei Servern erfordert.

<a name="pacemakerNotify"></a>

## <a name="understand-sql-server-resource-agent-for-pacemaker"></a>SQL Server-Agent-Ressource für Schrittmacher verstehen

SQL Server 2017 CTP 1.4 hinzugefügt `sequence_number` auf `sys.availability_groups` ermöglichen Schrittmacher wie auf dem neuesten Stand sekundäre identifizieren Replikate, die mit dem primären Replikat sind. `sequence_number`ist eine monoton ansteigende "bigint", die Aktualität des lokalen verfügbarkeitsgruppenreplikats darstellt. Schrittmacher Updates der `sequence_number` mit jeder Availability Group-konfigurationsänderung. Beispiele für Änderungen an der Konfiguration sind Failover, Replikat hinzufügen oder entfernen. Die Anzahl der primären Datenbank aktualisiert, dann auf sekundäre Replikate repliziert. Daher hat ein sekundäres Replikat, das der aktuellen Konfiguration verfügt wie die primäre Datenbank die gleichen Sequenznummer. 

Wenn Schrittmacher entscheidet, die ein Replikat zur primären höher stufen, sendet er zuerst eine *vorab heraufstufen* Benachrichtigung an alle Replikate. Die Replikate zurück, die Sequenznummer. Als Nächstes Schrittmacher tatsächlich versucht, ein Replikat zur primären höher stufen, stuft das Replikat nur selbst wenn die Sequenznummer der höchsten die Sequenznummern ist. Wenn eine eigene Sequenznummer nicht mit die höchste Sequenznummer übereinstimmt, lehnt das Replikat den Promote-Vorgang ab. Auf diese Weise kann nur das Replikat mit der höchsten Sequenznummer zu einem primären heraufgestuft werden, sodass es nicht zu Datenverlust kommt. 

Dieser Prozess erfordert mindestens ein Replikat verfügbar, für die heraufstufung mit der gleichen Sequenznummer wie die frühere primäre Datenbank. Der Agent Schrittmacher Ressourcensätze `required_synchronized_secondaries_to_commit` so, dass mindestens ein sekundäres Replikat wird, auf dem neuesten Stand und für das Ziel in der Standardeinstellung ein automatisches Failover verfügbar. Mit jeder Überwachung Aktion, den Wert des `required_synchronized_secondaries_to_commit` berechnet (und bei Bedarf aktualisiert). Die `required_synchronized_secondaries_to_commit` Wert ist "Anzahl der synchronen Replikate" geteilt durch 2. Zum Zeitpunkt der Failover der Ressourcen-Agent benötigt (`total number of replicas`  -  `required_synchronized_secondaries_to_commit` Replikate) So reagieren Sie auf die Benachrichtigung vorab heraufstufen. Das Replikat mit der höchsten `sequence_number` primäre heraufgestuft wird. 

Z. B. eine verfügbarkeitsgruppe mit drei synchronen Replikaten - ein primäres Replikat und zwei synchrone sekundäre Replikate.

- `required_synchronized_secondaries_to_commit`ist 1. (3 / 2-1 >).

- Die erforderliche Anzahl von Replikaten zu reagieren, um eine Aktion vorab zu erzielen, ist 2. (3: 1 = 2). 

In diesem Szenario haben zwei Replikate für die Reaktion für das Failover ausgelöst werden soll. Für das erfolgreiche automatische Failover nach einem Ausfall des primären Replikats, beide sekundäre Replikate müssen auf dem neuesten Stand und reagieren auf die Benachrichtigung vorab heraufstufen. Wenn sie online und synchron sind, haben sie die gleichen Sequenznummer. Die verfügbarkeitsgruppe stuft eine davon. Wenn nur eines der sekundären Replikate auf reagiert der vorab heraufstufen Aktion, der Resource-Agent kann nicht garantieren, dass die sekundäre Datenbank, die geantwortet hat die höchste Sequence_number hat und ein Failover wird nicht ausgelöst.

>[!IMPORTANT]
>Wenn `required_synchronized_secondaries_to_commit` ist Risiko eines Datenverlusts 0 vorhanden ist. Bei einem Ausfall primäre Replikat wird der Agent für die Ressource nicht automatisch einen Failover ausgelöst. Sie können entweder warten, vom primären zum Wiederherstellen oder manuell ein Failover mit `FORCE_FAILOVER_ALLOW_DATA_LOSS`.

Sie können auswählen, um das Standardverhalten überschreiben und verhindern, dass die verfügbarkeitsgruppenressource Einstellung `required_synchronized_secondaries_to_commit` automatisch.

Das folgende Skript legt `required_synchronized_secondaries_to_commit` auf 0 für eine verfügbarkeitsgruppe mit dem Namen `<**ag1**>`. Vor dem Ausführen von Replace `<**ag1**>` mit dem Namen der verfügbarkeitsgruppe.

```bash
sudo pcs resource update <**ag1**> required_synchronized_secondaries_to_commit=0
```

Wieder in den Standardwert, basierend auf der Konfiguration der verfügbarkeitsgruppe ausführen:

```bash
sudo pcs resource update <**ag1**> required_synchronized_secondaries_to_commit=
```

>[!NOTE]
>Wenn Sie die vorherigen Befehle ausführen, wird das primäre vorübergehend zum sekundären herabgestuft anschließend erneut heraufgestuft. Das Update der Ressource bewirkt, dass alle Replikate beenden und neu starten. Der neue Wert für`required_synchronized_secondaries_to_commit` wird nur festgelegt werden, sobald die Replikate neu gestartet werden, nicht sofort.

<!--Image references-->
[1]: ./media/sql-server-linux-availability-group-ha/1-read-scale-out.png
[3]: ./media/sql-server-linux-availability-group-ha/3-three-replica.png
