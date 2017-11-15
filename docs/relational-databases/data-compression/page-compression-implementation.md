---
title: Implementierung von Seitenkomprimierung | Microsoft-Dokumentation
ms.custom: 
ms.date: 06/30/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-data-compression
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- page compression [Database Engine]
- compression [SQL Server], page
ms.assetid: 78c83277-1dbb-4e07-95bd-47b14d2b5cd4
caps.latest.revision: "21"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: c4e9f753fdea30ad5852ec65a4c4df0c795c1fdb
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="page-compression-implementation"></a>Implementierung von Seitenkomprimierung
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  In diesem Thema wird zusammengefasst, wie [!INCLUDE[ssDE](../../includes/ssde-md.md)] Seitenkomprimierung implementiert. Diese Zusammenfassung enthält grundlegende Informationen, die Ihnen bei der Planung des Speicherplatzes helfen, den Sie für Ihre Daten benötigten.  
  
 Die Seitenkomprimierung ist für Tabellen, Tabellenpartitionen, Indizes und Indexpartitionen ähnlich. Die folgende Beschreibung der Seitenkomprimierung für eine Tabelle gilt gleichermaßen für die Seitenkomprimierung aller Objekttypen. In den folgenden Beispielen werden Zeichenfolgen komprimiert, jedoch werden dieselben Prinzipien von der Präfix- und Wörterbuchkomprimierung auch auf andere Datentypen angewendet.  
  
 Das Komprimieren der Blattebene von Tabellen und Indizes mit der Seitenkomprimierung besteht aus drei Vorgängen, die in der folgenden Reihenfolge ausgeführt werden:  
  
1.  Zeilenkomprimierung  
  
2.  Präfixkomprimierung  
  
3.  Wörterbuchkomprimierung  
  
 Wenn Sie Seitenkomprimierung verwenden, werden Seiten auf Nichtblattebene von Indizes lediglich mit der Zeilenkomprimierung komprimiert. Weitere Informationen zur Zeilenkomprimierung finden Sie unter [Row Compression Implementation](../../relational-databases/data-compression/row-compression-implementation.md).  
  
## <a name="prefix-compression"></a>Präfixkomprimierung  
 Für jede Seite, die komprimiert wird, verwendet die Präfixkomprimierung die folgenden Schritte:  
  
1.  Für jede Spalte wird ein Wert identifiziert, mit dem der Speicherplatz für die Werte in jeder Spalte verringert werden kann.  
  
2.  Es wird eine Zeile, die die Präfixwerte für jede Spalte darstellt, erstellt und in der CI-Struktur (Compression Information) gespeichert, die unmittelbar auf den Seitenkopf folgt.  
  
3.  Die wiederholten Präfixwerte in der Spalte werden von einem Verweis auf das entsprechende Präfix ersetzt. Wenn der Wert in einer Zeile nicht genau mit dem ausgewählten Präfixwert übereinstimmt, kann immer noch eine Teilübereinstimmung angezeigt werden.  
  
 Die folgende Abbildung zeigt eine Beispielseite einer Tabelle vor der Präfixkomprimierung.  
  
 ![Seite vor der Präfixkomprimierung](../../relational-databases/data-compression/media/skt-tblcompression1c.gif "Seite vor der Präfixkomprimierung")  
  
 Die folgende Abbildung zeigt dieselbe Seite nach der Präfixkomprimierung. Das Präfix wird in die Kopfzeile verschoben, und die Spaltenwerte werden in Verweise auf das Präfix geändert.  
  
 ![Seite nach der Präfixkomprimierung](../../relational-databases/data-compression/media/tblcompression2.gif "Seite nach der Präfixkomprimierung")  
  
 Der Wert 4b in der ersten Spalte der ersten Zeile zeigt an, dass die ersten vier Zeichen des Präfixes (aaab) sowie das Zeichen b für diese Zeile vorhanden sind. Daraus resultiert der Wert aaabb, welcher der ursprüngliche Wert ist.  
  
## <a name="dictionary-compression"></a>Wörterbuchkomprimierung  
 Nach dem Abschluss der Präfixkomprimierung wird die Wörterbuchkomprimierung angewendet. Die Wörterbuchkomprimierung sucht nach wiederholten Werten auf der Seite und speichert diese im CI-Bereich. Im Gegensatz zur Präfixkomprimierung ist die Wörterbuchkomprimierung nicht auf eine Spalte beschränkt. Die Wörterbuchkomprimierung kann wiederholte Werte ersetzen, die an einer beliebigen Stelle auf einer Seite auftreten. Die folgende Abbildung zeigt dieselbe Seite nach der Wörterbuchkomprimierung.  
  
 ![Seite nach der Wörterbuchkomprimierung](../../relational-databases/data-compression/media/tblcompression3.gif "Seite nach der Wörterbuchkomprimierung")  
  
 Beachten Sie, dass auf den Wert 4b von anderen Spalten der Seite verwiesen wurde.  
  
## <a name="when-page-compression-occurs"></a>Wenn Seitenkomprimierung auftritt  
 Wenn eine neue Tabelle mit Seitenkomprimierung erstellt wird, tritt keine Komprimierung auf. Die Metadaten für die Tabelle geben jedoch an, dass Seitenkomprimierung verwendet werden sollte. Wenn Sie auf der ersten Datenseite Daten hinzufügen, wird Zeilenkomprimierung auf die Daten angewendet. Da die Seite nicht voll ist, werden mit der Seitenkomprimierung keine Vorteile erzielt. Wenn die Seite voll ist, löst die nächste Zeile, die hinzugefügt wird, den Seitenkomprimierungsvorgang aus. Die gesamte Seite wird überprüft. Jede Spalte wird für die Präfixkomprimierung bewertet, und anschließend werden alle Spalten für die Wörterbuchkomprimierung bewertet. Wenn die Seitenkomprimierung auf der Seite ausreichend Platz für eine weitere Zeile geschaffen hat, wird die Zeile hinzugefügt. Auf die Daten wird Zeilen- und Seitenkomprimierung angewendet. Wenn der durch Seitenkomprimierung erzielte Platzgewinn abzüglich des für die CI-Struktur benötigten Platzes unbedeutend ist, wird für diese Seite keine Seitenkomprimierung verwendet. Wenn zukünftige Zeilen nicht mehr auf diese neue Seite passen, wird der Tabelle eine neue Seite hinzugefügt. Wie bei der ersten Seite wird auf diese neue Seite keine Seitenkomprimierung angewendet.  
  
 Wenn auf eine vorhandene Tabelle, die Daten enthält, Seitenkomprimierung angewendet wird, wird jede Seite neu erstellt und bewertet. Das Neuerstellen aller Seiten hat die Neuerstellung der Tabelle, des Indexes oder der Partition zur Folge.  
  
## <a name="see-also"></a>Siehe auch  
 [Datenkomprimierung](../../relational-databases/data-compression/data-compression.md)   
 [Row Compression Implementation](../../relational-databases/data-compression/row-compression-implementation.md)  
  
  
