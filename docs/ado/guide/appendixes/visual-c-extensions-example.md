---
title: Visual C++-Erweiterungen – Beispiel | Microsoft-Dokumentation
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- ADO, Visual C++
- Visual C++ [ADO], VC++ extensions example
ms.assetid: 9739c278-582c-402b-a158-7f68a1b2c293
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a54c32287a977899838a091543fc776577d54e02
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/01/2018
ms.locfileid: "47845198"
---
# <a name="visual-c-extensions-example"></a>Visual C++-Erweiterungen – Beispiel
Dieses Programm zeigt, wie Werte aus Feldern abgerufen und in C/C++-Variablen konvertiert werden.  
  
 In diesem Beispiel wird zudem nutzt die automatisch die COM-spezifischen Details des Aufrufs verarbeitet "intelligente Zeiger" `QueryInterface` und verweiszählung für die **IADORecordBinding** Schnittstelle.  
  
 Ohne zu intelligenten Zeigern würden Sie code:  
  
```  
IADORecordBinding   *picRs = NULL;  
...  
TESTHR(pRs->QueryInterface(  
          __uuidof(IADORecordBinding), (LPVOID*)&picRs));  
...  
if (picRs) picRs->Release();  
```  
  
 Mit intelligenten Zeigern, leiten Sie die `IADORecordBindingPtr` Geben Sie in der `IADORecordBinding` Schnittstelle mit dieser Anweisung:  
  
```  
_COM_SMARTPTR_TYPEDEF(IADORecordBinding, __uuidof(IADORecordBinding));  
```  
  
 Und instanziieren Sie den Zeiger wie folgt:  
  
```  
IADORecordBindingPtr picRs(pRs);  
```  
  
 Da die Visual C++-Erweiterungen von implementiert werden die **Recordset** -Objekt, das den Konstruktor für den intelligenten Zeiger, `picRs`, dauert die _`RecordsetPtr` -Zeiger ist, `pRs`. Der Konstruktor ruft `QueryInterface` mit `pRs` finden die `IADORecordBinding` Schnittstelle.  
  
```  
// Visual_Cpp_Extensions_Example.cpp  
// compile with: /EHsc  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
#include <icrsint.h>  
_COM_SMARTPTR_TYPEDEF(IADORecordBinding, __uuidof(IADORecordBinding));  
  
inline void TESTHR(HRESULT _hr) { if FAILED(_hr) _com_issue_error(_hr); }  
  
class CCustomRs : public CADORecordBinding {  
   BEGIN_ADO_BINDING(CCustomRs)  
      ADO_VARIABLE_LENGTH_ENTRY2(2, adVarChar, m_ch_fname, sizeof(m_ch_fname), m_ul_fnameStatus, false)  
      ADO_VARIABLE_LENGTH_ENTRY2(4, adVarChar, m_ch_lname, sizeof(m_ch_lname), m_ul_lnameStatus, false)  
   END_ADO_BINDING()  
  
public:  
   CHAR m_ch_fname[22];  
   CHAR m_ch_lname[32];  
   ULONG m_ul_fnameStatus;  
   ULONG m_ul_lnameStatus;  
};  
  
int main() {  
   ::CoInitialize(NULL);  
   try {  
      _RecordsetPtr pRs("ADODB.Recordset");  
      CCustomRs rs;  
      IADORecordBindingPtr picRs(pRs);  
  
      pRs->Open(L"SELECT * FROM Employee ORDER BY lname", L"dsn=DataPubs;Trusted_Connection=yes;", adOpenStatic, adLockOptimistic, adCmdText);  
  
      TESTHR(picRs->BindToRecordset(&rs));  
  
      while (!pRs->EndOfFile) {  
         // Process data in the CCustomRs C++ instance variables.  
         printf("Name = %s %s\n",  
            (rs.m_ul_fnameStatus == adFldOK ? rs.m_ch_fname: "<Error>"),   
            (rs.m_ul_lnameStatus == adFldOK ? rs.m_ch_lname: "<Error>") );  
  
         // Move to the next row of the Recordset.   Fields in the new row will   
         // automatically be placed in the CCustomRs C++ instance variables.  
  
         pRs->MoveNext();  
      }  
   }  
   catch (_com_error &e ) {  
      printf("Error:\n");  
      printf("Code = %08lx\n", e.Error());  
      printf("Meaning = %s\n", e.ErrorMessage());  
      printf("Source = %s\n", (LPCSTR) e.Source());  
      printf("Description = %s\n", (LPCSTR) e.Description());  
   }  
   ::CoUninitialize();  
}  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Mithilfe von Visual C++-Erweiterungen](../../../ado/guide/appendixes/using-visual-c-extensions.md)   
 [Visual C++-Erweiterungsheader](../../../ado/guide/appendixes/visual-c-extensions-header.md)
