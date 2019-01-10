
![image-20190109183130799](images/image-20190109183130799-7055090.png)



# Replacing an API Product



## Prerequisites

Before you begin, you must have completed the **lab1**.

## Objective

In this tutorial, you will update an existing API product by replacing it with a newer one. When an API product is replaced, the changes take effect immediately and all application subscriptions are updated automatically.  

---
## Replacing an API Product
1. In API Manager, if you have not previously pinned the UI navigation pane, click the **Navigate to** icon ![](images/navigate-to.png). The API Manager UI navigation pane opens. To pin the UI Navigation pane, click the **Pin menu** icon ![](images/pinned.png).

2. Click **Drafts** > **APIs**.

3. In the APIs panel, click **Weather Provider API** to open the REST proxy API.  
  ![](images/rep-api-list.png)

4. Change the **Version** to 2.0.0.  

5. Click the disk icon to save the API changes.  
  ![](images/rep-change-version.png)

6. Click **All APIs**.  
  ![](images/rep-all-apis.png)

7. Click **Products**.  
  ![](images/rep-api-list-2.png)

8. Select **Weather Provider API Product**.  
  ![](images/rep-draft-prod-list.png)

9. Change the **Version** to 2.0.0. Enter `Updated API` in the **Description** field. Click the disk icon to save the changes.  
  ![](images/rep-update-prod.png)

10. Click the **Stage** icon to upload the new version. Select the **Sandbox** catalog if it is not already selected.
  ![](images/rep-stage-prod-2.png)
    **Note**: It is possible to stage a new version to a different catalog, allowing control of what audience of developers can see this version. This capability can be helpful when moving API products from development to test to production.

11. Click **>>** to open the navigation menu, and select **Dashboard**.  
   ![](images/rep-dashboard.png)

12. Click **Sandbox**.  

13. Click the vertical ellipsis on the **Weather Provider API Product 2.0.0 Staged** line.  
   ![](images/rep-dash-prod-list-2.png)

14. Select **Replace an existing product**.  
   ![](images/rep-replace-prod.png)

15. Select **Weather Provider API Product 1.0.0** in the list of products presented. Click **Next**.  
   ![](images/rep-replace-dialog.png)

16. Select **Default plan**. Click **Replace**.  
   ![](images/rep-replace-dialog-2.png)

     As a result of this replacement, the Weather Provider API Product 1.0.0 is retired, and the Weather Provider API Product 2.0.0  is published. **Note**: It is possible to change the plan associated with this product during the replacement process. This is an easy way to alter the plan for an API product.
    ![](images/rep-prod-retired.png) 


## What you accomplished in this tutorial

In this tutorial, you completed the following activities:
1. Updated an API product.
2. Replaced an existing API product with an updated API product.

---








