---
title: Protokollieren von Aktivitäten | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- logging activity
ms.assetid: a777b3d9-2262-4e82-bc82-b62ad60d0e55
caps.latest.revision: 32
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ec9c672009668d8320380dd6163de7e5ccc61270
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="logging-activity"></a>Protokollieren von Aktivitäten
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Standardmäßig werden Fehler und Warnungen, die von [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] generiert werden, nicht protokolliert. Dieses Thema erläutert, wie Protokollierungsaktivitäten konfiguriert werden.  
  
## <a name="logging-activity-using-the-pdosqlsrv-driver"></a>Protokollieren von Aktivitäten mit dem PDO_SQLSRV-Treiber  
Die einzige Konfiguration, die für den PDO_SQLSRV-Treiber verfügbar ist, ist der pdo_sqlsrv.log_severity-Eintrag in der Datei „php.ini“.  
  
Fügen Sie am Ende der Datei „php.ini“ Folgendes ein:  
  
```  
[pdo_sqlsrv]  
pdo_sqlsrv.log_severity = <number>  
```  
  
Für**log_severity** sind die folgenden Werte möglich.  
  
|Wert|Beschreibung|  
|---------|---------------|  
|0|Die Protokollierung ist deaktiviert (Standardeinstellung, wenn nichts definiert ist).|  
|-1|Gibt an, dass Fehler, Warnungen und Hinweise protokolliert werden.|  
|1|Gibt an, dass Fehler protokolliert werden.|  
|2|Gibt an, dass Warnungen protokolliert werden.|  
|4|Gibt an, dass Hinweise protokolliert werden.|  
  
Protokollieren von Informationen wird der "phperrors.log"-Datei hinzugefügt.  
  
PHP liest die Konfigurationsdatei bei der Initialisierung und speichert die Daten in einem Cache. Außerdem stellt es eine API bereit, um die Einstellungen, die in die Konfigurationsdatei geschrieben werden, zu updaten und sofort zu verwenden. Mit dieser API können Anwendungsskripts die Einstellungen auch nach der PHP-Initialisierung ändern.  
  
## <a name="logging-activity-using-the-sqlsrv-driver"></a>Protokollieren von Aktivitäten mit dem SQLSRV-Treiber  
Um die Protokollierung aktivieren, können Sie die [Sqlsrv_configure](../../connect/php/sqlsrv-configure.md) -Funktion verwenden oder die "PHP.ini"-Datei ändern. Sie können Aktivitäten protokollieren, die in Initialisierungen, Verbindungen, Anweisungen oder Fehlerfunktionen auftreten. Sie können auch angeben, ob Fehler, Warnungen, Hinweise oder alle drei protokolliert werden sollen.  
  
> [!NOTE]  
> Sie können den Speicherort der Protokolldatei in der Datei „php.ini“ konfigurieren.  
  
### <a name="turning-logging-on"></a>Aktivieren der Protokollierung  
Protokollierung aktiviert, mithilfe der [Sqlsrv_configure](../../connect/php/sqlsrv-configure.md) Funktion an einen Wert für die **LogSubsystems** Einstellung. Zum Beispiel konfiguriert die folgende Codezeile den Treiber zur Protokollierung von Aktivitäten bei Verbindungen:  
  
`sqlsrv_configure("LogSubsystems", SQLSRV_LOG_SYSTEM_CONN);`  
  
Die folgende Tabelle beschreibt die Konstanten, die als Wert für die **LogSubsystems** -Einstellung verwendet werden können:  
  
|Wert (entsprechende ganze Zahl in Klammern)|Description|  
|-----------------------------------------------|---------------|  
|SQLSRV_LOG_SYSTEM_ALL (-1)|Aktiviert die Protokollierung aller Subsysteme.|  
|SQLSRV_LOG_SYSTEM_OFF(0)|Deaktiviert die Protokollierung. Dies ist die Standardeinstellung.|  
|SQLSRV_LOG_SYSTEM_INIT (1)|Aktiviert die Protokollierung der Initialisierungsaktivität.|  
|SQLSRV_LOG_SYSTEM_CONN (2)|Aktiviert die Protokollierung der Verbindungsaktivität.|  
|SQLSRV_LOG_SYSTEM_STMT (4)|Aktiviert die Protokollierung der Anweisungsaktivität.|  
|SQLSRV_LOG_SYSTEM_UTIL (8)|Aktiviert die Protokollierung der Fehlerfunktionsaktivität (z. B. Handle_error und Handle_warning).|  
  
Sie können mehr als einen Wert festlegen, zu einem Zeitpunkt für die **LogSubsystems** mithilfe des logischen OR-Operators (|) festlegen. Die folgende Codezeile aktiviert z. B. die Protokollierung der Aktivität für Verbindungen und Anweisungen:  
  
`sqlsrv_configure("LogSubsystems", SQLSRV_LOG_SYSTEM_CONN | SQLSRV_LOG_SYSTEM_STMT);`  
  
Sie können auch auf die Protokollierung aktivieren, durch Angeben eines ganzzahligen Werts für die **LogSubsystems** in der Datei "PHP.ini" festlegen. Z. B. die folgende Zeile zum Hinzufügen der `[sqlsrv]` -Abschnitts der "PHP.ini"-Datei die Protokollierung der Verbindungsaktivität aktiviert:  
  
`sqlsrv.LogSubsystems = 2`  
  
Durch die Addition von ganzzahligen Werten können Sie mehrere Optionen gleichzeitig angeben. Z. B. die folgende Zeile zum Hinzufügen der `[sqlsrv]` Abschnitt der Datei "PHP.ini" aktiviert die Protokollierung der Verbindungs-und:  
  
`sqlsrv.LogSubsystems = 6`  
  
### <a name="logging-errors-warnings-and-notices"></a>Protokollieren von Fehlern, Warnungen und Hinweisen  
Nachdem die Protokollierung aktiviert wurde, müssen Sie angeben, was protokolliert werden soll. Sie können eine oder mehrere der folgenden Möglichkeiten protokollieren: Fehler, Warnungen und Hinweise. Die folgende Codezeile gibt z. B., dass nur Warnungen protokolliert werden:  
  
`sqlsrv_configure("LogSeverity", SQLSRV_LOG_SEVERITY_WARNING);`  
  
> [!NOTE]  
> Die Standardeinstellung für **LogSeverity** ist **SQLSRV_LOG_SEVERITY_ERROR**. Wenn die Protokollierung aktiviert ist und keine Einstellung für die **LogSeverity** angegeben ist, werden nur Fehler protokolliert.  
  
Die folgende Tabelle beschreibt die Konstanten, die als Wert für die **LogSeverity** -Einstellung verwendet werden können:  
  
|Wert (entsprechende ganze Zahl in Klammern)|Description|  
|-----------------------------------------------|---------------|  
|SQLSRV_LOG_SEVERITY_ALL (-1)|Gibt an, dass Fehler, Warnungen und Hinweise protokolliert werden.|  
|SQLSRV_LOG_SEVERITY_ERROR (1)|Gibt an, dass Fehler protokolliert werden. Dies ist die Standardeinstellung.|  
|SQLSRV_LOG_SEVERITY_WARNING (2)|Gibt an, dass Warnungen protokolliert werden.|  
|SQLSRV_LOG_SEVERITY_NOTICE (4)|Gibt an, dass Hinweise protokolliert werden.|  
  
Sie können mehr als einen Wert festlegen, zu einem Zeitpunkt für die **LogSeverity** mithilfe des logischen OR-Operators (|) festlegen. Die folgende Codezeile gibt z. B. an, dass Fehler und Warnungen protokolliert werden sollten:  
  
`sqlsrv_configure("LogSeverity", SQLSRV_LOG_SEVERITY_ERROR | SQLSRV_LOG_SEVERITY_WARNING);`  
  
> [!NOTE]  
> Angeben eines Werts für die **LogSeverity** Einstellung Protokollierung nicht aktiviert ist. Schalten Sie die Protokollierung durch Angabe eines Werts für die **LogSubsystems** festlegen, dann legen Sie den Schweregrad der protokolliert werden durch Festlegen eines Werts für **LogSeverity**.  
  
Sie können auch eine Einstellung für die **LogSeverity** -Einstellung mithilfe von ganzzahligen Werten in der Datei „php.ini“ festlegen. Zum Beispiel wird durch Hinzufügen der folgende Zeile des `[sqlsrv]` -Abschnitts der „php.ini“-Datei nur die Protokollierung von Warnungen aktiviert.  
  
`sqlsrv.LogSeverity = 2`  
  
Durch die Addition von ganzzahligen Werten können Sie mehrere Optionen gleichzeitig angeben. Z. B. die folgende Zeile zum Hinzufügen der `[sqlsrv]` Abschnitt der Datei "PHP.ini" ermöglicht die Protokollierung von Fehlern und Warnungen:  
  
`sqlsrv.LogSeverity = 3`  
  
## <a name="see-also"></a>Siehe auch  
[Programmierhandbuch für den Microsoft-Treiber für PHP für SQLServer](../../connect/php/programming-guide-for-php-sql-driver.md)

[Konstanten &#40;Microsoft-Treiber für PHP für SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)

[sqlsrv_configure](../../connect/php/sqlsrv-configure.md)

[sqlsrv_get_config](../../connect/php/sqlsrv-get-config.md)

[API-Referenz für den SQLSRV-Treiber](../../connect/php/sqlsrv-driver-api-reference.md)  
  
