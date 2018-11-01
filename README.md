
COM Wrapper sample v1.0 - 2018-10-29

This sample application contains example code on how to integrate with the SFM solution. 
Much like the Forkrsvninsmodul (FM) solution the COM Wrapper receives calls from a COM API and handles the communication between the SFM API and the SFM Angular client.

The following process occurs on each call to the COM wrapper:

1. The COM Wrapper receives the xml from the COM API call that may or may not contain HelseId access and id tokens.

Case when HelseId tokens are present:

2. A call is made to the SFM backend API to perform patient updates if necessary and fetch a temporary patient ticket (string of max 200 characters) and url to access the SFM client. 

3. A new browser window is opened to direct the user to the URL received from the SFM backend API on step 2)


Case when tokens are not present:

2. Open a browser and redirect the user to HelseId login pages

3. After successful authenticaton retrieve valid access and id tokens from the HelseId authorization redirect

4. A call is made to the SFM backend API to perform patient updates if necessary and fetch a temporary patient ticket (string of max 200 characters) and url to access the SFM client. 

5. A new browser window is opened to direct the user to the URL received from the SFM backend API on step 2)



Available settings via appSettings.json file:

ApiEndpoint: The endpoint of the SFM backend
HelseIdEndpoint: The endpoint of HelseId 
HelseIdRedirectUri: The redirect Url where the tokens are received when the COM wrapper needs to redirect to HelseId for authentication
HelseIdClientId: The HelseId client id to perform authentication
HelseIdScope: The scopes being requested  when performing HelseId authentication


The following is a brief explanation of the project organization:

- Browser logic: Contains logic associated with handling browser requests 
- Configuration: Contains logic to handle the appSettings configuration file 
- OpenIdConnect: Contains data models and helper classes to handle OpenId communication with HelseId authentication
- StructureMap: StructureMap related classes
- Common: COM Api related classes

################
################
NOTE: To be able to run this project the FM.Common.dll file must be added to the .\lib\FM.Common\ directory. Contact Ole Martin Winnem for more info.
################
################


Additional notes:
- Run ComWrapperSampleApp /install once to register the COM application (Admin privileges are needed)
- StartPasient.ps1: Runs StartPasient COM interface method with the included patient file
- StartPasient.xml: The patient file with patient info + login information (access tokens)
