---
title: "&#220;berpr&#252;fen replizierter Tabellen auf Unterschiede (Replikationsprogrammierung) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "TSQL"
helpviewer_keywords: 
  - "tablediff (Hilfsprogramm)"
  - "Überprüfen replizierter Tabellen"
ms.assetid: cd253a17-0c85-42b4-912c-690169ebe799
caps.latest.revision: 20
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 20
---
# &#220;berpr&#252;fen replizierter Tabellen auf Unterschiede (Replikationsprogrammierung)
  Mithilfe der Artikelüberprüfung wird ermittelt, ob veröffentlichte Daten für Tabellenartikel auf dem Verleger und dem Verteiler identisch sind. Unterschiede können auf Nichtkonvergenz hinweisen. Weitere Informationen finden Sie unter [Überprüfen von replizierten Daten](../../../relational-databases/replication/validate-replicated-data.md). Die Überprüfung gibt jedoch lediglich Auskunft darüber, ob die Daten identisch sind oder nicht. Details zu Unterschieden zwischen der Quell- und der Zieltabelle werden nicht zurückgegeben. Das Befehlszeilenhilfsprogramm **tablediff** gibt ausführliche Informationen zu den Unterschieden zwischen zwei Tabellen zurück und kann sogar ein [!INCLUDE[tsql](../../../includes/tsql-md.md)] -Skript generieren, mit dem ein Abonnement mit den Daten auf dem Verleger in Übereinstimmung gebracht werden kann.  
  
> [!NOTE]  
>  Die **Tablediff** Dienstprogramm wird nur für unterstützt [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Server.  
  
### So überprüfen Sie replizierte Tabellen mithilfe von "tablediff" auf Unterschiede  
  
1.  Führen Sie an der Eingabeaufforderung auf einem beliebigen Server in einer Replikationstopologie [tablediff Utility](../../../tools/tablediff-utility.md)aus. Geben Sie die folgenden Parameter an:  
  
    -   **-Sourceserver** - Name des Servers, auf dem die Daten ist richtig, sind in der Regel der Verleger.  
  
    -   **-Sourcedatabase** - Name der Datenbank, die die richtigen Daten enthält.  
  
    -   **-Sourcetable** - Name der Quelltabelle für den Artikel, die verglichen werden.  
  
    -   (Optional) **-Sourceschema** -schemabesitzer der Quelltabelle, wenn nicht das Standardschema.  
  
    -   (Optional) **Quellbenutzer -** und **- Sourcepassword** bei SQL Server-Authentifizierung mit dem Verleger herstellen.  
  
        > [!IMPORTANT]  
        >  Verwenden Sie nach Möglichkeit die Windows-Authentifizierung. Wenn Sie die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Authentifizierung verwenden müssen, sollten die Benutzer zur Laufzeit zur Eingabe der Sicherheitsanmeldeinformationen aufgefordert werden. Wenn Anmeldeinformationen in einer Skriptdatei gespeichert werden müssen, muss die Datei an einem sicheren Ort gespeichert werden, um unberechtigten Zugriff zu vermeiden.  
  
    -   **-Destinationserver** - Name des Servers, auf dem die Daten verglichen wird, in der Regel ein Abonnent.  
  
    -   **-Destinationdatabase** - der Name einer Datenbank, die verglichen.  
  
    -   **-Destinationtable** - Name der Tabelle, die verglichen.  
  
    -   (Optional) **-Destinationschema** -schemabesitzer der Zieltabelle, wenn nicht das Standardschema.  
  
    -   (Optional) **Zielbenutzer -** und **- destinationpassword bei** Verwendung [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Authentifizierung für die Verbindung mit dem Abonnenten.  
  
        > [!IMPORTANT]  
        >  Verwenden Sie nach Möglichkeit die Windows-Authentifizierung. Wenn Sie die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Authentifizierung verwenden müssen, sollten die Benutzer zur Laufzeit zur Eingabe der Sicherheitsanmeldeinformationen aufgefordert werden. Wenn Anmeldeinformationen in einer Skriptdatei gespeichert werden müssen, muss die Datei an einem sicheren Ort gespeichert werden, um unberechtigten Zugriff zu vermeiden.  
  
    -   (Optional) Verwendung **- C** um einen Vergleich auf Spaltenebene auszuführen.  
  
    -   (Optional) Verwendung **- Q** hierzu eine schnelle Zeile und Schema lediglich die Zeilenanzahl Vergleich.  
  
    -   (Optional) Geben Sie einen Dateinamen und Pfad für **-o** um die Ergebnisse in eine Datei auszugeben.  
  
    -   (Optional) Geben Sie eine Tabelle in der Abonnementdatenbank in die Ergebnisse für insert **-et**. Wenn die Tabelle bereits vorhanden ist, geben Sie **-dt** zuerst die Tabelle löschen.  
  
    -   (Optional) Verwendung **-f** zum Generieren einer [!INCLUDE[tsql](../../../includes/tsql-md.md)] Datei, die Daten auf dem Abonnenten zu korrigieren, sodass sie Daten auf dem Verleger übereinstimmt. Verwendung **df -** an die Anzahl der [!INCLUDE[tsql](../../../includes/tsql-md.md)] -Anweisungen in jeder Datei.  
  
    -   (Optional) Verwendung **rc -** und **-ri** um die Anzahl der Wiederholungen für einen Vorgang und das Wiederholungsintervall anzugeben.  
  
    -   (Optional) Verwendung **-strenge** strikten Schemavergleich zwischen Quell-und Zieltabelle zu erzwingen.  
  
## Siehe auch  
 [Überprüfen der Daten am Abonnenten](../../../relational-databases/replication/validate-data-at-the-subscriber.md)  
  
  