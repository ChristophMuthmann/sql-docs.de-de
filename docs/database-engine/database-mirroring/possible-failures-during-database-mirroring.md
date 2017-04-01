---
title: "M&#246;gliche Fehler w&#228;hrend der Datenbankspiegelung | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Timeoutzeitraum [SQL Server-Datenbankspiegelung]"
  - "Softwarefehler [SQL Server]"
  - "Datenbankspiegelung [SQL Server], Problembehandlung"
  - "Timeoutfehler [SQL Server]"
  - "Problembehandlung [SQL Server], Datenbankspiegelung"
  - "Hardwarefehler"
  - "Fehler bei Datenbank-Spiegelungssitzungen [SQL Server]"
ms.assetid: d7031f58-5f49-4e6d-9a62-9b420f2bb17e
caps.latest.revision: 59
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 59
---
# M&#246;gliche Fehler w&#228;hrend der Datenbankspiegelung
  Physische, betriebssystembedingte oder [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Probleme können einen Fehler während einer Datenbank-Spiegelungssitzung verursachen. Die Datenbankspiegelung überprüft Komponenten, auf denen Sqlservr.exe beruht, nicht regelmäßig, um festzustellen, ob sie ordnungsgemäß ausgeführt werden oder nicht. Bei einigen Fehlertypen meldet die betroffene Komponente der Sqlservr.exe jedoch einen Fehler. Ein von einer anderen Komponente gemeldeter Fehler wird als *schwerwiegender Fehler*bezeichnet. Um andere Fehler zu erkennen, die andernfalls unbemerkt blieben, implementiert die Datenbankspiegelung eigene Timeoutmechanismen. Beim Auftreten eines solchen Timeouts nimmt die Datenbankspiegelung an, dass ein Fehler aufgetreten ist, und generiert einen *Softwarefehler*. Einige Fehler auf der SQL Server-Instanzebene führen jedoch nicht dazu, dass bei der Spiegelung ein Timeout eintritt und die Sitzung nicht erkannt wird.  
  
> [!IMPORTANT]  
>  Fehler, die in anderen Datenbanken als der gespiegelten Datenbank auftreten, werden in einer Datenbank-Spiegelungssitzung nicht erkannt. Des Weiteren ist es unwahrscheinlich, dass ein Datenträgerfehler erkannt wird, es sei denn, die Datenbank wird aufgrund eines Datenträgerfehlers neu gestartet.  
  
 Die Geschwindigkeit der Fehlererkennung und somit die Reaktionszeit der Spiegelsitzung auf den Fehler hängen davon ab, ob es sich um einen Hardware- oder Softwarefehler handelt. Bestimmte Hardwarefehler, wie z. B. Netzwerkfehler, werden sofort gemeldet. In bestimmten Fällen kann jedoch die Meldung von Hardwarefehlern durch komponentenspezifische Timeoutzeitspannen verzögert werden. Bei Softwarefehlern bestimmt die Timeoutzeitspanne die Geschwindigkeit der Fehlererkennung. Standardmäßig sind hierfür 10 Sekunden festgelegt. Dies ist der empfohlene Mindestwert.  
  
## Fehler aufgrund von Hardwarefehlern  
 Die folgenden Bedingungen stellen u. a. mögliche Ursachen für Hardwarefehler dar:   
  
-   Eine unterbrochene Verbindung oder ein fehlerhaftes Kabel  
  
-   Eine fehlerhafte Netzwerkkarte  
  
-   Eine Änderung des Routers  
  
-   Änderungen an der Firewall  
  
-   Endpunktneukonfigurationen  
  
-   Ausfall des Laufwerks mit dem Transaktionsprotokoll  
  
-   Ein Betriebssystem- oder Prozessfehler  
  
 Wenn beispielsweise das Protokolllaufwerk in der Prinzipaldatenbank nicht mehr reagiert und ausfällt, informiert das Betriebssystem Sqlservr.exe, dass ein schwerwiegender Fehler aufgetreten ist.  
  
 Einige Komponenten, wie z. B. Netzwerkkomponenten und bestimmte E/A-Subsysteme, verfügen über eigene Timeouts zur Fehlerbestimmung. Diese Timeouts sind völlig unabhängig von der Datenbankspiegelung, und diese erhält keinerlei Informationen über deren Existenz oder Verhalten. In diesen Fällen verlängert die Timeoutzeitspanne die Verzögerung zwischen dem Auftreten eines Fehlers und dem Erhalt des daraus entstehenden Hardwarefehlers durch die Datenbankspiegelung.  
  
> [!NOTE]  
>  Die einzige Art der aktiven Fehlerüberprüfung der Datenbankspiegelung findet bei Softwarefehlern statt. Weitere Informationen finden Sie nachfolgend in diesem Thema unter "Fehler aufgrund von Softwarefehlern".  
  
 Um die im Netzwerk auftretenden Fehlerbedingungen interpretieren zu können, erkundigen Sie sich bei einem Netzwerkingenieur, welche Fehlermeldungen an einen Port gesendet werden, wenn die folgenden Ereignisse bei einer TCP-Verbindung auftreten:  
  
-   DNS (Domain Name System) ist nicht funktionsfähig.  
  
-   Die Kabel sind nicht angeschlossen.  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows verfügt über eine Firewall, die einen bestimmten Port blockiert.  
  
-   Die Anwendung, die einen Port überwacht, erzeugt einen Fehler.  
  
-   Ein Windows-Server wurde umbenannt.  
  
-   Ein Windows-Server wurde neu gestartet.  
  
> [!NOTE]  
>  Das Spiegeln bietet keinen Schutz vor Problemen im Hinblick auf den Zugriff des Clients auf die Server. Nehmen wir beispielsweise an, eine öffentliche Netzwerkkarte verwaltet Clientverbindungen zu der Prinzipalserverinstanz, während eine private Netzwerkschnittstellenkarte den Spiegelungsverkehr zwischen den Serverinstanzen verwaltet. Wenn in einem solchen Fall die öffentliche Netzwerkkarte ausfällt, können die Clients nicht mehr auf die Datenbank zugreifen, obwohl die Datenbank weiterhin gespiegelt wird.  
  
## Fehler aufgrund von Softwarefehlern  
 Die folgenden Bedingungen stellen u. a. mögliche Ursachen für Spiegelungstimeouts dar:   
  
-   Netzwerkfehler, wie z. B. Timeouts für TCP-Verbindungen, gelöschte oder beschädigte Pakete oder Pakete in falscher Reihenfolge.  
  
-   Ein nicht reagierendes Betriebssystem, ein nicht reagierender Server oder Datenbankstatus.  
  
-   Ein Windows-Servertimeout.  
  
-   Unzureichende Verarbeitungsressourcen, wie z. B. Überlastung der CPU oder des Datenträgers, volles Transaktionsprotokoll oder unzureichender Arbeitsspeicher oder nicht genügend Threads. In diesen Fällen müssen Sie den Timeoutzeitraum erhöhen, die Arbeitsauslastung reduzieren oder die Hardware an die Arbeitsauslastung anpassen.  
  
### Der Spiegelungstimeout-Mechanismus  
 Aufgrund der Tatsache, dass Softwarefehler nicht direkt von einer Serverinstanz erkannt werden, kann ein Softwarefehler potenziell dazu führen, dass eine Serverinstanz unbegrenzt wartet. Um dies zu verhindern, implementiert die Datenbankspiegelung einen eigenen Timeoutmechanismus, der darauf basiert, dass jede Serverinstanz in einer Spiegelungssitzung in regelmäßigen Intervallen einen Ping über alle offenen Verbindungen sendet.  
  
 Damit eine Verbindung offen bleibt, muss eine Serverinstanz innerhalb der definierten Timeoutzeitspanne einen Ping über diese Verbindung erhalten. Hinzu kommt die Dauer, die zum Senden eines weiteren Pings erforderlich ist. Durch den Empfang eines Pings innerhalb des Timeoutzeitraums wird angezeigt, dass die Verbindung weiterhin offen ist und dass die Serverinstanzen über diese Verbindung kommunizieren. Die Serverinstanz setzt nach dem Empfangen eines Pings die Timeoutzähler dieser Verbindung wieder zurück.  
  
 Empfängt die Verbindung innerhalb des Timeoutzeitraums keinen Pingbefehl, geht die Serverinstanz davon aus, dass bei einer Verbindung ein Timeout aufgetreten ist. Die Serverinstanz schließt die Verbindung, bei der ein Timeout aufgetreten ist, und behandelt das Timeoutereignis gemäß des Status und des Betriebsmodus der Sitzung.  
  
 Ein Timeout wird auch dann als Fehler betrachtet, wenn der andere Server ordnungsgemäß ausgeführt wird. Falls der Timeoutwert einer Sitzung für die normale Reaktionsfähigkeit eines Partners zu niedrig ist, können Fehler auftreten, die in Wirklichkeit keine sind. Ein falscher Fehler tritt auf, wenn eine Serverinstanz erfolgreich Kontakt mit einer anderen Instanz aufnimmt, deren Antwortzeit so langsam ist, dass die Pings nicht vor Ablauf der Timoutspanne eintreffen.  
  
 Bei Sitzungen im Hochleistungsmodus beträgt die Timeoutzeitspanne immer 10 Sekunden. Dies ist im Allgemeinen ausreichend, um "falsche Fehler" zu verhindern. Bei Sitzungen im Hochsicherheitsmodus beträgt die Timeoutzeitspanne standardmäßig 10 Sekunden. Dieser Wert kann jedoch auch geändert werden. Es wird empfohlen, die Timeoutzeitspanne für die Spiegelung immer auf mindestens 10 Sekunden festzulegen, um irrtümliche Fehler zu vermeiden.  
  
 **So ändern Sie den Wert der Timeoutzeitspanne (nur Hochsicherheitsmodus)**  
  
-   Verwenden Sie folgende Anweisung: [ALTER DATABASE \<Datenbank> SET PARTNER TIMEOUT \<integer>](../../t-sql/statements/alter-database-transact-sql.md).  
  
 **So zeigen Sie den aktuellen Timeoutwert an**  
  
-   Führen Sie folgende Abfrage durch: **mirroring_connection_timeout** in [sys.database_mirroring](../../relational-databases/system-catalog-views/sys-database-mirroring-transact-sql.md).  
  
## Reagieren auf Fehler  
 Ungeachtet des Fehlertyps reagiert eine Serverinstanz, die einen Fehler erkennt, abhängig von ihrer Rolle, dem Betriebsmodus der Sitzung und dem Status der anderen Verbindungen in der Sitzung. Informationen über die Abläufe beim Ausfall eines Partners finden Sie unter [Database Mirroring Operating Modes](../../database-engine/database-mirroring/database-mirroring-operating-modes.md).  
  
## Siehe auch  
 [Einschätzen der Unterbrechung des Diensts während des Rollenwechsels &#40;Datenbankspiegelung&#41;](../../database-engine/database-mirroring/estimate-the-interruption-of-service-during-role-switching-database-mirroring.md)   
 [Betriebsmodi der Datenbankspiegelung](../../database-engine/database-mirroring/database-mirroring-operating-modes.md)   
 [Rollenwechsel während einer Datenbank-Spiegelungssitzung &#40;SQL Server&#41;](../../database-engine/database-mirroring/role-switching-during-a-database-mirroring-session-sql-server.md)   
 [Datenbankspiegelung &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)  
  
  