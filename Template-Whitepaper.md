ALM RANGERS
 ---

@ Add your Whitepaper title here
===

@ Add your authors here

@ Add your blurb here

---
NOTE: @ Add your note here
 ---

@ Add your subtitle_1 here
---

@ Add your content_1 here.


@ Add your subtitle_2 here
---

@ Add your content_2 here.


Table Styles
---

<table>
  <tr>
    <th align="left">Table Header 1</th>
    <th align="left">Table Header 2</th>		
    <th align="left">Table Header 3</th>
  </tr>
  <tr>
    <td valign="top"><a href="http://blogs.msdn.com/b/visualstudioalmrangers/">Column 1 Link 1</a></td>
    <td valign="top">Column 2</td>		
    <td valign="top">Column 3 - Heading 1:
      <ul>
        <li>Heading 1 - Bullet point 1</li>
      </ul>
      Column 3 - Heading 2:
      <ul>
        <li>Heading 2 - Bullet point 1</li>
        <li>Heading 2 - Bullet point 2</li>
        <li>Heading 2 - Bullet point 3</li>
        <li>Heading 2 - Bullet point 4</li>
      </ul>
    </td>
  </tr>
</table>

*Table 1 – @ Add your table name here*


Hyperlink Style
---
@ Add your [hyperlink](http://blogs.msdn.com/b/visualstudioalmrangers/) here.


Images Style
---

@ Add your image here. Remember to add your image to the 'media' folder under the 'Doc' folder.

![](media/image1.png)

*Figure 1 – @ Add image description here*

![](media/image2.png)

*Figure 2 – @ Add image description here*

Text styles
---

@ Here is how you apply **bold** to text.

Header styles
---

# Header 1 - We typcially don't use this style (see '@ Add your Whitepaper title here' above).
## Header 2 - We typcially don't use this style (see '@ Add your subtitle_1 here' above).
### Header 3
#### Header 4
##### Header 5
###### Header 6

Code Samples
---
### @ Add your code sample here

You can add code samples below:

```
This is a code sample.
var server = new TfsConfigurationServer (new Uri("http://<<server>>:8080/tfs"));
server.Authenticate();
var security   = collection.GetService<ISecurityService>();
var namespaces = security.GetSecurityNamespaces();
```

*Code 1 - @ Add your code sample description here*

To get a list of namespaces from the Server, use the **TfsConfigurationServer** object to establish a connection.

```
var server = new TfsConfigurationServer (new Uri("http://<<server>>:8080/tfs"));
server.Authenticate();
var security   = collection.GetService<ISecurityService>();
var namespaces = security.GetSecurityNamespaces();
```
*Code 2 - Using TFS OM to query TFS server-level security namespaces*

Peruse the
[ISecurityService](http://msdn.microsoft.com/en-us/library/microsoft.teamfoundation.framework.client.isecurityservice.aspx)
interface, the
[GetSecurityNamespace](http://msdn.microsoft.com/en-us/library/microsoft.teamfoundation.framework.client.isecurityservice.getsecuritynamespace.aspx),
and
[TfsConfigurationServer](http://msdn.microsoft.com/en-us/library/microsoft.teamfoundation.client.tfsconfigurationserver.aspx)
object to establish a connection

Project Collection-level permissions are set on a Team Project Collection-wide basis. These permissions are not specific to a single Team Project; instead, they contain permissions that can affect every Team Project in the Team Project Collection.

See [ISecurityService
Interface](http://msdn.microsoft.com/en-us/library/microsoft.teamfoundation.framework.client.isecurityservice.aspx),
[GetSecurityNamespace](http://msdn.microsoft.com/en-us/library/microsoft.teamfoundation.framework.client.isecurityservice.getsecuritynamespace.aspx),
and use the
[TfsTeamProjectCollection](http://msdn.microsoft.com/en-us/library/microsoft.teamfoundation.client.tfsteamprojectcollection.aspx) object to establish a connection.

Extensible sample tool to help you
---
---
NOTE: Download the complete sample code from GiHub (https://github.com/ALM-Rangers/Extracting-effective-permissions-from-TFS/tree/master/Source).
 ---

### A quick tour

The purpose of the custom sample program is to provide a real-world example of how to retrieve the security namespaces. It is a good start for learning the TFS security model APIs and for developing your own auditing tool. We tested the tool on TFS 2013 Update 3 and Visual Studio Online (as of October 2014).

You can use the XML output format to generate regular snapshots for a specific account. Since we structure the output, you can use it to compare snapshots to previous versions. The source code contains an XSL transform that generates a formatted html output from the XML report. We purposely omitted some tests to keep the code as clear as possible and to focus on accessing the API.

The command line parameters are simple:

-   **--collection**=\<URL of the collection\>\
    Specify the collection URL, similar to using the tf.exe tool, for example: http://yourservername:8080/tfs/yourcollection

-   **--users**=\<username 1\> \<username 2\>\
    Username format can be “domain\\account” for TFS Server or email for VSO account

-   **--f**=\<logfile\>\
    The username is added in the name of the log: if the argument is “c:\\temp\\auditlog.txt” and username is demo\\user, the audit file output would be c:\\temp\\auditlog\_demo\_user.xml”

-   **--html**\
    In addition to the xml log, produce a user-friendly html based report.

In case of an error, the sample program returns a non-zero exit code.

The program stops if the current user does not have the administrative rights on the collection.

For each user, the program retrieves the following permissions to generate the xml-output report file:

  * Project
  * Version control
  * Build
  * Warehouse
  * WorkItems
  * Areas
  * Iterations
  * Workspace

You can extract effective permissions for a user across all Team Projects within a Team Project Collection by executing the following command:

```
PermissionsExtractionTool.exe 
      -u "Windows Live ID\demo@hotmail.com" 
      --collection https:// demo.visualstudio.com/DefaultCollection 
      -f c:\temp\demo.xml
```

The sample program generates a comprehensive XML based report as shown below:

![](media/image3.png)

*Figure 2 - Sample Report*

![](media/image4.png)

*Figure 3 - Sample report mapping to web admin view*

### Generate a HTML Report from the XML Output

You can use any XSLT tool for this task. If you only have Visual Studio
2013, you can perform these four steps:

1.  Open the xml file in Visual Studio 2013
2.  Locate the XSLT document in the XslTemplates directory of the sample solution.
3.  Select the xml file in Visual Studio 2013, in the XML Menu click on “Start XSL without Debugging.”
4.  Select the xml transform.

The following extract shows a typical report generated by the sample tool and transformed using the XSLT document.

![](media/image5.png)

*Figure 4 - Sample Report*

Conclusion
---

This whitepaper summarizes our security research focused on security mapping. Here, we have discussed existing tooling, introduced you to some of the security namespaces, and provided a proof-of-concept sample solution, which you can use to explore and extend the effective security permissions extraction functionality.

Thanks for taking the time to read this and watch for more articles from the [ALM Rangers](http://aka.ms/vsarunderstand).

 ---
  **Hosam Kamel** is a Senior Premier Field Engineer (PFE) at Microsoft, and a Visual Studio ALM Ranger specializing in providing field-level support for Visual Studio Application Lifecycle Management (ALM) and Team Foundation Server. He focuses on helping software professionals and organizations build better applications and solutions using Microsoft Application Lifecycle Management technologies, practices, and tools working with development teams supporting them removing the traditional silos between development, testing, and project management to establish cohesive processes with the Visual Studio ALM tools. His experience with Team Foundation Server and Visual Studio started with the beginning of the VSTS and its product family nearly seven years ago. He is also an active Visual Studio ALM Ranger with lots of projects’ contributions. He has also authored several article, and spoken at various user groups, events, and conferences. Prior to joining Microsoft, Hosam worked as a Regional Technology Solution Professional for MEA Center of Expertise.

  **Michel Perfetti** is a Manager at Cellenza, a French consulting company. He has 15 years of experience in software development and MVP since 2006. He tries to apply the best ALM and agile techniques to his customers.
 ---
  **THANKS** to the following technical experts for reviewing this article: Baruch Frei, Bill Heys, Jon Guerin, Mario Rodriguez, Osmar Paes Landin Filho, Prasanna Ramkumar, Vinicius Moura, Willy-Peter Schaub.
 ---
