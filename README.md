<div align=center>

# [Converting MFC Application <br>into Chromium Project Browser Process](https://github.com/TangramDev/.github/blob/main/document/mfcexe.md)
  
<div align=center>

## (1)Prepare a MFC Project <br>(create a new Project, or open an existing Project)
<div align=center>

<h3 align=left>
<p>
  
Copy all files included with [***MFCPlus***](https://github.com/TangramDev/OpenWebRunTime/tree/master/src/sdk/MFCPlus) into the prepared MFC Desktop Software Project. Open the "pch.h(pch.cpp)" or "stdafx.h(stdafx.cpp)" file of the developer's desktop software project, add the following code at the end of the opened file at a suitable position:</p>
<p align=center>#include "WebRTApp.h" // for pch.h or stdafx.h</p>
<p align=center>#include "WebRTApp.cpp" // for pch.cpp or stdafx.cpp</p>
<br>	
	
<p>
<div align=center id="mfcdevmanifest"><img src="https://user-images.githubusercontent.com/26355688/183366016-6337524d-c195-4d0c-a2d5-8cd74f0baf17.jpg" width="80%"/></div>
</p>	
</h3>
<hr />

## (2)Code Modifications
<center>
        <table border="3" cellpadding="3">
            <thead>
                <tr>
                    <th> <strong>Code modification</strong>
                    <th> <strong>Description</strong>
                </tr>                     
            <tbody>
                <tr>
                    <td width="30%">
                        <strong><p align=center>Modify Base Class</strong> </p>
                    </td>
                    <td width="70%">
		     <strong>
		     Replace "public CWinApp(Ex)" with: <p align=center>public CWebRTApp(Ex)</p>
		     Replace "public CMDIFrameWndEx" with: <p align=center>public CWebRTMDIFrame</p>
		     </strong>
                    </td>
            </tbody>
	    <tbody>
                <tr>
                    <td width="30%">
                        <strong><p align=center>Dialog Application</strong> </p>
                    </td>
                    <td width="70%">
		     <strong><p>Modify the return value of</p><p><div align=center>BOOL CMFCDlgApp::InitInstance()</p><p align=left>to</p> <p align=center>TRUE</strong>.</p>
                        </p></strong>
                    </td>
            </tbody>	    
	    <tbody>
                <tr>
                    <td class="sunnysolution" width="30%">
                        <strong><p align=center>Document Serialization</p></strong>
                    </td>
                    <td class="sunnysolution" width="50%">
		      <strong>
                      </p>
                        <p>Add the following serialization code in the body of the Serialize (CArchive & ar) function:                            
                        </p>
                      <p>                   
                      
    void CMFCApplicationDoc::Serialize(CArchive& ar){
	  if (ar.IsStoring())
	  {
		  ar << theApp.GetDocTemplateID(this);
	  }
	  else
	  {
		  ar >> theApp.m_strCreatingDOCID;
	  }
    }
</p>
</strong>
                    </td>
            </tbody>
        </table>
</center>
