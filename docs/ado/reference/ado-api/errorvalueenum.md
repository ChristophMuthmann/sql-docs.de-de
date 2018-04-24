---
title: ErrorValueEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ErrorValueEnum
helpviewer_keywords:
- ErrorValueEnum enumeration [ADO]
ms.assetid: 9469ba3a-5e4f-4a10-bbb8-a51a6c9660ea
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a8a543a2e8816a23d420dd7bb007ae157d676f98
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="errorvalueenum"></a>ErrorValueEnum
Gibt den Typ des ADO-Laufzeitfehler.  
  
 Die Nummer des Fehlers in drei Formen werden aufgeführt:  
  
-   Positive Dezimalzahl – die niedrigen zwei Bytes der vollständigen Zahl im Dezimalformat. Diese Zahl wird in der standardmäßige Visual Basic Fehlermeldungsdialogfeld angezeigt. Beispiel: Laufzeitfehler "3707".  
  
-   Negative Decimal – die decimal Übersetzung der vollständigen Fehlernummer.  
  
-   Hexadezimale – die hexadezimale Darstellung der vollständigen Fehlernummer. Der Windows-Funktionscode ist in der vierten Ziffer. Ist der Einrichtungscode für ADO-Fehlernummern *ein*. Zum Beispiel: 0 x 800***ein***0E7B.  
  
> [!NOTE]
>  OLE DB-Fehler möglicherweise auf Ihre ADO-Anwendung übergeben werden. Diese können in der Regel identifiziert werden, durch ein Windows-Einrichtungscode von *4*. Beispielsweise 0 x 800***4***.  
  
|Konstante|Wert|Description|  
|--------------|-----------|-----------------|  
|**adErrBoundToCommand**|3707 -2146824581 0x800A0E7B|Kann nicht geändert werden die **ActiveConnection** Eigenschaft eine **Recordset** Objekt mit einer **Befehl** Objekt als Quelle.|  
|**adErrCannotComplete**|3732 -2146824556 0x800A0E94|Server kann den Vorgang nicht abschließen.|  
|**adErrCantChangeConnection**|3748 -2146824540 0x800A0EA4|Verbindung wurde abgelehnt. Neue Verbindung, die Sie angefordert hat, andere Eigenschaften als die bereits verwendet wird.|  
|**adErrCantChangeProvider**|3220 -2146825068 0X800A0C94|Der angegebene Anbieter unterscheidet sich von der bereits verwendet.|  
|**adErrCantConvertvalue**|3724 -2146824564 0x800A0E8C|Datenwert kann nicht für Datenüberlaufs Konflikt oder Daten konvertiert werden. Z. B. würden Konvertierung Daten abgeschnitten.|  
|**adErrCantCreate**|3725 -2146824563 0x800A0E8D|Datenwert kann nicht festgelegt oder abgerufen werden, da der Datentyp des Felds unbekannt ist, oder der Anbieter, nicht genügend Ressourcen zum Ausführen des Vorgangs musste entfernt werden.|  
|**adErrCatalogNotSet**|3747 -2146824541 0x800A0EA3|Vorgang erfordert eine gültige **ParentCatalog**.|  
|**adErrColumnNotOnThisRow**|3726 -2146824562 0x800A0E8E|Datensatz enthält dieses Feld nicht.|  
|**adErrDataConversion**|3421 -2146824867 0x800A0D5D|Anwendung verwendet einen Wert des falschen Typs für den aktuellen Vorgang.|  
|**adErrDataOverflow**|3721 -2146824567 0x800A0E89|Datenwert ist zu groß, um durch den Felddatentyp dargestellt werden.|  
|**adErrDelResOutOfScope**|3738 -2146824550 0x800A0E9A|Die URL des Objekts gelöscht werden soll, liegt außerhalb des Bereichs des aktuellen Datensatzes.|  
|**adErrDenyNotSupported**|3750-2146824538 0x800A0EA6|Anbieter unterstützt keine freigabebeschränkungen.|  
|**adErrDenyTypeNotSupported**|3751 -2146824537 0x800A0EA7|Die angeforderte Art der Einschränkung für die Freigabe unterstützt Anbieter nicht.|  
|**adErrFeatureNotAvailable**|3251 -2146825037 0x800A0CB3|Objekt oder der Anbieter kann nicht auf den angeforderten Vorgang auszuführen.|  
|**adErrFieldsUpdateFailed**|3749 -2146824539 0x800A0EA5|Fehler beim Aktualisieren der Felder. Weitere Informationen zu untersuchen der **Status** Eigenschaft der einzelnen Feldobjekte.|  
|**adErrIllegalOperation**|3219 -2146825069 0x800A0C93|Vorgang ist in diesem Kontext nicht zulässig.|  
|**adErrIntegrityViolation**|3719 -2146824569 0x800A0E87|Datenwert steht in Konflikt mit den Einschränkungen für die Integrität des Felds.|  
|**adErrInTransaction**|3246 -2146825042 0x800A0CAE|**Verbindung** -Objekt kann nicht explizit geschlossen werden, während in einer Transaktion.|  
|**adErrInvalidArgument**|3001 -2146825287 0x800A0BB9|Argumente des falschen Typs sind, sind außerhalb des zulässigen Bereichs, oder in Konflikt miteinander stehen.|  
|**adErrInvalidConnection**|3709 -2146824579 0x800A0E7D|Die Verbindung kann nicht verwendet werden, um diesen Vorgang auszuführen. Es ist entweder geschlossen oder in diesem Kontext ungültig.|  
|**adErrInvalidParamInfo**|3708 -2146824580 0x800A0E7C|**Parameter** falsch definiert ist. Inkonsistente oder unvollständige Informationen wurden bereitgestellt.|  
|**adErrInvalidTransaction**|3714 -2146824574 0x800A0E82|Die koordinierende Transaktion ist ungültig oder wurde nicht gestartet.|  
|**adErrInvalidURL**|3729 -2146824559 0x800A0E91|URL enthält ungültige Zeichen. Stellen Sie sicher, dass die URL korrekt eingegeben wurden.|  
|**adErrItemNotFound**|3265-2146825023 0x800A0CC1|Element kann nicht in der Auflistung gefunden werden, der der angeforderte Name oder Ordinalzahl entspricht.|  
|**adErrNoCurrentRecord**|3021-2146825267 0x800A0BCD|Entweder **BOF** oder **EOF** ist "true", oder der aktuelle Datensatz wurde gelöscht. Der angeforderte Vorgang ist einen aktuellen Datensatz erforderlich.|  
|**adErrNotExecuting**|3715 -2146824573 0x800A0E83|Vorgang kann während der Ausführung nicht ausgeführt werden.|  
|**adErrNotReentrant**|3710-2146824578 0x800A0E7E|Vorgang kann während der Verarbeitung des Ereignisses ausgeführt werden.|  
|**adErrObjectClosed**|3704 -2146824584 0x800A0E78|Vorgang ist nicht zulässig, wenn das Objekt geschlossen ist.|  
|**adErrObjectInCollection**|3367 -2146824921 0x800A0D27|Objekt ist bereits in der Auflistung. Kann nicht angefügt werden.|  
|**adErrObjectNotSet**|3420 -2146824868 0x800A0D5C|Objekt ist nicht mehr gültig.|  
|**adErrObjectOpen**|3705 -2146824583 0x800A0E79|Vorgang ist nicht zulässig, wenn das Objekt geöffnet ist.|  
|**adErrOpeningFile**|3002 -2146825286 0x800A0BBA|Datei konnte nicht geöffnet werden.|  
|**adErrOperationCancelled**|3712 -2146824576 0x800A0E80|Vorgang wurde vom Benutzer abgebrochen.|  
|**adErrOutOfSpace**|3734 -2146824554 0x800A0E96|Vorgang kann nicht ausgeführt werden. -Anbieter kann nicht genügend Speicherplatz verfügbar.|  
|**adErrPermissionDenied**|3720 -2146824568 0x800A0E88|Keine ausreichenden Berechtigungen wird verhindert, dass das Schreiben in das Feld.|  
|**adErrProviderFailed**|3000 -2146825288 0x800A0BB8|Anbieter den angeforderten Vorgang nicht ausgeführt werden.|  
|**adErrProviderNotFound**|3706 -2146824582 0x800A0E7A|Anbieter kann nicht gefunden werden. Es ist möglicherweise nicht ordnungsgemäß installiert.|  
|**adErrReadFile**|3003 -2146825285 0x800A0BBB|Datei konnte nicht gelesen werden.|  
|**adErrResourceExists**|3731 -2146824557 0x800A0E93|Kopiervorgang kann nicht ausgeführt werden. Objekt mit dem Namen von Ziel-URL bereits vorhanden ist. Geben Sie **AdCopyOverwrite** um das Objekt zu ersetzen.|  
|**adErrResourceLocked**|3730 -2146824558 0x800A0E92|Durch die angegebene URL dargestellte Objekt wird von einem oder mehreren Prozessen gesperrt. Warten Sie, bis der Prozess abgeschlossen ist, und wiederholen Sie den Vorgang.|  
|**adErrResourceOutOfScope**|3735 -2146824553 0x800A0E97|Quelle oder Ziel-URL ist außerhalb des Bereichs des aktuellen Datensatzes.|  
|**adErrSchemaViolation**|3722 -2146824566 0x800A0E8A|Datenwert steht in Konflikt mit dem Datentyp oder die Einschränkungen des Felds.|  
|**adErrSignMismatch**|3723 -2146824565 0x800A0E8B|Fehler bei der Konvertierung, da der Datenwert mit Vorzeichen handelte und der vom Anbieter verwendeten Datentyp des Felds kein Vorzeichen hatte.|  
|**adErrStillConnecting**|3713 -2146824575 0x800A0E81|Vorgang kann nicht ausgeführt werden, beim Herstellen einer Verbindung asynchron.|  
|**adErrStillExecuting**|3711 -2146824577 0x800A0E7F|Vorgang kann nicht ausgeführt werden, während der Ausführung asynchron.|  
|**adErrTreePermissionDenied**|3728 -2146824560 0x800A0E90|Berechtigungen sind nicht ausreichend, um die Struktur oder die Unterstruktur zuzugreifen.|  
|**adErrUnavailable**|3736 -2146824552 0x800A0E98|Der Vorgang wurde nicht abgeschlossen, und der Status ist nicht verfügbar. Das Feld darf nicht mehr verfügbar sein, oder der Vorgang wurde nicht ausgeführt.|  
|**adErrUnsafeOperation**|3716 -2146824572 0x800A0E84|Die Sicherheitseinstellungen auf diesem Computer verhindern den Zugriff auf eine Datenquelle in einer anderen Domäne.|  
|**adErrURLDoesNotExist**|3727 -2146824561 0x800A0E8F|Die Quell-URL oder das übergeordnete Element des Ziel-URL ist nicht vorhanden.|  
|**adErrURLNamedRowDoesNotExist**|3737 -2146824551 0x800A0E99|Durch diese URL benanntes Datensatz ist nicht vorhanden.|  
|**adErrVolumeNotFound**|3733 -2146824555 0x800A0E95|Das Speichergerät, die von der URL angegebene kann nicht Anbieter gefunden werden. Stellen Sie sicher, dass die URL korrekt eingegeben wurden.|  
|**adErrWriteFile**|3004 -2146825284 0x800A0BBC|Schreiben in Datei fehlgeschlagen.|  
|**adWrnSecurityDialog**|3717 -2146824571 0x800A0E85|Nur zur internen Verwendung. Darf nicht verwendet werden.|  
|**adWrnSecurityDialogHeader**|3718-2146824570 0x800A0E86|Nur zur internen Verwendung. Darf nicht verwendet werden.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC-Entsprechung  
 Paket: **com.ms.wfc.data**  
  
 Es werden nur die folgenden Teilmengen von ADO/WFC-Entsprechungen definiert.  
  
|Konstante|  
|--------------|  
|AdoEnums.ErrorValue.BOUNDTOCOMMAND|  
|AdoEnums.ErrorValue.DATACONVERSION|  
|AdoEnums.ErrorValue.FEATURENOTAVAILABLE|  
|AdoEnums.ErrorValue.ILLEGALOPERATION|  
|AdoEnums.ErrorValue.INTRANSACTION|  
|AdoEnums.ErrorValue.INVALIDARGUMENT|  
|AdoEnums.ErrorValue.INVALIDCONNECTION|  
|AdoEnums.ErrorValue.INVALIDPARAMINFO|  
|AdoEnums.ErrorValue.ITEMNOTFOUND|  
|AdoEnums.ErrorValue.NOCURRENTRECORD|  
|AdoEnums.ErrorValue.NOTEXECUTING|  
|AdoEnums.ErrorValue.NOTREENTRANT|  
|AdoEnums.ErrorValue.OBJECTCLOSED|  
|AdoEnums.ErrorValue.OBJECTINCOLLECTION|  
|AdoEnums.ErrorValue.OBJECTNOTSET|  
|AdoEnums.ErrorValue.OBJECTOPEN|  
|AdoEnums.ErrorValue.OPERATIONCANCELLED|  
|AdoEnums.ErrorValue.PROVIDERNOTFOUND|  
|AdoEnums.ErrorValue.STILLCONNECTING|  
|AdoEnums.ErrorValue.STILLEXECUTING|  
|AdoEnums.ErrorValue.UNSAFEOPERATION|  
  
## <a name="applies-to"></a>Gilt für  
 [Number-Eigenschaft (ADO)](../../../ado/reference/ado-api/number-property-ado.md)  
  
## <a name="see-also"></a>Siehe auch  
 [ADO Error Codes (ADO-Fehlercodes)](../../../ado/guide/appendixes/ado-error-codes.md)
