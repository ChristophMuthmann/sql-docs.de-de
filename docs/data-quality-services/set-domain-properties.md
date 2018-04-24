---
title: Festlegen von Domäneneigenschaften | Microsoft-Dokumentation
ms.custom: ''
ms.date: 11/08/2011
ms.prod: sql-non-specified
ms.prod_service: data-quality-services
ms.service: ''
ms.component: data-quality-services
ms.reviewer: ''
ms.suite: sql
ms.technology:
- data-quality-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.dqs.dm.domainproperties.f1
ms.assetid: 8a3c88ca-31d6-4f75-9aca-cf027c6d9845
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 522b09e704b6536d5b2748dae71fd2710a664b9e
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="set-domain-properties"></a>Festlegen von Domäneneigenschaften

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  In diesem Thema wird beschrieben, wie Domäneneigenschaften in [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) festgelegt werden.  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungsmaßnahmen  
  
###  <a name="Prerequisites"></a> Erforderliche Komponenten  
 Um Eigenschaften für eine Domäne festzulegen, müssen Sie eine Wissensdatenbank und eine Domäne erstellt haben.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Sie müssen über die Rolle „dqs_kb_editor“ oder „dqs_administrator“ in der DQS_MAIN-Datenbank verfügen, um Eigenschaften für eine Domäne festzulegen.  
  
##  <a name="Set"></a> Festlegen von Domäneneigenschaften  
  
1.  Um Eigenschaften für eine vorhandene Domäne festzulegen, öffnen Sie eine Wissensdatenbank in der Domänenverwaltungsaktivität (siehe [Open a Knowledge Base](../data-quality-services/open-a-knowledge-base.md)), und wählen Sie dann die entsprechende Domäne in der Liste **Domäne** aus. In der Standardeinstellung wird die Seite „Domäneneigenschaften“ angezeigt.  
  
2.  Legen Sie Eigenschaften für eine neue Domäne fest, nachdem Sie diese wie unter [Create a Domain](../data-quality-services/create-a-domain.md)beschrieben erstellt haben.  
  
3.  Klicken Sie auf **Fertig stellen** , um die Domänenverwaltungsaktivität abzuschließen, wie in [Beenden der Domänenverwaltungsaktivität](http://msdn.microsoft.com/library/ab6505ad-3090-453b-bb01-58435e7fa7c0)beschrieben.  
  
##  <a name="FollowUp"></a> Nachverfolgung: Nach dem Festlegen von Domäneneigenschaften  
 Nachdem Sie Domäneneigenschaften festgelegt haben, können Sie andere Domänenverwaltungstasks in der Domäne ausführen, Sie können die Wissensermittlung durchführen, um der Domäne Wissen hinzuzufügen, oder Sie können der Domäne eine Abgleichsrichtlinie hinzufügen. Weitere Informationen finden Sie unter [Durchführen der Wissensermittlung](../data-quality-services/perform-knowledge-discovery.md), [Verwalten einer Domäne](../data-quality-services/managing-a-domain.md) oder [Erstellen einer Abgleichsrichtlinie](../data-quality-services/create-a-matching-policy.md).  
  
##  <a name="Properties"></a> Domäneneigenschaften  
  
###  <a name="Name"></a> Domänenname und Beschreibung  
 Nachdem eine Domäne erstellt wurde, kann der Domänenname oder die Beschreibung geändert werden. Der Domänenname muss für die Wissensdatenbank eindeutig sein. Die Beschreibung kann bis zu 256 Zeichen enthalten.  
  
###  <a name="Type"></a> Datentyp  
 Wenn Sie die Domäne erstellen, wählen Sie einen der folgenden Datentypen für die Werte in der Domäne aus: **Zeichenfolge** (Standardeinstellung), **Datum**, **Ganze Zahl**oder **Dezimal**. Nachdem Sie die Domäne erstellt haben, können Sie den Datentyp anzeigen, jedoch nicht mehr ändern. Der für eine Domäne ausgewählte Datentyp definiert den Typ von Quelldaten, die der Domäne zugeordnet werden können. Informationen zu unterstützten Datentypen für jeden der vier Domänendatentypen in DQS finden Sie unter [Supported SQL Server and SSIS Data Types for DQS Domains (Unterstützte SQL Server- und SSIS-Datentypen für DQS-Domänen)](../data-quality-services/supported-sql-server-and-ssis-data-types-for-dqs-domains.md).  
  
###  <a name="Leading"></a> Führende Werte verwenden  
 Aktivieren Sie dieses Kontrollkästchen, um anzugeben, dass der führende Wert in einer Gruppe von Synonymen statt eines Werts ausgegeben wird, der ein Synonym dafür ist. Deaktivieren Sie **Führende Werte verwenden** , um anzugeben, dass jeder Synonymwert in seinem richtigen oder korrigierten Format ausgegeben und nicht durch den führenden Wert für die zugehörige Gruppe ersetzt wird.  
  
###  <a name="Normalize"></a> Zeichenfolge normalisieren  
 Wenn der Datentyp **Zeichenfolge**angegeben ist, klicken Sie hier, um die Sonderzeichen in den Quelldaten bei der Data Quality-Verarbeitung durch DQS zu ignorieren. DQS ersetzt die Sonderzeichen intern beim Laden der Daten in die Domäne durch NULL oder ein Leerzeichen. Ein Doppelpunkt, Bindestrich, Punkt, doppeltes Anführungszeichen oder Semikolon wird durch ein Leerzeichen ersetzt. Ein einfaches Anführungszeichen wird durch NULL ersetzt. Durch Verwendung des NULL-Werts werden die beiden Teile der Zeichenfolge verbunden.  
  
 Das Ignorieren von Sonderzeichen in einem Zeichenfolgenwert kann die Abgleichgenauigkeit vergrößern. Das Ähnlichkeitsergebnis zwischen zwei Zeichenfolgen kann vergrößert werden, indem Sonderzeichen durch NULL oder ein Leerzeichen ersetzt werden. Satzzeichen oder andere Symbole können sich in zwei Zeichenfolgen unterscheiden. Durch internes Ersetzen von Sonderzeichen kann das Ergebnis den unteren Schwellenwert für die Übereinstimmung in DQS überschreiten, sodass zwei Zeichenfolgen als Übereinstimmung erkannt werden, was andernfalls nicht der Fall gewesen wäre. Ob Sie Sonderzeichen ignorieren, hängt jedoch auch von dem Datentyp ab, für den Sie den Abgleich ausführen. Wenn Sie z. B. Daten aus dem englischen Maßsystem verarbeiten, kann das Ignorieren von doppelten und einfachen Anführungszeichen in den Produktdaten Fehler verursachen, wenn ein doppeltes Anführungszeichen für Zoll oder ein einfaches Anführungszeichen für Fuß steht.  
  
 Die Normalisierung wird beim Laden und Indizieren der Daten in den Datenverarbeitungsphasen der Ermittlungs-, Abgleichsrichtlinien-, Abgleichsprojekt- und Bereinigungsprojektaktivitäten ausgeführt. Bei Aktivierung werden Normalisierung und begriffsbasierte Beziehungstransformation vor der Analyse in einer Vorverarbeitungsphase durchgeführt. Sie werden für jede Domäne ausgeführt, bevor Algorithmen zur Berechnung der Ähnlichkeit zwischen Zeichenfolgen angewendet werden. Wenn eine Verbunddomänenanalyse angefordert wird, erfolgt diese vor der Normalisierung und begriffsbasierter Beziehungstransformation, da für die Trennzeichenanalyse Symbole erforderlich sind. Andere Vorgänge, z. B. Änderung an Domänenregeln und Domänenwerten, werden nach den Transformationen ausgeführt. Die resultierenden Daten werden durch das interne Ersetzen der Sonderzeichen in DQS nicht geändert.  
  
###  <a name="Format"></a> Formatausgabe  
 Wählen Sie die Formatierung aus, die beim Ausgeben der Datenwerte in der Domäne angewendet wird. Die Formatierung ist für den ausgewählten Datentyp spezifisch, wie in der folgenden Liste gezeigt. Bei Auswahl von **Keine** wird keines der Formate in der Liste angewendet.  
  
-   Für einen Zeichenfolgenwert können Sie angeben, dass die Zeichenfolge in Großbuchstaben, in Kleinbuchstaben oder in Großschreibung ausgegeben wird.  
  
-   Für einen Datumswert können Sie das Format von Tag, Monat und Jahr angeben.  
  
-   Für einen ganzzahligen Wert können Sie den Typ der Formatmaske angeben, die angewendet werden soll.  
  
-   Für einen Dezimalwert können Sie die Genauigkeit und den Typ der Formatmaske angeben, die angewendet werden soll.  
  
###  <a name="Language"></a> Sprache  
 Wenn der Datentyp **Zeichenfolge**ist, wählen Sie die Sprache aus, mit der die Domäne für die Rechtschreibprüfung verknüpft werden soll. Diese Auswahl gilt nur für die Rechtschreibprüfung, da die Ergebnisse der Rechtschreibprüfung von der verwendeten Sprache abhängig sind. Die Auswahl gilt nur für eine einzelne Domäne mit dem Datentyp „Zeichenfolge“. Die Spracheigenschaft ist für Verbunddomänen irrelevant. Die Sprache für jeden Teil einer Verbunddomäne wird von der relevanten Einzeldomäne bestimmt.  
  
 Die Standardsprache ist Englisch. Wenn Sie die Eigenschaft **Sprache** auf **Sonstige** festlegen, wird die Rechtschreibprüfung für die Domäne deaktiviert.  
  
> [!TIP]  
>  Wenn Ihre Sprache nicht in der Dropdownliste **Sprache** aufgeführt ist, müssen Sie **Sonstige**auswählen. Dadurch wird sichergestellt, dass Duplikate für Daten in der nicht aufgeführten Sprache auf der Basis des verfügbaren Wissens (Domänenregeln, Domänenwerte, TBRs, Abgleichsregel) von DQS in der Domäne bereinigt und eliminiert werden.  
  
###  <a name="Speller"></a> Rechtschreibprüfung aktivieren  
 Wenn der Datentyp **Zeichenfolge**ist, klicken Sie hierauf, um die DQS-Rechtschreibprüfung für die Domäne zu aktivieren. Die Rechtschreibprüfung funktioniert nur in Domänen mit dem Datentyp „Zeichenfolge“. Das Kontrollkästchen **Rechtschreibprüfung aktivieren** aktiviert die Rechtschreibprüfung nur für die mit dem Kontrollkästchen verknüpfte Einzeldomäne. Das Kontrollkästchen gilt nicht für eine Verbunddomäne.  
  
 Die Rechtschreibprüfung schlägt Syntax- und Überprüfungskorrekturen für Werte in der Domäne vor. Weitere Informationen finden Sie unter [Use the DQS Speller](../data-quality-services/use-the-dqs-speller.md).  
  
###  <a name="Syntax"></a> Syntaxfehleralgorithmen deaktivieren  
 Wenn der Datentyp **Zeichenfolge**ist, wählen Sie dies aus, um anzugeben, dass DQS während der Bereinigung keine Syntaxfehler in der Domäne identifiziert. Aktivieren Sie dieses Kontrollkästchen, wenn die Identifizierung von Syntaxfehlern für diese Domäne irrelevant ist. Die Identifizierung von Syntaxfehler ist für eine Seriennummer beispielsweise unwichtig. Dieses Steuerelement ist nur für den Datentyp „Zeichenfolge“ verfügbar. DQS überprüft keine anderen Datentypen als Zeichenfolgen auf Syntaxfehler.  
  
  
