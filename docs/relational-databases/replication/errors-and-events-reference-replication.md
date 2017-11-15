---
title: Fehler- und Ereignisreferenz (Replikation) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- errors [SQL Server replication], troubleshooting
- troubleshooting [SQL Server replication], errors
- replication [SQL Server], troubleshooting
- errors [SQL Server replication]
- errors and events reference [SQL Server replication]
ms.assetid: e67d1bab-47b6-441d-ab9c-251a2ca499e1
caps.latest.revision: "25"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 20e7e616a30c61840899c0bd168d72dbaabe99ce
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="errors-and-events-reference-replication"></a>Fehler- und Ereignisreferenz (Replikation)
  Dieser Abschnitt der Dokumentation enthält Informationen zu Ursachen und Lösungen für eine Reihe von Fehlern, die im Zusammenhang mit der Replikation auftreten können.  
  
|Fehler|MessageBox|  
|-----------|-------------|  
|[MSSQL_ENG002601](../../relational-databases/replication/mssql-eng002601.md)|Eine Zeile mit doppeltem Schlüssel kann in das „%1!s!“-Objekt mit dem eindeutigen „%.\*ls“-Index nicht eingefügt werden.|  
|[MSSQL_ENG002627](../../relational-databases/replication/mssql-eng002627.md)|Verletzung der %1!s!-Einschränkung '%2!s!'. Ein doppelter Schlüssel kann in das „%.\*ls“-Objekt nicht eingefügt werden.|  
|[MSSQL_ENG003165](../../relational-databases/replication/mssql-eng003165.md)|Die %1!s!-Datenbank wurde wiederhergestellt; beim Wiederherstellen/Entfernen der Replikation wurde jedoch ein Fehler erkannt. Die Datenbank ist offline. Weitere Informationen finden Sie im Thema 'MSSQL_ENG003165' in der SQL Server-Onlinedokumentation.|  
|[MSSQL_ENG003724](../../relational-databases/replication/mssql-eng003724.md)|Das %1!s! von '%3!s!' (%2!s!) ist nicht möglich, da das Objekt für die Replikation verwendet wird.|  
|[MSSQL_ENG004929](../../relational-databases/replication/mssql-eng004929.md)|Das %1!s!-Objekt '%2!s!' kann nicht geändert werden, da es für die Replikation veröffentlicht wird.|  
|MSSQL_ENG007395. Siehe [Troubleshooting Oracle Publishers](../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md).|Für den OLE DB-Anbieter '%1!s!' für den Verbindungsserver '%2!s!' konnte keine geschachtelte Transaktion gestartet werden. Eine geschachtelte Transaktion war erforderlich, da die Option XACT_ABORT auf OFF festgelegt war.|  
|[MSSQL_ENG014005](../../relational-databases/replication/mssql-eng014005.md)|Die Veröffentlichung konnte nicht gelöscht werden. Es besteht ein Abonnement für sie.|  
|[MSSQL_ENG014010](../../relational-databases/replication/mssql-eng014010.md)|Der Server '%1!s!' ist nicht als Abonnementserver definiert.|  
|[MSSQL_ENG014114](../../relational-databases/replication/mssql-eng014114.md)|'%1!s!' ist nicht als Verteiler konfiguriert.|  
|[MSSQL_ENG014117](../../relational-databases/replication/mssql-eng014117.md)|'%1!s!' ist nicht als Verteilungsdatenbank konfiguriert.|  
|[MSSQL_ENG014120](../../relational-databases/replication/mssql-eng014120.md)|Die %1!s!-Verteilungsdatenbank konnte nicht gelöscht werden. Diese Verteilerdatenbank ist einem Verleger zugeordnet.|  
|[MSSQL_ENG014121](../../relational-databases/replication/mssql-eng014121.md)|Der Verteiler '%1!s!' konnte nicht gelöscht werden. Dieser Verteiler besitzt zugeordnete Verteilungsdatenbanken.|  
|[MSSQL_ENG014144](../../relational-databases/replication/mssql-eng014144.md)|Der '%s'-Abonnent kann nicht gelöscht werden. Für ihn sind Abonnements in der %2!s!-Veröffentlichungsdatenbank vorhanden.|  
|[MSSQL_ENG014150](../../relational-databases/replication/mssql-eng014150.md)|Replikations-%1!: %2! (Agent) erfolgreich. %3!|  
|[MSSQL_ENG014151](../../relational-databases/replication/mssql-eng014151.md)|Replikations-%1!s!: Fehler beim %2!s!-Agent. %3!|  
|[MSSQL_ENG014152](../../relational-databases/replication/mssql-eng014152.md)|Replikations-%1!: %2! (Agent) ist für die Wiederholung geplant. %3!|  
|[MSSQL_ENG014157](../../relational-databases/replication/mssql-eng014157.md)|Das Abonnement des Abonnenten '%1!s!' für die %2!s!-Veröffentlichung ist abgelaufen und wurde gelöscht.|  
|[MSSQL_ENG014160](../../relational-databases/replication/mssql-eng014160.md)|Der Schwellenwert [%s:%s] für die [%s]-Veröffentlichung wurde festgelegt. Mindestens ein Abonnement für diese Veröffentlichung ist abgelaufen.|  
|[MSSQL_ENG014161](../../relational-databases/replication/mssql-eng014161.md)|Der Schwellenwert [%s:%s] für die [%s]-Veröffentlichung wurde festgelegt. Stellen Sie sicher, dass der Protokolllese-Agent und der Verteilungs-Agent ausgeführt werden und die Latenzzeitanforderung erfüllen können.|  
|[MSSQL_ENG014162](../../relational-databases/replication/mssql-eng014162.md)|Der Schwellenwert [%s:%s] für die [%s]-Veröffentlichung wurde festgelegt. Stellen Sie sicher, dass der Merge-Agent ausgeführt wird und die erwartete Anforderung erfüllen kann.|  
|[MSSQL_ENG014163](../../relational-databases/replication/mssql-eng014163.md)|Der Schwellenwert [%s:%s] für die [%s]-Veröffentlichung wurde festgelegt. Stellen Sie sicher, dass der Merge-Agent ausgeführt wird und die erwartete Anforderung erfüllen kann.|  
|[MSSQL_ENG014164](../../relational-databases/replication/mssql-eng014164.md)|Der Schwellenwert [%s:%s] für die [%s]-Veröffentlichung wurde festgelegt. Stellen Sie sicher, dass der Merge-Agent ausgeführt wird und die erwartete Anforderung erfüllen kann.|  
|[MSSQL_ENG014165](../../relational-databases/replication/mssql-eng014165.md)|Der Schwellenwert [%s:%s] für die [%s]-Veröffentlichung wurde festgelegt. Stellen Sie sicher, dass der Merge-Agent ausgeführt wird und die erwartete Anforderung erfüllen kann.|  
|[MSSQL_ENG018456](../../relational-databases/replication/mssql-eng018456.md)|Fehler bei der Anmeldung für den Benutzer „%.*ls'.%.\*ls“|  
|[MSSQL_ENG018752](../../relational-databases/replication/mssql-eng018752.md)|Nur jeweils ein Protokolllese-Agent oder eine protokollbezogene Prozedur (sp_repldone, sp_replcmds oder sp_replshowcmds) kann eine Verbindung mit einer Datenbank herstellen. Falls Sie eine protokollbezogene Prozedur ausgeführt haben, löschen Sie vor dem Starten des Protokolllese-Agents oder dem Ausführen einer weiteren protokollbezogenen Prozedur die Verbindung, über die sie ausgeführt wurde, oder führen Sie 'sp_replflush' über diese Verbindung aus.|  
|[MSSQL_ENG020554](../../relational-databases/replication/mssql-eng020554.md)|Vom Replikations-Agent wurde in %ld Minuten keine Statusmeldung protokolliert. Möglicherweise reagiert der Agent nicht mehr, oder das System ist stark ausgelastet. Überprüfen Sie, ob Datensätze an das Ziel repliziert werden und ob die Verbindungen mit dem Abonnenten, Verleger und Verteiler noch aktiv sind.|  
|[MSSQL_ENG020557](../../relational-databases/replication/mssql-eng020557.md)|Der Agent wird heruntergefahren. Weitere Informationen finden Sie im Auftragsverlauf des SQL Server-Agents für den Auftrag '%s'.|  
|[MSSQL_ENG020572](../../relational-databases/replication/mssql-eng020572.md)|Das Abonnement des Abonnenten '%s' für den '%s'-Artikel in der '%s'-Veröffentlichung wurde nach einem Datenüberprüfungsfehler neu initialisiert.|  
|[MSSQL_ENG020574](../../relational-databases/replication/mssql-eng020574.md)|Fehler bei der Datenüberprüfung für das Abonnement des Abonnenten '%s' für den '%s'-Artikel in der '%s'-Veröffentlichung.|  
|[MSSQL_ENG020575](../../relational-databases/replication/mssql-eng020575.md)|Die Datenüberprüfung für das Abonnement des Abonnenten '%s' für den '%s'-Artikel in der '%s'-Veröffentlichung wurde erfolgreich durchlaufen.|  
|[MSSQL_ENG020596](../../relational-databases/replication/mssql-eng020596.md)|Nur '%s' und Mitglieder der db_owner-Rolle können den anonymen Agent löschen.|  
|[MSSQL_ENG020598](../../relational-databases/replication/mssql-eng020598.md)|Die Zeile wurde bei der Anwendung des replizierten Befehls auf dem Abonnenten nicht gefunden.|  
|[MSSQL_ENG021075](../../relational-databases/replication/mssql-eng021075.md)|Die Anfangsmomentaufnahme für die %1!s!-Veröffentlichung ist noch nicht verfügbar.|  
|[MSSQL_ENG021076](../../relational-databases/replication/mssql-eng021076.md)|Die Anfangsmomentaufnahme für den %1!s!-Artikel ist noch nicht verfügbar.|  
|[MSSQL_ENG021286](../../relational-databases/replication/mssql-eng021286.md)|Die %1!s!-Konflikttabelle ist nicht vorhanden.|  
|[MSSQL_ENG021330](../../relational-databases/replication/mssql-eng021330.md)|Fehler beim Erstellen eines Unterverzeichnisses unter dem Replikationsarbeitsverzeichnis. (%1!s!)|  
|[MSSQL_ENG021331](../../relational-databases/replication/mssql-eng021331.md)|Fehler beim Kopieren der Benutzerskriptdatei auf den Verteiler. (%1!s!)|  
|[MSSQL_ENG021385](../../relational-databases/replication/mssql-eng021385.md)|Der Momentaufnahmevorgang konnte die %1!s!-Veröffentlichung nicht verarbeiten. Möglicherweise ist gerade eine Schemaänderungsaktivität aktiv, oder es werden neue Artikel hinzugefügt.|  
|MSSQL_ENG021617. Siehe [Troubleshooting Oracle Publishers](../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md).|SQL*PLUS konnte nicht ausgeführt werden. Stellen Sie sicher, dass die aktuelle Version des Oracle-Clientcodes auf dem Verteiler installiert ist.|  
|MSSQL_ENG021642. Siehe [Troubleshooting Oracle Publishers](../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md).|Die Version von SQL*PLUS, auf die über die Systemvariable Path zugegriffen wird, ist nicht aktuell genug, um die Veröffentlichung mit Oracle zu unterstützen. Stellen Sie sicher, dass die aktuelle Version des Oracle-Clientcodes auf dem Verteiler installiert ist.|  
|MSSQL_ENG021624. Siehe [Troubleshooting Oracle Publishers](../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md).|Der registrierte OLE DB-Anbieter von Oracle, OraOLEDB.Oracle, wurde auf dem Verteiler '%s' nicht gefunden. Stellen Sie sicher, dass die aktuelle Version des OLE DB-Anbieters von Oracle auf dem Verteiler installiert und registriert ist.|  
|MSSQL_ENG021626. Siehe [Troubleshooting Oracle Publishers](../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md).|Die Verbindung mit dem Oracle-Datenbankserver '%s' kann mithilfe des OLE DB-Anbieters von Oracle, OraOLEDB.Oracle, nicht hergestellt werden.|  
|MSSQL_ENG021627. Siehe [Troubleshooting Oracle Publishers](../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md).|Die Verbindung mit dem Oracle-Datenbankserver '%s' kann mithilfe des OLE DB-Anbieters von Microsoft, MSDAORA, nicht hergestellt werden.|  
|MSSQL_ENG021628. Siehe [Troubleshooting Oracle Publishers](../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md).|Die Registrierung des Verteilers '%s' kann nicht so aktualisiert werden, dass der OLE DB-Anbieter von Oracle, OraOLEDB.Oracle, in einem Prozess mit SQL Server ausgeführt werden kann. Stellen Sie sicher, dass der aktuelle Anmeldename autorisiert ist, Registrierungsschlüssel im Besitz von SQL Server zu ändern.|  
|MSSQL_ENG021629. Siehe [Troubleshooting Oracle Publishers](../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md).|Der CLSID-Registrierungsschlüssel, der anzeigt, dass der OLE DB-Anbieter von Oracle, OraOLEDB.Oracle, registriert wurde, ist auf dem Verteiler nicht vorhanden. Stellen Sie sicher, dass der OLE DB-Anbieter von Oracle auf dem Verteiler installiert und registriert ist.|  
|MSSQL_ENG021642. Siehe [Troubleshooting Oracle Publishers](../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md).|Für heterogene Verleger ist ein Verbindungsserver erforderlich. Ein Verbindungsserver mit dem Namen '%1!s!' ist bereits vorhanden. Entfernen Sie den Verbindungsserver, oder wählen Sie einen anderen Verlegernamen aus.|  
|MSSQL_ENG021663. Siehe [Troubleshooting Oracle Publishers](../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md).|Für die [%1!s!].[%2!s!]-Quelltabelle wurde kein gültiger Primärschlüssel gefunden.|  
|MSSQL_ENG021684. Siehe [Troubleshooting Oracle Publishers](../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md).|Der Administratoranmeldung für den '%s'-Oracle-Verleger sind unzureichende Berechtigungen zugeordnet.|  
|[MSSQL_ENG021797](../../relational-databases/replication/mssql-eng021797.md)|'%1!s!' muss eine gültige Windows-Anmeldung der folgenden Form sein: 'MACHINE\Login' oder 'DOMAIN\Login'. Lesen Sie die Dokumentation zu '%3!s!'.|  
|[MSSQL_ENG021798](../../relational-databases/replication/mssql-eng021798.md)|Der %1!s!-Agent-Auftrag muss vor dem Fortsetzen des Vorgangs über '%2!s!' hinzugefügt werden. Lesen Sie die Dokumentation zu '%3!s!'.|  
|[MSSQL_REPL020011](../../relational-databases/replication/mssql-repl020011.md)|Der Prozess konnte '%1' nicht auf '%2' ausführen.|  
|[MSSQL_REPL027056](../../relational-databases/replication/mssql-repl027056.md)|Vom Mergeprozess konnte der Generierungsverlauf auf '%1' nicht geändert werden. Führen Sie zur Problembehandlung einen Neustart der Synchronisierung mit ausführlicher Verlaufsprotokollierung aus, und geben Sie eine Ausgabedatei an, in die geschrieben werden soll.|  
|[MSSQL_REPL027183](../../relational-databases/replication/mssql-repl027183.md)|Vom Mergeprozess konnten Änderungen in Artikeln mit parametrisierten Zeilenfiltern nicht aufgezählt werden. Falls dieser Fehler weiterhin auftritt, erhöhen Sie das Abfragetimeout für diesen Prozess, reduzieren Sie die Beibehaltungsdauer für die Veröffentlichung, und verbessern Sie die Indizes für veröffentlichte Tabellen.|  
  
  
