# TFS
Hints & tips on using TFS

## Command line tool
To quickly search for a file:  
* Open powershell  
* Navigate to the TFS directory on your PC (root of local file copies)
* Locate the TF.EXE command and set the Alias for use:  
  **Set-Alias tfs "C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\tf.exe"**  
* Search for the file:  
  **tfs dir rptuseraccess.aspx /recursive /noprompt**
