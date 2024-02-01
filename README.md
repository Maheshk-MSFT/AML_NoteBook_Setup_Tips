# AzNoteBookTips
Azure Machine Learning NoteBook setup tips
<img width="950" alt="opn1" src="https://github.com/Maheshk-MSFT/AzNoteBookTips/assets/61469290/eb640061-75b2-4634-967c-177f9f071019">

Problem: 
I was trying to execute a speech SDK sample notebook for the first time as in this article
[https://learn.microsoft.com/en-us/azure/ai-services/speech-service/quickstarts/setup-platform?pivots=programming-language-python&tabs=linux%2Cubuntu%2Cdotnetcli%2Cdotnet%2Cjre%2Cmaven%2Cnodejs%2Cmac%2Cpypi#install-the-speech-sdk-for-python](https://learn.microsoft.com/en-us/azure/ai-services/speech-service/quickstarts/setup-platform) but no luck.  
I tried both local and Azure workbook svc too but faced the same error. >> "Module could not be found". I tried re-installing reqd lib's and also restarted the kernel - no improvement. 

**Resolution: 
**This issue is due to the conda environment "azureml_py38" being activated by default regardless of the selected Kernel version. For example, if the selected Kernel is Python 3.10 - SDKv2.

To check the active conda environment, in your terminal run the command "conda info --envs". The active conda environment is the one with an "*".

<img width="759" alt="opn2" src="https://github.com/Maheshk-MSFT/AzNoteBookTips/assets/61469290/4a97cb87-0a44-460c-bfbf-a235b3e58853">

To resolve, before installing the package, you may run "conda activate <environment-name>". 
 
Alternatively, you may also set the PATH environment variable so that it points to the environment of the target conda environment as follows, this may be done from the Notebook. 
	1. Check current environment.
	2. Update the envs path and set to $PATH environment variable. For example,
![image](https://github.com/Maheshk-MSFT/AzNoteBookTips/assets/61469290/449005a3-d6ba-4068-ad9e-f2b7ddf57b98)

Now, 
1. Install Speech SDK
![image](https://github.com/Maheshk-MSFT/AzNoteBookTips/assets/61469290/5dbf6085-9018-4213-acc8-e538b265cdd2)

2. Check Speech SDK
![image](https://github.com/Maheshk-MSFT/AzNoteBookTips/assets/61469290/89c4bdb9-dfdb-4e5d-8475-1e8be6b56155)

Additional useful commands, 
```
!pip insall --upgrade azure-cognitiveservices-speech
!pip show azure-cognitiveservices-speech
!pip list 
```
Also make sure to set the right SDK environment to execute the notebook. If you change the runtime, then reselect the machine by switching between the compute instances say VM -> Serverless and then to VM and then select the right version to see them working fine. 

<img width="910" alt="opn3" src="https://github.com/Maheshk-MSFT/AzNoteBookTips/assets/61469290/d10dc17f-910d-43b9-a3fc-c2e186e241c7">

<img width="1003" alt="opn4" src="https://github.com/Maheshk-MSFT/AzNoteBookTips/assets/61469290/cc8d9cfd-8f30-434f-ae72-73c52081b372">

     ```
         transcribeAudioFiletxt = speech_recognizer.text_results
     
        file1 = open('1669_transcribe.txt', 'w') 
        file1.write('\n'.join(str(i) for i in transcribeAudioFiletxt))
        file1.close()
      ```
Good refereence for python commands - https://www.geeksforgeeks.org/writing-to-file-in-python/?ref=lbp
