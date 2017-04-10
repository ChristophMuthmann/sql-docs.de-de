---
title: "Informationen zur &#196;nderungsnachverfolgung (SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "08/08/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Datenänderungen [SQL Server]"
  - "Nachverfolgen von Datenänderungen [SQL Server]"
  - "Änderungsnachverfolgung [SQL Server], Informationen zur Änderungsnachverfolgung"
  - "Änderungsnachverfolgung [SQL Server]"
  - "Daten [SQL Server], ändern"
ms.assetid: 5e0ef05a-8317-4c98-be20-b19d4cd78f12
caps.latest.revision: 36
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 34
---
# Informationen zur &#196;nderungsnachverfolgung (SQL Server)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Die Änderungsnachverfolgung ist eine einfache Lösung, die einen effizienten Änderungsnachverfolgungsmechanismus für Anwendungen bereitstellt. Normalerweise mussten Anwendungsentwickler benutzerdefinierte Mechanismen zur Änderungsnachverfolgung implementieren, damit die Anwendungen Änderungen an Daten in einer Datenbank abfragen und auf Informationen im Zusammenhang mit den Änderungen zugreifen konnten. Die Erstellung dieser Mechanismen war i. d. R. mit hohem Arbeitsaufwand verbunden und erforderte vielfach eine Kombination von Triggern, **timestamp** -Spalten, neuen Tabellen zum Speichern von Nachverfolgungsinformationen und benutzerdefinierten Cleanupprozessen.  
  
 Die Anforderungen an die Menge erforderlicher Informationen zu den Änderungen variieren je nach Anwendungstyp. Anwendungen können die Änderungsnachverfolgung verwenden, um die folgenden Fragen zu den an einer Benutzertabelle vorgenommenen Änderungen zu beantworten:  
  
-   Welche Zeilen wurden in einer Benutzertabelle geändert?  
  
    -   Es ist nur die Tatsache von Belang, dass eine Zeile geändert wurde, nicht jedoch, wie oft die Zeile geändert wurde oder welche Werte bei Zwischenänderungen festgelegt wurden.  
  
    -   Die aktuellen Daten können direkt aus der nachverfolgten Tabelle abgerufen werden.  
  
-   Wurde eine Zeile geändert?  
  
    -   Die Tatsache, dass eine Zeile geändert wurde, und Informationen zu der Änderung müssen verfügbar sein und zum Zeitpunkt der Änderung in derselben Transaktion aufgezeichnet werden.  
  
> [!NOTE]  
>  Wenn für eine Anwendung Informationen zu allen vorgenommenen Änderungen und die Zwischenwerte der geänderten Daten erforderlich sind, ist möglicherweise eher die Verwendung von Change Data Capture anstelle der Änderungsnachverfolgung zu empfehlen. Weitere Informationen finden Sie unter [Informationen zu Change Data Capture &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-data-capture-sql-server.md).  
  
## Unidirektionale und bidirektionale Synchronisierungsanwendungen  
 Anwendungen, die Daten mit einer Instanz von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] synchronisieren müssen, müssen in der Lage sein, Änderungen abzufragen. Die Änderungsnachverfolgung kann sowohl als Grundlage für unidirektionale als auch für bidirektionale Synchronisierungsanwendungen verwendet werden.  
  
### Unidirektionale Synchronisierungsanwendungen  
 Es können unidirektionale Synchronisierungsanwendungen, z. B. ein Client oder eine Zwischenspeicherungsanwendung auf der mittleren Ebene, erstellt werden, die die Änderungsnachverfolgung verwenden. Wie in der folgenden Abbildung dargestellt, müssen für eine Zwischenspeicherungsanwendung Daten in [!INCLUDE[ssDE](../../includes/ssde-md.md)] gespeichert und in anderen Datenspeichern zwischengespeichert werden. Die Anwendung muss in der Lage sein, den Cache auf dem aktuellen Stand zu halten, indem dieser mit allen an den Datenbanktabellen vorgenommenen Änderungen aktualisiert wird. Es werden keine Änderungen zurück an [!INCLUDE[ssDE](../../includes/ssde-md.md)] übergeben.  
  
 ![Zeigt Anwendungen mit unidirektionaler Synchronisierung](../../relational-databases/track-changes/media/one-waysync.gif "Zeigt Anwendungen mit unidirektionaler Synchronisierung")  
  
### Bidirektionale Synchronisierungsanwendungen  
 Es können auch bidirektionale Synchronisierungsanwendungen erstellt werden, die die Änderungsnachverfolgung verwenden. In diesem Szenario werden die Daten in einer Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] mit mindestens einem Datenspeicher synchronisiert. Die Daten in diesen Speichern können aktualisiert werden, und die Änderungen müssen wieder mit [!INCLUDE[ssDE](../../includes/ssde-md.md)] synchronisiert werden.  
  
 ![Zeigt Anwendungen mit bidirektionaler Synchronisierung](../../relational-databases/track-changes/media/two-waysync.gif "Zeigt Anwendungen mit bidirektionaler Synchronisierung")  
  
 Ein gutes Beispiel für eine bidirektionale Synchronisierungsanwendung ist eine gelegentlich verbundene Anwendung. In einer Anwendung dieses Typs fragt eine Clientanwendung einen lokalen Speicher ab und aktualisiert diesen. Wenn eine Verbindung zwischen einem Client und einem Server verfügbar ist, führt die Anwendung die Synchronisierung mit einem Server aus, und geänderte Daten fließen in beide Richtungen.  
  
 Die bidirektionalen Synchronisierungsanwendungen müssen Konflikte erkennen können. Zu einem Konflikt kommt es, wenn in der Zeit zwischen zwei Synchronisierungen die gleichen Daten in beiden Datenspeichern geändert wurden. Wenn eine Anwendung über die Fähigkeit zum Erkennen von Konflikten verfügt, kann sichergestellt werden, dass keine Änderungen verloren werden.  
  
## Funktionsweise der Änderungsnachverfolgung  
 Zum Konfigurieren der Änderungsnachverfolgung können Sie DDL-Anweisungen oder [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] verwenden. Weitere Informationen finden Sie unter [Aktivieren und Deaktivieren der Änderungsnachverfolgung &#40;SQL Server&#41;](../../relational-databases/track-changes/enable-and-disable-change-tracking-sql-server.md). Zum Nachverfolgen von Änderungen muss die Änderungsnachverfolgung zuerst für die Datenbank und dann für die Tabellen, die in dieser Datenbank nachverfolgt werden sollen, aktiviert werden. Die Tabellendefinition muss in keiner Weise geändert werden, und es werden keine Trigger erstellt.  
  
 Nachdem die Änderungsnachverfolgung für eine Tabelle konfiguriert wurde, werden bei der Verwendung einer DML-Anweisung, die sich auf die Zeilen in der Tabelle auswirkt, Änderungsinformationen für jede geänderte Zeile aufgezeichnet. Zum Abfragen von geänderten Zeilen und Informationen zu den Änderungen können Sie [Änderungsnachverfolgungsfunktionen](../../relational-databases/system-functions/change-tracking-functions-transact-sql.md)verwenden.  
  
 Die Werte der Primärschlüsselspalte sind die einzigen Informationen aus der nachverfolgten Tabelle, die mit den Änderungsinformationen aufgezeichnet werden. Diese Werte identifizieren die Zeilen, die geändert wurden. Zum Abrufen der aktuellen Daten dieser Zeilen kann eine Anwendung die Werte der Primärschlüsselspalte verwenden, um die Quelltabelle mit der nachverfolgten Tabelle zu verknüpfen.  
  
 Informationen zu den an den einzelnen Zeilen vorgenommenen Änderungen können auch mithilfe der Änderungsnachverfolgung abgerufen werden. Dazu zählen z. B. der Typ des DML-Vorgangs, der die Änderung (Einfügung, Update oder Löschung) bewirkt hat, oder die Spalten, die im Rahmen eines Updatevorgangs geändert wurden.  
  
## Siehe auch  
 [Aktivieren und Deaktivieren der Änderungsnachverfolgung &#40;SQL Server&#41;](../../relational-databases/track-changes/enable-and-disable-change-tracking-sql-server.md)   
 [Verwenden der Änderungsnachverfolgung &#40;SQL Server&#41;](../../relational-databases/track-changes/work-with-change-tracking-sql-server.md)   
 [Verwalten der Änderungsnachverfolgung &#40;SQL Server&#41;](../../relational-databases/track-changes/manage-change-tracking-sql-server.md)   
 [Nachverfolgen von Datenänderungen &#40;SQL Server&#41;](../../relational-databases/track-changes/track-data-changes-sql-server.md)  
  
  