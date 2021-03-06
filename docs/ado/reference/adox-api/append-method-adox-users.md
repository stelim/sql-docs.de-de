---
title: Append-Methode (ADOX-Benutzer) | Microsoft-Dokumentation
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Users::raw_Append
- Users::Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: b80bc5d5-78ca-4f75-956b-2ac658029cc7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e56391357e7a11c47efdf0ffaf3c9ae9704d5db3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/01/2018
ms.locfileid: "47787204"
---
# <a name="append-method-adox-users"></a>Append-Methode (ADOX-Benutzer)
Fügt ein neues [Benutzer](../../../ado/reference/adox-api/user-object-adox.md) -Objekt an die [Benutzer](../../../ado/reference/adox-api/users-collection-adox.md) Auflistung.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Users.Append User[,Password]  
```  
  
#### <a name="parameters"></a>Parameter  
 *Benutzer*  
 Ein **Variant** -Wert, enthält die **Benutzer** anzufügende Objekt oder den Namen des Benutzers zum Erstellen und anfügen.  
  
 *Kennwort*  
 Optional. Ein **Zeichenfolge** -Wert, der das Kennwort für den Benutzer enthält. Die *Kennwort* Parameter entspricht der Wert von der [ChangePassword](../../../ado/reference/adox-api/changepassword-method-adox.md) Methode eine **Benutzer** Objekt.  
  
## <a name="remarks"></a>Hinweise  
 Die **Benutzer** Auflistung von einem [Katalog](../../../ado/reference/adox-api/catalog-object-adox.md) Benutzer alle des Katalogs darstellt. Die **Benutzer** Sammlung für einen [Gruppe](../../../ado/reference/adox-api/group-object-adox.md) nur die Benutzer, die eine Mitgliedschaft in der Gruppe darstellt.  
  
 Wenn der Anbieter beim Erstellen von Benutzern nicht unterstützt wird, tritt ein Fehler auf.  
  
> [!NOTE]
>  Vor dem Anfügen einer **Benutzer** -Objekt der **Benutzer** Auflistung von einer **Gruppe** -Objekt, eine **Benutzer** Objekt mit demselben [Name ](../../../ado/reference/adox-api/name-property-adox.md) wie diejenige, die angefügt werden im bereits vorhanden sind, muss die **Benutzer** Auflistung von der **Katalog**.  
  
## <a name="applies-to"></a>Gilt für  
 [Users-Auflistung (ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Gruppen und Benutzer Append, ChangePassword Methods Example (VB)](../../../ado/reference/adox-api/groups-and-users-append-changepassword-methods-example-vb.md)   
 [Append-Methode (ADOX-Spalten)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append-Methode (ADOX-Gruppen)](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Append-Methode (ADOX Indizes)](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Append-Methode (ADOX-Schlüssel)](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Append-Methode (ADOX Prozeduren)](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Append-Methode (ADOX-Tabellen)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append-Methode (ADOX-Ansichten)](../../../ado/reference/adox-api/append-method-adox-views.md)
