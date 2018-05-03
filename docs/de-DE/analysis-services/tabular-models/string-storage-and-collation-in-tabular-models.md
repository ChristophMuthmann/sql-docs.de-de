---
title: Zeichenfolgenspeicher und-Sortierung in tabellenmodellen | Microsoft Docs
ms.custom: ''
ms.date: 02/21/2018
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 8516f0ad-32ee-4688-a304-e705143642ca
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: f61c3effcc3e892e39a239485b2d9781fbd30577
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="string-storage-and-collation-in-tabular-models"></a>Zeichenfolgenspeicher und-Sortierung in tabellenmodellen
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Zeichenfolgen (Textwerte) werden in einem stark komprimierten Format in Tabellenmodellen gespeichert. Aufgrund dieser Komprimierung erhalten Sie unter Umständen unerwartete Ergebnisse, wenn Sie vollständige Zeichenfolgen oder Teilzeichenfolgen abrufen. Da das Zeichenfolgengebietsschema und die Sortierungen hierarchisch vom nächsten übergeordneten Objekt geerbt werden, wenn die Zeichenfolgensprache nicht explizit definiert wird, können das Gebietsschema und die Sortierung des übergeordneten Objekts beeinflussen, wie die einzelnen Zeichenfolgen gespeichert werden, und ob die Zeichenfolge entsprechend der übergeordneten Sortierung eindeutig ist oder mit ähnlichen Zeichenfolgen zusammengefügt wurde.  
  
 Dieser Artikel beschreibt den Mechanismus, mit dem Zeichenfolgen komprimiert und gespeichert werden, und enthält Beispiele dazu, wie Sortierung und Sprache die Ergebnisse von Textformeln in tabellenmodellen beeinflussen.  
  
## <a name="storage"></a>Speicherung  
 In Tabellenmodellen werden alle Daten stark komprimiert, um eine zu hohe Auslastung des Arbeitsspeichers zu vermeiden. Infolgedessen werden alle Zeichenfolgen, die als lexikalisch äquivalent eingestuft werden können, nur einmal gespeichert. Die erste Instanz der Zeichenfolge wird als kanonische Darstellung verwendet, und anschließend wird jede entsprechende Zeichenfolge im gleichen komprimierten Wert wie das erste Vorkommen indiziert.  
  
 Die Hauptfrage lautet folgendermaßen: Woraus besteht eine lexikalisch äquivalente Zeichenfolge? Zwei Zeichenfolgen werden als lexikalisch äquivalent eingestuft, wenn sie als das gleiche Wort gelten. Wenn Sie zum Beispiel in einem englischen Wörterbuch den Begriff **violin** (Geige) suchen, finden Sie möglicherweise den Eintrag **Violin** oder **violin**, abhängig von den redaktionellen Richtlinien, die für das Wörterbuch gelten, doch im Allgemeinen werden beide Begriffe als identisch bzw. äquivalent betrachtet, und die unterschiedliche Schreibweise mit kleinem bzw. großem Anfangsbuchstaben wird ignoriert. In einem Tabellenmodell ist der entscheidende Faktor, durch den bestimmt wird, ob zwei Zeichenfolgen lexikalisch äquivalent sind, nicht die redaktionelle Richtlinie oder die Benutzereinstellung, sondern das Gebietsschema und die Sortierreihenfolge, die der Spalte zugewiesen sind.  
  
 Daher sollte die Entscheidung, ob Groß- und Kleinschreibung als identisch oder verschieden behandelt werden sollen, von der Sortierung und dem Gebietsschema abhängen. Für ein bestimmtes Wort innerhalb des Gebietsschemas dient das erste Vorkommen des Wortes, das in einer bestimmten Spalte enthalten ist, daher als kanonische Darstellung des Begriffs, und die Zeichenfolge wird in einem nicht komprimiertem Format gespeichert.  Alle anderen Zeichenfolgen werden anhand des ersten Vorkommens getestet, und wenn sie dem Äquivalenztest entsprechen, werden sie dem komprimierten Wert des ersten Vorkommens zugewiesen. Wenn die komprimierten Werte später abgerufen werden, werden sie mit dem nicht komprimierten Wert des ersten Vorkommens der Zeichenfolge dargestellt.  
  
 Ein Beispiel veranschaulicht dieses Verfahren. Die folgende Spalte "Klassifizierung - Englisch" wurde einer Tabelle entnommen, die Informationen zu Pflanzen und Bäumen enthält. Für jede Pflanze (die Namen der Pflanzen werden hier nicht angezeigt) wird in der Klassifizierungsspalte die allgemeine Kategorie der Pflanze angegeben.  
  
|Klassifizierung - Englisch|  
|-------------------------------|  
|trEE|  
|PlAnT|  
|trEE|  
|PlAnT|  
|PlAnT|  
|trEE|  
|PlAnT|  
|trEE|  
|trEE|  
|PlAnT|  
|trEE|  
  
 Möglicherweise stammten die Daten aus zahlreichen verschiedenen Quellen, sodass die Schreibweise und die Verwendung von Akzenten inkonsistent war und die Unterschiede unverändert in der relationalen Datenbank gespeichert wurden. Im Allgemeinen sind die Werte jedoch entweder **Plant** oder **Tree**, wobei sich nur die Schreibweise (groß/klein) unterscheidet.  
  
 Wenn diese Werte in ein Tabellenmodell geladen werden, das die Standardsortierung und die Sortierreihenfolge für amerikanisches Englisch verwendet, ist die Schreibweise nicht von Bedeutung. Dementsprechend würden für die gesamte Spalte nur zwei Werte gespeichert werden:  
  
|Klassifizierung - Englisch|  
|-------------------------------|  
|trEE|  
|PlAnT|  
  
 Wenn Sie im Modell die Spalte **Klassifizierung - Englisch**verwenden, werden beim Anzeigen der Pflanzenklassifizierung nicht die ursprünglichen Werte mit ihren diversen unterschiedlichen Schreibweisen angezeigt, sondern es erscheint lediglich das erste Vorkommen. Der Grund hierfür ist, dass alle Groß- und Kleinschreibungsvarianten von **tree** in dieser Sortierung und diesem Gebietsschema als äquivalent betrachtet werden. Daher wurde nur eine Zeichenfolge beibehalten, und die erste Instanz der Zeichenfolge, die vom System gefunden wird, wird gespeichert.  
  
> [!WARNING]  
>  Möglicherweise möchten Sie festlegen, welche Zeichenfolge als erste gespeichert werden soll (unter Berücksichtigung der von Ihnen als korrekt eingestuften Schreibweise), doch dies kann sich als sehr schwierig erweisen. Es existiert keine einfache Möglichkeit, im Voraus zu bestimmen, welche Zeile zuerst vom Modul verarbeitet werden soll, vorausgesetzt, dass alle Werte als identisch eingestuft werden. Stattdessen sollten beim Festlegen des Standardwerts alle Zeichenfolgen bereinigt werden, bevor das Modell geladen wird.  
  
## <a name="locale-and-collation-order"></a>Gebietsschema und die Sortierreihenfolge  
 Wenn Zeichenfolgen (Textwerte) miteinander verglichen werden, wird Äquivalenz normalerweise durch den kulturellen Aspekt bestimmt, der die Interpretation solcher Zeichenfolgen beeinflusst. In einigen Kulturen kann sich die Bedeutung einer Zeichenfolge durch einen Akzent oder die Großschreibung eines Zeichens vollständig ändern. Daher werden solche Unterschiede in der Regel berücksichtigt, wenn sie Äquivalenz für eine bestimmte Sprache oder einen Bereich festlegen.  
  
 Wenn Sie Ihren Computer verwenden, ist er normalerweise bereits entsprechend Ihren eigenen kulturellen Erwartungen und dem linguistischen Verhalten konfiguriert, und Zeichenfolgenoperationen wie das Sortieren und Vergleichen von Textwerten verhalten sich erwartungsgemäß. Die Einstellungen, die sprachspezifisches Verhalten steuern, werden durch die **Gebietsschema- und Regionseinstellungen** in Windows definiert. Anwendungen lesen diese Einstellungen und ändern deren Verhalten entsprechend. In einigen Fällen verfügt eine Anwendung möglicherweise über eine Funktion, die Ihnen das Ändern des kulturellen Verhaltens der Anwendung oder der Methode zum Zeichenfolgenvergleich ermöglicht.  
  
 Wenn Sie eine Tabellenmodelldatenbank erstellen, erbt die Datenbank standardmäßig diese kulturellen und linguistischen Einstellungen im Formular einer Sprachen-ID und -sortierung.  
  
-   Die Sprachen-ID definiert den Zeichensatz, den Sie entsprechend der Kultur für die Zeichenfolgen verwenden möchten.  
  
-   Die Sortierung definiert die Reihenfolge der Zeichen und ihrer Äquivalenz.  
  
 Wichtig: Eine Sprachen-ID kennzeichnet nicht nur eine Sprache, sondern auch das Land oder die Region, in dem bzw. der die Sprache verwendet wird. Jede Sprachen-ID weist auch eine Standardsortierungsspezifikation auf. Weitere Informationen zu Sprachen-IDs finden Sie unter [Von Microsoft zugewiesene Gebietsschemabezeichner (LCIDs)](http://msdn.microsoft.com/goglobal/bb964664.aspx). Sie können die LCID DEC-Spalte verwenden, um die richtige ID zu erhalten, wenn Sie einen Wert manuell einfügen. Weitere Informationen zum SQL-Konzept von Sortierungen finden Sie unter [COLLATE &#40;Transact-SQL&#41;](../../t-sql/statements/collations.md). Informationen zu den Sortierungskennzeichnern und den Vergleichsstilen für Windows-Sortierungsnamen finden Sie unter [Name der Windows-Sortierung &#40;Transact-SQL&#41;](../../t-sql/statements/windows-collation-name-transact-sql.md). Das Thema [SQL Server-Sortierungsname &#40;Transact-SQL&#41;](../../t-sql/statements/sql-server-collation-name-transact-sql.md) ordnet die Namen der Windows-Sortierung den für SQL verwendeten Namen zu.  
  
 Sobald die Tabellenmodelldatenbank erstellt wurde, erben alle neuen Objekte im Modell die Sprach- und Sortierattribute von den Datenbankattributen. Dies gilt für alle Objekte. Der Vererbungspfad beginnt beim Objekt und sucht das übergeordnete Element für jedes zu erbende Sprach- und Sortierattribut. Wenn keine Attribute gefunden werden, wird der Vorgang am Anfang fortgesetzt, und die Sprach- und Sortierattribute werden auf der Datenbankebene gesucht. Anders ausgedrückt: Wenn Sie keine Sprach-und Sortierattribute für ein Objekt angeben, erbt das Objekt standardmäßig die Attribute des nächsten übergeordneten Elements.  
  
 Für Spalten werden die Sprach-und Sortierattribute bei der Erstellung gemäß den folgenden Regeln geerbt:  
  
1.  Das übergeordnete Dimensionsobjekt wird nach Sprach- und Sortierattributen durchsucht. Wenn beide Werte vorhanden sind, werden sie in die Spaltenattribute kopiert. Wenn nur ein Wert vorhanden ist, wird der andere Wert vom vorhandenen Wert abgeleitet, und beide Werte werden. zugewiesen Falls kein Wert vorhanden ist, fahren Sie mit dem nächsten Schritt fort.  
  
2.  Das Datenbankobjekt wird mit der gleichen Methode durchsucht, die in Schritt 1 für Dimensionen beschrieben wurde. Wenn keine Attribute gefunden werden, fahren Sie mit dem nächsten Schritt fort.  
  
3.  Das Serverobjekt wird mit der gleichen Methode durchsucht, die in Schritt 1 für Dimensionen beschrieben wurde. Wenn keine Attribute gefunden werden, wird in der Spalte die Windows-Sprachen-ID verwendet, und das Sortierattribut wird von diesem Wert abgeleitet.  
  
 Wichtig: Normalerweise haben die Sprachen-ID und die Sortierreihenfolge in der Quelldatenbank nur wenige oder gar keine Auswirkungen auf die Speicherung von Werten in der Tabellenmodellspalte. Eine Ausnahme liegt vor, wenn die Quelldatenbank die angeforderten Werte transformiert oder filtert.  
  
  
