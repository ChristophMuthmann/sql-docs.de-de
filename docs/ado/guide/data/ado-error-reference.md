---
title: ADO-Fehlerreferenz | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- errors [ADO], number reference
- errors [ADO], ErrorValueEnum
- ErrorValueEnum enumeration [ADO]
ms.assetid: f653393e-d4b0-4c34-ad5f-2bdf56bc1305
caps.latest.revision: "4"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 202ece8496decb7ada7300cbfca79158bd7d2338
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="ado-errors"></a>ADO-Fehler
Die **ErrorValueEnum** Konstante beschreibt die ADO-Fehlerwerte. Eine vollständige Liste dieser Enumerationskonstanten, einschließlich der Werte, finden Sie unter [Anhang B: ADO-Fehler](../../../ado/guide/appendixes/appendix-b-ado-errors.md). In diesem Abschnitt werden einige der interessanteren Fehler untersuchen und erläutern einige bestimmten Situationen, in denen sie oder Lösungen zum Beheben des Problems auslösen können. Sowohl die **ErrorValueEnum** Konstante und die kurze positive Dezimalzahl aufgeführt sind.

|Number|ErrorValueEnum-Konstante|Beschreibung/mögliche Ursachen|
|------------|-----------------------------|----------------------------------|
|**3000**|**adErrProviderFailed**|Fehler beim Anbieter zum Ausführen des angeforderten Vorgangs.|
|**3001**|**adErrInvalidArgument**|Argumente des falschen Typs sind, sind außerhalb des zulässigen Bereichs, oder in Konflikt miteinander stehen. Dieser Fehler wird häufig durch einen Tippfehler in einer SQL SELECT-Anweisung verursacht. Beispielsweise kann ein falsch geschriebener Feldnamen oder Tabellenname dieser Fehler generiert. Dieser Fehler kann auch auftreten, wenn ein Feld oder eine Tabelle mit dem Namen in einer SELECT-Anweisung im Datenspeicher nicht vorhanden ist.|
|**3002**|**adErrOpeningFile**|Datei konnte nicht geöffnet werden. Ein falsch geschriebener Dateiname angegeben wurde, oder eine Datei verschoben, umbenannt oder gelöscht wurde. Das Laufwerk ist möglicherweise vorübergehend nicht verfügbar oder Netzwerkverkehr verhindern möglicherweise eine Verbindung, über ein Netzwerk.|
|**3003**|**adErrReadFile**|Datei konnte nicht gelesen werden. Der Name der Datei falsch angegeben wird, die Datei wurde möglicherweise verschoben oder gelöscht, oder die Datei ist möglicherweise beschädigt.|
|**3004**|**adErrWriteFile**|Schreiben in Datei fehlgeschlagen. Möglicherweise haben Sie eine Datei geschlossen und dann versucht, darauf zu schreiben, oder die Datei ist möglicherweise beschädigt. Wenn die Datei auf einem Netzlaufwerk befindet, können vorübergehende Netzwerkprobleme Schreiben auf einem Netzlaufwerk verhindern.|
|**3021**|**adErrNoCurrentRecord**|Entweder **BOF** oder **EOF** ist "true", oder der aktuelle Datensatz wurde gelöscht. Der angeforderte Vorgang ist einen aktuellen Datensatz erforderlich.<br /><br /> Es wurde versucht, zum Aktualisieren von Datensätzen mit **suchen** oder **Seek** Zeiger für den Datensatz auf den gewünschten Datensatz zu verschieben. Wenn der Datensatz nicht gefunden wird, **EOF** wird "true" sein. Dieser Fehler kann auch auftreten, nach einer fehlgeschlagenen **AddNew** oder **löschen** da kein aktueller Datensatz vorhanden ist, wenn diese Methoden nicht.|
|**3219**|**adErrIllegalOperation**|Vorgang ist in diesem Kontext nicht zulässig.|
|**3220**|**adErrCantChangeProvider**|Der angegebene Anbieter unterscheidet sich von einer bereits in Verwendung.|
|**3246**|**adErrInTransaction**|**Verbindung** -Objekt kann nicht explizit geschlossen werden, während in einer Transaktion. Ein **Recordset** oder **Verbindung** Objekt, das derzeit in einer Transaktion beteiligt ist, kann nicht geschlossen werden. Rufen Sie entweder **RollbackTrans** oder **CommitTrans** vor dem Schließen des Objekts.|
|**3251**|**adErrFeatureNotAvailable**|Das Objekt oder der Anbieter kann keine Ausführen des angeforderten Vorgangs. Einige Vorgänge hängen von einer bestimmten Anbieterversion ab.|
|**3265**|**adErrItemNotFound**|Element kann nicht in der Auflistung entspricht der angeforderte Name oder Ordinalzahl gefunden werden. Ein falscher Feld oder die Tabelle Name wurde angegeben.|
|**3367**|**adErrObjectInCollection**|Objekt ist bereits in der Auflistung. Kann nicht angefügt werden. Ein Objekt kann nicht zweimal dieselbe Sammlung hinzugefügt werden.|
|**3420**|**adErrObjectNotSet**|Objekt ist nicht mehr gültig.|
|**3421**|**adErrDataConversion**|Anwendung verwendet einen Wert des falschen Typs für den aktuellen Vorgang. Sie können eine Zeichenfolge, die einen Vorgang angegeben sein, die einen Stream, z. B. erwartet.|
|**3704**|**adErrObjectClosed**|Vorgang ist nicht zulässig, wenn das Objekt geschlossen ist. Die **Verbindung** oder **Recordset** wurde geschlossen. Beispielsweise kann eine andere Routine ein globales Objekt geschlossen haben. Sie können diesen Fehler verhindern, indem Sie überprüfen die **Zustand** Eigenschaft, bevor Sie einen Vorgang ausführen.|
|**3705**|**adErrObjectOpen**|Vorgang ist nicht zulässig, wenn das Objekt geöffnet ist. Ein Objekt, das geöffnet ist, kann nicht geöffnet werden. Felder kann nicht angefügt werden, um ein offenes **Recordset**.|
|**3706**|**adErrProviderNotFound**|Anbieter kann nicht gefunden werden. Es ist möglicherweise nicht ordnungsgemäß installiert.<br /><br /> Der Name des Anbieters ist möglicherweise falsch angegeben, der angegebene Anbieter möglicherweise nicht installiert werden, auf dem Computer, auf dem Ihr Code ausgeführt wird, oder die Installation ist möglicherweise beschädigt.|
|**3707**|**adErrBoundToCommand**|Die **ActiveConnection** Eigenschaft eine **Recordset** -Objekt, das verfügt über eine **Befehl** als Updatequelle Objekt, kann nicht geändert werden. Die Anwendung versucht, ein neues zugewiesen **Verbindung** -Objekt an eine **Recordset** , besitzt eine **Befehl** Objekt als Quelle.|
|**3708**|**adErrInvalidParamInfo**|**Parameter** Objekt wurde nicht ordnungsgemäß definiert. Inkonsistente oder unvollständige Informationen wurden bereitgestellt.|
|**3709**|**adErrInvalidConnection**|Die Verbindung kann nicht verwendet werden, um diesen Vorgang auszuführen. Es ist entweder geschlossen oder in diesem Kontext ungültig.|
|**3710**|**adErrNotReentrant**|Vorgang kann während der Verarbeitung des Ereignisses ausgeführt werden. Ein Vorgang kann nicht in einem Ereignishandler ausgeführt werden, die bewirkt, dass das Ereignis erneut ausgelöst. Beispielsweise Navigationsmethoden nicht aufgerufen werden innerhalb einer **WillMove** -Ereignishandler.|
|**3711**|**adErrStillExecuting**|Vorgang kann nicht ausgeführt werden, während der Ausführung asynchron.|
|**3712**|**adErrOperationCancelled**|Vorgang wurde vom Benutzer abgebrochen. Die Anwendung aufgerufen hat die **CancelUpdate** oder **CancelBatch** -Methode und der aktuelle Vorgang wurde abgebrochen.|
|**3713**|**adErrStillConnecting**|Vorgang kann nicht ausgeführt werden, beim Herstellen einer Verbindung asynchron.|
|**3714**|**adErrInvalidTransaction**|Die koordinierende Transaktion ist ungültig oder wurde nicht gestartet.|
|**3715**|**adErrNotExecuting**|Vorgang kann während der Ausführung nicht ausgeführt werden.|
|**3716**|**adErrUnsafeOperation**|Die Sicherheitseinstellungen dieses Computers lassen den Zugriff auf eine Datenquelle in einer anderen Domäne.|
|**3717**|**adWrnSecurityDialog**|Nur zur internen Verwendung. Verwenden Sie keine. (Der Eintrag ist der Vollständigkeit halber enthalten. Dieser Fehler sollte nicht in Ihrem Code angezeigt werden.)|
|**3718**|**adWrnSecurityDialogHeader**|Nur zur internen Verwendung. Verwenden Sie keine. (Eintrag der Vollständigkeit halber enthalten. Dieser Fehler sollte nicht in Ihrem Code angezeigt werden.)|
|**3719**|**adErrIntegrityViolation**|Datenwert steht in Konflikt mit den Einschränkungen für die Integrität des Felds. Einen neuen Wert für eine **Feld** würde dazu führen, dass einen doppelten Schlüssel. Ein Wert, der 1-Seite einer Beziehung zwischen zwei Datensätzen forms kann nicht aktualisiert werden.|
|**3720**|**adErrPermissionDenied**|Keine ausreichenden Berechtigungen wird verhindert, dass das Schreiben in das Feld. Der Benutzer mit dem Namen in der Verbindungszeichenfolge verfügt nicht über die erforderlichen Berechtigungen zum Schreiben in eine **Feld**.|
|**3721**|**adErrDataOverflow**|Datenwert ist zu groß, um durch den Felddatentyp dargestellt werden. Ein numerischer Wert, der zu groß für das vorgesehene Feld zugewiesen wurde. Ein long Integer-Wert wurde z. B. ein Feld kurze ganze Zahl zugewiesen.|
|**3722**|**adErrSchemaViolation**|Datenwert steht in Konflikt mit dem Datentyp oder die Einschränkungen des Felds. Der Datenspeicher verfügt, die von abweichen validierungseinschränkungen der **Feld** Wert.|
|**3723**|**adErrSignMismatch**|Fehler bei der Konvertierung, da der Datenwert mit Vorzeichen handelte und der vom Anbieter verwendeten Datentyp des Felds kein Vorzeichen hatte.|
|**3724**|**adErrCantConvertvalue**|Datenwert kann nicht für Datenüberlaufs Konflikt oder Daten konvertiert werden. Z. B. würden Konvertierung Daten abgeschnitten.|
|**3725**|**adErrCantCreate**|Datenwert kann nicht festgelegt oder abgerufen werden, da der Datentyp des Felds unbekannt ist, oder der Anbieter, nicht genügend Ressourcen zum Ausführen des Vorgangs musste entfernt werden.|
|**3726**|**adErrColumnNotOnThisRow**|Datensatz enthält dieses Feld nicht. Ein ungültiger Feldname angegeben wurde oder ein Feld nicht in der **Felder** auf die Auflistung des aktuellen Datensatzes verwiesen wurde.|
|**3727**|**adErrURLDoesNotExist**|Die Quell-URL oder das übergeordnete Element des Ziel-URL ist nicht vorhanden. Die Quelle oder das Ziel-URL entsteht ein Rechtschreibfehler. Sie müssen möglicherweise `http://mysite/photo/myphoto.jpg` Wenn sollten Sie tatsächlich haben `http://mysite/photos/myphoto.jpg` stattdessen. Der Tippfehler in der übergeordneten URL (in diesem Fall *Foto* anstelle von *Fotos*) hat den Fehler verursacht hat.|
|**3728**|**adErrTreePermissionDenied**|Berechtigungen sind nicht ausreichend, um die Struktur oder die Unterstruktur zuzugreifen. Der Benutzer mit dem Namen in der Verbindungszeichenfolge besitzt nicht die erforderlichen Berechtigungen.|
|**3729**|**adErrInvalidURL**|URL enthält ungültige Zeichen. Stellen Sie sicher, dass die URL richtig eingegeben wurde. Die URL folgt das Schema für den aktuellen Anbieter registriert (werden z. B. Internet Publishing-Anbieter registriert für http).|
|**3730**|**adErrResourceLocked**|Durch die angegebene URL dargestellte Objekt wird von einem oder mehreren Prozessen gesperrt. Warten Sie, bis der Prozess abgeschlossen ist, und wiederholen Sie den Vorgang. Das Objekt, das Sie zugreifen möchten wurde von einem anderen Benutzer oder von einem anderen Prozess in der Anwendung gesperrt. Dies liegt wahrscheinlich in einer Umgebung mit mehreren Benutzern auftreten können.|
|**3731**|**adErrResourceExists**|Kopiervorgang kann nicht ausgeführt werden. Objekt mit dem Namen von Ziel-URL bereits vorhanden ist. Geben Sie **AdCopyOverwrite** um das Objekt zu ersetzen. Wenn Sie keinen angeben **AdCopyOverwrite** beim Kopieren von Dateien in einem Verzeichnis, von der Kopiervorgang schlägt fehl, wenn Sie versuchen, ein Element zu kopieren, die bereits am Ziel vorhanden ist.|
|**3732**|**adErrCannotComplete**|Der Server kann nicht der Vorgang abgeschlossen. Dies kann daran liegen der Server mit anderen Vorgängen ausgelastet ist oder es möglicherweise nicht genügend Ressourcen.|
|**3733**|**adErrVolumeNotFound**|Das Speichergerät, die von der URL angegebene kann nicht Anbieter gefunden werden. Stellen Sie sicher, dass die URL richtig eingegeben wurde. Die URL des Speichergeräts ist möglicherweise falsch, aber dieser Fehler kann aus anderen Gründen auftreten. Das Gerät ist möglicherweise offline, oder eine große Menge des Netzwerkverkehrs möglicherweise verhindern, dass die Verbindung hergestellt wird.|
|**3734**|**adErrOutOfSpace**|Vorgang kann nicht ausgeführt werden. -Anbieter kann nicht genügend Speicherplatz verfügbar. Es ist möglicherweise nicht genügend Arbeitsspeicher oder Festplattenspeicherplatz für temporäre Dateien auf dem Server.|
|**3735**|**adErrResourceOutOfScope**|Quelle oder Ziel-URL ist außerhalb des Bereichs des aktuellen Datensatzes.|
|**3736**|**adErrUnavailable**|Vorgang konnte nicht abgeschlossen, und der Status ist nicht verfügbar. Das Feld darf nicht mehr verfügbar sein, oder der Vorgang wurde nicht ausgeführt. Ein anderer Benutzer möglicherweise geändert oder gelöscht des Felds, das Sie zugreifen möchten.|
|**3737**|**adErrURLNamedRowDoesNotExist**|Durch diese URL benanntes Datensatz ist nicht vorhanden. Beim Öffnen einer Datei mit einem **Datensatz** Objekt der Dateiname oder der Pfad zur Datei falsch geschrieben wurde.|
|**3738**|**adErrDelResOutOfScope**|Die URL des Objekts gelöscht werden soll, ist außerhalb des Bereichs des aktuellen Datensatzes.|
|**3747**|**adErrCatalogNotSet**|Vorgang erfordert eine gültige **ParentCatalog**.|
|**3748**|**adErrCantChangeConnection**|Verbindung wurde abgelehnt. Die neue Verbindung, die Sie angefordert hat verschiedene Merkmale demjenigen, der bereits in Verwendung.|
|**3749**|**adErrFieldsUpdateFailed**|Fehler beim Aktualisieren der Felder. Um weitere Informationen zu erhalten, überprüfen Sie die **Status** Eigenschaft der einzelnen Feldobjekte. Dieser Fehler kann in zwei Situationen auftreten: beim Ändern einer **Feld** Objektwerts gerade ändern oder Hinzufügen eines Datensatzes in der Datenbank und beim Ändern der Eigenschaften der **Feld** Objekt selbst.<br /><br /> Die **Datensatz** oder **Recordset** Updatefehler aufgrund eines Problems mit einem der Felder im aktuellen Datensatz. Auflisten der **Felder** Auflistung und Überprüfen der **Status** Eigenschaft vom jeweiligen Feld können Sie die Ursache des Problems zu ermitteln.|
|**3750**|**adErrDenyNotSupported**|Anbieter unterstützt keine freigabebeschränkungen. Es wurde versucht, die Dateifreigabe einzuschränken, und Ihr Anbieter unterstützt nicht das Konzept.|
|**3751**|**adErrDenyTypeNotSupported**|Die angeforderte Art der Einschränkung für die Freigabe unterstützt Anbieter nicht. Es wurde versucht, eine bestimmte Art von der Dateifreigabe herstellen Einschränkung, die von Ihrem Anbieter nicht unterstützt wird. Finden Sie die Dokumentation des Anbieters, um zu bestimmen, welche Einschränkungen Dateifreigabe unterstützt werden.|
