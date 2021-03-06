---
title: Aggregatfunktion (Berichts-Generator und SSRS) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 16ce643f-bbb3-40a5-ba78-7aed73156f3e
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 2adafc32be75ff6386d3a892b6a8d253274820d9
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/02/2018
ms.locfileid: "48109750"
---
# <a name="aggregate-function-report-builder-and-ssrs"></a>Aggregatfunktion (Berichts-Generator und SSRS)
  Gibt ein benutzerdefiniertes Aggregat des angegebenen Ausdrucks gemäß der Definition durch den Datenanbieter zurück.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Aggregate(expression, scope)  
```  
  
#### <a name="parameters"></a>Parameter  
 *expression*  
 Der Ausdruck, für den die Aggregation auszuführen ist. Der Ausdruck muss aus einem einfachen Feldverweis bestehen.  
  
 *Bereich*  
 (`String`) Der Name eines Datasets, einer Gruppe oder eines Bereichs mit den Berichtselementen, auf die die Aggregatfunktion anzuwenden. *Bereich* muss eine Zeichenfolgenkonstante sein und darf kein Ausdruck sein. Wenn *scope* nicht angegeben ist, wird der aktuelle Bereich verwendet.  
  
## <a name="return-type"></a>Rückgabetyp  
 Wird durch den Datenanbieter bestimmt. Gibt `Nothing` Falls der Datenanbieter diese Funktion nicht unterstützt oder Daten nicht verfügbar sind.  
  
## <a name="remarks"></a>Hinweise  
 Die `Aggregate`-Funktion bietet die Möglichkeit, Aggregate zu verwenden, die auf der externen Datenquelle berechnet werden. Die Unterstützung dieser Funktion hängt von der Datenerweiterung ab. Beispielsweise ruft die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenverarbeitungserweiterung vereinfachte Rowsets von einer MDX-Abfrage ab. Einige Zeilen im Resultset können auf dem Datenquellenserver berechnete Aggregatwerte enthalten. Diese Werte werden als *Serveraggregate*bezeichnet. Zum Anzeigen von Serveraggregaten im grafischen Abfrage-Designer für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]klicken Sie in der Symbolleiste auf die Schaltfläche **Aggregat anzeigen** . Weitere Informationen finden Sie unter [Benutzeroberfläche des MDX-Abfrage-Designers für Analysis Services (Berichts-Generator)](../analysis-services-mdx-query-designer-user-interface-report-builder.md).  
  
 Beim Anzeigen der Kombination aus Aggregat- und Detaildatasetwerten in Detailzeilen eines Tablix-Datenbereichs werden Serveraggregate in der Regel nicht einbezogen, da es sich nicht um Detaildaten handelt. Sie können jedoch alle für das Dataset abgerufenen Werte anzeigen und die Art der Berechnung und Anzeige für die Aggregatdaten anpassen.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] erkennt die Verwendung der der `Aggregate` -Funktion in Ausdrücken Ihres Berichts, um zu bestimmen, ob Serveraggregate in Detailzeilen angezeigt. Wenn Sie einschließen `Aggregate` in einem Ausdruck in einem Datenbereich können Serveraggregate nur in Ergebniszeilen für Gruppen oder gesamtergebniszeilen, nicht in Detailzeilen erscheinen. Wenn Sie Serveraggregate in Detailzeilen anzeigen möchten, verwenden Sie die `Aggregate`-Funktion nicht.  
  
 Sie können dieses Standardverhalten ändern, indem Sie den Wert der Option **Teilergebnisse als Detailzeilen interpretieren** des Dialogfelds **Dataseteigenschaften** ändern. Wenn diese Option auf `True` festgelegt wird, werden alle Daten, einschließlich der Serveraggregate, als Detaildaten angezeigt. Ist die Option auf `False` festgelegt, werden Serveraggregate als Gesamtbeträge angezeigt. Die Einstellung für diese Eigenschaft beeinflusst alle Datenbereiche, die mit diesem Dataset verknüpft sind.  
  
> [!NOTE]  
>  Die Gruppenausdrücke aller Gruppen, die das Berichtselement enthalten, das auf `Aggregate` verweist, müssen aus einfachen Feldverweisen bestehen, z. B. `[FieldName]`. Sie können keine `Aggregate` in einem Datenbereich, der komplexe Gruppenausdrücke verwendet. Für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -datenverarbeitungserweiterung muss Ihre Abfrage MDX-Felder des Typs enthalten `LevelProperty` (nicht `MemberProperty`) zur Aggregation mit Unterstützung der `Aggregate`Funktion.  
  
 Das*Expression* -Objekt kann Aufrufe von geschachtelten Aggregatfunktionen enthalten. Dabei gelten folgende Ausnahmen und Bedingungen:  
  
-   Das*Scope* -Objekt für geschachtelte Aggregate muss dem Bereich des äußeren Aggregats entsprechen oder darin enthalten sein. In allen eindeutigen Bereichen des Ausdrucks muss ein Bereich eine untergeordnete Beziehung zu allen anderen Bereichen haben.  
  
-   Das*Scope* -Objekt für geschachtelte Aggregate darf nicht der Name eines Datasets sein.  
  
-   *Ausdruck* darf keinen `First`, `Last`, `Previous`, oder `RunningValue` Funktionen.  
  
-   Das*Expression* -Objekt darf keine geschachtelten Aggregate enthalten, die ein *recursive*-Objekt angeben.  
  
 Weitere Informationen finden Sie in der [Aggregatfunktionsreferenz (Berichts-Generator und SSRS)](report-builder-functions-aggregate-functions-reference.md) und unter [Ausdrucksbereich für Gesamtwerte, Aggregate und integrierte Auflistungen (Berichts-Generator und SSRS)](expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
 Weitere Informationen zu rekursiven Aggregaten finden Sie unter [Creating Recursive Hierarchy Groups (Report Builder and SSRS) (Erstellen von rekursiven Hierarchiegruppen (Berichts-Generator und SSRS))](creating-recursive-hierarchy-groups-report-builder-and-ssrs.md).  
  
## <a name="comparing-the-aggregate-and-sum-functions"></a>Vergleichen der Aggregate-Funktion und der Sum-Funktion  
 Die `Aggregate` Funktion unterscheidet sich von numerischen Aggregatfunktionen wie `Sum` darin, dass die `Aggregate` Funktionsergebnis ist einen Wert, der von der datenerweiterung für Datenanbieter oder datenverarbeitungserweiterung berechnet wird. Numerische Aggregatfunktionen wie `Sum` Rückgabewert, der vom Berichtsprozessor auf einem Satz von Daten aus dem Dataset, die vom bestimmt berechnet wird die *Bereich* Parameter. Weitere Informationen finden Sie in den im Thema [Aggregatfunktionsreferenz (Berichts-Generator und SSRS)](report-builder-functions-aggregate-functions-reference.md) aufgelisteten Aggregatfunktionen.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Codebeispiel wird ein Ausdruck veranschaulicht, der ein Serveraggregat für das Feld `LineTotal`abruft. Der Ausdruck wird einer Zelle in einer Zeile, die zur Gruppe `GroupbyOrder`gehört, hinzugefügt.  
  
```  
=Aggregate(Fields!LineTotal.Value, "GroupbyOrder")  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Ausdrucksverwendungen in Berichten &#40;Berichts-Generator und SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Beispiele für Ausdrücke &#40;Berichts-Generator und SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [Datentypen in Ausdrücken (Berichts-Generator und SSRS)](expressions-report-builder-and-ssrs.md)   
 [Ausdrucksbereich für Gesamtwerte, Aggregate und integrierte Auflistungen &#40;Berichts-Generator und SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
