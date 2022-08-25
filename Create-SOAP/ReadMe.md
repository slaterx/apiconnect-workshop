# IBM API Connect

## Create and Secure an API to Proxy an Existing SOAP Web Service

[Return to main APIC lab page](../ReadMe.md)

---

# Table of Contents
- [1. Introduction](#introduction)

- [2. Import an API into the Developer Workspace](#import_api)

- [3. Configure the API ](#configure_api)
	* [3a. Configure Client Secret API Key Security](#configure_security)
	* [3b. Review and update the Target-URL for Sandbox Environment](#target_url)
	* [3c. Review the Proxy Call in Designer](#proxy)

- [4. Test the API](#test_api)

- [5. Publish API](#publish_api)
	* [5a. Create Customer Product and Add API](#customer_product)

- [6. Summary](#summary)

---

# 1. Introduction <a name="introduction"></a>

In this lab, we will get a chance to use the IBM API Connect (APIC) Designer and its intuitive interface to import and edit an API using the Web Service Description Language (WSDL) of an existing SOAP web service.

In this tutorial, we will explore the following key capabilities:

-   Creating an API by importing an WSDL definition for an existing SOAP service

-   Configuring ClientID/Secret Security, endpoints, and proxy to invoke an endpoint

-   Testing the API in the developer toolkit

-   Publish an API for developers


# 2. Import an API into the Developer Workspace <a name="import_api"></a>

1\. In a browser, enter the URL for the Platform Navigator that is provided by your instructor.

If you're not logged before, follow these instructions to access to the Platform Navigator  ->
[Login to the Platform Navigator](../Login-pn/ReadMe.md). After that, click on **IBM Cloud Pak** in the upper left.

![alt text][pic104]

2\. Navigate to the API Connect instance.

![alt text][pic6]

3\. If first time logging in the login page is presented, click on **Techcon LDAP** and put the credentials again.

![alt text][pic8]

4\. Confirm that you are in the provider organization for your username (upper right) and then click on **Develop APIs and products**.

![alt text][pic9]

5\. We are now able to begin to create APIs and Products.  Click **Add**.

![alt text][pic10]

6\. Click **API (from REST, GraphQL or SOAP)**.

![alt text][pic11]

7\. Click **From existing WSDL service (REST proxy)** under **Create** and click **Next**.

![alt text][pic12]

8\. Download the [WSDL here](resources/countries.wsdl), then drag and drop the file that you just downloaded or click to upload. Once you have dragged and dropped or uploaded, you will see the WSDL file listed under and should see a notification that the "WSDL has been successfully validated". Click **Next**.

![alt text][pic13]

9\. The WSDL services in the SOAP endpoint will be listed. Click **Next**.

![alt text][pic14]

10\. Now, you will be allowed to customize the API. Rename title and base path to "Countries", then click **Next**.

![alt text][pic14-1]

11\. Make sure that the **Activate API** <span style="color: red">is not</span> selected and click **Next**.

![alt text][pic14-2]

12.\ The API should be imported successfully as shown in the image below.  Click **Edit API**.

![alt text][pic15]
    
[pic6]: images/6.png
[pic7]: images/7.png
[pic8]: images/8.png
[pic9]: images/9.png
[pic10]: images/10.png
[pic11]: images/11.png
[pic12]: images/12.png
[pic13]: images/13.png
[pic14]: images/14.png
[pic14-1]: images/14-1.png
[pic14-2]: images/14-2.png
[pic15]: images/15.png
[pic104]: images/104.png

# 3. Configure the API <a name="configure_api"></a>

After importing the existing API, the first step is to configure basic security before exposing it to other developers. By creating a client key and secret security, we are able to identify the application using the API. 

Next, we will define the backend endpoints where the API is actually running. IBM API Connect supports pointing to multiple backend endpoints to match your multiple build stage environments. 

Finally, we will configure the proxy call to invoke the endpoint.

## 3a. Configure API Key Security <a name="configure_security"></a>

1\. Make sure that the **Design** tab is selected and click on **Security Schemes**. 

![alt text][pic23]

You will see that there's already a clientID type scheme. Clicking on it, will show that the variable name is **X-IBM-Client-Id** and that it is expected to be delivered via header. Now, we will create the clientSecret. Click on the **+** next to **Security Schemes**.

![alt text][pic31]

2\. For the **Security Definition Name (Key)**, enter a name (e.g., **clientSecret**) and select **apiKey** in the drop-down menu for **Security Definition Type**.

![alt text][pic32]

3\. Select **client_secret** from the drop-down menu for **Key Type (optional)**, select **header** from the drop-down menu for **Located In**, and enter a name (e.g., **X-IBM-Client-Secret**) for **Variable name**.   Click **Create**.

![alt text][pic33]

4\. Click **Save**.

![alt text][pic26]

5\. Once saved, you will see an indicator window appear that shows that **Your API has been updated**.  Click on the **X** to close the window.

![alt text][pic22]

6\. Make sure that the **Design** tab is selected and click on **Security**. Then click on Add.

![alt text][pic34]

7\. Select **"clientId"** and **"clientSecret"** and click **Create**.

![alt text][pic35]

8\. Click **Save**.

![alt text][pic26]

9\. Once saved, you will see an indicator window appear that shows that **Your API has been updated**.  Click on the **X** to close the window.

![alt text][pic22]

## 3b. Define a Target-URL for Sandbox Environment <a name="target_url"></a>

1\. Make sure that the **Design** tab is selected and click on **Host**.

![alt text][pic38]

2\. Delete the variable $(catalog.host)

![alt text][pic39]

3\. Navigate to the **Gateway** tab.

![alt text][pic40]

4\. Make sure that the **Gateway** tab is selected and expand **Properties**.  Click on **+** to create a new entry called **target-url**.

![alt text][pic41]

5\. In **Property Value (optional)**, enter the value from SOAP wsdl service (in this example it is country-soap-endpoint.apps.grievous.coc-ibm.com).  **Note:**  Make sure to include a **http://** at the beginning and remove the **:** and **port number** (e.g. **:80**) from the end.

![alt text][pic42]

6\. Click **Create**.

7\. Click **Save**.

![alt text][pic26]

8\. Once saved, you will see an indicator window appear that shows that **Your API has been updated**.  Click on the **X** to close the window.

![alt text][pic22]

## 3c. Configure Proxy Call in Designer <a name="proxy"></a>

1\. Navigate to the **Gateway** tab.

![alt text][pic48]

2\. Make sure the **Gateway** tab is selected and click on **Policies**.

![alt text][pic49]

3\. Click on any of the **getCountry:invoke** task in the assembly panel.

![alt text][pic50]

4\. Confirm that the **URL** so that it reads the hostname used above (with http) and **/ws** as path. Remove the port if necessary. Click on the **x** to close the panel.

![alt text][pic51]

5\. Click **Save**.

![alt text][pic52]

6\. Once saved, you will see an indicator window appear that shows that **Your API has been updated**.  Click on the **X** to close the window.

![alt text][pic53]

[pic22]: images/22.png
[pic23]: images/23.png
[pic24]: images/24.png
[pic25]: images/25.png
[pic26]: images/26.png
[pic27]: images/27.png
[pic28]: images/28.png
[pic29]: images/29.png
[pic30]: images/30.png
[pic31]: images/31.png
[pic32]: images/32.png
[pic33]: images/33.png
[pic34]: images/34.png
[pic35]: images/35.png
[pic36]: images/36.png
[pic37]: images/37.png
[pic38]: images/38.png
[pic39]: images/39.png
[pic40]: images/40.png
[pic41]: images/41.png
[pic42]: images/42.png
[pic43]: images/43.png
[pic44]: images/44.png
[pic45]: images/45.png
[pic46]: images/46.png
[pic47]: images/47.png
[pic48]: images/48.png
[pic49]: images/49.png
[pic50]: images/50.png
[pic51]: images/51.png
[pic52]: images/52.png
[pic53]: images/53.png
[pic105]: images/105.png

# 4. Test the API <a name="test_api"></a>

In the API Designer, you have the ability to test the API immediately after creation in the Assemble view!

1\. Switch the toggle from Offline to Online. This step automatically publishes the API.

![alt text][pic54]

2\. You will see an indicator window appear that shows that **Your API has been updated**.  Click on the **X** to close the window.  You should see that the API is now Online.

![alt text][pic55]

3\. Click on the **Test** tab.

![alt text][pic56]

4\. For the **Request**, select the request that begins with **POST** and ends in **../countries/getCountry**. You will see that some parameters are filled (including the security API keys).

![alt text][pic56-1]

Click on **Body** and use the following content as payload:

```json
{"name": "Brazil"}
```

Then click on **Send**.

![alt text][pic57]

**Note:** If this is the first time testing the API after publishing it, you may get a **No response received** popup. Click **Here** and accept the certificate to see the 401 message.

![alt text][pic58]

To add an exception in the Chrome browser, click in the whitespace of the page.

![alt text][pic59]

Blindly type **thisisunsafe**.  This should direct you to a new page that states **400 - Bad Request**.

![alt text][pic63]

Navigate back to the **API Connect** browser window.

To add an exception in the Firefox browser, click **Advanced** and click **Accept the Risk and Continue**.

![alt text][pic61]

![alt text][pic62]

This will direct you to a new page that states **400 - Bad Request**.

![alt text][pic63]

Navigate back to the **API Connect** browser window.

5\. Click **Send**.

![alt text][pic57]

6\. The **Response** will show the details of chosen Country.

![alt text][pic64]



[pic54]: images/54.png
[pic55]: images/55.png
[pic56]: images/56.png
[pic56-1]: images/56-1.png
[pic57]: images/57.png
[pic58]: images/58.png
[pic59]: images/59.png
[pic60]: images/60.png
[pic61]: images/61.png
[pic62]: images/62.png
[pic63]: images/63.png
[pic64]: images/64.png
[pic65]: images/65.png
[pic66]: images/66.png
[pic67]: images/67.png
[pic68]: images/68.png
[pic69]: images/69.png
[pic70]: images/70.png
[pic71]: images/71.png
[pic72]: images/72.png
[pic73]: images/73.png
[pic74]: images/74.png
[pic75]: images/75.png
[pic76]: images/76.png
[pic77]: images/77.png
[pic78]: images/78.png
[pic79]: images/79.png

# 5. Publish API <a name="publish_api"></a>

In this lab, we will make the API available to developers. In order to do so, the API must be first put into a product and then published to the Sandbox catalog. A product dictates rate limits and API throttling.

When the product is published, the Invoke policy defined in the previous lab is written to the gateway. 

## 5a. Create a Product and Add API <a name="customer_product"></a>

1\. From the vertical navigation menu on the left, click **Develop**.

![alt text][pic80]

2\. Click the **Products** tab.

![alt text][pic82]

3\. Click **Add** and click **Product** from the drop-down menu.

![alt text][pic83]

![alt text][pic84]

4\. Click **New product** and click **Next**.

![alt text][pic85]

5\. Enter **Countries** for the **Title** and click **Next**.

![alt text][pic86]

6\. Select the **Countries** API and click **Next**.

![alt text][pic87]

7\. Keep the **Default Plan** as is and click **Next**.

![alt text][pic88]

8\. Select **Publish product** and confirm that **Visibility** is set to **Public** and **Subscribability** is set to **Authenticated**.  Click **Next**.

![alt text][pic89]

9\.  The Product is now published successfully with the API base URL listed and available for developers from the Developer Portal.  Click **Done**.

![alt text][pic90]

[pic80]: images/80.png
[pic81]: images/81.png
[pic82]: images/82.png
[pic83]: images/83.png
[pic84]: images/84.png
[pic85]: images/85.png
[pic86]: images/86.png
[pic87]: images/87.png
[pic88]: images/88.png
[pic89]: images/89.png
[pic90]: images/90.png

# 6.Summary <a name="summary"></a>

Congratulations, you have completed the **Create and Secure an API** lab. Throughout the lab, you learned how to:

-   Create an API by importing an OpenAPI definition for an existing REST service

-   Configure ClientID/Secret Security, endpoints, and proxy to invoke endpoint

-   Test a REST API in the Developer Toolkit

-   Publish an API for developers

[Return to main APIC lab page](../ReadMe.md)
