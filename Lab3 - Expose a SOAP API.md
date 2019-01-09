![image-20190109183130799](images/image-20190109183130799-7055090.png)



# Exposing a SOAP service as a REST API



---
## Objective
In API Manager, you will create a REST API that will accesses a existing SOAP Service and expose it as a REST API.

## Prerequisites
1. Before you begin, you will need to get an API Connect running on premise or on IBM Cloud.

   **And you should be connected to the API Manager.**

2. Before you begin, copy the  https://raw.githubusercontent.com/IBM-Bluemix-Docs/apiconnect/master/tutorials/weatherprovider.wsdl  file to your local filesystem.

---
## Setting up a REST API definition
1. On the API Manager page, if you have not previously pinned the UI navigation pane then click the **Navigate to** icon ![](images/navigate-to.png). The API Manager UI navigation pane opens. To pin the UI Navigation pane, click the **Pin menu** icon ![](images/pinned.png).
2. Select **Drafts** in the UI navigation pane and then click the **APIs** tab. The **APIs** tab opens.
  ![](images/drafts-api-1.png)
3. Select **Add +** > **New API**.
4. Specify basic information about the API.
  - In the **Title** field, enter `Weather Data`.
  - Leave the **Name** field as `weather-data` when it is filled while you enter your title.	
  - Leave the **Base** Path field as `/weather-data`.
  - Leave the **Version** field as `1.0.0`.
5. Expand **Additional properties** to specify additional properties for the API.
  - From the **API template** field, select **Default** to indicate that you want to use the default template to create the API definition.
  - Leave the remaining fields unchanged.
  ![](images/new-api-1.png)
6. Add your API to a new Product and then create the API definition.
  - Select **Add a product**.
  - In the **Title** field, use `Weather Data product` as the default.
  - Leave the **Name** and **Version** fields unchanged.
  - Ensure that the **Publish this product to a catalog** check box is selected and then select **Sandbox** as the target Catalog.
  ![](images/new-api-2.png)
  - Click **Create API**. The **Design** tab for the draft of your API definition opens.
7. Your API is now created. The Design page displays. Click **Security** in the navigation bar.
  ![](images/api-security-1.png)
8. Uncheck the **ClientID** option.
  ![](images/api-security-2.png)

  >![](images/info.png)
  >You may notice that there is a yellow triangular icon that appears next to the save disk icon.  This is a warning that there are definition that may have been defined but not yet used. (This won't affect the API definition.)
9. In the **Definitions** section, click the **Add Definition** icon ![](images/add-icon.png) and then expand the new definition by clicking it.
10. Name the definition `Weather Data Output`.
11. The definition will have five properties. Click **Add Property** four times to add the additional properties. Rename the `Property Name` using the following as a guide and use the default for the `Description`, `Type` and `Example`:
   ![](images/definition-new-1.png)
12. In the **Paths** section, click the **Add Path** icon ![](images/add-icon.png).
13. In the **Path** field of your newly created Path, replace the contents with `/getweatherdata`.
14. Expand the **GET /getweatherdata** operation by clicking it.
   ![](images/path-new-1.png)
15. For your **GET /getweatherdata** operation, click **Add Parameter**, and then click **Add new parameter**.
16. Name your new parameter `zip_code` and leave the rest as default.
17. In the **Schema** column of the **200 OK** response in the **Responses** section, select your **Weather Data Output** definition. For the response to the API call, the object define in by the **Weather Data Output** will be the response object.
   ![](images/path-new-2.png)
18. Click the Save icon ![](images/save-icon.png) to save your changes.

---
## Adding and configuring your web service invocation
To add and configure the invoke and map policies that integrate your web service into your API definition, complete the steps below.
1. In the **Services** section, click the **Add service** icon ![](images/add-icon.png). The `Import web service from WSDL` window opens.
	![](images/upload-file-1.png)
2. Select **Upload file**.
3. In the **File Upload** window, specify the location to the `weatherprovider.wsdl` file that you downloaded in `step 2` of the **Prerequisites** section and click **Open** to continue.
4. Select the **weatherService** SOAP service and then click **Done**. In the **Services** section, **WeatherService** web service is listed with a single **weatherRequest** operation.
	![](images/upload-file-2.png)

	![](images/services-add-1.png)	
5. Navigate to the **Assemble** tab and then ensure that **DataPower Gateway policies** is selected.
6. Delete the existing **invoke** policy on the canvas by hovering your cursor over the policy and then clicking the **Delete policy** icon ![](images/delete-icon.png).
	![](images/delete-invoke-1.png)	
7. From the palette, drag the **weatherRequest** web service onto the dashed box that is displayed on the canvas. An invoke policy and two map policies are placed in the assembly. The first map policy assigns variables to the input of your web service invocation, while the second policy assigns outputs of your web service invocation to variables. The outputs of the first map and the inputs of the second map are generated from the WSDL provided in step 4.
	![](images/services-add-2.png)	
8. Click the **weatherRequest: input** map policy and then click the **Edit inputs** icon ![](images/edit-icon.png) in the Input column of the property sheet.
	![](images/services-add-3.png)	
9. Click **+ parameters for operation** and select `get /getweatherdata`.
10. Click **Done** to add the `zip_code` parameter.
	![](images/webservice-input-1.png)
11. Click the circle corresponding to **zip_code string** on the input side and then click the circle corresponding to **zipcode string** on the output side.  
	![](images/webservice-input-2.png)
12. Close the property sheet.
13. Click the **weatherRequest: output** map policy in the palette and then click the **Edit outputs** icon ![](images/edit-icon.png) in the Output column of the property sheet.
14. Select **+ outputs for operation** and select `get /getweatherdata`.
15. Select **Done** to add the `Weather Data Output` output definition.
	![](images/webservice-output-1.png)
16. Click the circle corresponding to **zip string** on the input side and then click the circle corresponding to **zip string** on the output side. Map the remaining parameters using the following as a guide.
	![](images/webservice-output-2.png)
17. Click the **Save** icon ![](images/save-icon.png) to save your changes.

You have included the web service invocation in your assembly and mapped an input parameter to the appropriate part of the SOAP request and mapped the appropriate part of the SOAP response to a JSON output.

---
## Testing your API definition
To test your API definition by using the API Manager test tool, complete the steps below.
1. Click the **Test** icon ![](images/test-icon.png) under the **Assembly** tab to reveal the test pane.
	![](images/test-pane-1.png)
2. If you have used the test tool before, click **Change setup**.
3. Choose `Weather Data product 1.0.0` from the list of products.
	![](images/choose-product-1.png)
4. Click **Republish product**.
5. Click **Next**.
6. Select `get /getweatherdata` from the list of operations.  
	![](images/select-operation-1.png)
7. Scroll down to the **zip_code** field, enter `90210`.  
	![](images/test-api-1.png)
8. Click **Invoke**. The API returns the current weather.  
	![](images/test-api-2.png)

---
## What you did in this tutorial
In this tutorial, you completed the following activities:
1. Set up a REST API definition
2. Configured an API to invoke an existing web service and return its output
3. Tested your API definition

---

